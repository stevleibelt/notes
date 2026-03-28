# notes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/events/7412.html) by [LaForge](https://events.ccc.de/congress/2015/Fahrplan/speakers/1757.html)
* open source in mobile communication (OpenBSC)
    * started about 16 years ago after proprietary implementations
    * today where linux is in 1994 / 1995 - capable but not taken seriously
    * still very small number of active developers
    * still very small capital
* umts architecture is pretty complex
    * 3g will be shutted down before 2g in europe
    * would be a waste of time to reimplement that bunch of strange ideas
    * the lower you get in umts, the more complex it gets
    * keep the lower level untouched (base stations, femto cells) and not start at the first level
    * umts was created with "the unified mobile telephone protocol aka >>the last word in mobile telephone protocol<<"
* uses ASN.1 syntax for defining protocol messages
    * IE is an information element
    * in an ideal world, you code use a ASN.1 code generator
    * in real world, it is not that easy
        * different encoding rules
        * no free software generator available that generates that special objects
        * hard to find example traces - no examples so far
* alternatives to the existing asn1c compiler
    * write all realted code in erlang, but no one is contributing to it
    * use propietary ASN.1 compiler
    * so it seems we have to stick with asn1c and extend it
* how to make asn1c work for luh
    * eurocom has a patch for adding APER support for asn1c
    * information object classes are hard
    * type prefixing
* we need volunteers now at [OpenBSC](http://openbsc.osmocom.org/)
