# nodes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/events/7195.html) by [cornelius diekmann](https://events.ccc.de/congress/2015/Fahrplan/speakers/4862.html) (his [github account](https://github.com/diekmann)
* free as in freedom and open source firewalls are not the issue
* the issue came from the rule sets
    * "there are no good high-complexity rule sets"
    * "firewalls are (still) poorly configured"
    * tools do not understand real-world firewall rules
* specification
    * documentation
    * what is a correct ruleset
    * goal is spoofing protection (based on the model of iptables)
* implementation
    * code, too
    * performance
* [isabelle](http://isabelle.in.tum.de)
    * has defined syntax
    * and expression
    * since we can verify the behaviour of the firewall has not changed, we can
        * unfold complex rulesets into simple boolean expressions
        * replace function jumping by simple top to bottom processing
        * get a compressed graphic about the ruleset (and find bugs)
