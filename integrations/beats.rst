Beats
-----

Beats are lightweight agents developed by Elastic that ship logs from your 
servers to Terabytes.

* Filebeat: Log files
* Metricbeat: Metrics
* Packetbeat: Network data/metrics

Any of the Beats https://www.elastic.co/products/beats
can be installed from the official elasticsearch website and
used with Terabytes as long as they contain the following additional fields::

      fields:
        token: TOKEN

token
    a secret Terabytes token that needs to accompany each log line from your servers.
    You can obtain one when you setup your account by emailing admin@terabytes.io

To set these fields, follow the official documentation:

* Filebeat: https://www.elastic.co/guide/en/beats/filebeat/current/configuration-filebeat-options.html#configuration-fields
* Metricbeat: https://www.elastic.co/guide/en/beats/metricbeat/current/configuration-general-options.html#libbeat-configuration-fields

Note: ensure that ``fields_under_root`` is set to ``true``

Beat output must be specified as logstash with the following host::

    logstash.terabytes.io:5000

and certificate authority as tb.crt file, which can be obtained from
https://raw.githubusercontent.com/terabytes-io/filebeat/master/tb.crt

Additionally, for Filebeat, please ensure that the following fields are also set:

tb_codec (required for Filebeat)
    Codec of the log line.

    ``line``: a simple log line with parsing determined by the "type" field.

    ``json``: log line in JSON format


type (required for Filebeat)
    currently supported types are ``syslog`` and ``access_log`` for Filebeat

    ``syslog``: parsed using logstash grok filter ``syslog_message``

    ``access_log``: parsed using logstash grok filter ``COMBINEDAPACHELOG``

Quickstart
----------

One of the easiest way to get started is to use a filebeat docker container
from https://github.com/terabytes-io/filebeat

The docker image contains a simple configuration for collecting
``/var/log/auth.log`` and ``/var/log/syslog`` files::

    docker run -d -v /var/log:/var/log/host:rw \
    --hostname $(hostname) --name terabytes \
    -e TOKEN=token terabytes/filebeat:latest

