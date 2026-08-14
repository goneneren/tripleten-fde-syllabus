# AI Forward Deployed Engineer — Six-Project LocalStack Program

## Executive summary

This candidate program prepares experienced software engineers to work as AI Forward Deployed Engineers: discovering ambiguous client problems, scoping delivery, building and evaluating production-shaped AI systems, managing stakeholders, and handing a bounded solution into operation. It is project-first and includes all just-in-time theory, implementation, documentation, review, and defense work within **22 weeks × 20 hours/week = 440 hours**.

Projects 1–5 run locally with Docker Compose, LocalStack Hobby, and selected open-source containers. Students use individually owned LocalStack accounts on their laptops for personal, non-production educational work; no real AWS account or public endpoint is used. Project 6 first passes the same local acceptance path and then deploys one temporary, protected endpoint in a course-managed AWS sandbox. The total per-student program allowance remains **$20 for approved LLM APIs and $180 for AWS**.

This is not an entry-level or zero-to-hero program. Admission requires a practical assessment of Python, Git, REST APIs, SQL and relational databases, Docker, debugging, and basic cloud concepts. Customer-facing assessments are asynchronous and deterministic, using role cards, transcripts or stakeholder bots, timed injects, evidence templates, recorded defenses, and common rubric anchors.

### LocalStack delivery stack

- **Orchestration and application runtime:** Docker Compose, LocalStack, Python, FastAPI, PostgreSQL, and Redis.
- **Object and document storage:** LocalStack S3; DynamoDB is used only where a bounded metadata or state use case justifies it.
- **Search and retrieval:** PostgreSQL/pgvector and LocalStack OpenSearch APIs; performance parity is not assumed.
- **Messaging and integration:** LocalStack SQS with a dead-letter queue and selected SNS, Lambda, EventBridge, or API Gateway REST exercises.
- **Identity and secrets:** development-mode Keycloak plus LocalStack IAM APIs, SSM Parameter Store, Secrets Manager, and KMS APIs.
- **AI:** LangGraph, Ollama, optional local vLLM, Ragas, and Arize Phoenix; unsupported managed AI services use local open-source equivalents.
- **Observability and security:** OpenTelemetry, Prometheus, Grafana, Jaeger or Tempo, selected LocalStack CloudWatch APIs, Semgrep, Trivy, and Gitleaks.
- **Cloud transition:** supplied AWS templates replace local endpoint URLs and sentinel credentials in Project 6; students do not build a general cloud platform.

### LocalStack adoption and fidelity boundary

- LocalStack is a preferred local AWS API emulator, not evidence of AWS production fidelity.
- Before launch, TripleTen should obtain written confirmation that mandatory use in this paid educational program is compatible with the Hobby terms. If it is not, use the open-source program variant.
- Students create and control individual accounts and tokens. TripleTen does not distribute tokens or operate shared Hobby infrastructure.
- Local projects use sentinel AWS credentials and explicit local endpoint URLs. Host AWS credential folders are never mounted into student containers.
- Hobby IAM APIs may be exercised, but IAM policy enforcement is not graded. Local state is recreated through deterministic initialization scripts rather than assumed persistent.
- Service availability does not imply complete API, performance, security, or operational parity. Each project publishes its assessed subset and known limitations.

## Program and project summary

| Project | Weeks | Hours | Engagement outcome |
|---|---:|---:|---|
| 1. Client Discovery and System Diagnostics | 1–3 | 60 | Diagnose an unreliable AI-enabled workflow and recommend a bounded next decision. |
| 2. Enterprise Data Integration and Hybrid RAG | 4–7 | 80 | Deliver and defend a retrieval system over messy enterprise data. |
| 3. Reliable AI Service Delivery | 8–11 | 80 | Stabilize an AI service under provider failures and changing requirements. |
| 4. Security, Guardrails and Governance Approval | 12–15 | 80 | Secure a high-value AI workflow and obtain a defensible risk decision. |
| 5. Multi-Agent Workflow Under Ambiguity | 16–19 | 80 | Build and evaluate one bounded, auditable agent workflow. |
| 6. AWS Capstone, Adoption and Handback | 20–22 | 60 | Deploy the accepted system temporarily, prove value and safety, hand it back, and tear it down. |
| **Total** | **22** | **440** | **Six sequential field-delivery engagements.** |

