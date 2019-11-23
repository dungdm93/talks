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
