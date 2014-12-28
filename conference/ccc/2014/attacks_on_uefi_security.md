# [2014-12-28 by rafal wojtczuk and corey kallenberg](https://events.ccc.de/congress/2014/Fahrplan/events/6129.html)

* objectiv is to overwrite the chip holds the content of the uefi firware
* only software attacks against the firmware

# why bother?

* stack of privilege (from high to less)
    * bios
    * kernel (can be compromised by the bios)
    * application (can be compromised by the bios)
* the firmware can:
    * compromise the rest of the software stack
    * brick the plattform
    * survive os reinstallations
* ideal place for a rootkit

# features vs security

* the chipset provides features to
    * reprogram the contents of the firmware (uefi bios)
    * protect to firmware against arbitrary programming attemps
* its up to the oem to utilize [...]

# previous attacks

* complex memory corruption vulnerabilities
* required expensive and tedious testing to exploit
* unlikely to be exploited "in the wild"

# today attacks

* prevalent among UEFI and legacy BIOS systems
* result in reflash of firmware and/or SMM (system management mode) breakin
* straight forward enough to DIY, no exotic equipment neede

## multi-layered protection

* there are multiple layers of protection that prevent arbitrary flash programming attempts
* we will evaluate and then break through each layer in series
* layers
    * BIOS_CNTL
    * SMM (system management mode)
    * Protected Range Mask

### bios control registrer (BIOS_CNTL)

* write access to the flash is only possible if BIOSWE (bios write enable, R/WLO) is set
* setting BLE (bios lock enable, R/W) allows SMM to arbitrate writhe access to the flash
* lot of northbridge functions are pushed in the cpu today
* they found a race condition patch in BIOS_CNTL so you only need two cores to break this layer

### system management mode

* inspired by the misery of [darth venamis](http://starwars.wikia.com/wiki/Darth_Venamis)
* the bits that lock down SMM and the firmware are cleared during a reset
* "sleep"/"suspend" are typically implemented as an ACPI S3 sleep, which results in these lockdown bits being cleared
* S3 sleep = deep coma :-)
* during boot, the "platform configuration" is saved to a "boot script" so that s3 resume can happen more efficiently
* included in the boot script are the contents of registers involved in locking down the platform (such as TSEG and BIOS_CNTL)
* contents of the boot script were stored in ACPI NVS (unprotected) RAM on the consumer systems we looked at
* attacker can manipulate the boot script in the RAM
* pointer to the boot script can be dicovered by reading "AcpiGlobalVariable" (so simple point the pointer to the own boot script)
* there is a protection called "SMM lockbox" but it is currently only used on an UEFI development motherboard (and even this can be hooked)
* SMM is protected from non-SMM CPU access by SMM Range Registers (SMRR)
* SMM is protected from DMA (direct memory access triggerd by pci devices) by TSEG (TSEG is unlocked in boot script context)
* so we are able to disable TSEG by locking it to a value aboe SMRAM (FF000000)
* DMA code is very device specific, so we wait until context has returned to the os and then use a hard disk driver to initiate the DMA transaction on our behalf
* boot script format differs from manufactures

### protected range mask

* SMM is in the trusted area right now
* SMM can reflash the firmware by leveraging the normal firmware update path
* but an upcomming hardware feature will address this in the future
* a lot of systems do not even make use of protected range mask
