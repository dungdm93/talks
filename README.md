## 1. Install nginx-ingress
```bash
helm install stable/nginx-ingress \
    --name=nginx-ingress \
    --namespace=nginx-ingress
```

## 2. Logging
### 2.1 Installation
```bash
helm repo add elastic https://helm.elastic.co
helm repo update

helm upgrade --install elasticsearch elastic/elasticsearch \
    --namespace=kube-observability \
    --values=elasticsearch.yaml
helm upgrade --install kibana elastic/kibana \
    --namespace=kube-observability \
    --values=kibana.yaml
```
