# [ansible basic](http://programm.froscon.de/2015/events/1512.html)

by [oleg](oleg@fiksel.info) [fiksel](http://fiksel.info) from [CSP Inc.](http://www.cspi.com/)

# agenda

* about me
* introduction in automation management
* ansible
* end

# introduction

* goals
    * not a comparison between different configuration management systems
    * basic knowledge what it can and what not
    * first steps in ansible
    * examples
* why should I do it
    * easy -  configuration is consolidated versioned
    * repeatable - every machine looks like a twin of the other
    * scalable - from one to many
    * provisioning and configuration management

# ansible

* started 2012
* simple
    * YAML syntax
    * top down runtime scenario (no logic inside)
* agentless (ssh and python as only dependency)
* can be used as pssh (ansible -i 10.0.0.1, 10.0.2, all -m command -a `/bin/date`)  (run `/bin/date` on each machine)
* how to run a playboo? `ansible-playbook -i <inventory> <playbook>.yaml`
    * write a playbook that can run multiple times without chaning the final state of the system
* facts
    * are fetched from a host and exported as variables, which can be used in playbooks
    * can be turned off (`gather_facts: no`)
    * own facts can be created
* handlers
    * a handler is a well defined task
    * a handler is executed when notified
    * ansible validates the playbook and executes the handler only once (if needed) or as less as possible

# [best practice](https://docs.ansible.com/playbooks_best_practices.html)

```
stage                       #inventory file for stage environment
production                  #inventory file for production environment

group_vars/                 #assign variables to particular server groups
    group1
host_vars/                  #system specific variables
    hostname1

site.yaml                   #master playbookt
webserver.yaml              #playboot for webserver tier

roles/
    common/                 #this hierarchy represents a "role"
        tasks/
            main.yaml       #tasks file can include smaller files if warranted
        handler/
            main.yaml       #handler files
        templates/
            ntp.conf.j2     #files for use with the template resource templates end in .j2
        files/
            my_script.sh    #script files for use with the script resource
        vars/
            main.yaml       #variables associated with this role
        defaults/
            main.yaml       #default lower priority variables for the role
        meta/
            main.yaml       #role dependencies
    monitoring/             #same kind of the structure like for common
        ...
```

# examples

## add line to hosts

```
#not perfect since dependend on whitespaces
ansible -i test-node, all -m lineinfile -a `dest=/etc/hosts line="192.168.0.1 test-node"`
```

```
#also not perfect, you can work with templates
#bades about this solution, `/etc/hosts` is empty for a short periode of time
---
- hosts: all
  tasks:
  - name: clean up /etc/hosts
    linefile: dest=/etc/hosts regexp=192\.168\.0 state=absent
  - name: add new /etc/hosts entry
    linefile: dest=/etc/hosts line="192.168.0.1 test-node"
```

## fetch all facts from a host


```
ansible hostname -m setup
#or
ansible -i hostname, all -m setup
```

## example for handlers

```
---
- hosts: webserver
  handlers:
  - name: restart apache
    service: name=httpd state=restarted
  tasks:
  - name: ensure apache is at the latest version
    yum: name=httpd state=latest
  - name: write apaceh configuration file
    template: src=/srv/httpd.j2 dest=/etc/httpd.conf
    notifiy:
    - restart apache
  - name: ensure apache is running
    service: name=httpd state=started enabled=yes
```

# summary

* try ansible
* read documentation
* read other playbooks
* think on playbook idempotence
* split big playbooks into roles
* roleback is not part of ansible
    * try it on stage system
    * try to update only some per time
* use a jumphost server to easy up secutry issue
    * [wikipedia](https://en.wikipedia.org/wiki/Jump_Server)
    * [gentoo](https://wiki.gentoo.org/wiki/SSH_jump_host)
    * [searchengine query](https://duckduckgo.com/?q=jumphost)

# links

* https://docs.ansible.com/
* https://wiki.archlinux.org/index.php/Ansible
* http://rundeck.org/ (self service portal for ansible, alternative for ansible tower)
* https://www.thoughtworks.com/products/go-pipeline-visibility (self service portal for ansible, alternative for ansible tower)
