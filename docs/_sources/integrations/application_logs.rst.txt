Application Logs
----------------

We suggest using JSON logging for all application logs.
Additionally, you should setup :doc:`distributed_tracing` for all your 
services by logging the ``X-Request-ID`` header in all your logs.

Refer to the :doc:`access_logs` section for how to add the ``X-Request-ID`` 
to your web servers.

Python
^^^^^^

**python-json-logger**
: https://github.com/madzak/python-json-logger

**json-log-formatter**
: https://github.com/marselester/json-log-formatter

Django
""""""

**django-logging-json**
: https://github.com/cipriantarta/django-logging

Ruby
^^^^

**ougai**
: https://github.com/tilfin/ougai

**logstash-logger**
: https://github.com/dwbutler/logstash-logger

Rails
"""""

**lograge**
: https://github.com/roidrage/lograge

**logstasher**
: https://github.com/shadabahmed/logstasher


NodeJS
""""""

**roarr**
: https://github.com/gajus/roarr


Golang
^^^^^^

**logrus**
: https://github.com/sirupsen/logrus

Use ``log.SetFormatter(&log.JSONFormatter{})`` for JSON logging

**zap**
: https://github.com/uber-go/zap

**zerolog**
: https://github.com/rs/zerolog

Rust
^^^^

**slog**
: https://github.com/slog-rs/slog

**json_logger**
: https://github.com/rsolomo/json_logger

Java/Scala
^^^^^^^^^^

* If you are using log4j:

**log4j-json**
: https://github.com/michaeltandy/log4j-json

**log4j-jsonevent-layout**
: https://github.com/logstash/log4j-jsonevent-layout

* If you are using java.util.logging:

**logstash-util-formatter**:
: https://github.com/SYNAXON/logstash-util-formatter

* If you are using logback

**logback-encoder**
: https://github.com/logstash/logstash-logback-encoder

Play Framework
""""""""""""""

**play-json-logger**
: https://github.com/hmrc/play-json-logger



