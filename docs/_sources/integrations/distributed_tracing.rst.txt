.. _distributed_tracing:
Distributed Tracing
===================

Debugging across micro-services can be painful - adding a unique external
request id and passing the request id to all services can help you trace
requests across the stack.

This unique tracing id can be forwarded as HTTP headers and logged as 
part of all access logs. This gives the following benefits:

* Measure latency at each service
* Debug individual requests and failure points
* Visualizing a complex micro-service architecture

You can read more about the benefits of Distributed Tracing here:
http://microservices.io/patterns/observability/distributed-tracing.html

Terabytes can receive access logs and application logs from all your services.
A little effort in adding unique-ids to your requests will yield tremendous benefits.

Terabytes Integrations Guides at :doc:`integrations` can help you 
add and log unique request ids.
