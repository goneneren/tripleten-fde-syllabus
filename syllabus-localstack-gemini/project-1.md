# Project 1 - System Diagnostics, API Scaling & LocalStack Telemetry

## Project Description

Students diagnose a provided monolith-based enterprise reference platform running locally via Docker Compose alongside LocalStack Base (S3 service). They trace request paths across code, PostgreSQL, Redis, and LocalStack S3 AWS SDK (`boto3`) calls, repair observability defects in OpenTelemetry and Prometheus/Grafana, run a reproducible load test, correct an AI-generated capacity analysis, and evaluate the latency impacts of mocked LLM API calls on the traditional backend. The project stays local-first so every student completes the diagnostic workflow without cloud spending.

**Scope of LocalStack in this project: a traced boundary, not a measured one.** Students learn the `boto3` client/`endpoint_url` pattern and see AWS SDK calls appear as spans in Jaeger. They do not measure, benchmark, or extrapolate from emulated S3 timings — LocalStack S3 is a local process on a Docker volume and its latency and throughput profile bears no relationship to real S3. All quantitative conclusions come from the deterministic provider scenario pack and the real PostgreSQL/Redis tier. This scoping is deliberate: P1 is the program's most overloaded project (22.3 h/wk in weeks 1–3), and its subject is empirical performance diagnosis, which is precisely what an emulator cannot teach. First hands-on `boto3` implementation work lands in Project 2.

## Skills

- Run and inspect a provided production-shaped system with LocalStack AWS emulation in Docker Compose.
- Trace a request across code, logs, metrics, distributed traces, PostgreSQL, Redis, and LocalStack S3 `boto3` SDK calls.
- Repair exactly two observability defects: one trace propagation issue (including AWS SDK spans) and one metric/dashboard issue.
- Use Prometheus, Grafana, Jaeger, OpenTelemetry, and application logs to diagnose system performance.
- Run a controlled `k6` or Locust load cycle that reproduces API bottlenecks (focusing on simulated LLM latency and the real PostgreSQL/Redis tier).
- Calculate capacity from traffic, storage, latency, and growth assumptions, using **published AWS service quotas and documented SDK connection-pool defaults** as inputs rather than measurements taken from the emulator.
- Audit an AI-generated capacity artifact for math errors, weak assumptions regarding LLM token throughput, and unsupported recommendations.
- Write a concise scaling review and ADR based on empirical evidence.

## Tech Setup

- Provided reference platform with API, worker, PostgreSQL, Redis, LocalStack (S3 emulated service), and synthetic load generator.
- Docker Compose local runtime with one-command startup (`docker compose up`).
- Prometheus, Grafana, Jaeger, OpenTelemetry SDK with `boto3` auto-instrumentation, and application logs.
- Prebuilt Grafana dashboard with one misleading or incomplete signal.
- Broken trace propagation scenario (spanning FastAPI → `boto3` S3 call → Postgres) and one metric defect.
- Deterministic provider-latency scenario pack with published development cases and held-out grading cases.
- Capacity notebook seed with traffic, storage, and AWS SDK concurrency inputs, pre-populated from published AWS quotas and `botocore` pool defaults.
- Shared `boto3` client factory with sentinel credentials and injected `endpoint_url`, plus the CI gate that fails on clients constructed outside it.
- Seeded flawed AI capacity analysis, expected-issue list, and review rubric.
- Mermaid or equivalent C4 diagram tooling.

## Learning Objectives

- Explain how the reference platform and local AWS SDK interactions work at runtime.
- Compare monolith and microservice trade-offs from observed behavior, focusing on AI service separation and S3 diagnostic payload storage.
- Interpret golden-signal dashboards and Jaeger traces under load, identifying latency introduced by external AI dependencies and by the real data tier.
- Repair unsafe or incomplete observability instrumentation across HTTP and AWS SDK boundaries.
- Estimate 10x growth impact with named assumptions for AI token throughput and cloud SDK connection pooling, citing published quotas and stating explicitly which figures an emulator cannot supply.
- Explain why an emulated dependency is valid evidence for *call structure and correctness* but not for *latency, throughput, or capacity*.
- Defend the first likely scaling bottleneck using telemetry and capacity math.
- Reject at least one false scaling explanation using empirical evidence.
- Communicate a practical scaling recommendation to engineering leadership via an ADR.

## Theory Topics

- System architecture basics, request paths, state locations, and C4 diagrams.
- Monolith vs. microservices as a diagnostic baseline.
- Scale reasoning, latency percentiles, throughput, queues, bottlenecks, and AWS SDK connection pooling.
- Observability first principles, metrics, dashboards, distributed tracing, and metric cardinality.
- LocalStack Base fundamentals, `boto3` SDK endpoint overrides (`endpoint_url="http://localstack:4566"`), and the fidelity boundary between emulated and real AWS.
- LLM fundamentals for reviewing AI-generated engineering analysis.
- ADR writing and evidence-based technical recommendations.

## Delivery Limits

- No cloud deployment or public endpoint is permitted. The full project, including the demonstration, runs locally through Docker Compose using LocalStack Base.
- The required latency behavior is exercised through the deterministic provider scenario pack and the real PostgreSQL/Redis tier, not paid or public cloud services.
- **No performance, latency, throughput, or capacity conclusion may be drawn from emulated AWS calls.** The rubric must reject any load-test finding, dashboard claim, or ADR recommendation whose evidence is a LocalStack timing. LocalStack is in scope for trace structure, call correctness, and instrumentation only.
- **Students write no new `boto3` service logic in this project.** The client factory and S3 call sites are provided; students fix instrumentation around them. Hands-on AWS SDK implementation begins in Project 2.
- Sentinel AWS credentials and the injected `endpoint_url` are mandatory and non-optional. Students must not configure real AWS credentials, and the scaffold must not read the host `~/.aws`. Bypassing the client factory is a CI failure, not a style note.
- No production feature work is required.
- Students do not build the reference platform from scratch.
- Students repair exactly two observability defects; extra instrumentation is optional.
- The platform, LocalStack container, `boto3` client factory and its CI gate, load generator, dashboards, broken trace, bad metric, capacity notebook, flawed AI artifact, expected findings, and rubric must be provided before launch.

## Workload

| Field | Hours |
| :--- | ---: |
| Theory time | 15 |
| Project work time | 52 |
| Workload calc | 67 |

⚠️ **Pending re-cost.** These hours are inherited from the canonical program. This edition adds an estimated **+2 hours** (observation-only LocalStack scope). At 67 hours across 3 weeks this project is already 22.3 h/wk — the most overloaded in the program — so the addition must be offset by displaced scope, not absorbed. See [Workload Impact](overview-and-module-map.md#workload-impact-pending-re-cost).
