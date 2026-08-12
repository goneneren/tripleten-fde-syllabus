# AI FDE Project Module Map (22 Week Program - LocalStack Edition)

This module map adapts the 5 shared enterprise projects specifically for the **AI Forward Deployed Engineer (AI FDE)** role, integrating a **licensed LocalStack tier** into the local Docker Compose runtime across Projects 1–4, and bridging to the Project 5 AWS Capstone.

> **Status: unadopted variant.** This is an alternative to the canonical `syllabus/` program, not a replacement for it. Three items must be resolved before it can be costed or launched: the [licensing question](#localstack-licensing-and-cost-unresolved), the [workload re-cost](#workload-impact-pending-re-cost), and the [P4 IAM tier check](#emulation-fidelity-boundaries). Tier naming throughout this edition is **Base** — the free tier is named **Hobby**, and "Community"/"Pro" are legacy names that should not appear in student-facing material.

**Core Concept: Same Repository, AWS SDK API Parity**
FDE students use containerized starter repositories running LocalStack (`localstack/localstack`) alongside PostgreSQL/pgvector, Redis, and AI serving engines. Students write production Python AWS SDK code (`boto3`) and CLI commands (`awslocal`) locally. Parity here is **API-level**: the same SDK calls, parameter shapes, and error types as production, with none of its performance or authorization characteristics. **Projects 1–4 operate strictly within `docker-compose` with $0 cloud spend, enforced by sentinel credentials and a mandatory client factory rather than by instruction; Project 5 deploys that locally accepted stack to a temporary protected AWS endpoint under the documented $180 infrastructure cap.**

### Program Comparison: AI FDE vs. System Engineering (LocalStack Edition)

| Project | Shared Starter Repo | SE Focus (Core) | AI FDE Focus (Core) |
| :--- | :--- | :--- | :--- |
| **P1: Diagnostics & Scaling** | Monolith, Prom/Grafana, Load Tester | Traces, DB Bottlenecks, Load Testing | API Diagnostics, LocalStack S3 telemetry tracing, LLM latency scenarios, Observability |
| **P2: Polyglot Data Tier** | Postgres, Redis, LocalStack, Auth | gRPC boundaries, Redis replication, Idempotency | LocalStack S3 Document Lake (`s3://enterprise-docs`), S3 event notifications, DynamoDB tracking, Pgvector Data Prep |
| **P3: Operations & Resilience** | K8s (`kind`), CI/CD, Event Bus, LocalStack | Terraform/OpenTofu, Kafka, Chaos Lab | Docker Compose, LocalStack SQS/SNS Queues, DLQs, local vLLM/Ollama serving, AWS SDK Retries/Circuit Breakers |
| **P4: Security & Compliance** | IAM, LocalStack Secrets, LLM Adapter | K8s Secrets, RBAC, CI Security Gates | OWASP LLM, LocalStack SSM Parameter Store & Secrets Manager, Guardrails AI, CloudWatch Logs audit, PII Redaction |
| **P5: Autonomous AI System** | RAG, LangGraph, Telemetry, LocalStack | Basic RAG, CI Smoke Evals, Telemetry | Advanced RAG, Multi-Agent LangGraph, LocalStack `awslocal` Pre-flight checks, LLM-as-a-Judge, Fine-Tuning, protected AWS deployment |

## LocalStack Licensing and Cost (Unresolved)

This edition requires a **licensed** LocalStack tier for Projects 1–4. It cannot be costed until the item below is settled with LocalStack, because the published rates do not support a per-student 5.5-month license at the rate previously assumed in this document.

Published rates: **Base** is $39/license/month on annual billing and **$45/license/month on monthly billing**; **Ultimate** is $89/license/month annual. The free **Hobby** tier is scoped to "hobbyists & other non-commercial usage."

| Billing scenario | Per student | + $180 AWS + $20 LLM | Viable? |
| :--- | ---: | ---: | :--- |
| Monthly billing, 6 cycles × $45 | $270.00 | **$470.00** | Yes — **use as the planning number** |
| Annual seat, 12 × $39, not reused | $468.00 | $668.00 | No — program pays for 6.5 idle months |
| Annual seat reused across 2 cohorts/yr | ~$234.00 | ~$434.00 | Only if LocalStack permits seat reassignment |
| Hobby (free) tier | $0.00 | $200.00 | Only if student use qualifies as non-commercial |

**Planning number for this edition: $470 per student** (monthly billing), a 135% increase over the canonical program's $200. Do not quote a lower figure until one of the reduction paths below is confirmed in writing.

### Required actions before this edition can be launched or priced

1. **Ask LocalStack whether licenses can be reassigned between students across cohorts.** This is the only path to the ~$234/student figure and it is the difference between a $434 and a $470 program.
2. **Ask LocalStack whether a student in a paid bootcamp qualifies for the non-commercial Hobby tier.** The individual learner is plausibly non-commercial while the program mandating it is not. This is genuinely ambiguous and must not be assumed either way. A "yes" removes the license cost entirely and makes this edition strictly cheaper than the canonical program on tooling.
3. **Apply to LocalStack's education / open-source program.** Qualifying OSI-licensed projects can receive free Ultimate licenses. A publicly published curriculum or starter-repo set may qualify.
4. **Resolve the CI licensing model.** Every project in this edition requires LocalStack integration tests in CI. Decide between a program-owned CI license and per-student keys in CI secrets. Per-student keys in `Actions secrets` are a credential-sprawl risk in a program that teaches Gitleaks in P4, and they are the less defensible option. Budget CI minutes for ~30–60s of additional container startup per job.
5. **Verify the P4 tier requirement** (see [Emulation Fidelity Boundaries](#emulation-fidelity-boundaries)). If P4 needs Ultimate, every figure in the table above rises.

If none of paths 1–3 land, compare $470/student against the canonical $200 program and decide whether AWS SDK muscle memory in P1–P4 is worth $270/student, given that P5 already exercises `boto3` against real AWS.

## Emulation Fidelity Boundaries

LocalStack provides **API and behavioral parity, not performance or authorization parity**. Two consequences bind this curriculum, and both must appear in student-facing material:

- **No performance conclusions may be drawn from emulated services.** LocalStack S3 is a local process backed by a Docker volume; its latency, throughput, and IOPS profile bears no relationship to real S3. Load tests, capacity math, and bottleneck analysis must treat emulated AWS calls as *instrumented boundaries to trace*, never as *performance characteristics to measure or extrapolate*. This constraint falls hardest on Project 1, whose entire subject is empirical performance diagnosis.
- **IAM policy evaluation is approximate.** LocalStack does not fully replicate the AWS policy engine across conditions, resource policies, permission boundaries, and SCPs. A least-privilege policy that passes locally can behave differently in AWS. Project 4 must state this and must not present a local pass as production-ready authorization.

**Open tier question for P4:** Base advertises *basic* IAM policy enforcement; *advanced* IAM policy testing is an Ultimate feature. Project 4 grades `AssumeRole`, S3 bucket policies, **and KMS key policies**, which is likely beyond "basic". Verify against the current feature matrix before pricing — Ultimate is $89/license/month on annual billing against Base's $39, so a mid-program upgrade more than doubles the $270 license line. LocalStack has not published an Ultimate monthly-billing rate here; obtain it before costing that scenario.

## Local Credential Safety (Required Scaffold Control)

Projects 1–4 claim $0 cloud spend, and students write `boto3` from Day 1. A student with real credentials in `~/.aws` and a single missing `endpoint_url` will silently call **real AWS** and bill their own account. The scaffold must make that failure impossible rather than relying on instructions:

- Compose sets sentinel credentials (`AWS_ACCESS_KEY_ID=test`, `AWS_SECRET_ACCESS_KEY=test`) and a fixed sentinel region for every service.
- A shared client factory is the only sanctioned way to construct a `boto3` client; it injects `endpoint_url` from configuration.
- A lint or test gate fails CI when a `boto3.client(...)` / `boto3.resource(...)` call is constructed outside that factory.
- Starter repos ship no AWS profile references and never mount the host `~/.aws` into a container.

## Workload Impact (Pending Re-Cost)

**The hour tables in Projects 1–5 are inherited unchanged from the canonical program and do not yet account for the LocalStack surface this edition adds.** Every project gained an AWS service surface and a second SDK; no project gained an hour. That must be resolved before launch.

Estimated additional student hours introduced by this edition:

| Project | Added surface | Est. added hours |
| :--- | :--- | ---: |
| P1 | `boto3` endpoint overrides, `awslocal`, AWS SDK spans (observation-only scope) | +2 |
| P2 | S3 document lake, S3 event notifications, DynamoDB job-state tracking | +8 |
| P3 | SQS/SNS topology, DLQ inspection, `boto3` retry/backoff configuration | +8 |
| P4 | SSM Parameter Store, Secrets Manager, IAM policy evaluation, CloudWatch Logs | +6 |
| P5 | `awslocal` pre-flight verification script | +3 |
| **Total** | | **+27** |

That takes the program from ~452 to ~479 hours, or ~21.8 h/week against a ~20 h/week target. Weekly load is already above target in P1 (22.3 h/wk) and P2 (21.6 h/wk), so the added hours cannot simply be absorbed. Choose one before launch:

- **Option A — extend the envelope.** Accept ~21.8 h/week, or add weeks. Changes the program's advertised commitment.
- **Option B — displace existing scope** (recommended). Cut ~27 hours of canonical content and document each trade explicitly per project. P1 is the priority: it is the most overloaded project, sits in weeks 1–3, and its LocalStack scope is already reduced to observation-only by the fidelity boundary above.

Do not publish per-project hour tables from this edition until Option A or B is chosen and the tables are updated to match.

## Labels

- `[CORE]` - Required FDE project work students build, operate, document, or defend using Docker Compose and LocalStack. P5 also includes its documented temporary protected AWS deployment after local acceptance.
- `[SUPPORTING]` - Just-in-time theory or practice that supports the core FDE work.
- `[OPTIONAL]` - Useful extension or deeper review.
- `[POSITIONING]` - Strategic knowledge (marketing-visible, architectural evaluation) without forcing implementation. Infrastructure like K8s or live Terraform modules falls here for FDEs until P5.
- `[AI]` - Modules specifically added or required for the AI FDE track (e.g., Fine-tuning, Guardrails, Evaluation). LocalStack and AWS SDK modules are `[CORE]`, not `[AI]`: they are general cloud-engineering skills, not AI-specific ones.

## 22-Week AI FDE Syllabus Structure (LocalStack Edition)

```text
Projects/
├── Project 1: System Diagnostics & API Scaling (Weeks 1-3)
│   ├── Chapter 1.1 How Systems Fit Together [CORE]
│   ├── Chapter 1.2 Monolith vs Microservices [CORE]
│   ├── Chapter 1.3 Meet the Reference Platform (Docker Compose & LocalStack S3) [CORE]
│   ├── Local credential safety: sentinel creds & the boto3 client factory [CORE]
│   ├── Chapter 2.1 Reasoning About Scale [CORE]
│   ├── Chapter 2.2 Finding API Bottlenecks [CORE]
│   ├── Chapter 14.1 LLM Fundamentals for Engineers [CORE]
│   ├── AWS SDK (boto3) request tracing & the emulation fidelity boundary [CORE]
│   ├── AI-generated capacity notebook audited for LLM latency & rate limits [AI]
│   ├── Deterministic provider latency scenario [CORE]
│   ├── Chapter 2.3 Observability First Principles [CORE]
│   ├── Chapter 9.1 Metrics & Dashboards (Prometheus/Grafana/Jaeger) [CORE]
│   └── Chapter 17.1 C4 Diagrams & ADRs [SUPPORTING]
├── Project 2: Data Layer, Vector Search & Hybrid RAG (Weeks 4-7)
│   ├── Chapter 3.1 REST Done Right (FastAPI) [CORE]
│   ├── Chapter 3.2 API Versioning & Evolution [SUPPORTING]
│   ├── Chapter 16.1 AI-Native Development & Data Prep [CORE]
│   ├── LocalStack S3 Document Lake (s3://enterprise-docs) & S3 Notifications [CORE]
│   ├── LocalStack DynamoDB Metadata & Job State Tracking [CORE]
│   ├── Chapter 5.1 Relational Data & pgvector at Production Level [CORE]
│   ├── Chapter 6.3 Caching with Redis [CORE]
│   ├── Unstructured Data Extraction & Document Chunking [AI]
│   ├── Local Embedding Generation (FastEmbed) [AI]
│   ├── Hybrid Retrieval Systems (pgvector + BM25) [AI]
│   ├── Enterprise-data scenario pack and held-out retrieval case [CORE]
│   └── Chapter 18.1 Use Case & Architecture [SUPPORTING]
├── Project 3: Resilience, Microservices & Local LLM Serving (Weeks 8-12)
│   ├── Chapter 7.1 Docker Deeply & Docker Compose Orchestration [CORE]
│   ├── LocalStack SQS & SNS Event Queues & Dead Letter Queues (DLQs) [CORE]
│   ├── AWS SDK Retries, Exponential Backoff, and Circuit Breakers [CORE]
│   ├── Chapter 8.2 CI/CD Pipelines [CORE]
│   ├── Chapter 9.3 Alerting SLOs & the Failure Lab [CORE]
│   ├── Chapter 10.2 Partial-Failure Patterns & LLM API Retries [CORE]
│   ├── Local LLM Model Serving: vLLM via Docker (Ollama fallback) [AI]
│   ├── LLM Provider Adapters, Rate Limits, and Circuit Breakers [AI]
│   ├── Deterministic LocalStack SQS & Provider-emulator failure lab [CORE]
│   └── Chapter 19.1 Deploy & Observe (Local LLM API Endpoint) [CORE]
├── Project 4: Zero-Trust Security, Guardrails & Governance (Weeks 13-16)
│   ├── Chapter 12.1 Threat Modeling & Zero-Trust (STRIDE for AI) [CORE]
│   ├── Chapter 12.2 Identity, Access & RBAC [CORE]
│   ├── LocalStack SSM Parameter Store & Secrets Manager [CORE]
│   ├── Local IAM Policy Evaluation & its divergence from the AWS policy engine [CORE]
│   ├── LocalStack CloudWatch Logs for Guardrail Audit Events [CORE]
│   ├── Chapter 13.1 Securing the Pipeline [CORE]
│   ├── Chapter 13.2 Compliance by Design (EU AI Act & HIPAA) [CORE]
│   ├── Chapter 16.3 AI Governance [CORE]
│   ├── OWASP LLM Top 10: Prompt Injection Mitigation & Red-Teaming [AI]
│   ├── Output Guardrails (Guardrails AI), Hallucination Checks & PII Redaction [AI]
│   └── Provider-emulator prompt-injection and PII scenarios [CORE]
└── Project 5: Autonomous Multi-Agent Platform & Defense (Weeks 17-22)
    ├── Chapter 18.2 Production Definition of Done [CORE]
    ├── Chapter 14.3 RAG as Production Architecture [CORE]
    ├── Cross-Encoder Reranking [CORE]
    ├── Chapter 15.1 Agentic Frameworks (LangGraph / CrewAI) [CORE]
    ├── Autonomous Agent State Graphs & Tool Execution Sandboxing [CORE]
    ├── Human-in-the-Loop Oversight & State Management [AI]
    ├── LocalStack awslocal Pre-Flight Verification Script [CORE]
    ├── Chapter 15.2 Evaluation Pipelines [CORE]
    ├── CI Smoke Evaluation Gates (Cached Fixtures) [CORE]
    ├── LLM-as-Judge Calibration & Ragas Metrics [AI]
    ├── PEFT Fine-Tuning (LoRA) for Specialized Tasks [AI]
    ├── Chapter 15.3 AI Observability (Arize Phoenix / Tracing) [CORE]
    ├── Bounded AWS Deployment, Cost Controls, and Teardown Evidence [CORE]
    └── Chapter 20.2 Final Architecture Review [CORE]
```
