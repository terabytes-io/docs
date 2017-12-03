
Overview
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