## Program delivery contract

- Every task estimate includes just-in-time theory, implementation, documentation, review, and defense.
- Every project produces a client-facing decision or communication artifact.
- Projects 1–5 are locally runnable and graded; no public endpoint or cloud deployment is allowed.
- Project 5 creates the capstone repository. Project 6 deploys, accepts, hands back, and tears down that same repository.
- Published and held-out scenarios use the same interface but separate evidence. Reviewers grade decisions and evidence, not improvisational performance.
- LocalStack teaches selected AWS API contracts and local-to-cloud configuration boundaries. Students must explain its fidelity limits and may not claim that local evidence proves AWS performance, IAM enforcement, durability, or production security.
- Optional local GPU work never affects pass/fail grading. AWS GPU access is available only in Project 6 under its budget and scheduling controls.

## Project 1 — Client Discovery and System Diagnostics

### Project summary

Students enter an unreliable AI-enabled enterprise workflow as an FDE, not as a greenfield developer. They clarify the business problem, navigate a supplied local system, diagnose a seeded failure, and defend an evidence-backed recommendation. The emphasis is discovery, evidence triage, ownership, and communication under ambiguity.

- **Schedule:** Weeks 1–3 / 60 hours
- **Local environment:** Docker Compose, LocalStack S3 and selected CloudWatch APIs, FastAPI, PostgreSQL, Redis, OpenTelemetry, Prometheus, Grafana, and Jaeger or Tempo.
- **Project evidence:** discovery record, repaired system, before/after evidence, ADR, recommendation playback, and diagnostic handoff.

### Task 1.1 — Engagement kickoff and stakeholder discovery (14 hours)

- **[Summary]** Establish what the client is trying to achieve before investigating implementation details.
- **[Skills]** Customer discovery, active listening, problem framing, stakeholder mapping, assumption management, success criteria.
- **[Tools]** Asynchronous role cards, supplied transcript or stakeholder bot, timed injects, discovery template, decision log.
- Trace users, workflow, desired business outcome, constraints, and known exceptions.
- Separate reported symptoms, assumptions, and facts requiring technical validation.
- Capture open questions, decision owners, competing priorities, and measurable success criteria.
- Produce a discovery record from a deterministic asynchronous simulation.

### Task 1.2 — Runtime orientation and evidence triage (10 hours)

- **[Summary]** Understand the supplied platform quickly enough to investigate one important request path.
- **[Skills]** Codebase orientation, request tracing, log and metric interpretation, architecture reading, technical prioritization.
- **[Tools]** Docker Compose, LocalStack, AWS CLI or `awslocal`, FastAPI, PostgreSQL, Redis, OpenTelemetry, Prometheus, Grafana, Jaeger or Tempo.
- Run the supplied API, worker, database, cache, LocalStack, and observability services locally.
- Follow one request through code, logs, metrics, and a distributed trace.
- Use the supplied architecture map rather than producing a complete C4 model.
- Treat monolith-versus-microservices as a decision prompt, not a baseline theory module.

### Task 1.3 — Diagnose and repair the seeded failure (18 hours)

- **[Summary]** Reproduce the client-visible failure and make one evidence-backed repair.
- **[Skills]** Reproduction, hypothesis testing, bottleneck analysis, observability repair, validation, causal reasoning.
- **[Tools]** Pytest, k6, LocalStack CloudWatch APIs, OpenTelemetry, Prometheus, Grafana, Jaeger or Tempo, deterministic provider emulator.
- Run one bounded load and provider-latency scenario.
- Repair one trace, metric, or dashboard defect selected by the scenario.
- Identify the first supported bottleneck and reject one plausible false explanation.
- Re-run the same scenario and record before-and-after evidence.

