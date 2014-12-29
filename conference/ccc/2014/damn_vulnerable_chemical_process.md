# [2014-12-29 by Marmusha](https://events.ccc.de/congress/2014/Fahrplan/events/6463.html)

* cyber physical systems are it systems "embedded" in an application in the physical world
* simulation models are expensive (you can not simple build a staging system and destroy it ... unless you have a lot of money)

# damn vunerable chemical process

* contains two models
    * tennessee eastman (TE) chemical process - good for black box research
    * vinyl acetat monomer (VAM) process - more complex 
* process is written in c-code and free
* the execution is happening in matlab/simulink :-(
* currently on [github](https://github.com/satejnik)

# typical understanding SCADA hacking

* obtaining access != obtaining control
* breaking into system != breaking the system

# attack objective

* equipment damage
    * overstress equipment
    * violation of safety limits
* production damage
    * product quality and product rate
    * operatiing costs
    * maintenance efforts
* compliance violation
    * safety
    * pollution
    * contractual agreements

# process related properties

* first, find the controlling units
* second, know the timeframe (how long does it takes until my changes takes effects)

## break attack

* try to attack the water hammer candidates (steam, cooling, valves)

## production damage

* chemical supply pipes
* cooling system

## compliance violation

* open the valve
* stange stuff in emission controll

# attack stages of a SCADA attack

* access (traditional hacking)
* discovery (each unit is different)
    * what and how the process is producing
    * how is it controlled
    * how is it build and wired
* control
    * how do i have to change what to achive which goal
* damage
    * what can be manipulated
* cleanup
    * how to hide me
        * "record and play back" of default model
        * derive process model
        * crafted sensor signals (feed in your generated signals, hide your actions in believable noise)
    * what will they tink happend

# scenario - catalyst deactiviation

* maximum economic damage
    * simple destroy the pipe where the final product pops out
    * kill the catalyst
* instead of DoS attack a system down, you need to read an manipulate the process data (which takes some time)
* physical environment is a communication media
* "unseen state" of the other component may have "hidden impact" ("weird machines" by sergey bratus)
