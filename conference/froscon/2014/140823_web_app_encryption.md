# [Didi Hoffman](http://programm.froscon.de/2014/events/1310.html)

# what is security

* if you get it wrong, it became really expensive
* security is always a tradeoff

# security is more about planing

* look at the stack and loot at threats
* look at the waht is valueable (data, code, files)
* look at how to mitigate this

# threats

## physical access fail

* if someone has physical access to your machine, it is compromised
* make sure your servers are at a secure location
* try to monitor your servers to detect suspects
* add protection to detect fiddling

## someone steals my hard drives

### mitigation

* most oses offer native hd encryption
* LUKS is super easy
* perfomance hit is near 0
* some problems at reboot
* this should be the default for ALL computers

### someone gets ssh on the server

* don't have user accounts on server (never have root open to ssh)
* user certificates
* use configuration management for chances (fabric, [salt](http://www.saltstack.com/), etc.)
* use fail2ban
* use kernel features to randomize memory / encrypt swap
* only allow ssh from certain ip addresses
* consider having honey pots but never on production machine and network

### somebody uploads "dangerous" files

* have different process serve media and static files
* [verify upload files](https://github.com/ahupp/python-magic)
* think of maximum file size as well as upload count (a user should never be allowed to upload more than n files)
* check file permissions and access
* check filename (unicode?)

### someone downloads files he should not

* use [private_media](https://github.com/RacingTadpole/django-private-media)
    * awesome tool to manage media files
    * loose some performance because of checks
    * uses ApacheXSendfileSecure

### AJAX is your enemy (in Django)

* a lot of useful security checks are not done with dajaxice
* performance is not the best
* afterthought in Django
* difficult to get right and secure

### someone breaks into my apache/nginx

* only use modules that you really need
* be really careful when configuring
* only use configuration management
* keep packages up to date (get professional support)

### someone can ead source files

* keep all security relevant information somewhere else
    * passwords
    * secret key
    * gitssh keys

# someone can write into my source file

* use tripwire
* use git diff
* check permissions

### someone can execute code

* once you have written a file change permission to read only
* in the database disallwo delete (or even update)
* have backup as extra process
* make your source file read only

### someone can modify / read your backup

* use extra process with different user
* use write only storage
* use encrypted storage and transmission
* signed it with your pgp key
* check certs of destination storage
* never through away backups

### someone can read your traffic

* always use https
* get a ca signed cert (snake-oil but people will expect it)

### someone can read your database

* now we work with db_tabke:{select}, etc.
* not very scalable and nice
* currently we overwrite "delete method"
* write data encrypted to db (use keyczar)
* write data encrypted to db (use keyczar)

## something new 

### postgreSQL front end

* learns queries from your test cases and user behaviour
* detects (first manual) variables
* notifies on unseen query
* assigns trust to every query
* can have handcrafted rules
    SELECT * FROM users => ERROR
    SELECT * FROM users WHERE users.name = 'foobar' => OK

### user does not trust you

* encrypt client side
* why would the user trust your javascript
* provide plugin to check javascript hash
* make plugin and javascript open source and serve from different sources
* many services do not thing about it
* try to deliver a hash from the expected javascript your user should get to increase trust

### otherwise it is all there (in Django)

* crose-site scripting (xss)
* sql injection
* cross-site request forgery

### you do not notice it

* have a central log (currently scp with munin)
* monitor your logs
* emails are not enough
* have error followups
* have notification propagation