### Task 1.4 — Problem framing and recommendation playback (10 hours)

- **[Summary]** Translate technical evidence into a decision the stakeholder can act on.
- **[Skills]** Technical synthesis, option framing, effort estimation, business communication, audience adaptation.
- **[Tools]** Recommendation template, lightweight estimation worksheet, architecture decision record.
- Rewrite the initial problem statement using verified workflow evidence.
- Present bounded alternatives, including a no-AI or process-change option when appropriate.
- Estimate effort and capacity using explicit assumptions.
- Record separate engineering-detail and business-impact explanations.

### Task 1.5 — Diagnostic handoff (8 hours)

- **[Summary]** Leave the client with an auditable diagnosis and a bounded next decision.
- **[Skills]** Ownership, handoff writing, risk communication, recommendation defense, scope control.
- **[Tools]** Git, pull request, ADR, evidence packet, recorded asynchronous defense.
- Submit the repair, evidence packet, concise ADR, and updated workflow trace.
- Record unresolved risks, excluded work, and next discovery questions.
- Respond to a timed stakeholder challenge without inventing evidence.
- Defend ownership of the recommendation in a recorded response.

## Project 2 — Enterprise Data Integration and Hybrid RAG

### Project summary

Students scope and deliver a retrieval system over messy client documents without turning the engagement into a platform rewrite. They work through data ownership and access constraints, construct a reproducible ingestion path, implement hybrid retrieval, evaluate failure modes, and defend a statement of work.

- **Schedule:** Weeks 4–7 / 80 hours
- **Local environment:** Docker Compose, LocalStack S3, bounded DynamoDB metadata, LocalStack OpenSearch APIs, PostgreSQL/pgvector, supplied document parser, local embeddings, and a supplied cross-encoder.
- **Project evidence:** data discovery record, ingestion report, retrieval API, golden set, evaluation report, and defended SoW.

### Task 2.1 — Data and use-case discovery (12 hours)

- **[Summary]** Determine whose decision retrieval supports and which data can be used safely.
- **[Skills]** Data discovery, domain interviewing, ownership mapping, access analysis, acceptance-criteria design.
- **[Tools]** Stakeholder role cards, data inventory, access matrix, golden-query template.
- Analyze asynchronous responses from domain, data-owner, and compliance stakeholders.
- Document source ownership, access constraints, freshness needs, and failure consequences.
- Define measurable retrieval acceptance criteria before choosing technical methods.
- Identify one process or data-quality problem that RAG should not conceal.

### Task 2.2 — Messy-document ingestion (20 hours)

- **[Summary]** Build a reproducible ingestion pipeline for a deliberately bounded enterprise document set.
- **[Skills]** Ingestion design, metadata normalization, deduplication, chunking, embedding, data-quality validation.
- **[Tools]** LocalStack S3 and DynamoDB, AWS CLI or `awslocal`, supplied PDF/HTML parser, PostgreSQL, Python, local embedding model, Docker Compose.
- Use the supplied robust parser with text-based PDFs and clean, bounded table structures; OCR library selection is out of scope.
- Store source documents in LocalStack S3, track bounded ingestion state in DynamoDB, and normalize metadata, duplicate identifiers, malformed content, and access labels.
- Implement bounded chunking and local embedding through the supplied pipeline scaffold.
- Produce ingestion-quality evidence for published and held-out fixtures.

### Task 2.3 — Hybrid retrieval service (24 hours)

