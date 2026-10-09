# Smoke Test

A microservice generated from the platform golden path.

Owned by **draco121**. Generated from the platform golden path:
[java-template-service](https://github.com/draco121/java-template-service).

## Run it

```bash
mvn spring-boot:run
curl localhost:8080/actuator/health
curl "localhost:8080/api/greeting?name=you"
```

## What you got for free

| Concern | Where | What it does |
|---|---|---|
| Structured logs | `application.yml` → `logging.structured` | Every log line is JSON, searchable by `requestId` and `traceId` |
| Request ids | `platform/RequestIdFilter.java` | Every response carries `X-Request-Id` |
| Tracing | `spring-boot-starter-opentelemetry` | Sends traces to `OTEL_EXPORTER_OTLP_ENDPOINT` |
| Metrics | `/actuator/prometheus` | Request counts, latencies, JVM stats |
| Health checks | `/actuator/health/liveness`, `/readiness` | Ready for Kubernetes probes |
| Error format | `spring.mvc.problemdetails` | Errors are JSON (RFC 9457), never stack traces |
| Formatting | Spotless + google-java-format | `mvn verify` fails on bad formatting, `mvn spotless:apply` fixes it |
| CI + security gate | `.github/workflows/ci.yml` | Build, test, formatting, then the platform's central security gate |
| Catalog entry | `catalog-info.yaml` | Shows up in the developer portal with its owner |
| Container | `Dockerfile` | Small, non-root image with a health check |

## Write your feature

Add your code under `src/main/java/dev/workshop/smoketest/`. Everything above keeps working.
