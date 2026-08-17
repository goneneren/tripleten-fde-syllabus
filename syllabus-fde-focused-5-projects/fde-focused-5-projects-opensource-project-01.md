# Project 01 — Client Discovery and System Diagnostics

## #

- 1

## Project

- Client Discovery and System Diagnostics

## Project description 

- Students enter an unreliable AI-enabled enterprise workflow as an FDE, not as a greenfield developer. They clarify the business problem, navigate a supplied local system, diagnose and repair one seeded failure, and defend an evidence-backed next decision.
- The project emphasizes discovery, evidence triage, causal reasoning, scope control, ownership, and stakeholder communication under ambiguity. Just-in-time theory is introduced while tracing the workflow, testing hypotheses, interpreting telemetry, and preparing the diagnostic handoff.

## Skills

- Conduct customer discovery, map stakeholders, separate symptoms and assumptions from verified facts, and define measurable success criteria.
- Orient quickly in an unfamiliar codebase and trace one request through code, logs, metrics, PostgreSQL, Redis, and distributed traces.
- Reproduce a deterministic failure, test hypotheses, repair one observability defect, and validate the result with before-and-after evidence.
- Identify the first supported bottleneck and reject one plausible but unsupported explanation.
- Frame bounded options, estimate effort and capacity with explicit assumptions, and adapt technical evidence for business stakeholders.
- Produce an ADR, evidence packet, risk record, recommendation, and defensible client handoff.

## Tech setup

- Pinned reduced Docker Compose profile with FastAPI, PostgreSQL, Redis, OpenTelemetry, Prometheus, Grafana, and Tempo.
- Pytest, k6, and a deterministic provider emulator with published and held-out scenarios.
- Supplied architecture map, seeded trace/metric/dashboard defect, discovery template, role cards, fixed transcript, and checkpoint-triggered injects.
- Git, pull-request workflow, ADR template, recommendation template, estimation worksheet, decision log, and evidence packet.

## Learning Objectives

- Explain the client workflow, desired outcome, constraints, stakeholders, and evidence gaps before changing the system.
- Run and interpret the supplied local platform and follow one important request path across its runtime signals.
- Reproduce and repair the assigned failure while preserving a clear causal evidence chain.
- Use telemetry and bounded load evidence to justify a bottleneck diagnosis and a practical next decision.
- Present alternatives, assumptions, effort, business impact, unresolved risks, and excluded work without inventing evidence.
- Deliver and defend an auditable diagnostic handoff through the required Instructor Presentation / Review.

## Theory topics

- FDE discovery, active listening, stakeholder mapping, workflow tracing, assumption management, and measurable success criteria.
- Runtime architecture, request paths, state locations, codebase orientation, and monolith-versus-microservices as a decision prompt.
- Logs, metrics, traces, golden signals, latency, throughput, bottlenecks, controlled load, and evidence triage.
- Hypothesis testing, causal reasoning, observability defects, before-and-after validation, and residual uncertainty.
- Effort and capacity estimation, option framing, ADRs, scope control, risk communication, and audience adaptation.

## Delivery Limits

- Starts from the supplied initial legacy system in Repository 1.
- Runs and is graded locally; no cloud account, public endpoint, or production deployment is allowed.
- Students investigate the supplied system rather than rebuilding it and use the supplied architecture map instead of producing a complete C4 model.
- The assessed repair is bounded to the scenario-selected trace, metric, or dashboard defect and one deterministic failure path.
- Discovery and stakeholder pressure are graded through deterministic asynchronous materials; optional live practice does not affect completion.
- The project ends with one graded Instructor Presentation / Review recording of at most 10 minutes; evidence may be resubmitted, but implementation is not reopened.

## Theory time (25% allocation)

- 15
- Hours: 15

## Project work time (75% allocation)

- 45
- Hours: 45

## Workload calc

- Formula: `=I3+J3`
- Calculated total: 60 hours
- Allocation basis: 25% theory time and 75% project work time from the canonical project estimate.

Source: `syllabus-fde-focused-5-projects/fde-focused-5-projects-opensource.md`
