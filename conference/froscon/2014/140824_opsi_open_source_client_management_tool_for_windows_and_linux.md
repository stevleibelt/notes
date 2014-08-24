# [Detlef Oertel](http://programm.froscon.de/2014/events/1344.html)

# what is opsi

* client management tool for windows and linux based on linux server
* automatic os installation
* automatic software distribution
* categorize and fetch installed hard- and software
* a lot of extensions
* supported clients
    * windows xp up to windows 8.1 or server 2003 to 2012
    * linux most common (debian, ubuntu, opensuse, sles, centos, fedora, redhat)

# core functionalities

* file patching
* logging

## windows

* starte a linux based boot image or use pxe
* installation in an unattended way
    * support for adding drivers for pci, usb, hd audio
    * installation of opsi-client-agent
* or use an image installation

## windows

* boot opsi-linux-bootimage by pxe od cd
* install minimum system with network and ssh (no x11)
* install client agent im no gui modus

## opsi client agent and software distribution

* do stuff in admin context
* install stuff
* configure stuff

### general way

* client start after boot and before login
* access to central configuration via encrypted webservice
* script based installation via opsi-script
* finally, giving access to login

### or

* event based
* start at login
* start at network startup
* timebased
* push installation
* start at shutdown

# technology

* management gui
* opsi client agent
* opsi linux bootimage
* opsi admin (command line)
* opsi webservice
* information stored at files or in MySQL
* network boot products for operation system installation
* local boot products for software
* windows and linux client commands are compatible to each others

# uefi support (the shit nobody wants but industry sells it, my two cents ...)

## in the sense of

* fixed both (uefi/mbr)
* uefi only with csm
* uefi only

## whats important for the opsi context

* new and still in changeable mood
* bios defines the bit (32 or 64)
* gpt partition
* secure boot (not supported yet)
* no real "trennung" between bios and or in sense of "ordering of booting"

# how they earn money

* new extensions are for money only
* as long as the return of investment is reached
* than it goes to lgpl and fully fledged open source
* but, money is still needed to support the ongoing envolving
