# notes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/schedule/2.html) by [fefe](https://events.ccc.de/congress/2015/Fahrplan/schedule/2.html)
* how to fix this
    * just fix all bugs in the code
    * reduce code exposure
    * make exploitation harder
        * non executable stack
        * stack cookies, hardened heap
        * ASLR / PIE, ROP protection
        * ban dangerous apis and train devs
        * bug bounty
    * drop privileges, wear straitjacket
        * the less the code can do, the less the attacker can attach
* difference between "the code cando" and not "the code does"
* do not use services running as superuser
* common patterns
    * app drops privileges
    * privilege separation
    * admin confines app in jail, container or vm
    * app confines itself
    * access control via broker service
* idea: do privileged operation first, then drop privileges
* privilege separation
    * put dangerous part into separate process
    * confine that process as much as possible
    * e.g., make sure it can not open sockets or files
* admin confines app in jail, container or vm
    * think as firewall rules for syscalls
    * easy for simple process but that are not the ones we are looking for
    * nothing an admin or the distro guy can do this pretty well
* app confines itself
    * only gets to see small and maybe empty part of the filesystem
    * you can not open files or create sockets
    * no signals, no ptrace, no ioctl
    * but pretty hard for different plattforms
    * and not enough since firefox (for e.g.) needs signals, files and sockets
* access control via broker service
    * split app in "work horse" and "access controller" (broker)
    * work horse does not have filesystem access and can not create sockets
    * but has an open unix domain socket to broker
    * if the work horse needs something, it is asking the broker
    * the broker can do additional checks
    * make sure the work horse can not trick the broker
* dropping privileges in the old school way
    * process have to uids
    * the uid and the effective uid
    * if you are setuid root, you uid stays the same but the euid is 0
    * so dropping privileges is as easy as seteuid(getuid()), right?
    * nope, it is not
    * there is a third ui, the "save uid"
* but have we actually dropped privileges?
    * what if the dynamic linker is broken?
    * what if the codebase (command) you are using is broken (you are trusting a whole bunch of code)
* we want to limit access to
    * filesystem
    * system v ipc
    * other processes (e.g. signals)
    * sockets
    * routing table
* approaches
    * namespaces
        * put togehter a fake file system for your process
        * can also be used for uids and pids
    * prision and guard (aka jails)
        * unix checks permissions during open, not during writing
        * trick: disallow all open/socket operations but provide a broker that can do it fou you
    * descriptor passing
        * pretty complex and not save for work
* dropping privileges
    * filesystem
        * chroot
            * create empty, root owned, read only directory (like /var/jail)
            * a process in the chroot jail can still use sockets, send signals, debug etc.
            * linking dependencies into the jail (check if they can not be modified)
            * link /proc into the jail which exposes information from outside the jail
        * bsd secure level
            * root can increase securelevel and nobody can ever decrese it (only via reboot)
        * jail
            * pimped chroot
            * admin can allow
                * access to raw sockets or sysv ipc
                * mount or unmount jail friendly file systems
                * qouta administration
            * root in the jail is not the root
            * no namespaces for uids and pids
            * jails are not running their own init
            * admin can set resource limits and cpu sets to limit the peak
            * used to create containers and also to chroot processes or process groups
        * capsicum, cap_enter, tame, pledge
            * all with pretty cool ideas but with kludged api
        * linux capabilities
            * from the dark old times
            * lets split up the superuser powers
            * not really used
        * systrace
            * system wide profiles
            * other syscalls either raise gui alarm or get auto denied
            * lat updates in 2009
            * profile is either shipped or created by a training phase (where the process could be hacked already)
        * selinux and appamore
            * pimped systrace
        * seccomp mode 2
            * works and is pretty fast
            * but ugly as hell to write the rules
            * and can not inspect buffers
* but all is not working if there is a kernel bug
* in windows, it is really complicated (no namespace, no chroot - read the chromium sandbox documentation)
* summary
    * pretty good place in the functionality
    * fine grained lock down is possible
    * paranoid software authors can sacrifice performance to gain more security (trailblazer is openssh here)
    * use it in your own code since this is nothing an admin should do
