# notes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/events/7288.html) by [J. Alex Halderman](https://events.ccc.de/congress/2015/Fahrplan/speakers/4228.html) and [Nadja Heniner](https://events.ccc.de/congress/2015/Fahrplan/speakers/3547.html)
* work is a joint work
* thanks to snowden, we know that the nsa is breaking the crypto
* we have to figure out who the nsa is breaking the crypto
* try to attack the underlying crypto
* breaking rsa by factoring with the number field sieve
    * how long does it take to factor using the number field sieve?
        * 512-bit RSA less than four hours on EC2
        * 768-bit RSA around 1000 core years which is less than one calendar year
        * 1024-bit RSA around 1 million core years
        * 2048-bit RSA minimum recommended key size today
* "[new directions in cryptography](https://www.cs.jhu.edu/~rubin/courses/sp03/papers/diffie.hellman.pdf)" paper of diffe and hellman says as introduction "We stand today on the brink of a revolution in cryptography"
* this provides perfect forward security as long as both would create new random key for each message
* but, we war wrong when we told you diffiehellman is way better than rsa
* the problem is, you can use the numbre field sieve discrete log algorithm
    * which takes as long as it takes for rsa
    * how long does it take to factor using the number field sieve?
        * 512-bit DH around 10 core years
        * 768-bit DH around 35k core years
        * 1024-bit DH 45 million core years
        * 2048-bit DH minimum recommended key size today
* but what if you want to break many connections that use the same public parameter?
    * you can split the algorithm into two parts
    * the second one is the easier one
    * how long does it take to factor using the number field sieve? - oh, shit
        * 512-bit DH around 10 core minutes
        * 768-bit DH around 35k core days
        * 1024-bit DH 30 core-days
* exploiting diffie hellman
    * [logjam](https://en.wikipedia.org/wiki/Logjam_%28computer_security%29) attack
        * anyone can use HTTPS backdoors from '90s crypto wat to pwn modern browsers
        * it was forbidden by law to export a key length greater 56 bits outside of the usa
        * the server sends a list of supported cipher suites and the client uses this cipher suites
        * used by 
            * FREAK attack for RSA
            * logjam attack for DH
                * active downgrade attack to export diffie hellman with a 512 bit prime number
                * the attacker is a man in the middle and modifies the messages by breaking the 512 bit key
* how widely shared are diffie hellman public parameters?
    * 97 percent of hosts that support DHE_EXPORT chose one of three 512 bit primes:
        * 80 percent apache 2.2
        * 13 percent mode_ssl
        * 4 percent JDK
    * 90 percent of all are using this few primes
* attacking the most common 512 bit primes
    * with an optimized version, it takes around 70 seconds of 80 percent of the top pages from alexa
* logjam mitigation
    * major browsers have raised minimum dh length to 1024 or 768 (safari)
    * TLS 1.3 draft includes an anti-downgrade flag in client random
    * move to elliptic curve cryptography
    * use 2048 bit primes
* mass surveillance
    * goverments can exploit 1024 bit discrete log for wide range
    * if you special purpose hardware, you can get up to 80 percent speedup
* is the nsa doing this? (assumptions/conspiricy)
    * "the nsa mage an enormous breakthrough eseveral years ago"
    * "everybody is a target"
    * "this computing breakthrough was going to vie them the ability to crack current public encryption"
    * and they have the big "black budget"
    * the nsa can decrypt passivly vpn traffic
