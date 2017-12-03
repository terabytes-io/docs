.. Terabytes documentation master file, created by
   sphinx-quickstart on Sun Dec  3 01:09:53 2017.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

.. title:: Terabytes: Hosted ELK
.. image:: terabytes_logo.png

Terabytes is a hosted Elasticsearch Logstash Kibana (ELK) stack.
It is built on top of a scalable architecture with reliability in mind.

It is a no-frills, cheaper alternative to pricey enterprise logging solutions,
without compromising on your storage and log searching needs.

.. toctree::
   :maxdepth: 2
   :caption: Contents:


Features
========

* Alerting using ElastAlert (Slack, Pagerduty etc.)
* Simplified logstash configuration for known log types
* Google Authentication for Kibana
* Shared and user-level kibana indexes

Each organization gets a dedicated Kibana instance which sits on top of a multi-tenant
elasticsearch. These are multiple elasticsearch clusters in various locations with replication.

Each Elasticsearch machine is a bare-metal server with:

* 8-12 cores
* 48-64GB RAM
* 4-6TB HDD


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


Elasticsearch Indexes
---------------------
Elasticsearch indexes will be created per day, based on the ``type`` specified
in the filebeat fields.

The index naming convention is ``organization_name-log_type-YYYY-MM-DD``
e.g. ``microsoft-access_logs-2000-01-01``


Kibana Indexes
--------------
Each user in your organization can have their own kibana index for creating
and storing their visualizations and dashboards. This kibana index is named
``.kibana_username@organization.com``

A shared kibana index is also provided which is shared across your organization.
It is called ``.kibana_organization``

You can switch between your personal vs shared index using the ``Own Home`` tab
in Kibana UI.

Alerting
--------
Alerting is provided using ElastAlert which you can access on the Kibana UI.
For alerting reference, refer to https://github.com/Yelp/ElastAlert
and https://github.com/Yelp/elastalert/tree/master/example_rules
