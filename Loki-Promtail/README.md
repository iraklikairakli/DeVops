# LOKI-VELI
```sh
helm upgrade --reuse-values -f loki-stack/values.yml  loki grafana/loki-stack --namespace monitoring
helm show values  grafana/loki-stack --namespace monitoring
helm install loki grafana/loki-stack --version "${HELM_CHART_VERSION}"   --namespace=monitoring  --create-namespace   -f "loki-stack-values-v2.6.4.yaml" # edit values yml when install chart with helm
```