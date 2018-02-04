.. _access-logs:

Access Logs
-----------

You can configure your existing web server to log in JSON format.

.. _nginx:

Nginx
^^^^^

Nginx logs can be formatted to JSON format using the following directive in
the http context::

    log_format logstash_json escape=json '{ "timestamp": "$time_iso8601", '
        '"host": "$host", '
        '"remote_addr": "$remote_addr", '
        '"remote_user": "$remote_user", '
        '"body_bytes_sent": "$body_bytes_sent", '
        '"request_time": "$request_time", '
        '"status": "$status", '
        '"request": "$request", '
        '"request_method": "$request_method", '
        '"http_referrer": "$http_referer", '
        '"tracing_id": "$http_x_request_id", '
        '"http_user_agent": "$http_user_agent" }';

Then add this in your server configuration::

      access_log /var/log/nginx/www.example.org-access.json logstash_json;

Refer to the Nginx Logging documentation: https://www.nginx.com/resources/admin-guide/logging-and-monitoring/
for adding additional fields to your logs.

**Distributed Tracing**

Refer to :doc:`distributed_tracing` for more details.

If Nginx is the entry point for all your HTTP requests (e.g. using Nginx as a load balancer)
then you can create a new unique request id in the server configuration::

       location / {
          proxy_pass http://upstream;
          proxy_set_header X-Request-ID $request_id;
       }

``$request_id``: http://nginx.org/en/docs/http/ngx_http_core_module.html#var_request_id

If Nginx is upstream to other services, nginx can log the ``X-Request-ID`` header
to trace the request. You can log request headers using ``$http_<header>``
and sent headers with ``$sent_http_<header>``.

.. _apache:

Apache
^^^^^^

Apache logs can be formatted to JSON using the following ``LogFormat``::

    LogFormat "{ \"time\":\"%t\", \"tracing_id\":\"%{uniqueid}i\", \"remoteIP\":\"%a\", \"host\":\"%V\", \"request\":\"%U\", \"query\":\"%q\", \"method\":\"%m\", \"status\":\"%>s\", \"userAgent\":\"%{User-agent}i\", \"referer\":\"%{Referer}i\" }" logstash_json

Then change your access.log in your VirtualHost section to::

    CustomLog ${APACHE_LOG_DIR}/access.log logstash_json

Refere to the Apache LogFormat directive for additional configuration options:
http://httpd.apache.org/docs/2.2/mod/mod_log_config.html#logformat

**Distributed Tracing**

Refer to :doc:`distributed_tracing` for more details.

You can create a new unique request id using ``mod_unique_id`` and add it to the request headers using::

    RequestHeader set uniqueid %{UNIQUE_ID}e

You can add it to access.log using ``%{uniqueid}i``. The above ``LogFormat`` already contains ``uniqueid`` logging.

If the request to Apache already contains ``X-Request-ID``, you can log it using ``%{X-Request-ID}i`` as ``tracing_id`` in the above ``LogFormat``.

.. _haproxy:

HAProxy
^^^^^^^

HAProxy logs can be formated to JSON using the following ``log-format``::

    log-format {"timestamp":%Ts,"status":%ST,"request":"%r","remote_addr":"%ci","bytes_read":%B,"upstream_addr":"%si","frontend_name":"%f","backend_name":"%b","retries":%rc,"bytes_uploaded":%U,"upstream_response_time":"%Tr","upstream_connect_time":"%Tc","session_duration":"%Tt","termination_state":"%ts","tracing_id":"%ID","headers":"%hr","host":"%H"}

**Distributed Tracing**

Refer to :doc:`distributed_tracing` for more details.

Adding a new unique request id to HAProxy ``frontend`` can be done using::

      unique-id-format %{+X}o\ %ci%cp_%fi%fp_%Ts_%rt%pid
      unique-id-header X-Request-ID
      capture request header X-Request-ID len 64

Read the documentation: 

``unique-id-format``: https://cbonte.github.io/haproxy-dconv/1.7/configuration.html#4-unique-id-format

``unique-id-header``: https://cbonte.github.io/haproxy-dconv/1.7/configuration.html#4.2-unique-id-header

You can add the newly created unique id to logs using ``%ID``. The above ``log-format`` already contains ``%ID`` logging.

If the request to HAProxy already contains a ``X-Request-Id`` you can log it using::

    http-request capture req.hdr(X-Request-ID) len 64

And then use ``%[capture.req.hdr(0)]`` as the ``tracing_id`` in your ``log-format``.

