# Project 03 — Reliable AI Service Delivery

- Edition status: Alternative under evaluation; not the program of record.
- Canonical edition: The Open-Source edition remains canonical.
- Licensing boundary: Mandatory LocalStack use depends on written confirmation that its licensing is compatible with this paid program.
- Student fallback: A student who cannot obtain a LocalStack token may use the open-source variant without penalty.

## #

- 3

## Project

- Reliable AI Service Delivery

## Project description 

- Students stabilize a retrieval-enabled AI service whose provider behavior and client priorities change under load. They operate local inference and deterministic provider paths, derive a defensive contract for an undocumented legacy service, implement a bounded resilience pattern, connect it to an SLO, renegotiate a changed requirement, and hand over an executable incident process.

## Skills

- Use provider abstraction and observed behavior to derive a tolerant interface specification for an undocumented legacy service.
- Handle inconsistent schemas, hidden rate limits, stale fields, denied operations, latency, malformed responses, and outages.
- Configure deadlines, bounded retry and backoff, circuit breaking, fallback, idempotency, and SQS visibility-timeout and dead-letter handling.
- Recover failed messages through one LocalStack SQS dead-letter path using the supplied JobQueue adapter.
- Define a client-visible SLO and actionable alert, run one reversible failure lab, and document residual risk.
- Analyze the scope, risk, schedule, and cost impact of a changing requirement and negotiate which commitment moves.
- Write honest engineering and stakeholder incident communications and an executable detection, mitigation, rollback, and escalation runbook.

## Tech setup

- Docker Compose with Ollama, FastAPI, deterministic provider and undocumented legacy-service emulators, and LocalStack SQS/DLQ.
- `awslocal`, the supplied client factory and JobQueue adapter, sentinel credentials and region, deterministic queue initialization, and JobQueue FIDELITY.md.
- Supplied provider adapter, resilience library, schema and rate-limit scenarios, Pytest, and bounded backoff configuration.
- OpenTelemetry, Prometheus, Grafana, k6, supplied failure injector, and timeline evidence.
- Timed asynchronous change injects, impact template, change log, incident templates, runbook template, and written briefing format.

## Learning Objectives

- Operate local and deterministic model paths through one portable provider boundary.
- Derive and implement a defensive legacy-service client from observed behavior rather than undocumented assumptions.
- Keep the client workflow safe across approved latency, rate-limit, malformed-response, and outage scenarios.
- Recover a failed message through one LocalStack SQS dead-letter path and state which real-SQS delivery behaviors the result does not prove.
- Tie one user-impact SLO and alert to reproducible detection, mitigation, and recovery evidence.
- Renegotiate a changed reliability requirement and complete an evidence-grounded operational handoff.

## Theory topics

- Provider abstraction, portable service boundaries, legacy integration discovery, schema tolerance, and permission/rate-limit inference.
- Deadlines, transient-failure classification, retry and backoff, circuit breakers, fallback, idempotency, and asynchronous failure handling.
- SQS visibility timeouts, dead-letter queues, failed-message recovery, JobQueue adapters, endpoint-safe configuration, and local-versus-real-SQS fidelity.
- SLOs, actionable alerts, user-visible failure, reversible failure testing, incident timelines, and residual-risk analysis.
- Changing-requirement clarification, impact analysis, prioritization, negotiation, change control, and context-switching trade-offs.
- Incident communication, uncertainty, audience adaptation, runbooks, escalation paths, and reusable operational patterns.
- Kubernetes, managed inference, and fine-tuning only as decision-level architecture alternatives.

## Delivery Limits

- Starts from TripleTen's reference solution to Project 2 in Repository 3; earlier student defects do not propagate.
- Runs and is graded locally; Projects 1-4 use no hosted LLM API, real AWS service, or public endpoint.
- The assessed path uses one supplied provider adapter, one configured resilience pattern, one LocalStack SQS dead-letter path, one SLO/alert, and one reversible failure lab.
- Local stages use only `awslocal`, sentinel credentials, and the supplied client factory; host AWS credentials are never mounted.
- Deterministic initialization recreates queue state, and no task assumes LocalStack persistence.
- Broad chaos suites, general messaging platforms, and hands-on fine-tuning are out of scope.
- Students must cite JobQueue FIDELITY.md and cannot claim LocalStack SQS evidence proves real-SQS performance, durability, authorization, quotas, or network behavior.
- Requirement changes are processed through deterministic asynchronous injects and explicit trade-off records rather than silently absorbed.
- The project ends with one graded operational-handoff presentation of at most 10 minutes.

## Theory time (25% allocation)

- 20
- Hours: 20

## Project work time (75% allocation)

- 60
- Hours: 60

## Workload calc

- Formula: `=I5+J5`
- Calculated total: 80 hours
- Allocation basis: 25% theory time and 75% project work time from the canonical project estimate.

Source: `syllabus-fde-focused-5-projects/fde-focused-5-projects-localstack.md`
