# Project 05 — Bounded Agent Workflow and AWS Capstone

- Edition status: Alternative under evaluation; not the program of record.
- Canonical edition: The Open-Source edition remains canonical.
- Licensing boundary: Mandatory LocalStack use depends on written confirmation that its licensing is compatible with this paid program.
- Student fallback: A student who cannot obtain a LocalStack token may use the open-source variant without penalty.

## #

- 5

## Project

- Bounded Agent Workflow and AWS Capstone

## Project description 

- Students complete one continuous capstone engagement in Repository 5. In Phase 5.A, during Weeks 16-19 (80 hours), they turn an ambiguous automation request into one bounded, auditable LangGraph workflow, evaluate it locally, process a late change, and pass the technical acceptance gate. In Phase 5.B during Weeks 20-22 (60 hours), they deploy that exact accepted release through a protected course-managed AWS profile, demonstrate acceptance and cost evidence, prepare users and operators, complete Final Demo Day, hand back the system, and prove teardown.

## Skills

- Discover an ambiguous workflow, map exceptions and human decisions, define authority and escalation boundaries, and track changing assumptions.
- Frame a measurable value hypothesis, reduce scope, estimate delivery and operating cost, and define acceptance, rollback, override, and exclusion conditions.
- Build one bounded state-graph workflow with typed tools, schema validation, sandboxing, step/token/request/tool limits, human checkpoints, and a complete audit trail.
- Design deterministic success, refusal, escalation, and recovery scenarios; analyze Ragas, LLM-judge variance, traces, latency, cost, and user-visible failures.
- Process a late change, disclose evaluation gaps, pass the technical gate, and preserve release provenance through an immutable tag and manifest.
- Carry the LocalStack S3/SQS/SSM adapters through Phase 5.A, then switch endpoint URLs, sentinel credentials, and supplied adapters to the fixed real-AWS profile without changing business logic.
- Verify controls and release identity, manage acceptance/cost evidence, prepare adoption and operations, demonstrate, hand back, and tear down.

## Tech setup

- Phase 5.A: Docker Compose, carried-forward LocalStack S3/SQS/SSM adapters, `awslocal`, supplied client factory, sentinel credentials and region, LangGraph, Pydantic, Project 2 retrieval API, Ollama, and PostgreSQL.
- Phase 5.A evaluation: Ragas, Arize Phoenix, OpenTelemetry, Pytest, cached fixtures, deterministic metric scripts, and the relevant FIDELITY.md files.
- Workflow maps, role cards, assumption log, value/cost canvas, SoW addendum, acceptance checklist, change request, evaluation report, readiness memo, and release manifest.
- Phase 5.B: supplied real-AWS launch templates and deploy/teardown scripts, AWS CLI, real AWS adapters, ECR, one EC2 t3.large CPU host, S3, SQS/DLQ, SSM Parameter Store, CloudWatch, and Caddy.
- Course verifier, held-out scenario pack, budget report, protected endpoint, RACI, runbooks, user guide, escalation map, Final Demo Day run sheet, and field-playbook template.

## Learning Objectives

- Convert a vague automation request into a bounded workflow, authority model, value hypothesis, acceptance floor, rollback plan, and accountable decision structure.
- Implement an auditable agent workflow that cannot exceed its agreed authority and explain why retrieval, prompting, or tool constraints are appropriate.
- Prove useful behavior and expose failure through reproducible evaluation, calibrated manual judging, trace inspection, latency, and cost evidence.
- Pass the Phase 5.A Instructor Presentation / Review and create an immutable accepted release tag and manifest before provisioning AWS.
- Translate LocalStack endpoint configuration and adapters to the supplied real-AWS configuration without changing business logic.
- Deploy the accepted release through supplied adapters and verify provenance, access controls, TLS, rate limits, cost controls, held-out acceptance, and a real-AWS failure mode.
- Complete adoption and operational handback, Final Demo Day, final cost evidence, verified teardown, and a sanitized reusable portfolio/playbook.

## Theory topics

- Workflow discovery, ambiguity and exception management, authority design, escalation, decision ownership, and deterministic-versus-agent choices.
- Value framing, scope reduction, delivery/operating cost, acceptance design, rollback, human override, and autonomy negotiation.
- LangGraph state graphs, typed tools, schema validation, sandboxing, budgets and limits, human-in-the-loop control, audit trails, and fine-tuning decision criteria.
- Agent evaluation, golden scenarios, deterministic CI metrics, Ragas, LLM-as-judge calibration, variance, traces, observability, latency, cost, and failure interpretation.
- Change control, technical acceptance gates, evaluation-gap disclosure, release provenance, immutable manifests, and deployment readiness.
- LocalStack-to-real-AWS translation, endpoint injection, portable adapters, sentinel-versus-real credentials, FIDELITY.md boundaries, and evidence gaps.
- Least privilege, protected endpoints, real-AWS failure modes, cost governance, acceptance, adoption, handback, demonstration, and teardown.

## Delivery Limits

- Starts from TripleTen's reference solution to Project 4 in Repository 5; earlier student defects do not propagate.
- Phase 5.A is local and uses the carried-forward LocalStack S3/SQS/SSM adapters through `awslocal`; it must pass the published technical gate before Phase 5.B.
- Phase 5.B deploys only the exact instructor-accepted release, uses the real AWS CLI and supplied real-AWS adapters, and does not apply the local-endpoint CI gate to its real-AWS configuration.
- Host AWS credential directories are never mounted during local stages; Phase 5.B uses only the supplied course-managed access path.
- Students build one bounded LangGraph workflow, not a general agent platform; hands-on fine-tuning and required GPU work are out of scope.
- The program issues at most $20 for approved LLM API traffic and $180 for AWS, with a normal AWS target of at most $80; students never use personal API or AWS accounts or payment methods.
- AWS uses one fixed course-managed account/profile, one t3.large CPU host, one protected endpoint, a 14-day reviewer window, and at most one approved remediation deployment.
- GPU, NAT gateway, load balancer, managed database/search, second public IP, second always-on instance, student-created IAM principals, and untagged resources are prohibited.
- Phase 5.A acceptance must authorize provisioning and the first verified endpoint must occur by the end of Week 20, starting the 14-day reviewer window; reviewer SLA is three business days, Final Demo Day occurs by day 12, and verified teardown by day 14.
- LocalStack evidence does not prove real-AWS performance, durability, authorization, encryption, quotas, or network behavior; Final Demo Day and teardown require real-AWS evidence.

## Theory time (25% allocation)

- 35
- Hours: 35

## Project work time (75% allocation)

- 105
- Hours: 105

## Workload calc

- Formula: `=I7+J7`
- Calculated total: 140 hours
- Allocation basis: 25% theory time and 75% project work time from the canonical project estimate.

Source: `syllabus-fde-focused-5-projects/fde-focused-5-projects-localstack.md`
