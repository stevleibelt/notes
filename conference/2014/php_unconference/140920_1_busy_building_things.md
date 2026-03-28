# Busy Building Things

Buillding the perfect web application with these [12 wired tricks](http://12factor.net/) - by [ole michaelis](http://www.codestars.eu)
Slides available at [slird.io](http://slidr.io/)

## Back into Hsitory

* deployment by uploading to ftp
* dependencies controlled by svn:externals
* pear

## Now

* vim composer.json (dependencies managed (isolated) by composer per application)
* git add <files>
* git commit
* git push orgin master
* still a bunch of configuration files and lines after setting up a "new project"
    * why not configure your environment within your environment
    * like $_ENV['DB_HOST']
* how to scale
    * divide and conquer
    * learned that sharding should only be the last way to go
    * build simple small services
    * build simple processes (quick start and shutdown)
* there are no logs, they are event streams
    * your application simple logs to stdout/rsyslog
* let your admin process run into dedicated environment

## 12 Factors

* [codebase](http://12factor.net/codebase)
    * one codebase in an vcs
    * multiple tags
    * easyup deployment per environment
* [dependencies](http://12factor.net/dependencies)
    * isolated dependencies per application
* [configuration](http://12factor.net/config)
    * stop configuration in your environment
* [backing services](http://12factor.net/backing-services)
    * thread backing services as attached services
    * all services are "blackboxes"
* [build, release and run](http://12factor.net/build-release-run)
    * strictly separate build and run stages
    * do not download same dependecies per deployment per machine ;-)
* [processes](http://12factor.net/processes)
    * execute the apps as one or more processes
* [port binding](http://12factor.net/port-binding)
    * export services via port binding
* [concurrency](http://12factor.net/concurrency)
    * scale out with your process model
* [disposability](http://12factor.net/disposability)
    * maximum robustness with fast startup and graceful shutdown
* [development/production parity](http://12factor.net/dev-prod-parity)
    * keep development, staging and production as similar as possible
    * simple, your environment should work offline as well
* [logs](http://12factor.net/logs)
    * treat logs as an event stream
* [admin process](http://12factor.net/admin-processes)
    * run admin and management tasks as one-off processes
