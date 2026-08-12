# Project 1 - System Diagnostics, API Scaling & LocalStack Telemetry

## Project Description

Students diagnose a provided monolith-based enterprise reference platform running locally via Docker Compose alongside LocalStack Base (S3 service). They trace request paths across code, PostgreSQL, Redis, and LocalStack S3 AWS SDK (`boto3`) calls, repair observability defects in OpenTelemetry and Prometheus/Grafana, run a reproducible load test, correct an AI-generated capacity analysis, and evaluate the latency impacts of mocked LLM API calls and local cloud SDK calls on the traditional backend. The project stays local-first so every student completes the diagnostic workflow without cloud spending.

## Skills

- Run and inspect a provided production-shaped system with LocalStack AWS emulation in Docker Compose.
- Trace a request across code, logs, metrics, distributed traces, PostgreSQL, Redis, and LocalStack S3 `boto3` SDK calls.
- Repair exactly two observability defects: one trace propagation issue (including AWS SDK spans) and one metric/dashboard issue.
- Use Prometheus, Grafana, Jaeger, OpenTelemetry, and application logs to diagnose system performance.
- Run a controlled `k6` or Locust load cycle that reproduces API bottlenecks (focusing on simulated LLM latency and local S3 IOPS/SDK overhead).
- Calculate capacity from traffic, storage, latency, AWS SDK connection limits, and growth assumptions.
- Audit an AI-generated capacity artifact for math errors, weak assumptions regarding LLM token throughput, and unsupported recommendations.
- Write a concise scaling review and ADR based on empirical evidence.

## Tech Setup

- Provided reference platform with API, worker, PostgreSQL, Redis, LocalStack (S3 emulated service), and synthetic load generator.
- Docker Compose local runtime with one-command startup (`docker compose up`).
- Prometheus, Grafana, Jaeger, OpenTelemetry SDK with `boto3` auto-instrumentation, and application logs.
- Prebuilt Grafana dashboard with one misleading or incomplete signal.
- Broken trace propagation scenario (spanning FastAPI $\rightarrow$ `boto3` S3 call $\rightarrow$ Postgres) and one metric defect.
- Deterministic provider-latency scenario pack with published development cases and held-out grading cases.
- Capacity notebook seed with traffic, storage, and AWS SDK concurrency inputs.
- Seeded flawed AI capacity analysis, expected-issue list, and review rubric.
- Mermaid or equivalent C4 diagram tooling.

## Learning Objectives

- Explain how the reference platform and local AWS SDK interactions work at runtime.
- Compare monolith and microservice trade-offs from observed behavior, focusing on AI service separation and S3 diagnostic payload storage.
- Interpret golden-signal dashboards and Jaeger traces under load, identifying latency introduced by external AI dependencies and AWS SDK calls.
- Repair unsafe or incomplete observability instrumentation across HTTP and AWS SDK boundaries.
- Estimate 10x growth impact with named assumptions for AI token throughput and cloud SDK connection pooling.
- Defend the first likely scaling bottleneck using telemetry and capacity math.
- Reject at least one false scaling explanation using empirical evidence.
- Communicate a practical scaling recommendation to engineering leadership via an ADR.

## Theory Topics

- System architecture basics, request paths, state locations, and C4 diagrams.
- Monolith vs. microservices as a diagnostic baseline.
- Scale reasoning, latency percentiles, throughput, queues, bottlenecks, and AWS SDK connection pooling.
- Observability first principles, metrics, dashboards, distributed tracing, and metric cardinality.
- LocalStack Community fundamentals and `boto3` SDK endpoint overrides (`endpoint_url="http://localstack:4566"`).
- LLM fundamentals for reviewing AI-generated engineering analysis.
- ADR writing and evidence-based technical recommendations.

## Delivery Limits

- No cloud deployment or public endpoint is permitted. The full project, including the demonstration, runs locally through Docker Compose using LocalStack Base.
- The required latency behavior is exercised through the deterministic provider scenario pack and LocalStack S3, not paid or public cloud services.
- No production feature work is required.
- Students do not build the reference platform from scratch.
- Students repair exactly two observability defects; extra instrumentation is optional.
- The platform, LocalStack container, load generator, dashboards, broken trace, bad metric, capacity notebook, flawed AI artifact, expected findings, and rubric must be provided before launch.

## Submission & Assessment Criteria

- **Automated Tests**: CI pipeline must pass (linting, basic integration tests validating LocalStack S3 connectivity).
- **Required Artifacts**: PR containing the two observability fixes (FastAPI + `boto3` trace propagation) and the finalized ADR for API scaling.
- **Client Defense**: A 5-minute Loom video demonstrating the reproducible load test and explaining the telemetry findings on the dashboard (including AWS SDK spans).
- **Pass/Fail Rubric**: Must be explicitly supplied in the `projects/` directory prior to launch, defining Must-Have criteria for the ADR.

## Workload

| Field | Hours |
| :--- | ---: |
| Theory time | 15 |
| Project work time | 52 |
| Workload calc | 67 |
