# notes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/events/7352.html) by [joanna rutkowska](https://events.ccc.de/congress/2015/Fahrplan/speakers/6124.html) from [invisible things lab](http://invisiblethingslab.com)
* pcs are extensions of our brain 
* and as the brains, full of failurs and not trustworthy
* trust means
    * trusted (can be compromised, is not secure)
    * secure (resistent against attacks)
    * trustworthy
* stack of trust
    * applications
        * gnupg
        * tor
        * pond
        * ssh
        * openvpn
        * luks
    * operation system
        * qubes os
        * tails
        * gnode
        * subgraph 0s
        * grsecurity
    * hardware
* whats wrong with intel x86 laptops today
    * totaly integrated into one bunch of silicon
    * but not the 
        * spi (beacause of boot security or malicious peripherals?) 
        * "management engine" (which is infact a backdooring or rootkiting infrastructure and "zombification")
* currently tpm, txt, uefi secure bios can not fix the issue of not trusting hte boot process
* currently, everyone can write code for the hardware
* intel wants to change this that
* currently, intel me is not able to disable
* how to solve this issue (or at least make it harder a bit)?
    * by a trusted stick
    * firmware (me, bios, fsp) and system (/boot, /) are read only
    * private key
    * optional internal disk
        * r/o protection for system partitions
        * encryption for users partitions
        * trusted firmware
