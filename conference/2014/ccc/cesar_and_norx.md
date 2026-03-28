# [2014-12-29 by Philipp Jovanovic and aumasson](https://events.ccc.de/congress/2014/Fahrplan/events/6137.html)

* [norx](https://norx.io/)
* [norx on github](https://github.com/norx/NORX)
* [cesar](http://competitions.cr.yp.to/caesar.html)

# block cipher modes

* ecb, cbc, cfb, ofb and ctr are from the 70s
* they had "fault tolerance" in mind also

# block cipher modes failures

* ecb mode - same message will result in same cypher text
* cbc mode - IV (initialization vector) has to be random (not only an iterator)
* ctr mode - reused nonce
* exploiting malleability
    * ecb: rearrange/replay blocks
    * ctr, ofb: bitwise modification of blocks
    * cbc: change current ciphertext block to predictably change the next plaintext block (during decryption)
* chosen boundary attacjs
    * ecb, cbc, cfb: partial chosen-plaintext control
    * decrypt messages byte by byte

# authenticated encryption (AE)

* input
    * key
    * nounce
    * message
* output
    * ciphertext
    * authentication tag
    * protects Confidential, Integrity, Authenticity
    * protects traffic in IPSec and many more

# authenticated encryption with additional data (AEAD)

* input
    * message
    * additional data
    * key
    * nounce
* output
    * ...

# AE(AD) constructions

* by generic composition
    * combine symmetric cipher and a MAC
        * Encypt-and-MAC
        * MAC-than-encrypt
        * Encrypt-then-MAC (generally better)
* dedicated methods
    * authenticated block ciper modes
        * ccm, gcm (NIST standardized, minor issues)
        * ocb (patented but mostly free to use)
        * eax
    * dedicated authenticated ciphers
        * grain-128-a
        * helix / phelix
        * hummingbird-1/2 (broken)
    * sponge functions ...

# common risks with AE

* interaction between cipher and MAC (key reuse, etc.)
* SEC(cipher+MAC) <= MIN(SEC(Cipher),SEC(MAC))
* custom ciphers/modes if not suitable standard
* "misues" (constant or repeated nonces, etc.)
* bad parameters choice (such as GCM tag size)
* all led to some problems ...

# crypto failurs

* padding oracle attacks (since 2002)
    * BEAST
    * Licky Thirteen
    * POODLE
* WEP (since 2007)
    * key recovery attacks within minutes
    * exploits biases in RC4 and "misuse"
    * aircrack-ng
* TLS (and RC4) (since 2013)
    * RC4 biases shown to be usable against TLS
    * exploits weaknesses in RC4 (again)
* RC4 and HIVE (since 2014)
    * using RC4 as pseudo number generator
    * RC4 is fast (but insecure ... as apples swift)

# CESAR

## what it is

* competition (for)
* authenticated
* encryption
* security
* applicability (, and)
* robustness

## general

* replacing than AES-GCM (used nearly everywhere)
* started 13.03.2014
* expected finished at the end of 2017
* sponsored but not organized/controlled by NIST
* led by DJB
* 57 submissions :-)
    * 39 are currently save
    * 13 have major bugs
    * 5 have minor bugs

## what is wrong with AES-GCM?

* unnecessarily complex (to implement)
* fast only if AES/Galois hardware built in
* without hardware support, even more complicated to implement
* auth key recovery if nonce is reused
* academics find new attacks every year
* aes itself currently is not broken

# NORX (NOt aRX)

## design goals

* high security
* high speed (in software and hardware)
* simplicity (of specs and code)
* online / one-pass
* scalability (parallelism, unrolling)
* high key agility (no "key schedule")
* side-channel leaks robustness (especially timings)

## NORX parameters and proposed instances

* word bit size (32 up to 64)
* parallelism degree (0 up to 255)
* number of rounds (1 up to 63)
* tag bit size (less then 10 words)

## NORX Mode

* "monkey duplex" construction (from SHA3)
* process header, payload and trail data in one pass
* data expansion via multirate padding: 10\*1