- **[Summary]** Implement the smallest production-shaped retrieval boundary that meets the agreed use case.
- **[Skills]** Dense and sparse retrieval, reranking, authorization metadata propagation, API extension, migration use.
- **[Tools]** PostgreSQL/pgvector, LocalStack OpenSearch APIs, supplied local cross-encoder, FastAPI, Alembic, AWS CLI or `awslocal`.
- Combine pgvector dense retrieval with keyword retrieval through the assessed LocalStack OpenSearch API subset.
- Rerank hybrid candidates locally before returning the final result set.
- Preserve source metadata and authorization attributes through retrieval.
- Extend the supplied versioned API and reuse provided migrations, repositories, and connection pooling.

### Task 2.4 — Retrieval evaluation and failure analysis (14 hours)

- **[Summary]** Demonstrate when retrieval succeeds, when it fails, and why.
- **[Skills]** Golden-set design, retrieval metrics, latency analysis, error attribution, evidence-based iteration.
- **[Tools]** Pytest, evaluation fixtures, recall/precision metrics, OpenTelemetry, notebooks or supplied reporting script.
- Build a compact golden query set with relevance expectations.
- Measure retrieval quality and latency against agreed criteria.
- Attribute misses to parsing, chunking, metadata, dense retrieval, keyword retrieval, or reranking.
- Recommend one bounded improvement supported by evidence.

### Task 2.5 — Scope and statement-of-work defense (10 hours)

- **[Summary]** Convert discovery and technical findings into a delivery agreement.
- **[Skills]** SoW writing, scope control, estimation, negotiation, change rejection, acceptance definition.
- **[Tools]** SoW template, estimation worksheet, assumption log, recorded stakeholder inject.
- Define outcomes, deliverables, assumptions, exclusions, acceptance criteria, and responsibilities.
- Estimate the next increment and identify its largest uncertainty.
- Process a stakeholder request that expands scope without moving time or budget.
- Defend what will not be built and record the resulting decision.

## Project 3 — Reliable AI Service Delivery

### Project summary

Students stabilize a retrieval-enabled AI service whose provider behavior and client priorities change under load. They operate local inference and deterministic provider paths, implement a bounded resilience pattern, connect it to an SLO, renegotiate a changed requirement, and hand over an executable incident process.

- **Schedule:** Weeks 8–11 / 80 hours
- **Local environment:** Docker Compose, LocalStack SQS/DLQ and SNS, Ollama or optional local vLLM, provider emulator, OpenTelemetry, Prometheus, and Grafana.
- **Project evidence:** resilient service, scenario results, SLO and alert, failure timeline, approved change record, incident communications, and runbook.

### Task 3.1 — Local AI runtime and service boundary (18 hours)

- **[Summary]** Operate the platform through one portable model-provider boundary.
- **[Skills]** Provider abstraction, local inference operations, service-boundary design, fallback reasoning, hardware-aware delivery.
- **[Tools]** Docker Compose, Ollama, optional local vLLM, FastAPI, deterministic provider emulator.
- Run the supplied multi-service environment locally.
- Use one provider adapter across local inference and deterministic scenarios.
- Use Ollama for the common path; local vLLM is optional when hardware supports it.
- Explain Kubernetes and cloud topology only as relevant alternatives.

### Task 3.2 — Provider resilience (20 hours)

- **[Summary]** Keep the client workflow safe during latency, rate-limit, malformed-response, and outage scenarios.
- **[Skills]** Deadlines, retry and backoff, circuit breaking, fallback, idempotency, asynchronous failure handling.
- **[Tools]** LocalStack SQS, dead-letter queue and SNS, AWS SDK, provider emulator, Tenacity or supplied resilience library, Pytest, OpenTelemetry.
- Implement one primary pattern: bounded retry with backoff or circuit breaker with fallback.
- Enforce deadlines, structured failures, and idempotent behavior where required.
- Use LocalStack SQS and a dead-letter queue where the selected workflow requires asynchronous recovery; use SNS only for the supplied notification path.
- Prove behavior through deterministic provider scenarios.

### Task 3.3 — SLO and failure lab (18 hours)

