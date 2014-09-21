# Profiling in PHP

## Tools

* xdebug
    * xdebug.profile_enable=1
    * xdebug.profile_output_dir=/tmp/xdebug
    * hugh performance impact on production
* [k]cachgrind
* xhprof (php extension)
    * no performance impact when its not enabled (but loaded as extension)
    * small performance impact when enabled
    * [xh guis](https://github.com/search?utf8=%E2%9C%93&q=xhprof+gui) are available (also by [qafoolabs](https://github.com/QafooLabs/profiler)
        * qafoolabs profiler is currently closed beta
        * maybe open beta in a month or two
* use software as a service business solutions like "new relic" or "app dynamics" (currently, both based in usa)
* framework toolbars (symfony debug toolbar)
    * try to collect system informations by a small amount of users (maximum one percentage, random selected)
    * kibana, graphite and elastic search
* strace
* dtrace

## Tipps

* never write to filesystem on production
* if you wan to write your profiling into a database, register this as shutdown event
* use [xhprof](https://github.com/QafooLabs/xhprof) by qafoolabs since it provides a way to write into the database afterwards (by using the shutdown process ;-))

## Sum Things Up for Profiling

* developemt
    * xdebug
    * xhprof
* stage
    * xdebug if needed
    * xhprof
    * xhgui
* production
    * xhprof
        * elastic search
    * commercial
        * new relic
        * app dynamics
        * qafoo profiler
