
Elasticsearch
=============

Elasticsearch indexes will be created per day, based on the ``type`` field 
specified in your logs.

The index naming convention is ``organization_name-log_type-YYYY-MM-DD``
e.g. ``microsoft-access_logs-2000-01-01``

Direct Elasticsearch access is not provided.
