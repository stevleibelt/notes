# notes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/events/7528.html) by [roland bracewell shoemaker](https://events.ccc.de/congress/2015/Fahrplan/speakers/6259.html)
* in april 1995, netscape drafted SSL/TLS
* [lets encrypt](https://github.com/letsencrypt)
    * free and open source as well as automated and transparent CA
    * based on standardized protocol for domain validation, certificate issuance and management (ACME)
    * already public and widely trusted
    * needed a bunch of money with big sponsored budget
* the rule makers
    * self governing body composed of trusted CA's and major browser vendors (5 browsers and around 45 CAs)
    * validation levels (technically no differences between this levels)
        * domain
        * organization (more complicated)
        * extendedn (most complicated)
* where does lets encrypt fit in
    * zero cost for issuance, renewal and revocation (and everything else)
    * DV only, no plans for EV or OV
    * maximum periods of validity is 90 days
    * multiple domain certificates using SANs
    * issuing from intermediate cross-signed by IdenTrust
* timeline
    * closed beta unti from 01.09.2015 to 03.12.2015
    * until today, they have issued over 200k certificates across 440k DNS name
    * already the fifth largest certificate authorithy (CA)
    * over 120k individual registrations
    * 2 certificates per registration
    * around one percent ot revocations so far
* why
    * rails the total number of connections going over HTTPS
    * get hosting providers and CDNs to use lets encrypt
* future
    * DNS based validation challenge
    * proof of possession challenge
    * multi-path validation
