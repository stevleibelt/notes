# [2014-12-28 by ruedi](https://events.ccc.de/congress/2014/Fahrplan/events/6294.html)

# what is it all about?

* industry tries to sell us a new security model
* trusted computing is the selling phrase
* the industry takes care about updates
* windows 8 uses TPM (trusted platform module), currently on arm based systems
* even the public authority (BSI) thinks loud about the problem of trusting a profit oriented company like microsoft
* microsoft and its operation systems containing a lot of bugs
    * bugs can torpedo the tpm
    * microsoft reships updated fix again (please install the same bugfix again)
    * they even fucked up their update root certificate so no update is working anymore
    * certificate infrastructure totally broken
    * updates has to download and install manually
    * still no final fix
* with NSA and FBI (denies programs, capabilities or practices), we can not trust usa tech companies
* since hardware manufactures wanted to have the "ms windows 8 ready" logo, even open source software users having the tpm module inside

# enforces to trusted computing

* no "by default opt in"
* easy way to opt out
* cutting edge cryptography
* data privacy friendly cryptography
* international control and certification by creating the tpm module (since the keys in the tpm modules are static/not changeable)
* disclosure and certification from the tc relevant windows 8 source codes
* anti-trust legislation of microsoft

# alternatives

* alternative security architecture
    * replace tpm keys
    * open hardware
    * open software
    * smart cards with personal trusting anchor
* alternative transposition
    * european transposition (trust into the law)
    * european trusting architecture
* direct anonymous attestation ([DAA](http://en.wikipedia.org/wiki/Direct_Anonymous_Attestation))

# central question - who allows to boot what?

* microsoft defines what boots
* linux systems are booting by an emergency construction with a signature by microsoft
    * technical problematic
    * legal problematic
* the signatur for the emergancy construction is from microsoft
    * can be closed every time