- **[Summary]** Connect one operational objective to a client-visible failure and recovery workflow.
- **[Skills]** SLO design, alerting, reversible failure testing, incident timelines, residual-risk analysis.
- **[Tools]** Prometheus, Grafana, OpenTelemetry, Toxiproxy or supplied failure injector, k6.
- Define one user-impact SLO and one actionable alert.
- Run one reversible failure lab and capture detection, mitigation, and recovery evidence.
- Validate the selected resilience behavior under failure.
- Document remaining failure modes without constructing a broad chaos suite.

### Task 3.4 — Changing-requirements simulation (12 hours)

- **[Summary]** Re-plan delivery after a stakeholder changes a reliability requirement.
- **[Skills]** Clarification, impact analysis, negotiation, prioritization, change control, decision documentation.
- **[Tools]** Timed asynchronous inject, impact template, change log, recorded response.
- Clarify the outcome, urgency, decision owner, and hidden trade-off.
- Assess effects on scope, risk, schedule, and operational cost.
- Negotiate which commitment moves out when the new requirement moves in.
- Record the approved change rather than silently absorbing it.

### Task 3.5 — Incident communication and operational handoff (12 hours)

- **[Summary]** Communicate a failure honestly and leave an executable recovery process.
- **[Skills]** Incident communication, audience adaptation, uncertainty communication, runbook design, escalation planning.
- **[Tools]** Incident templates, runbook template, timeline evidence, recorded briefing.
- Write separate engineering and stakeholder incident updates.
- Record a short briefing while recovery information remains uncertain.
- Deliver a focused detection, mitigation, rollback, and escalation runbook.
- Convert the failure lesson into one reusable delivery pattern.

## Project 4 — Security, Guardrails and Governance Approval

### Project summary

Students secure one high-value AI workflow and make the result inspectable by engineering, security, compliance, and business stakeholders. They select proportionate controls, implement one bounded security boundary, test it against held-out attacks, and obtain a documented risk decision without overstating educational evidence.

- **Schedule:** Weeks 12–15 / 80 hours
- **Local environment:** Keycloak in development mode, LocalStack SSM Parameter Store, Secrets Manager, KMS, IAM and CloudWatch APIs, Semgrep, Trivy, Gitleaks, OpenTelemetry, and supplied attack scenarios.
- **Project evidence:** stakeholder risk record, threat model, tested controls, control matrix, residual-risk register, and executive decision.

### Task 4.1 — Security and governance discovery (12 hours)

- **[Summary]** Identify actors, sensitive data, decision rights, and risk tolerance.
- **[Skills]** Security discovery, workshop facilitation, conflict reconciliation, risk treatment, governance ownership.
- **[Tools]** Stakeholder role cards, data-flow template, risk register, asynchronous workshop injects.
- Reconcile engineering, security, compliance, and business expectations.
- Map sensitive data, availability needs, audit expectations, and decision rights.
- Distinguish risks requiring control, acceptance, transfer, or feature removal.
- Record conflicts and accountable decision owners.

### Task 4.2 — Threat model and control selection (18 hours)

- **[Summary]** Model one workflow deeply enough to choose proportionate controls.
- **[Skills]** STRIDE, trust-boundary analysis, abuse-case design, prompt-injection analysis, control selection.
- **[Tools]** Threat-model template, data-flow diagram, OWASP LLM guidance, control decision record.
- Identify assets, actors, trust boundaries, and high-impact abuse cases.
- Emphasize prompt injection and unsafe output handling.
- Select controls using evidence and reject unnecessary complexity.
- Treat legal frameworks as engineering-control mapping, not certification.

### Task 4.3 — Implement the security boundary (30 hours)

