Getting started
===============

Write in to admin@terabytes.io to request a token for your organization detailing
your estimated numbers for

* log lines per day
* log size in GB per day
* log types (nginx access logs etc.)

We will provide you with a token with which you can send logs to us for free for
30 days, with a max of 1GB of logs per day.

Your kibana will be located at organization_name.terabytes.io, where you can
log in with your organization's google account.

Filebeat Docker
---------------

The easiest way to get started is to use a filebeat docker container
from https://github.com/terabytes-io/filebeat

The docker image contains a simple configuration for collecting
``/var/log/auth.log`` and ``/var/log/syslog`` files::

    docker run -d -v /var/log:/var/log/host:rw \
    --hostname $(hostname) --name terabytes \
    -e TOKEN=token terabytes/filebeat:latest


Standalone Filebeat
-------------------
Filebeat can also be installed from the official elasticsearch website and
used with Terabytes by adding the following under prospectors::

      fields:
        tb_codec: line
        token: TOKEN
        type: syslog


tb_codec
    Codec of the log line.

    ``line``: a simple log line with parsing determined by the "type" field.

    ``json``: log line in JSON format

token
    token obtained by emailing admin@terabytes.io

type
    currently supported types are ``syslog`` and ``access_log``

    ``syslog``: parsed using logstash grok filter ``syslog_message``

    ``access_log``: parsed using logstash grok filter ``COMBINEDAPACHELOG``

Filebeat Output must be specified as logstash with the following host::

    logstash.terabytes.io:5000

and certificate authority as tb.crt file, which can be obtained from
https://raw.githubusercontent.com/terabytes-io/filebeat/master/tb.crt

