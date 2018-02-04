Terabytes Overview
==================

Terabytes was born out of the need to manage terabytes of logs
for lean engineering startups and businesses.

Examples of such logs include:

* Access Logs from Apache, Nginx, HAProxy etc.
* Application Logs from Rails, Golang, etc.
* Client side Logs from Android/iOS apps, Javascript instrumentation.
* Client side network performance Logs
* AWS Cloud Trail for all AWS audit logging
* AWS S3 access logs
* Azure performance logs

Deploying your own ELK cluster is fairly easy for smaller workloads.
Maintaing a cluster while ensuring reliability, security and scalability is
hard unless you have a dedicated DevOps Engineer running the logging system.

Terabytes runs a large ELK cluster which solves 2 major problems for your 
DevOps team:

* Minimal configuration and maintenance overhead
* Extensible logging platform with zero lock-in

Terabytes aims to provide multiple storage and analytics backends for logs,
apart from Elasticsearch such as Hadoop for MapReduce or Presto for SQL queries.
