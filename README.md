# ai-gateway Enterprise Example Stack

This guide explains how to set up the **ai-gateway enterprise** service using example stacks. The ai-gateway service provides a scalable, production-ready API gateway for AI and data workloads, supporting integration with Postgres, Redis, and ClickHouse.

### 1. Clone the repository

```sh
git clone git@github.com:langdb/helm-chart.git
cd helm-chart
```

### 2. Deploy using Helm

```sh
cd helm/ai-gateway
helm install ai-gateway . 
```

This will deploy:
- ai-gateway (using the default image)
- uses External Postgres, Redis, and ClickHouse


### 1. Update `values.yaml`:

```yaml
env:
  CLICKHOUSE_HOST: <external-clickhouse-host>
  REDIS_HOST: <external-redis-host>
  POSTGRES_HOST: <external-postgres-host>
  POSTGRES_USER: <your-user>
  POSTGRES_PASSWORD: <your-password>
  POSTGRES_DB: <your-db>
config: |
  # ai-gateway configuration
  http:
    host: "0.0.0.0"
    port: 8080
```

This will automatically mount your config.yaml into the container at `/app/config.yaml` and the ai-gateway will use it on startup.

### Access ai-gateway

Visit: [http://localhost:8080](http://localhost:8080)

---

## Accessing the Service (Kubernetes)

By default, the service is exposed as a `ClusterIP`. To access it externally, you can port-forward:

```sh
kubectl port-forward svc/ai-gateway 8080:80
```

Then access the gateway at `http://localhost:8080`.

---

## Example Commands

### Install dependencies (if needed)

```sh
helm dependency update
```

### Uninstall

```sh
helm uninstall ai-gateway
```
---