- **[Summary]** Implement and verify the smallest control set needed for the workflow.
- **[Skills]** OIDC/RBAC integration, prompt and output controls, PII redaction, audit logging, secrets management, CI security.
- **[Tools]** Keycloak, LocalStack SSM Parameter Store, Secrets Manager, KMS and IAM APIs, FastAPI, Presidio or supplied redactor, Semgrep, Trivy, Gitleaks, Pytest.
- Protect one endpoint using the supplied development OIDC/RBAC scaffold.
- Add prompt-injection handling, output validation, PII redaction, and audit logging at one AI boundary.
- Move one secret into LocalStack SSM or Secrets Manager, exercise encryption through the assessed KMS API subset, and configure one deterministic CI security gate.
- Test published and held-out attack and data-leakage scenarios; application authorization is graded, but Hobby IAM policy enforcement is not.

### Task 4.4 — Governance evidence and adversarial review (12 hours)

- **[Summary]** Make security claims inspectable by people who did not build the system.
- **[Skills]** Evidence mapping, adversarial review, AI-output verification, residual-risk writing, human-oversight design.
- **[Tools]** Control matrix, test evidence, risk register, supplied flawed AI-generated artifact.
- Link risks, controls, tests, evidence, and owners.
- Review a flawed AI-generated threat or compliance artifact for overclaims and omissions.
- Record residual risks and limits of the evidence.
- Define required human oversight and review triggers.

### Task 4.5 — Executive risk decision (8 hours)

- **[Summary]** Obtain a go, conditional-go, or no-go decision without hiding uncertainty.
- **[Skills]** Executive communication, risk translation, boundary defense, decision facilitation, accountability.
- **[Tools]** Executive brief, recorded defense, timed pressure inject, decision record.
- Present value, material risks, implemented controls, and remaining exposure.
- Respond to pressure to describe educational evidence as production certification.
- Recommend a decision and defend its conditions.
- Record the outcome, owner, conditions, and review date.

## Project 5 — Multi-Agent Workflow Under Ambiguity

### Project summary

Students turn a vague automation request into one bounded, auditable LangGraph workflow. They define the authority boundary, implement the smallest useful agent flow, evaluate it with deterministic scenarios, process a late change, and defend the solution to technical and business audiences. This project creates the repository deployed in Project 6.

- **Schedule:** Weeks 16–19 / 80 hours
- **Local environment:** LangGraph, Project 2 retrieval, LocalStack S3/SQS/Secrets Manager/CloudWatch APIs, Ollama, Ragas, Arize Phoenix, PostgreSQL, and Docker Compose.
- **Project evidence:** workflow map, value hypothesis, bounded agent, audit trail, evaluation report, approved change, and dual-room recorded defense.

### Task 5.1 — Ambiguous client brief and workflow discovery (12 hours)

- **[Summary]** Turn a vague automation request into an observable workflow and decision problem.
- **[Skills]** Workflow discovery, ambiguity management, exception analysis, authority design, assumption tracking.
- **[Tools]** Process map, stakeholder role cards, timed injects, assumption log, decision inventory.
- Trace current handoffs, exceptions, failure costs, and human decision points.
- Identify where deterministic software is safer or cheaper than an agent.
- Define authority, escalation conditions, prohibited actions, and decision owners.
- Update assumptions as stakeholder information changes.

### Task 5.2 — Scope and value hypothesis (10 hours)

- **[Summary]** Select a narrow agent use case with an evidence-based business outcome.
- **[Skills]** Value framing, scope reduction, cost estimation, acceptance design, rollback planning, autonomy negotiation.
- **[Tools]** Value hypothesis canvas, cost model, SoW addendum, acceptance checklist.
- Define value through revenue, risk, time, or operating cost.
- Estimate delivery and operating cost from named assumptions.
- Set acceptance, exclusion, rollback, and human-override conditions.
- Defend a smaller scope when broad autonomy is requested.

### Task 5.3 — Bounded agent implementation (24 hours)

