# notes

* [talk](https://events.ccc.de/congress/2015/Fahrplan/events/7130.html) by [netanel rubin](https://events.ccc.de/congress/2015/Fahrplan/speakers/5034.html)
* perl monks response
    * sad news from germany
    * heterogenous group of chaotic punks who love to see themselves in the hacker image of hollywood media
    * crude use of propaganda in the camel images
    * RTFM
    * you are using the old perl
* the new madness
    * function declarations cannot specify argument data types
    * because arguments are of unknow data type, functions contain code to handle multiple types
    * hashes and arrays are considered "secure" because they cannot be created by user input
    * bugzilla code contains many functions that can handle both, scalar and non-scalar argument types, so lets exploit it ;-)
    * a user can not create a hash data type in cgi
    * but bugzilla supports formats like json or xml
* now what?
    * unknonw argument type is bad
    * multiple code for multiple data types is bad
    * assuming non-scalar types as secure is very bad
* so we really cannot create hashes by the user?
    * list of scalars in CGI.PM
    * array of scalars in Catalyst
    * array of scalars in Mojolicious
* data what?
    * expecting arguments adata type is false
    * expecting secure hashes and arrays is false
    * expecting scalar user input is fals
    * so is expecting false in perl? ;-)
* the pinnacle
    * you can assign "file" as get parameter and as uploaded files
    * so param() returns now a list of all the parameter values
    * "<>" does not work with strings ... unless the string is "ARGV"
* put we want to execude code
    * lets look to open()
    * open() opens a file descreiptor to a given path unless the string contains "|" 
* but, he did not created that code on its own
    * he copied it from the official CGI.PM docs
