# [Thorsten Rinne](http://programm.froscon.de/2014/events/1442.html)

* team lead a company
* [speakerdeck](https://speakerdeck.com/thorsten)

# so you think you have seen everything

* daily frequent short crashes
* weekly long outages
* many million users per month
* 2.4 million lines of code of php and html
* on average, 3000 reads and 2000 writes per seconds, also on peaks
* mysql 4.1 and php 4.4.9
* 6 software developers
* 6000 tickets in mantis
* the ceo says "you do what i do"
* each engineed had its own room
* and a real phone ringing all the time
* no team leed
* ceo is no software architect
* support team was not allowed to talk to the engineers
* bi and metrics have been confidential (for ceo only)
* no version control
* application only runs on production machines
* the whole application was one monolithic monster
* each developer copied all files from production system onto his "development folder" on production
* changes where merged later manually
* used charset "win-1252"
* source code and media data distributed by nfs
* build in 2003
* two administration user interface (new and old one and both are used)
* accounting happened in oracle on debian 3.1
* all media files are on ine machine in one directory
* all servers are self assembled
* the hoster had the tendency to reboot the wrong machine

# lets talk about architecture

## master and slaves

* slave = frontend
* master = backend
* 2 masters and 14 slaves
* "optimizers" indexes and copies databases per file copy from master to slave
* indexing took up to 36 hours (for each change made in the "backend")
* mysql was patched
* search was built upon mysql full text search and uses myisam (with about 100 mio search terms)
* search for "black" took 45 seconds

## MyISAM

* cascading locks (full table locks)
* copy of db took about 12 hours (no updates at this time)
* file copy, so no migration to MySQL 5

# what has been done?

* delete mantis and started with jira and confluence
* started using github to a private repository
* starting with a clean and new wiki
* the config project
    * replace all hardcoded paths, ips etc to get the code running in a vm
* the deployment project
    * use capistrano for deployment to get rid of nfs instrastructure for the code
* both projects took up to seven month (while doing bugfixes and feature implementation)
* deleted duplicated code (decreased lines of code from 2.4 mio to 1.7 mio by using phpcpd)
* switched some tables from MyISAM to InnoDB
* removed nfs almost everywhere
* splitted code into a frontend, backend and inhouse repository
* frontend servers upgraded to php 5.3
* backend servers upgraded to php 5.3 (in total took four months)
* removed all useless features (log files checking, asking people if someone is using it, removed code and waited for months ;-))

# started writing new code

* changed architecture into SOA
* rewrote frontend with symfony2 and elasticsearch (took only three months, search query now at 45 ms)
* continuous integration with jenkins
* vagrant, virtual box and puppet
* new hoster
* all new projects built with symfony2
* tdd for all new code
* for some months ago, a slow migration is started of the old master codebase
    * composer support
    * monolog
* two from the six old developers are still there (now in total nine developers)
* now 500000 lines of code and up to 35000 reads per seconds in mysql (with peaks of 60000 read per seconds)

# architecture now

* three frontend servers covered by loadbalance
* elastic search
* old code is on new hardware and new operation system (debian 7)
* zend opcache
* percona 5.6
* mysql is master master replication
* added a middleware for the database that converts the 450 tables to below 50 in a smater way
* database changes are now around 60 seconds

# learnings

+ refactoring agile way, small steps with a lot of iterations
* scrum and kanban in parallel
    * kanban for new stuff
    * scrum for ongoing stuff
* delete old code and write it new
* removed a lot of useless features
* rewrite stuff that is completely broken
* startet with refactoring all the time (product owner supports that)
    * code reviews
    * added columns "reviewed" at there ticket system
* write tests (jasmine and phpunit)
* no consultants and it is doable
