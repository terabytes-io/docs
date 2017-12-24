Logstash
========

Terabytes ingests logs using Logstash Beats and TCP input plugins.

If you use any of the beats (Filebeat, Metricbeat or Packetbeat)
point your beats output to ``logstash.terabytes.io:5000``

If you prefer sending logs over TCP (e.g. if using Logspout)
you can point your logs output to ``logstash.terabytes.io:5001``