- **[Summary]** Implement one auditable workflow that cannot exceed its agreed authority.
- **[Skills]** State-graph design, tool integration, schema validation, sandboxing, budget controls, human-in-the-loop design.
- **[Tools]** LangGraph, Pydantic, Project 2 retrieval API, LocalStack SQS and Secrets Manager, Ollama, PostgreSQL, Docker Compose.
- Build one bounded multi-step tool flow rather than a general agent platform.
- Reuse Project 2 retrieval, use LocalStack SQS for the supplied bounded asynchronous tool path, and add step, token, request, and tool limits.
- Preserve tool calls, state transitions, failures, and human decisions in an audit trail.
- PEFT/LoRA preparation is optional and local-only in Project 5; learners without suitable hardware use the common deterministic baseline. Any AWS GPU execution is deferred to Project 6.

### Task 5.4 — Agent evaluation and observability (18 hours)

- **[Summary]** Prove useful behavior and expose important failures without relying on demo impressions.
- **[Skills]** Scenario-set design, agent evaluation, trace analysis, cost analysis, judge calibration, failure interpretation.
- **[Tools]** Ragas, Arize Phoenix, OpenTelemetry, selected LocalStack CloudWatch APIs, Pytest, cached fixtures, bounded LLM-as-judge worksheet.
- Cover success, refusal, escalation, and recovery in a compact golden scenario set.
- Run deterministic CI smoke evaluations using cached fixtures.
- Use Ragas for bounded retrieval and response-quality evaluation and Phoenix for trace inspection.
- Calibrate a small manual LLM-as-judge sample; it is not the CI authority.

### Task 5.5 — Change control and dual-room defense (16 hours)

- **[Summary]** Revise the solution under pressure and defend it to technical and business audiences.
- **[Skills]** Change control, impact analysis, technical defense, executive storytelling, adoption-risk communication.
- **[Tools]** Change request, architecture evidence, evaluation report, recorded technical and executive defenses.
- Process a late stakeholder request through explicit analysis and approval.
- Explain architecture, safety boundaries, evaluation gaps, and rejected alternatives to engineers.
- Present value, limitations, adoption risk, and the next investment decision to a simulated executive.
- Record approved change, deferred work, and uncertainty.

## Project 6 — AWS Capstone, Adoption and Handback

### Project summary

Students take the locally accepted Project 5 repository through a supplied, protected AWS deployment path. They agree on responsibilities and cost controls, demonstrate acceptance evidence, prepare users and operators, defend the engagement asynchronously, and prove teardown. The project teaches bounded cloud delivery—not general AWS administration.

- **Schedule:** Weeks 20–22 / 60 hours
- **Cloud boundary:** one course-managed AWS sandbox, one temporary protected endpoint, a 14-day maximum window, and mandatory teardown.
- **Budget:** $20 maximum for approved LLM APIs and $180 maximum for AWS; normal delivery should target materially below the ceiling.
- **GPU boundary:** optional, program-scheduled evidence sessions only; recommended pilot allowance 4–8 GPU hours per student, with automated stop controls. The persistent endpoint must remain CPU/API-backed.
- **Project evidence:** deployment agreement, protected endpoint, verifier report, acceptance decision, handback pack, recorded defenses, final cost, and teardown proof.

### Task 6.1 — Capstone kickoff and deployment agreement (8 hours)

- **[Summary]** Agree on responsibilities, acceptance evidence, cost limits, and exit conditions before using AWS.
- **[Skills]** Deployment planning, RACI definition, readiness assessment, cost governance, acceptance design, escalation planning.
- **[Tools]** Readiness checklist, RACI, AWS budget dashboard, delivery plan, teardown contract.
- Review security, support, data, access, dependencies, and decision owners.
- Confirm the $20 API cap, $180 AWS cap, 14-day window, approved region, tags, and teardown deadline.
- Define milestones, responsibilities, escalation paths, acceptance criteria, and rollback/no-go threshold.
- Pass the local gate before provisioning cloud resources.

### Task 6.2 — Protected AWS deployment (18 hours)

