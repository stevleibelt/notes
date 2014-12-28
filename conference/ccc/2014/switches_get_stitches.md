# [2014-12-28 by Eireann Leverett](https://events.ccc.de/congress/2014/Fahrplan/events/6196.html)

* [slides](https://events.ccc.de/congress/2014/Fahrplan/system/attachments/2509/original/SwitchesGetStitches.pdf)

## default pitfalls

* session cookie hash is the current ip address (extended with uptime)
* firmware can be uploaded is sometimes just one unauthenticated HTTP request (CSRF)
    * including configuration
    * including password
* firmware can be downloaded the same way
* also on personal section, firmwares are alive for more then three months
* regular patch times in ICS/SCADA is between 12 and 18 months (currently siemens is really quick with a reaction time below 3 months)
* [SCADA](http://en.wikipedia.org/wiki/SCADA) needs your help in industrial systems 
* ICS systems typically have very, very serious uptime requirements (a DoS can be a show stopper/critical problem)
* web admin session is running on a HTTPS session, but firmware upgrade happens over FTP or TFTP (unsecure, firmware file is uploaded in clear text)
* use tools like "binwalk" or "file" (as example for "pcap"), search for zlib parts in the binary, "cut" and uncompress them with "dd" and "gzip -dc"
* grep for bugs (hex string) on binaries
* do not use default keys
* fix problems for XSS, DOS attachs
* do not use wak excuses like "Sorry, product reached end of life" for infrastructure critical system
* so, as owner of the hardware, try to buy the code to fix the problem on your side
* if you generate the keys on the client side, use secure connection (prefent man in the middle attack)
* what about patch own keys in?
    * generate key with same size of known password
    * slice and insert the key into the binary
    * is there a crc check?
    * why not patch the crc check also
* current way is to take the old insecure and buggy protocol and wrapp them with ssl/tls (which is also broken as we know)
    * do not use cleartext passwords under ssl
    * enable ssh with a password
