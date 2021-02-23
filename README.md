# Aliyun CloudMonitor Exporter

exporter for Aliyun CloudMonitor. Written in Golang, inspired by [aliyun-exporter](https://github.com/aylei/aliyun-exporter).

## Develop

```bash
git clone https://github.com/fengxsong/aliyun-exporter
cd aliyun-exporter
make tidy
```

## Build

```bash
# Binary
make bin
# docker image
make docker-build
```

## Usage

```bash
make bin
# print example of config
./build/_output/bin/aliyun-exporter print-config --ak xxxx --secret xxxx [NAMESPACES...]
# run
./build/_output/bin/aliyun-exporter serve [--config=/path/of/config]
```

## Deploy

### Docker-compose

Pre-requisites:

- Docker
- docker-compose

```bash
# copy and modify example.yaml first
cd deploy
docker-compose up -d
```

### Kubernetes

Pre-requisites:

- Kubernetes
- helm

```bash
helm install -n monitoring aliyun-exporter deploy/aliyun-exporter
kubectl get po -n monitoring -w
```

### prometheus job

```yaml
- job_name: 'aliyun-exporter'
  scrape_interval: 60s
  scrape_timeout: 60s
  static_configs:
  - targets: ['aliyun-exporter:9527']
```

### prometheus rules

todo...

## Limitation

- an exporter instance can only scrape metrics from single region
- ...

## TODO

- dynamic rate limiter
- grafana dashboard

## Ref

- https://partners-intl.aliyun.com/help/doc-detail/51939.htm?spm=a2c63.p38356.b99.150.7c8312d7lwqVVC
- https://partners-intl.aliyun.com/help/doc-detail/163515.htm?spm=a2c63.p38356.a3.4.326357304ihN0P
- https://github.com/aliyun/alibaba-cloud-sdk-go