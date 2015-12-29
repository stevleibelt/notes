# notes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/events/7255.html) by [zakir durumeic](https://events.ccc.de/congress/2015/Fahrplan/speakers/5006.html)
* [SMTP](https://en.wikipedia.org/wiki/Simple_Mail_Transfer_Protocol)  was not build with security in mind
* we simple added encryption afterwards
* by the rfc, a server may not support STARTTLS
* not like in HTTPS, it is unclear what name should go on the certificate
* so we started trusting each certificate that exist
* email is still a fragile ecosystem
* even top email providers are using strange ciphers or generic certificates (matching more than the mx server nor matching the domain)
* currently, only ms exchange support STARTTLS out of the box
* STARTTLS protects against passive eavesdropping, nothing else
* take a look to the [slides](slides/7255_paper.pdf) to see how easy it is to do a man in the middle attack to force client and server speaking cleartest
* lying DSN sever (also have a look into the [slides](slides/7255_paper.pdf)
* authenticating email
    * sender policy framework (SPF)
        * sender publishes a dns record that specifies what servers can send mail for the domain
        * recipient looks up senders SPF and checks if the message was sent from the valid hosts
    * domainkeys identified mail (DKIM)
        * sender publishes a public key in the dns record
        * sender attaches signature in the messages headers
        * recipient looks up the key and checks the message signature
    * domain message authentication, reporting and conformence (DMRRC)
        * sender publishes a mail policx in the dns record
        * recipient checks the senders policy
* moving forward
    * SMTP Strict Transport Security (like HTTPS HSTS key pinning)
    * Authenticated Received Chain (ARC) (replacement for DKIM that handles mailing lists)
* conclusion
    * mail community started deploying new security extensions
    * but progress is slow on many organizations
    * since not each suppots encryption, it is only a nice to have
    * STARTTLS is not a long-term solution anymore
    * a lot of work has to be done
