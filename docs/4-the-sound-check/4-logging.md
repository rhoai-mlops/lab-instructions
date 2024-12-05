## Aggregated Logging

> OpenShift’s built in logging is deployed as an operator using the LokiStack. By default collects all output from all containers that are logging to system out. This means no logging needs to be configured explicitly in the application. Logs are collected using a collector running on each nodes, then popped into LokiStack where they are indexed in a timeseries as JSON. OpenShift has a built in visualisation UI, but you can also use an external Grafana as well.


TBD

