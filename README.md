## 1. Install nginx-ingress
```bash
helm upgrade --install nginx-ingress stable/nginx-ingress \
    --namespace=nginx-ingress \
    --values=nginx-ingress.yaml
```

## 2. Logging
### 2.1 Installation
```bash
helm repo add elastic https://helm.elastic.co
helm repo update

# ElasticSearch
helm upgrade --install elasticsearch elastic/elasticsearch \
    --namespace=kube-observability \
    --values=elasticsearch.yaml

# Kibana
helm upgrade --install kibana elastic/kibana \
    --namespace=kube-observability \
    --values=kibana.yaml

# Fluent-bit
helm upgrade --install fluent-bit stable/fluent-bit \
    --namespace=kube-observability \
    --values=fluent-bit.yaml
```

## 3. Monitoring
### 3.1 Installation
```bash
export CRD_BASE_URL=https://github.com/coreos/prometheus-operator/raw/v0.34.0/example/prometheus-operator-crd
kubectl apply -f "${CRD_BASE_URL}/prometheus.crd.yaml"
kubectl apply -f "${CRD_BASE_URL}/alertmanager.crd.yaml"
kubectl apply -f "${CRD_BASE_URL}/servicemonitor.crd.yaml"
kubectl apply -f "${CRD_BASE_URL}/podmonitor.crd.yaml"
kubectl apply -f "${CRD_BASE_URL}/prometheusrule.crd.yaml"

helm upgrade --install prometheus-operator stable/prometheus-operator \
    --namespace=kube-observability \
    --values=prometheus-operator.yaml
```

Note:
```
Grafana:
    username: admin
    password: prom-operator
```
