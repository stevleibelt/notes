# [2014-12-27 by Sebastian Schinzel](https://events.ccc.de/congress/2014/Fahrplan/events/5960.html)

# general

* lots and lots of ssl/tls bugs in the last few years
* talk is about to validate if a bug is still available this days
* how to fix a bug the protocol (and still keep the protocol valid)

# [bleichenbachers attacks](http://de.wikipedia.org/wiki/Kryptoanalyse#Known_Plaintext) works on all except ecc and diffie-hellmann-suites (in 1998)

## countermeasuers

* let us stick to PKCS#1 v.15 for compatibility
* unify error conditions (send simple one "the server makes a booboo" error message)

## current state

* still working
* bad thing, the longer the key size, the easier to break it (1024 is better than 4096 :-()
* proposed a fix for tls 1.2
* proposed a way to fix for tls 1.0 and tls 1.1 (a very performance fix)
* tried timing attacks (with patched MatrixSSL client)
    * language with no memory managed stuff inside like c, assembler
    * choose your part of the network wisel (no wireless, near as possible to target
    * disable power management ("cpufreq-utils", "cpu c states", "fix a process to a single core")
    * use old and cheap network interface (no interrupt coalescing)
    * stop all tasks and daemons on locale machine (no gui etc.)
    * skip the first hundereds measurements (they are in the "cache warming" time frame)
* OpenSSL 1.0.1i has implemented the proposed 1.0/1.1 way:
    * OpenSSL did PMS-checking very good
    * successful attack will take up to 50 to the power of 12

# summary

* timing attacks against single digit microseconds in TCP connections are practical (in local networks)
* bad designs in cryptographic protocols may taunt yo for decades to come (protocol is broken since more than a decade)
    * MAC-then encrypt (first decrypt, then check if its valid - a lot of code is running before checking)
    * RSA + PKCS#1 v1.5
    * ...
* implementing TLS is a minefield
