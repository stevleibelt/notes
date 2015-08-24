# [towards a server-less web](http://programm.froscon.de/2015/events/1627.html)

by [Max Jonas Werner](https://blog.makk.es/)
[video](http://media.ccc.de/browse/conferences/froscon/2015/froscon2015-1627-towards_a_server-less_web.html)

# current

## two options how to transfere informations

* do it on your own (doable only with lots of knowledge)
* let someone else do it (by loosing control over your data)

## networking in browsers

| - | asynchronious | architecture | communication |
| HTTP | no | client/serve | unidirectional |
| Server-Sent Events | yes | client/server | unidirectional |
| WebSocekt | yes | client/server | bidirectional |
| WebRTC | yes | pear/peer | bidirectional |

# wished

* take back control
* by using WebRTC (Web Real Time Communication)
    * multiple definition exists
    * it is a 
        * project
        * web api
        * web communcation standard

# this is WebRTC

* enables direct communication between web browsers
* nat traversal
* no intermediary server necessary
* secure rtp for audio and video data
* sctp over dtls for generic data
* signaling via sdp offer and answer
* optional source autentication (it is there but not used yet)
* how to fetch the address of the other peer (signaling) is explicity not part of this standard

# [BOPlish](https://github.com/boplish)

## what do we need?

* routing of data
* concret names and name resolution
* simple api

# use case - document sharing

* you have uploaded the file into your web storage
* uri: bop://max@example.org/document/family.png?csum=sha256:a23d...

## recap and outlook

* boplish provides a framework for distributed content communities
* it is as simple as pulling in boplish.js
* WebRTC is cumbersome at times
* todo 
    * mobility
    * content offloading
    * networkt/P2P stability
    * security
