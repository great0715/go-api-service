# Release Lab API · Go Backend Example

A standalone Go HTTP service demonstrating API routing, JSON input validation, thread-safe in-memory state, health checks, graceful shutdown, testing, Docker packaging, and GitHub Actions CI. Created as an **original portfolio demonstration**, not as a deployed customer project.

## Run locally

Requires **Go 1.23+**.

```bash
go run .
```

In another terminal:

```bash
curl http://localhost:8080/healthz
curl -X POST http://localhost:8080/api/releases \
  -H 'Content-Type: application/json' \
  -d '{"service":"website","environment":"staging","version":"v1.2.0"}'
curl http://localhost:8080/api/releases
```

## Tests and checks

```bash
go test -race ./...
go vet ./...
```

GitHub Actions runs tests, vet, and a Docker build automatically on pushes and pull requests to this repository.

## Docker

```bash
docker build -t release-lab-api .
docker run --rm -p 8080:8080 release-lab-api
```

## Endpoints

| Method | Path | Description |
| --- | --- | --- |
| GET | `/healthz` | Returns `{"status":"ok"}` |
| GET | `/api/releases` | Lists in-memory release records |
| POST | `/api/releases` | Creates an in-memory queued release record |

The POST body contains `service`, `environment` (`staging` or `production`), and `version`.

## Scope and security notes

This is a learning/reference service, **not a production deployment service**. Data disappears on restart. It does not authenticate clients, persist records, or actually initiate deployments. It would need authentication, authorization, durable storage, rate limiting, audit logging, and deployment safeguards before any real-world deployment.

## Related portfolio

- [Live portfolio](https://great0715.github.io/)
- [GitHub profile](https://github.com/great0715)
