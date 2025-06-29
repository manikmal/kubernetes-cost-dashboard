# Kubernetes Cost Dashboard

A real-time cost visibility setup for Kubernetes using:

- **Prometheus** for metrics
- **Grafana** for dashboards
- **Kubecost** for cost analysis
- **Minikube** for local development

---

## 🛠 Stack

- Kubernetes (Minikube)
- Helm 3
- Prometheus
- Grafana
- Kubecost
- Sample workload

---

## 🚀 Quick Start

### 1. Start Minikube

```bash
minikube start --memory=4096 --cpus=2
```

---
### Set up

## Adding Helm repos

helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm repo add grafana https://grafana.github.io/helm-charts
helm repo add kubecost https://kubecost.github.io/cost-analyzer/
helm repo update

## Prometheus install 

helm install prometheus prometheus-community/prometheus


## Install Grafana

helm install grafana grafana/grafana \
  --set adminPassword=admin \
  --set service.type=NodePort \
  -f helm/grafana/values.yaml

## Install kubecost

helm install kubecost kubecost/cost-analyzer \
  -f helm/kubecost/values.yaml


##  Deploy Sample Workload

kubectl apply -f workloads/sample-deployment.yaml


## Kubecost:

kubectl port-forward svc/kubecost-cost-analyzer 9090:9090
## --> Visit: http://localhost:9090


## Guide on medium 
## --> https://manikmalhotra6.medium.com/how-i-built-a-real-time-kubernetes-cost-monitoring-dashboard-with-kubecost-f19c498d01d6
