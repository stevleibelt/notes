# [Jens Kühnel](http://programm.froscon.de/2014/events/1327.html)

* structured logging with free/open source tools
* [webside](http://it-hure.de)

# [i love logging](http://ilovelogging.org/)

* based on a mailinglist for people interessted in open source logging using different tools

# syslog vs. structured logging

* syslog is plain (timestamp, category, free text filed)
    * BSD syslog (no year number inside, no subseconds, messages maximum length is 1023)
    * IETF (no BSD issues plus timezones but still simple free text field)
* structured logging is general JSON based
    * CEE / Project Lumberjack
    * GELF (graylog)
    * logstash
    * systemd Journal

# ways of the log message

* program log source -> syslog -> transformation/normalization -> analysis -> storage -> output
* program log source -> syslog and transformation/normalization -> analysis -> storage -> output
* program log source -> file log -> with collection shipper -> stransformation/normalization -> analysis -> storage -> output
* program log source -> transformation/normalization -> analysis -> storage -> output
* program logs sources generates structured log data -> analysis -> storage -> output
* storage 
    * elastic search
    * mongoDB
* -> = transport way
    * syslog
    * tcp
    * udp (fire and forget)
    * redis
    * AMQP/STOMP (ActiveMQ/RabittMQ)
    * 0mq
    * logstash-forwarder (Lumberjack)

# major tools (T = Transport, S = Shipper, N = Normalization, O = Output)

* Rsyslog TSN
* Syslog-ng TSN
* Graylog2 NO (easy up separation of who is allowed to see what)
* Logstash TSN
* Kibana O
* nx-logs
* logstash-forwarder (aka Lumberjack, transaction save and secured)

# my search for a logging solution

## requirements

* user separation
* interactive search
* automatic normalization
* widespread use

## used tools at the moment

* graylog2
* logstash
* rsyslog
* [kibana](http://www.elasticsearch.org/overview/kibana/) can deal with graylog2 and logstash
* ...

## example implementation (each part should be interchangeable)

[provider] -> logstash or fluentd -GELF-UDP-> graylog2 -> elastic search and mongoDB
