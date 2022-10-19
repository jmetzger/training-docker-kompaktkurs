# cAdvsior / prometheus 


## Überblick 

```
cAdvisor + Prometheus + Grafana 

https://github.com/google/cadvisor
https://prometheus.io/docs/guides/cadvisor/

a. Was ist cAdvisor ? 
Sammelt Metriken von allen docker containern und stellt sie zentral
zur Verfügung 

b. Warum cAdvisor und Prometheus ?
cAdvisor exposes container and hardware statistics as Prometheus metrics out of the box. By default, these metrics are served under the /metrics HTTP endpoint. This endpoint may be customized by setting the -prometheus_endpoint and -disable_metrics or -enable_metrics command-line flag

c. Warum Prometheus ?
Speichert zeitserien sehr gut in einen zeitreihen - datenbank (influxdb)
-> Hier Komponenten vorstellen. 

d. Evtl. Grafana ? 
Hier werden die Daten hübsch in Grafiken aufbereitet.
```

## Aufbau / Funktionsweise prometheus 

```


```

## Reference:

  * https://prometheus.io/docs/guides/cadvisor/
