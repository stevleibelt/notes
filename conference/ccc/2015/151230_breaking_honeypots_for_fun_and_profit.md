# notes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/events/7277.html) by [deansysman](https://events.ccc.de/congress/2015/Fahrplan/speakers/6077.html), [gadi evron](https://events.ccc.de/congress/2015/Fahrplan/speakers/1342.html) and [itamar sher](https://events.ccc.de/congress/2015/Fahrplan/speakers/6384.html)
* available open source projects
    * [artillery](https://github.com/artillery)
        * returns random messages
        * blocks ips by package (so you can spoof the ip address)
    * [beartrap](https://github.com/chrisbdaemon/BearTrap/)
        * fakes an ftp
        * returns an empty 503 for anything else (easy to detect)
        * blocks ips by package (so you can spoof the ip address)
    * [honeyd](https://github.com/DataSoft/Honeyd)
    * [kippo](https://github.com/desaster/kippo)
        * ssh honeypot
        * collects forensic data on top of the detection
    * [dionaea](http://www.edgis-security.org/honeypot/dionaea/)
        * collects information about the tools the attacker uses
        * still easy to detect dionaea
        * tries to behave as real services by implementing the known exploits and to caputure the malware
    * [glastopf](http://glastopf.org/)
        * web application honeypot
        * more or less detectable by "this is a really great entry"
        * logs any kind of web interaction and gives alert if triggered
    * [kfsensor](http://www.keyfocus.net/kfsensor)
        * honeypot for windows
        * closed source
        * gives you a default web site that no one else has
        * blocks ips by package (so you can spoof the ip address)
    * [nova](https://github.com/DataSoft/Nova)
    * [conpot](http://conpot.org)
* scanning the internet with [zmap](https://zmap.io) to see honeypots deployed in the world
    * most honeypots are in taiwan, followed by united states of america and japan
    * most honeypots are deployed by taiwan isps
* [the modern honeynetwork](https://threatstream.github.io/mhn/) is a package to combine multiple honeypots
* professional attackers can still detect honeypots
* [research community](http://0x90.ninja)
* why not behave real machines act as honeypots? ;-)
