### REMOVE ME
Find and replace all `app-template` to your project's name.
As well, do it for `github.com/JMURv/golang-clean-template`, that used in go backend.


### GitHub Actions
Specify **Docker Hub** `USERNAME`, `PASSWORD`, `BACKEND_IMAGE_NAME` and `FRONTEND_IMAGE_NAME` secrets in GH Actions repo.

This is required to build and push docker image.
### END

## Stack
|          | Technology |
|----------|------------|
| Backend  | Golang     |
| Frontend | Next.js    |

---
## Configuration
### App
Configuration files for local `backend `development placed in `backend/config`.

Configuration files for `docker` development placed in `/configs/envs`

- Create your own `.env` based on `.env.example`:
```shell
cp backend/config/.env.example backend/config/.env && \
cp configs/envs/.env.example configs/envs/.env.dev && \
cp configs/envs/.env.example configs/envs/.env.prod
```

## Build
### Locally
#### Backend
In backend root folder run:
```shell
go build -o bin/main ./cmd/main.go
```
After that, you can run app via `./bin/main`

#### Frontend
In frontend root folder run:
```shell
npm run build
```
___

### Docker
In the root folder run:
```shell
task dc-dev-build
```

or run:
```shell
task dc-prod-build
```

To build `dev` or `prod` containers respectively.

## Run
### Docker Compose
Run dev (requires `configs/envs/.env.dev`):
```shell
task dc-dev
```

Run dev with observation containers:
```shell
task dc-dev-obs
```

Run prod (requires `configs/envs/.env.prod`):
```shell
task dc-prod
```

Run prod with observation containers:
```shell
task dc-prod-obs
```
Observe profile starts svcs like: prometheus, jaeger, node-exporter, grafana and etc.

Services are available at:

| Сервис           | Адрес                  |
|------------------|------------------------|
| App (HTTP)       | http://localhost:8080  |
| App (GRPC)       | http://localhost:50050 |
| App (PROMETHEUS) | 	http://localhost:8085 |
| App (Frontend)   | http://localhost:4000  |
| Prometheus       | http://localhost:9090  |
| Node-exporter    | http://localhost:9100  |
| Jaeger           | http://localhost:16686 |
| Loki             | http://localhost:3100  |
| Grafana          | http://localhost:3000  |

More information could be found inside compose.yaml.
___

### K8s

- Create your own `configMap` and `secretMap` based on examples:
```shell
cp k8s/cfg/cfg.example.yaml k8s/cfg/cfg.yaml && \
cp k8s/cfg/secret.example.yaml k8s/cfg/secret.yaml 
```

Apply manifests:
```shell
task k-up
```

Shutdown manifests:
```shell
task k-down
```

## Tests (Backend)
### Integration
Run:
```shell
task t-integration
```
It will spin up all containers for integration testing automatically using testcontainers.

### Load testing
Run:
```shell
task dc-k6
```
It will spin up all prod environment, including observation containers and starts k6 scenario. Grafana has prebuilt dashboard for k6.
