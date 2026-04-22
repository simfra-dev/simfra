**simfra** - AWS cloud emulator

A single-container AWS simulator with 80+ services and 3,500+ operations. All services on one port, real cross-service interactions, optional persistence to SQLite. No AWS account required.

> **Early development** — APIs and behavior may change between releases.

## Infrastructure as code testing

API-only mode. Validate Terraform plans and test infrastructure modules without provisioning real resources.

```bash
docker run -p 4599:4599 ghcr.io/simfra-dev/simfra:latest
```

```bash
export AWS_ENDPOINT_URL=http://localhost:4599
export AWS_ACCESS_KEY_ID=AKIAIOSFODNN7EXAMPLE
export AWS_SECRET_ACCESS_KEY=wJalrXUtnFEMI/K7MDENG/bPxRfiCYEXAMPLEKEY
export AWS_S3_USE_PATH_STYLE=true

terraform init && terraform apply
```

## Application development & training

Docker-backed services with persistence. Lambda runs your code, RDS runs real MySQL/PostgreSQL, EKS creates real Kubernetes clusters, ElastiCache runs actual Redis. State survives restarts.

```bash
docker run -p 4599:4599 \
  -e SIMFRA_DOCKER=true \
  -e SIMFRA_DATA_DIR=/data \
  -v /var/run/docker.sock:/var/run/docker.sock \
  -v simfra-data:/data \
  ghcr.io/simfra-dev/simfra:latest
```

## Documentation

Full documentation at **[simfra.dev](https://simfra.dev)**:

- [Getting Started](https://simfra.dev/docs/getting-started) - installation, Terraform, AWS SDKs, configuration
- [Architecture](https://simfra.dev/docs/architecture) - request lifecycle, storage model, cross-service interactions
- [Services](https://simfra.dev/docs/services) - full service table with fidelity levels and capabilities

## Issues

Use [GitHub Issues](https://github.com/simfra-dev/simfra/issues) to report bugs, request features, or ask questions.
