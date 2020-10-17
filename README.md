# helm & helmfile

## helm

### add repo

```
$ helm repo add stable https://kubernetes-charts.storage.googleapis.com/
```

```
$ helm repo list
NAME    URL
stable  https://kubernetes-charts.storage.googleapis.com/
```

### search chart

```
$ helm search repo envoy
NAME                    CHART VERSION   APP VERSION     DESCRIPTION
stable/envoy            1.9.2           1.11.2          Envoy is an open source edge and service proxy,...
stable/ambassador       5.3.2           0.86.1          DEPRECATED A Helm chart for Datawire Ambassador
stable/contour          0.2.0           v0.15.0         Contour Ingress controller for Kubernetes
```

### install chart
```
$ helm install envoy stable/envoy
NAME: envoy
LAST DEPLOYED: Sat Oct 17 10:02:09 2020
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
```
