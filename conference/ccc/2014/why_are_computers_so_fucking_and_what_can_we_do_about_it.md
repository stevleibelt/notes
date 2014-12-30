# [2014-12-30 by Peter Sewell](https://events.ccc.de/congress/2014/Fahrplan/events/6574.html)

# what to know about computers?

* there are a lot
* they get wrong
* you have one line with wrong code insode

# why pcs are more tricky than steam engines

* [too much code](http://www.informationisbeautiful.net)
* to much legacy complexity
* computer are not built by
    * smart people
    * in big groups
    * subject to commercial and open source pressures
    * using the best components available
    * and for course with the best management
* how do we build software
    * specify in prose
    * write code
    * write some ad hoc tests
    * test and fix (in an undefined number of loops)
* to many
    * execution paths
    * states
    * possible inputs
* too discrete,  change one bit and everything is screwed up

# what to do?

* better "software enginerring" (more unit tests, assertions, better coordination ... but it is not making a big change)
* use 1970 languages instead of 1960 languages in 2014
    * expressive type systems
    * guarantees of type- and memory-safety
    * enforcment of abstraction boundaries
    * user-defined inductive types, pattern, matching, functions and stuff
* use languages that have been designed
    * syntax (BNF grammers)
    * behaviour (operational semantics)
    * typing (type systems and inference)
* prove correctness
    * CompCert
    * CompCertTSO
    * CakeML
    * Vellvm
    * RockSalt
    * setL4
    * Crypto protocols
    * prove?
        * programmer
            * test a couple of examples
            * it compiled
        * program analysis
            * run approximate analysis tool
        * scientist
            * do careful controlled experiments
        * mathematican
            * write careful mathematical argument to convince a human
        * honest program proof
            * the machine checked proof in tool with small TCB
            * Coq, HOL4 etc.
            * but it is hard
* soecify and test behaviour of key interfaces
    * x86, ARM, IBM POWER
    * TCP and Sockets API
    * C/C++11
    * OCaml core language
    * C language
    * ELF

# architectural fiction

* you can not write software that covers all special cases how hardware (and legacy hardware) is acting (because of speed optimisation)

# empirical science to the rescue

* invent mathematically prices model of multiprocessor behaviour
* make tool to find all model-allowed behaviour of tests
* compare against experimental data from production
* discuss with architects
* prove correctness of C/C++
* goto 1

# rocket sicne?

* specifying the inteded behaviour of a system
* in some precise and clear language
* in a form that is "executable as test oracle"
* design your protocols for testing

# recap

* use better programming languages
* make real specifications of key abstractions
* full-on formal verification of key components
* not appropriate for everything but for the key infrastructure
