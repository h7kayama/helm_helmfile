# helm & helmfile

## helm

### setup
```
$ brew install helm
```

### search chart

#### from helm hub
```
$ helm search hub envoy
URL                                                     CHART VERSION   APP VERSION     DESCRIPTION
https://hub.helm.sh/charts/helm-stable/envoy            1.9.2           1.11.2          Envoy is an open source edge and service proxy,...
https://hub.helm.sh/charts/wener/ambassador             6.5.4           1.7.1           A Helm chart for Datawire Ambassador
https://hub.helm.sh/charts/datawire/ambassador          6.5.10          1.8.1           A Helm chart for Datawire Ambassador
...
```

#### from repo
```
$ helm repo add stable https://kubernetes-charts.storage.googleapis.com/

$ helm repo list
NAME    URL
stable  https://kubernetes-charts.storage.googleapis.com/

$ helm search repo envoy
NAME                    CHART VERSION   APP VERSION     DESCRIPTION
stable/envoy            1.9.2           1.11.2          Envoy is an open source edge and service proxy,...
stable/ambassador       5.3.2           0.86.1          DEPRECATED A Helm chart for Datawire Ambassador
stable/contour          0.2.0           v0.15.0         Contour Ingress controller for Kubernetes
```

### deploy
```
$ helm install envoy stable/envoy
NAME: envoy
LAST DEPLOYED: Sat Oct 17 10:02:09 2020
NAMESPACE: default
STATUS: deployed
REVISION: 1
TEST SUITE: None
```

#### with values
```
$ helm install envoy stable/envoy -f envoy/values.yaml
```

### undeploy
```
$ helm uninstall envoy
```

### create
```
$ helm create foo

$ helm lint foo
==> Linting foo
[INFO] Chart.yaml: icon is recommended

1 chart(s) linted, 0 chart(s) failed

$ helm package foo
Successfully packaged chart and saved it to: /Users/h7kayama/ghq/github.com/h7kayama/helm_helmfile/foo-0.1.0.tgz

$ helm install foo foo-0.1.0.tgz
NAME: foo
LAST DEPLOYED: Thu Oct 22 23:41:39 2020
NAMESPACE: default
STATUS: deployed
REVISION: 1
NOTES:
1. Get the application URL by running these commands:
  export POD_NAME=$(kubectl get pods --namespace default -l "app.kubernetes.io/name=foo,app.kubernetes.io/instance=foo" -o jsonpath="{.items[0].metadata.name}")
  echo "Visit http://127.0.0.1:8080 to use your application"
  kubectl --namespace default port-forward $POD_NAME 8080:80
```

## helmfile

### setup
```
$ brew install helmfile
```

### deploy
```
$ helmfile sync
```

#### with values
```envoy/helmfile.yaml
releases:
  - name: helmfile-envoy
    namespace: helmfile-envoy
    chart: stable/envoy
    values:
      - values.yaml
```

### with environments
```envoy/helmfile.yaml
environments:
  {{ .Environment.Name }}:
    values:
      - environments/{{ .Environment.Name }}-values.yaml
```

```
$ helmfile -e staging sync
```

### undeploy
```
$ helmfile destroy
```
