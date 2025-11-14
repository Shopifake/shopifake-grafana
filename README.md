# Grafana

Visualizes metrics from Prometheus.

## Deploy

```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update
helm install grafana grafana/grafana -f values.yaml -n observability --create-namespace
```

## Configure Prometheus URL

The Prometheus URL is configured via the `PROMETHEUS_URL` environment variable. Override it:

```bash
helm upgrade grafana grafana/grafana -f values.yaml \
  --set env[0].value="http://your-prometheus:9090" \
  -n observability
```

## Architecture

```
Grafana → Prometheus → OpenTelemetry Collector
```

## Access

```bash
kubectl port-forward -n observability svc/grafana 3000:80
```

Default credentials: `admin` / `changeme`

## Get admin password

```bash
kubectl get secret -n observability grafana -o jsonpath="{.data.admin-password}" | base64 --decode
```
