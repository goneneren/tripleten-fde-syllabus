# Project 3 - Resilience, Microservices & Local LLM Serving

## Project Description

Students operate the platform in a production-like local environment using strictly Docker Compose (eschewing local Kubernetes for FDEs to focus on AI ops). They run local LLM serving with vLLM where supported and Ollama as the grading-equivalent fallback, use a deterministic provider emulator for failure injection, configure one SLO alert, implement retries and circuit breakers, and run one failure lab. Terraform/OpenTofu, Kafka, and Kubernetes remain decision-level/positioning topics.

## Skills

- Package and run services with Docker and Docker Compose Orchestration.
- Deploy local LLM serving infrastructure (vLLM where supported, Ollama as the grading-equivalent fallback) alongside traditional backend services.
- Build or complete CI/CD gates for tests, deployment checks, and rollback awareness.
- Design one SLO-based alert tied to user impact (e.g., LLM generation timeout).
- Implement event-driven reliability and LLM API resiliency (Retries, Circuit Breakers, Fallbacks).
- Run one failure-lab scenario (simulated LLM API outage) and explain recovery with operational evidence.
- Audit AI-generated infrastructure and CI configuration for exposure, unsafe defaults, and missing gates.

## Tech Setup

- Containerized platform services from earlier projects.
- Docker Compose scaffold that students modify instead of writing from scratch.
- Local LLM provider adapter (vLLM Docker container where supported, Ollama fallback) plus deterministic provider emulator for latency, rate-limit, malformed-response, and outage scenarios.
- CI/CD pipeline with tests, security checks, deployment stages, and teardown validation.
- Prometheus, Grafana, logs, one SLO alert rule scaffold, and one reversible failure-lab script.
- Redpanda or single-node Kafka via Docker Compose for the selected resilience pattern (Positioning focus for FDE).
- Seeded flawed AI CI artifact, expected-issue list, and review rubric.

## Learning Objectives

- Deploy a multi-service platform + AI serving engine into a local production-like Docker environment.
- Explain how infrastructure, deployment, scaling, and topology choices affect LLM reliability.
- Explain Kubernetes, managed EKS, and Terraform at a positioning level without requiring full implementation.
- Define one SLO alert tied to a user-impacting AI failure.
- Handle partial failure with one implemented API reliability pattern and recovery workflow.
- Prove resilience claims through one failure-lab evidence packet.
- Review AI-generated CI suggestions for unsafe defaults and missing safeguards.

## Theory Topics

- Docker, Docker Compose Orchestration deeply.
- CI/CD pipelines, deployment gates, rollback, and teardown.
- Alerting, SLOs, observability, and failure-lab practice (Focusing on AI APIs).
- LLM Provider Adapters, Rate Limits, Circuit Breakers, and API Resiliency.
- CAP, consistency models, partial-failure patterns, and backpressure.
- Kubernetes Core concepts and Managed EKS positioning (Positioning).
- OpenTofu/Terraform fundamentals and cloud topology (Positioning).
- Messaging patterns and Kafka basics (Positioning).

## Delivery Limits

- Per-student always-on EKS or local Kubernetes (`kind`) is not required; Docker Compose is strictly used for FDEs.
- No cloud deployment or public endpoint is permitted; the entire failure lab runs locally.
- Terraform/OpenTofu is optional or instructor-led.
- Students configure local LLM serving, configure one SLO alert, implement one LLM resilience pattern, and run one failure lab.
- `vLLM` is the scaffold default for local model-serving evidence. Ollama is a grading-equivalent local fallback when hardware cannot run vLLM; the provider emulator is the required deterministic CI and failure-lab path.
- Extra Kafka depth, multiple resilience patterns, and full chaos suites are optional or scaffolded.
- The Docker Compose scaffold, CI config, Redpanda setup, failure script, dashboards, flawed AI artifact, expected issues, and rubric must be provided before launch.

## Submission & Assessment Criteria

- **Automated Tests**: CI pipeline must pass (deployment gates, rollback awareness).
- **Required Artifacts**: PR containing the LLM API resilience pattern (e.g., Retry / Circuit Breaker) and the SLO alert configuration.
- **Client Defense**: A 5-minute Loom video walking through the simulated LLM failure lab and showing how the system degrades gracefully based on telemetry.
- **Pass/Fail Rubric**: Must be explicitly supplied in the `projects/` directory, defining Must-Have criteria for the circuit breaker implementation.

## Workload

| Field | Hours |
| :--- | ---: |
| Theory time | 24 |
| Project work time | 72 |
| Workload calc | 96 |
