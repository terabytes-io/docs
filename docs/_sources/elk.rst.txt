
Terabytes ELK
=============

Elasticsearch
-------------

Elasticsearch indexes follow the following conventions:

* The ``type`` field is used to determine the suffix of your Elasticsearch Index. e.g. logs of type ``python`` will be ``company_name-python-*`` indices.

* Indices are either deleted or archived to cold storage based on your pricing plan. Please refer to http://terabytes.io/pricing for Plans.

Direct Elasticsearch access is provided upon request.

Logstash
--------

Terabytes ingests logs using Logstash Beats and TCP input plugins.

If you use any of the beats (Filebeat, Metricbeat or Packetbeat)
point your beats output to ``logstash.terabytes.io:5000``

If you prefer sending logs over TCP (e.g. if using Logspout)
you can point your logs output to ``logstash.terabytes.io:5001``

Kibana
------

Each user in your organization can have their own kibana index for creating
and storing their visualizations and dashboards. This kibana index is named
``.kibana_username@organization.com``

A shared kibana index is also provided which is shared across your organization.
It is called ``.kibana_organization``

You can switch between your personal vs shared index using the ``Own Home`` tab
in Kibana UI.

