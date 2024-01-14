# Prometheus<>Grafana<>Loki docker-compose setup

This Compose contains there elements `prometeus`, `Grafana` and `loki` for monitoring Stack.

# setup
- Change the Backend url inside `prometheus-config.yml`
- up the docker compose

```bash
docker compose up -d
```
- go to `localhost:3000` for grafana dashboard
    - username: admin
    - password: admin

# backend setup
Hint for node js use `prom-client` library