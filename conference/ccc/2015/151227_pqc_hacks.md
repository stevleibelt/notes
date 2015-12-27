# notes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/events/7210.html) by [djb](https://events.ccc.de/congress/2015/Fahrplan/speakers/3538.html) and [tanja lange](https://events.ccc.de/congress/2015/Fahrplan/speakers/3714.html)
* D-Wave quantum computer is not universal
    * can not store stable qubits
    * can not perform basic qubit operations
    * can not run shors algoritm
    * can not run other quantum algorithms we care about
    * has not managed to find any computation justifying its price
* but quantum computers are coming and are scary
    * [massive research efforts done](https://en.wikipedia.org/wiki/Timeline_of_quantum_computing)
    * IBM says "we are there in 10 or 15 years"
    * ... that is, 2022 or 2027
    * shors algoritm solves in polynomial time
        * RSA is dead
        * DSA is dead
        * ECDSA is dead
    * this breaks all current public key crypthography on the internet
    * also grovers algorithm speeds up brote-force searches
    * AES-128 and AES-256 are broken in an "ok" time
* countermeasures
    * physical cryptographe
        * very limited functionality
        * easy to screw up
        * easy to backdoor
        * hard to audit
    * but there is hope
        * initial recommendation (see slides)
        * maybe hash based systen helps
        * signatures is something quantum computers can not do very well
        * error correction (parity checks with matrix)
* it is urgent
    * todays encrypted communucation is stored by attackers
    * in can be decrypted years later
    * if you got rich, important or something else, you might be fucked up
* links
    * [pqcrypto.org](https://pqcrypto.org)
    * [pqcrypto.eu.org](https://pqcrypto.eu.org)
