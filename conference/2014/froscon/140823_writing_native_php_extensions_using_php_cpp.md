# [Emiel Bruijntjes](http://programm.froscon.de/2014/events/1437.html)

* copernica marketing software
* [author](http://bruijntjes.net/) of the [php-cpp library](http://www.php-cpp.com/)
* at [twitter](https://twitter.com/EmielBruijntjes)
* [slides](http://www.php-cpp.com/talks/mallorca/)

# why

* shows example of bubble sort in php and in native ("just removed the dollar sign")
    * cpp is faster
    * cpp takes a lot less memory (up to 20 times), you know the "memory_limit" is pushed as far as your machine can provide
    * your algorithms will also be accessible from other languages

# the php architecture

* php is implemented in c
* all built in functions are written in c
    * they are slow
* your code is written in php
    * this is slow by default

# php extensions

* luckily, php has a c api
* this api is not well documented

# the documentation

* Google (outdated and hugh howtos to write simple "hello world")
* Headfiles of zend
* The DateTime class
* "Extending and Ebedding PHP" by Sara Golemon

# conclusion

* we have a very large php code base
* and some parts could really benefit from having a native implementation
...

# changing the api

* many programmers think that writing in c/c++ is complicated
* but, there are many c/c++ libraries with a very good api
* even script-language libraries

# design choices

* writing a native php extension should be simple
* using straight forward plain c++ code
* complicated stuff should be encapsulated in simple classes
* the zend engine and ist headers files should be hidden
* php-cpp is a wrapper around zend
* it completely hides all the complicated zend stuff
* it is not as fast as native c extensions could be (because it hides complicated stuff)
* do not use it to past stuff back from php-cpp back to php

# hello world in php-cpp

    # Php::Value is the general value struct that can contain all types of content
    Php::Value hello_world()
    {
            return "hello world!";
    }

# classes

* its more complicated to write it in c with zend and it only works with the current php version (api changes are often in php/zend)
* the php-cpp class looks nearly the same as in php
* php-cpp supports all magic methods plus bonus functions like "__toInteger()", "__toBool()", "__toFloat()" and "__compare()" (also native zend functions)
* php-cpp supports magic interfaces (Countable, ArrayAccess, Serializable, Traversable)

# throwing exceptions

* fully implemented
* you can throw and catch exception in php-cpp to php and vice versa

# working with callbacks

* it is implemented :-)

# supported versions

* 5.3
* 5.4
* 5.5
* 5.6
