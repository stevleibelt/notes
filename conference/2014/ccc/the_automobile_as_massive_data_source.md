# [2014-12-28 by Jimmy Schulz and Dr. Rüdiger Hanig](https://events.ccc.de/congress/2014/Fahrplan/events/6265.html)

* [slides](https://events.ccc.de/congress/2014/Fahrplan/system/attachments/2515/original/31C3_V1.0.pdf)
* by [load-ev](http://www.load-ev.de/) and [gurillia](http://www.gurillia.de)
* vw's leader says "your data is mine"

# agenda

* ODB2
* stakeholder
* data retention
* help?

# the ODB2 interface

* ecu
* ODB2
* can-bus
* on board navigation ...
* all datas are measured
* in granularity, length and structure depending on the size of memory
* simple data
    * pace
    * fuel level
    * gps coordinates
    * acceleration
    * rpm
    * ...
* attacks (successful)
    * wired ODB2 interface
    * installed wireles interfaces (wifi, bluetooth)

# stakeholder

* a leasing company is very interested in the way how you drive a car
* government is wants to know (because of tax affairs)
* car sharing (current position and status of gas etc. are transmitted permanently)
* car rental
* the police if you are involved in a crash
* the hospital if you are involved in a crash
* the lawyer if you are involved in a crash
* car insurance if you are involved in a crash
* vda (Verband der Automobilindustrie) created some principles
* classification of car data stakeholders
    * manufacture
    * maintaner
    * service

## example

* assistance by a automobile association (like adac)
* small repairs / transport to garage or replacment the vehicles based on data from the car
* so they are requested to car related data (ECU and ODB2) / malfunctions / access to change data by an interface

# data retention / big brother in the car?

## what data is stored

* car related data (milage, malfunction, speed)
* personal related data (location, time and dates)
* even more personal data (phone calls, address book, music playlist)

## who else has access to your data

* if you are using a rental car, the company or nearby everyone (the company, the garage ...)
* unless you control the data, everyone with access owns your data
* your gara, your car manufacture, your automobile
* mobile devices and all apps running on that devices

## where is the data stored?

* in the car (unknown duration and structure)
* the computer centers of your car manufacture (tending to use cloud services)
* in your garage (car related, service related and personal related data)
* in the computer centers of google, microsoft, apple based on your mobile phone

# what would help?

* awareness
* open interfaces and standards
* encryption (access keys) of all data starting in the car
* transparancy (which data is stored where for how long and for what reason and can be accessd by who?)
* data privacy declaration in simple speach
