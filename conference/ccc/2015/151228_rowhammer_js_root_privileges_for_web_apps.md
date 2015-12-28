# notes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/events/7197.html) by [clementine maurice](https://events.ccc.de/congress/2015/Fahrplan/speakers/5943.html) and [daniel gruss](https://events.ccc.de/congress/2015/Fahrplan/speakers/6293.html)
* june 2014, first flipping was available by using clflush
* july 2015, first flipping was available without using clflush by them both
* "rowhammer is like breaking into an appartment by repeatedly slamming a neighbor's door until the vibrations open the door you were after" - Motherboard Vice
* only non-cached accesses reach DRAM
* original attacks use clflush instruction
    * flush line from cache
    * next access will be served from the DRAM
* rowhammer attack with the clflush
    * until the bit flips
    * reload and flush the two banks around the bank containing the bit you want to flip
    * how to measure if you hit a cache?
        * measure timing (cache hit vs. miss)
        * run on shared libraries to spy on other processes (since someone else has loaded the data into the cache)
        * automated attacks
* rowhammer attack without clflush (to be independent of specific instructions)
    * use regular memory access for evication
    * <missing point>
    * what is complicated
        * how to get access to the physical address
            * fixed map from physical addresses to DRAM cells
            * undocumented for intel
            * reverse-engineering by Seaborn for Sandy Bridge
            * and by them for Sandy Bridge and others
            * OS optimization and use 2 MB pages
                * last 21 bits (2MB) of physical address
                * = last 21 bits (2MB) of virtual address
                * = last 21 bits (2MB) of JS array indices
                * several DRAM rows per 2MD page
                * several congruent addresses per 2MD page
        * which physical address to access?
            * function H that maps slices is undocumented
            * use LRU replacement policy (replace oldest first)
            * on newer CPU's LRU replacement is more randomized, so it is not useable anymore
            * cache eviction strategy by accessing "1, 2, 1, 2, 2, 3, 2, 3, 4 ..." which is 99 percente accurate
        * how to get accurate timing in JavaScript?
            * native code with "rdtsc"
            * JavaScript "window.performance.now()"
            * recent patch by rounding the time by five microseconds
            * but this does not influences the rowhammering
* how to build exploits?
    * port root exploit by mike seaborn to JavaScript
        * page table spraying
        * needs shared memory which is not available in JavaScript
        * but we have deduplicated zero pages so this is some kind of shared memory in JavaScript
    * physical memory access exploit in JavaScript
        * find exploitable bitflip (address and writable bit=
        * release btflip page
        * <missing points>
        * is is possible but it is not that easy to flip a bit
* countermeasures
    * patch hardware and implement dynamic row refreshing
        * not doable on legacy hardware
    * patch the bios by increasing refresh rate
        * might not be sufficient for all machines
        * needs a bios update, who does that?
    * patch the os
        * not prevent bit flipping for memory of the same process
        * but prevent flipping for different privileged physical memory pools
* conclusions
    * cache eciction fast enough to replace clflush
    * independent of programming language and available instructions
    * hardware-fault attack induced in JavaScript
    * remote attacks through websites
    * so maybe in the future, there will be a rowhammer.js framework
