# Project 3 - Resilience, LocalStack SQS/SNS & Local LLM Serving

## Project Description

Students operate the platform in a production-like local environment using strictly Docker Compose and **LocalStack Base** (SQS and SNS services). They run local LLM serving with vLLM where supported and Ollama as the grading-equivalent fallback, use LocalStack SQS and SNS for resilient asynchronous task queues and Dead Letter Queues (DLQs), use a deterministic provider emulator for failure injection, configure AWS SDK (`boto3`) retry and circuit breaker mechanics, configure one SLO alert, and run one failure lab. Terraform/OpenTofu, Kafka, and Kubernetes remain decision-level/positioning topics.

## Skills

- Package and run services with Docker, Docker Compose, and LocalStack (SQS/SNS).
- Build asynchronous queue architectures using LocalStack SQS queues, SNS topics, and Dead Letter Queues (DLQs) for failed AI task retries.
- Deploy local LLM serving infrastructure (vLLM where supported, Ollama as the grading-equivalent fallback) alongside traditional backend services.
- Implement AWS SDK (`boto3`) and LLM API resiliency patterns (Retries with Exponential Backoff, Circuit Breakers, Fallbacks).
- Build or complete CI/CD gates for tests, deployment checks, and rollback awareness.
- Design one SLO-based alert tied to user impact (e.g., SQS queue backlog age or LLM generation timeout).
- Run one failure-lab scenario (simulated LocalStack SQS queue outage / LLM API outage) and explain recovery with operational telemetry evidence.
- Audit AI-generated infrastructure and CI configuration for exposure, unsafe defaults, and missing gates.

## Tech Setup

- Containerized platform services from earlier projects.
- Docker Compose scaffold with LocalStack Base (SQS and SNS emulated services).
- Local LLM provider adapter (vLLM Docker container where supported, Ollama fallback) plus deterministic provider emulator for latency, rate-limit, malformed-response, and outage scenarios.
- LocalStack SQS queue initializer script (`awslocal sqs create-queue --queue-name ai-task-queue`).
- CI/CD pipeline with integration tests, LocalStack queue tests, deployment checks, and rollback validation.
- Prometheus, Grafana, logs, one SLO alert rule scaffold, and one reversible failure-lab script.
- Seeded flawed AI CI artifact, expected-issue list, and review rubric.

## Learning Objectives

- Deploy a multi-service platform + LocalStack SQS/SNS queues + AI serving engine into a local Docker environment.
- Explain how cloud queue topology, backpressure, and asynchronous processing affect LLM reliability.
- Explain Kubernetes, managed EKS, and Terraform at a positioning level without requiring full local implementation.
- Implement Dead Letter Queue (DLQ) inspection and retry backoff using `boto3`.
- Define one SLO alert tied to a user-impacting AI queue or inference failure.
- Handle partial failure with implemented API reliability patterns (Retries, Circuit Breakers) and recovery workflows.
- Prove resilience claims through one failure-lab evidence packet.
- Review AI-generated CI suggestions for unsafe defaults and missing safeguards.

## Theory Topics

- Docker, Docker Compose Orchestration deeply.
- Cloud Messaging patterns (AWS SQS, SNS, Fanout, FIFO, and Dead Letter Queues in LocalStack).
- AWS SDK (`boto3`) Client Config: Retries, Max Connections, Timeouts, and Backoff strategies.
- CI/CD pipelines, deployment gates, rollback, and teardown.
- Alerting, SLOs, observability, and failure-lab practice (Focusing on AI APIs and queue depth).
- LLM Provider Adapters, Rate Limits, Circuit Breakers, and API Resiliency.
- CAP, consistency models, partial-failure patterns, and backpressure.
- Kubernetes Core concepts and Managed EKS positioning (Positioning).
- OpenTofu/Terraform fundamentals and cloud topology (Positioning).

## Delivery Limits

- Per-student always-on EKS or local Kubernetes (`kind`) is not required; Docker Compose with LocalStack is strictly used for FDEs.
- No cloud deployment or public endpoint is permitted; the entire failure lab runs locally.
- Terraform/OpenTofu is optional or instructor-led.
- Students configure local LLM serving, LocalStack SQS/SNS queue DLQs, configure one SLO alert, implement one LLM/AWS SDK resilience pattern, and run one failure lab.
- `vLLM` is the scaffold default for local model-serving evidence. Ollama is a grading-equivalent local fallback when hardware cannot run vLLM; the provider emulator and LocalStack SQS script drive deterministic CI and failure-lab paths.
- Extra Kafka depth, multiple queue providers, and full chaos suites are optional or scaffolded.
- The Docker Compose scaffold, LocalStack configuration, CI config, failure script, dashboards, flawed AI artifact, expected issues, and rubric must be provided before launch.

## Submission & Assessment Criteria

- **Automated Tests**: CI pipeline must pass (deployment gates, LocalStack SQS queue tests, rollback awareness).
- **Required Artifacts**: PR containing the AWS SDK / LLM API resilience pattern (e.g., Retry / Circuit Breaker with SQS DLQ handling) and the SLO alert configuration.
- **Client Defense**: A 5-minute Loom video walking through the simulated SQS/LLM failure lab and showing how the system degrades gracefully based on telemetry.
- **Pass/Fail Rubric**: Must be explicitly supplied in the `projects/` directory, defining Must-Have criteria for the circuit breaker and DLQ implementation.

## Workload

| Field | Hours |
| :--- | ---: |
| Theory time | 24 |
| Project work time | 72 |
| Workload calc | 96 |
