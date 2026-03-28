# [A CouchDB replication endpoint in PHP](http://talks.qafoo.com)

by Kore

## Why / Use Cases?

* sometimes no internet
* couchdb has a multi master setup protocol
    * but sometimes you need more
        * do more before putting stuff into the couchdb
        * adapt data before syncing to mobile
    * make your (php) application offline capable
    * replicate your MySQL Database into a CouchDB and vice versa

## Is there anything out there?

### Client

* pouchDb
* Hood.ie
* TouchDb

### Server

* Apache CouchDB
* Cloudant
* PouchDB Server
* Replipy (Python)

### Replicator

* Replicate (JavaScript)
* Replipy (Python)

## The Replication Protocol

* "multiple source of truth" instead of "[single source of truth](https://en.wikipedia.org/wiki/Single_Source_of_Truth)"
* using http

## Steps of Implementation

* figrue out how current protocol is implemented (by using networktool like [mitmdump](http://mitmproxy.org/doc/mitmdump.html))
* replay integration tests against own endpoint
* replace dates and random ids in [requets and responses](https://github.com/Kagency/http-replay)
* fix failurs
* understand and refactor and document
* using symfony as http framework
    * all logic implemented in framework agnostic controllers / services or repositories
* using a repository to store information with any backend
    * currently only an in-memory backend is actively used / tested
* [couchdb-endpoint](https://github.com/Kagency/couchdb-endpoint)
* still work in progress

## Problems?

* replication problems
    * take a look to hoody
