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

One of the easiest way to get started is to use a filebeat docker container
from https://github.com/terabytes-io/filebeat

The docker image contains a simple configuration for collecting
``/var/log/auth.log`` and ``/var/log/syslog`` files::

    docker run -d -v /var/log:/var/log/host:rw \
    --hostname $(hostname) --name terabytes \
    -e TOKEN=token terabytes/filebeat:latest

