Architecture Overview
=====================

Each log-line is sent from your server using an open source
agent with a security token.

Logs are authenticated by Terabytes and queued in a Kafka Stream
before being processed and ingested into Elasticsearch.

Kafka with 7-day retention ensures that none of the logs are
lost and can be reprocessed if required.

There are 2 geographically distributed Elasticsearch
clusters, hosted with different providers.
Logs are ingested into both clusters at the same time. This 
ensures that we can quickly failover from one cluster to another
in the event of any failure.

Each Elasticsearch machine is a bare-metal server with:

* 8-12 cores
* 32-64GB RAM
* 4-6TB HDD