- **[Summary]** Deploy the locally accepted stack through the supplied course-managed AWS path.
- **[Skills]** Local-to-cloud translation, protected deployment, secrets handling, least privilege, cost-aware operation, release verification.
- **[Tools]** Supplied CloudFormation or OpenTofu templates, AWS CLI, ECR, course-selected compute, S3, CloudWatch, Secrets Manager or SSM.
- Replace LocalStack endpoint URLs and sentinel credentials with supplied real-AWS bindings; do not rebuild application logic.
- Configure trusted TLS, reviewer authentication, rate and request limits, synthetic evidence data, and bounded retention.
- Enforce IMDSv2 where applicable, least privilege, controlled egress, approved tags, and secrets outside Git.
- Use GPU only during an approved scheduled session; never operate an always-on GPU endpoint.

### Task 6.3 — Acceptance, operations and cost evidence (12 hours)

- **[Summary]** Demonstrate that the deployed system meets technical and business acceptance conditions.
- **[Skills]** Acceptance testing, cloud observability, failure triage, cost analysis, remediation prioritization, stakeholder communication.
- **[Tools]** Course verifier, CloudWatch, AWS Cost Explorer or supplied budget report, held-out scenario pack.
- Run held-out functional, security, resilience, and teardown-readiness checks.
- Show quality, latency, failure, and cost evidence against agreed criteria.
- Triage one simulated acceptance failure and communicate its delivery impact.
- Keep remediation inside the endpoint, assessment window, and budget.

### Task 6.4 — Adoption and operational handback (8 hours)

- **[Summary]** Prepare the client organization to operate, govern, and appropriately use the system.
- **[Skills]** Adoption planning, enablement, runbook design, ownership transfer, limitation communication, success measurement.
- **[Tools]** Operator runbook, user guide, escalation map, limitations register, asynchronous enablement scenario.
- Identify user groups, workflow changes, adoption risks, and responsible owners.
- Produce operator guidance, user guidance, escalation paths, and known limitations.
- Respond to skeptical-user questions through a deterministic recorded simulation.
- Define post-launch measures for usage, value, quality, and safety.

### Task 6.5 — Technical and business defenses (8 hours)

- **[Summary]** Defend the completed engagement in two rooms using audience-appropriate evidence.
- **[Skills]** Technical defense, executive communication, evidence discipline, constraint response, acceptance negotiation.
- **[Tools]** Recorded defense, timed asynchronous scenario inject, architecture evidence, value brief, acceptance record.
- Record a technical defense covering architecture, controls, evaluations, operations, cost, and residual risks.
- Record an executive defense covering value, adoption status, limitations, and next investment.
- Respond via a recorded defense to a timed asynchronous scenario inject without inventing evidence or promising unapproved scope.
- Obtain a simulated accept, conditional-accept, or reject decision with rationale.

### Task 6.6 — Teardown and reusable field playbook (6 hours)

- **[Summary]** Close the engagement safely and turn customer-specific learning into reusable delivery knowledge.
- **[Skills]** Teardown verification, engagement closure, evidence retention, knowledge reuse, sensitive-data separation.
- **[Tools]** AWS CLI, supplied teardown script, cost report, resource inventory, field-playbook template.
- Remove and verify instances, volumes, public IPv4 addresses, tokens, parameters, traces, images, buckets, and endpoint records.
- Deliver final cost, teardown, acceptance, and unresolved-risk evidence.
- Separate reusable patterns from client-specific and sensitive information.
- Publish a concise discovery-to-handback playbook and product-feedback record.

## Workload verification

| Project | Calculation | Hours |
|---|---:|---:|
| Project 1 | 3 weeks × 20 | 60 |
| Project 2 | 4 weeks × 20 | 80 |
| Project 3 | 4 weeks × 20 | 80 |
| Project 4 | 4 weeks × 20 | 80 |
| Project 5 | 4 weeks × 20 | 80 |
| Project 6 | 3 weeks × 20 | 60 |
| **Program** | **22 weeks × 20** | **440** |

