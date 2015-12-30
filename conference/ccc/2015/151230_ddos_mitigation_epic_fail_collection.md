# notes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/events/7523.html) by [dalmoz](https://events.ccc.de/congress/2015/Fahrplan/speakers/6257.html)
* method
    * we control our own botnet
    * we log each
    * two teams
        * red team on the customer and are just logging
        * blue team are the attackers
* run of the mill ddos attacks in the wild
    * rely heavily on the bandwith consumption
    * 53 percent of attacks are using less than two Gbps
    * most attacks does not require brains
* strike harder does not mean use a lager botnet
    * there is more to a web site than the front end
    * overload the backend to make the system work for you
    * keep it stealthy because they might use the "magic of sniffing" (use your own code to remove the general signatures the most ids are looking for)
    * think of amplification in a general way
* general amplification factores
    * network (the usual suspect)
    * cpu (very limited on some mediators and web application servers)
    * memory (volatie, everything uses it, multi-step operations is the prime target)
    * storage (can be filled up or exhausting the I/O buffer)
* facepalm from ten to one
    * 10 - limit the rate of incoming packets (you can and do not want to limit the outgoing packets since a simple get request could trigger a bigger file download)
    * 9 - it is ok now, monitoring shows everything is back to normal (had not accessed the site via a webbrowser)
    * 8 - backend servers are not important to protect against ddos
    * 7 - protect your domain by putting a "magic box" before all your servers (defense mechanism is training out all trafic first and do some magic afterwards)
    * 6 - we do not trust the vendor, we do not give them certificates (so https is not covered, lets to ssl renegotiation to put some load on the cpu)
    * 5 - we need big data, collect all the logs (logs need to be handled otherwise you get into a storage boom)
    * 4 - we are under attack - enforce the on-demand scrubbing service (have you started the learning mode? if so, cross the finger that the attacker is doing legitimate traffic)
    * 3 - so what cdn is not dynamic? lets enable it (not in the cache? ask the origin! which is hard to prevent since the request always comes from the cdn and you do not want to block them)
    * 2 - so lets protect the cdn by adding a highly unlikly strange name for the subdomain (lets scan the ip range or even easier, use WHOIS e.g. use http://viewdns.info and attack the real ip address directly)
    * 1 - block them ... now! (he blocked a "bigger" bunch of ips, meaning a whole /16 stack - around 116 M ip addresses, so lets send packets with strange ip addresses :-D - maybe by using its own address ^^)
