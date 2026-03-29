# notes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/events/7174.html) by [Florian Grunow](https://events.ccc.de/congress/2015/Fahrplan/speakers/3993.html) and [Niklaus Schiess](https://events.ccc.de/congress/2015/Fahrplan/speakers/6354.html) from [ernw](http://www.ernw.de]
* agenda
    * motivation
    * architecture
    * lifting the fox
    * conclusions
    * questions
* disclaimer
    * never visited DPRK
    * analyzed iso is found on the internet
    * it is not about making fin of them
    * no focus on security in this talk
* motiviation
    * the os has leakes at the end of 2014
    * no in-depth analysis yet available
    * the world should know what it is about
* architecture
    * operation system
        * desktop and server versions are available
        * fully featured general purpose desktop system based on kde
        * kernel 2.6.38.8 with a lot of self written kernel modules
        * developed by korean computer center (KCC)
        * SELinux with costum modules
        * iptables
        * snort
        * custom services
        * custom applications (also crypto tools)
    * additional components - lifting the fog
        * intcheck - integrity checking (maybe one of the main focus while creating this system)
            * a daemon that checks integrity of various (system related) files
            * configurable via system preferences
            * prints error messages when integrity checks fail
        * securityd
            * kind of mimics os x's securityd
                * includes various plugins
            * includes /usr/libos.so.0.0.0
                * provides a validate_os() function
                * integrity checking
                * hardcoded MD5 checksums
            * kdm also calls validate_os()
                * during startup
                * reboot loop if integrity checks fails
        * esig-cb
            * rtscan.ko
                * hooks several system calls
                * creates /dev/res
                * protects PIDs (even not root can kill it)
                * protects files (even not root can write them)
                * hides files (even not root can read them)
            * scnprc - the virus scanner
                * provides a gui that looks like a virus scaner (transparent for the user)
                * started by kdeinit
                * different ways to trigger scanning
                * loads rtscan.ko kernel module
                * starts opprc
                * pattern updating (hardcoded intranet ips)
                * can be used to delete malicious files (developer decides what is "malicious")
            * opprc - the evil twin
                * running in the background (not transparent for the user)
                * cannot be killed (protected pid)
                * shares a lot of code with scnprc
                * watermarks files (mostly when you open a file, maybe to track the origin of the file and each one who distributed this file)
        * completely disable custom components
            * get root (via rootsetting application)
            * kill securityd
            * kill intcheck
            * disable rtscan via ioctl
            * kill scnprc and opprc
            * replace /usr/lib/libos.so.0
            * delete /usr/share/autostart/scnprc.desktop
* conclusions
    * no backdoors?
        * maybe via updates
        * not included because of leaked isos
        * dprk changed a lot of code, maybe simple not found
    * self protecting system
        * integrity checking
        * system hardening
    * bad
        * "virus scanning" and watermarking
        * security issues like file permissions and custom code uses basic protections
    * guesses
        * preliminary tried to protect the system
        * built for home computers
        * they know backdoors are buillshit
        * [take a look](github.com/takeshixx/redstar-tools)
* questions

