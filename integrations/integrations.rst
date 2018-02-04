.. _integrations:
Integrations
============

Terabytes can ingest logs in various formats depending on the ``tb_codec`` and 
``type`` field set in your JSON logs (or added as a field in your Beats Configuration):

Here are some common points which are valid across all our integrations:

* If you are sending logs in JSON format, you can send any ``type`` field, which best
describes your logs.

* If you are sending logs in ``line`` format, the parsing is determined by the ``type`` field.

The ``type`` field is also used to determine the suffix of your Elasticsearch Index.
e.g. logs of type ``python`` will be ``company_name-python-*`` indices.

We suggest using Filebeat for logs originating on your servers (e.g. access logs, 
application logs, system logs etc.)

.. toctree::
   :maxdepth: 5
   :caption: Integrations:

   beats
   distributed_tracing
   access_logs
   application_logs

