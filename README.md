### REMOVE ME
Find and replace all `app-template` to your project's name.
As well, do it for `github.com/JMURv/golang-clean-template`, that used in go backend.


### GitHub Actions
Specify **Docker Hub** `USERNAME`, `PASSWORD` and desired `IMAGE_NAME` secrets in GH Actions repo.

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

Run prod (requires `configs/envs/.env.prod`):
```shell
task dc-prod
```

Also, there is ability to up svcs like: `prometheus`, `jaeger`, `node-exporter`, `grafana`.

You can include necessary svcs manually in your desired `compose*.yaml` file from `compose-base.yaml`.

Services are available at:

| Сервис         | Адрес                  |
|----------------|------------------------|
| App (HTTP)     | http://localhost:8080  |
| App (GRPC)     | http://localhost:50050 |
| App (Frontend) | http://localhost:4000  |
| Prometheus     | http://localhost:9090  |
| Jaeger         | http://localhost:16686 |
| Grafana        | http://localhost:3000  |

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

## Tests
### Integration
Spin up all containers for `integration` tests:
```shell
task dc-test
```
Wait until all containers are ready and then run:
```shell
task t-integration
```
