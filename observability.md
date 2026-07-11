# Observability
- ye btayega latency kya hai, pura check krega after deployment, it is ability of a runnig system

# Understanding production failures
-Complete failure -server stop responding,crash
-Parital failure- some points work, some dont,alerts dont fire
-Performance failures- slow but alive
-Intermittent failure-(fails randomly)
-Degradation failure-failures build over time
-dependecny failure-third-party timeouts
-Change-induce failure-after deployment

## THree pillars
```
Metrics-
1) how busy the system is
2)how fast or slow it is

Logs-
1)Undestanding what exactly happened

Traces-
Understanding how a single request travelled through the system


```

## Telemetry
-automated process of collecting,transmitting, and analyzing data.

## Used stack
-LGTM stack
- for metrics (prometheus)-grafana stack
- used for grafana mimir(promethues)

- for logs-loki
-for traces -tempo

## Metrics
```
- produce time-series data
- stored in TSDB( time series database)
- why?? TDSB-> easy for query on time
- implements alerts 
-?? when to implement alerts? at which threshold
-Four golden signals

a) Latency-
b) Traffic-
c) Errors- how many requests are failing or behaving differently
d) Saturation- how close to a system is to its limit,it predicts future failure


```
### Prometheus
```
api call se prometheus data scrape krta hai
and the language used here is promql which is used to query,aggregate metrics,calcualte rates,analye trends

```
### understanding cpu usqge in nodejs
-
```
/user-cpu
const start=performance.now()- tells about how much time the tab is open
/system-cpu
ye btata hai kitna system read kr rha hai file
ye microseconds mei batata hai

process.uptime()-> ye seconds mein btata hai

```

#### instrumentation
- add code in ur app so that it can emit telemetry data
- use prom-client package from npm
- promclient.defaultmetrics()
- ek prometheus.yml file hoti hai iske scrape mein jaakar jobs daaloge tab hi tmhara server ka endpoint ka metric btayega
-![alt text](observability-images/image-48.png)