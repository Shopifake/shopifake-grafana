# Grafana

Visualizes metrics from Prometheus.

## Deploy

```bash
helm repo add grafana https://grafana.github.io/helm-charts
helm repo update

# Deploy with custom admin password
helm install grafana grafana/grafana -f values.yaml \
  --set-string adminPassword="your-secure-password" \
  -n observability --create-namespace
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

Login with `admin` / `<your-password>`
