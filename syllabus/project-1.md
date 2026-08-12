# Project 1 - System Diagnostics and API Scaling

## Project Description

Students diagnose a provided monolith-based enterprise reference platform running locally via Docker Compose. They trace one important request path, repair observability defects, run a reproducible load test, correct an AI-generated capacity analysis, and evaluate the latency impacts of mocked LLM API calls on the traditional backend. The project stays local-first so every student can complete the diagnostic workflow without cloud access.

## Skills

- Run and inspect a provided production-shaped system instead of building it from scratch.
- Trace a request across code, logs, metrics, distributed traces, PostgreSQL, and Redis.
- Repair exactly two observability defects: one trace propagation issue and one metric/dashboard issue.
- Use Prometheus, Grafana, Jaeger, OpenTelemetry, and application logs to diagnose behavior.
- Run a controlled `k6` or Locust load cycle that reproduces API bottlenecks (specifically focusing on simulated LLM latency).
- Calculate capacity from traffic, storage, latency, and growth assumptions.
- Audit an AI-generated capacity artifact for math errors, weak assumptions regarding LLM token throughput, and unsupported recommendations.
- Write a concise scaling review and ADR based on evidence.

## Tech Setup

- Provided reference platform with API, worker, PostgreSQL, Redis, and synthetic load generator.
- Docker Compose local runtime with one-command startup.
- Prometheus, Grafana, Jaeger, OpenTelemetry, and application logs.
- Prebuilt dashboard with one misleading or incomplete signal.
- Broken trace propagation scenario and one metric defect.
- Deterministic provider-latency scenario pack with published development cases and held-out grading cases.
- Capacity notebook seed with traffic and growth inputs.
- Seeded flawed AI capacity analysis, expected-issue list, and review rubric.
- Mermaid or equivalent C4 diagram tooling.

## Learning Objectives

- Explain how the reference platform works at runtime.
- Compare monolith and microservice trade-offs from observed behavior, focusing on AI service separation.
- Interpret golden-signal dashboards and traces under load, identifying latency introduced by external AI dependencies.
- Repair unsafe or incomplete observability instrumentation.
- Estimate 10x growth impact with named assumptions for AI token throughput.
- Defend the first likely scaling bottleneck using telemetry and capacity math.
- Reject at least one false scaling explanation using evidence.
- Communicate a practical scaling recommendation to engineering leadership.

## Theory Topics

- System architecture basics, request paths, state locations, and C4 diagrams.
- Monolith vs. microservices as a diagnostic baseline.
- Scale reasoning, latency percentiles, throughput, queues, and bottlenecks.
- Observability first principles, metrics, dashboards, tracing, and metric cardinality.
- LLM fundamentals for reviewing AI-generated engineering analysis.
- ADR writing and evidence-based technical recommendations.

## Delivery Limits

- No cloud deployment or public endpoint is permitted. The full project, including the demonstration, runs locally through Docker Compose.
- The required latency behavior is exercised through the deterministic provider scenario pack, not a paid or public LLM API.
- No production feature work is required.
- Students do not build the reference platform from scratch.
- Students repair exactly two observability defects; extra instrumentation is optional.
- The platform, load generator, dashboards, broken trace, bad metric, capacity notebook, flawed AI artifact, expected findings, and rubric must be provided before launch.

## Submission & Assessment Criteria

- **Automated Tests**: CI pipeline must pass (linting, basic integration tests).
- **Required Artifacts**: PR containing the two observability fixes and the finalized ADR for API scaling.
- **Client Defense**: A 5-minute Loom video demonstrating the reproducible load test and explaining the telemetry findings on the dashboard.
- **Pass/Fail Rubric**: Must be explicitly supplied in the `projects/` directory prior to launch, defining Must-Have criteria for the ADR.

## Workload

| Field | Hours |
| :--- | ---: |
| Theory time | 15 |
| Project work time | 52 |
| Workload calc | 67 |
