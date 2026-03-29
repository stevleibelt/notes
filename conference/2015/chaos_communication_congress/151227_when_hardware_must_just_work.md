# notes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/events/7171.html) by [david kaplan](https://events.ccc.de/congress/2015/Fahrplan/speakers/5921.html)
* what is a testbench
    * generate stimulus
    * apply stimulus to design being verified (DBV)
    * capture the response
    * check for correctness
    * coverage analysis: hit/analyze 100% as defined as functions
* testbench speed
    * system level testing (~ 1HZ) - pretty slow
    * core level testing (~ 10 HZ)
    * multi-unit level testing (~ 50HZ)
    * unit level testing (~ 100 HZ)
    * actual silicon (~ 3 GHZ)
* what is hard to test / errors are not found
    * system level behaviour
        * protocol violations
        * FIFO overruns/underruns
    * multiple random events
        * 5 unlikely asyncrhonous events in a row
    * long runtime events
    * statistically unlikely matches
        * multiple loads where 20 address bits match
* what happened?
    * modern cpus support JTAG
    * JTAG hardware implements various commands
* what if the cpu hungs
    * scan!
    * scan enables reading all flip-flop state in the cpu (like crash dump)
    * flops are chained together to enable shifting out data through the JTAG port
    * limitations
        * only get data in flops
        * only from a single point in time
        * interesting information may be long gone
* so how to fix this problem?
    * costly solutions
        * maybe respin the silicon
        * base layer
        * metal layer
        * often extra gates will be built ins
    * less costly solutions
        * disable bits for risky features
        * typically used for performance or power enhancements
        * microcode patch
            * modern x86 cpus use microcode to implement more complex functionality such as
                * complex x86 instructions
                * interrupt delivery
                * power management
            * microcode is built into the silicon, but a patch RAM exists
                * can be used to replace/supplement existing microcode to fix bugs
                * limited in size and capability
* a little note on security
    * do you really know who is using your debug interfaces?
    * debug interface security should always be considered and tested
    * typical solutions
        * disable some or all JTAG commands
        * ensure debug access to sensitive information is blocked in production
        * require authentication to use a debug interface
        * require signed CPU microcode updates
* further resources
    * see the [slides](https://events.ccc.de/congress/2015/Fahrplan/system/event_attachments/attachments/000/002/801/original/When_HW_must_just_work_--_FINAL.pdf)
