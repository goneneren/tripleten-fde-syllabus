# AI Forward Deployed Engineer (AI FDE) Syllabus: 5-Project Program (LocalStack Edition)

## 22-Week Bootcamp Program | ~20 Hours / Week Commitment (~452 Hours Total)

---

## 🚀 Program Manifesto & Local-First Philosophy

The **AI Forward Deployed Engineer (AI FDE)** program is designed to build production-ready engineers who can architect, deploy, and evaluate enterprise AI solutions. 

> **Status: unadopted variant.** This LocalStack edition is an alternative to the canonical `syllabus/` program, not a replacement. It carries a materially higher per-student cost and an un-reconciled workload increase. See [Program Cost](#-program-cost-planning-470student) and the [workload re-cost](overview-and-module-map.md#workload-impact-pending-re-cost) before quoting either figure.

### Key Program Principles:
1. **Local-First Development with LocalStack AWS Emulation & Bounded AWS Capstone**: Projects 1–4 run and are graded locally on the student's machine via **Docker Compose** using open-source containers and **LocalStack AWS Emulation** (S3, SQS, SNS, SSM Parameter Store, Secrets Manager, DynamoDB, and CloudWatch Logs). They do not expose public endpoints; Project 1 explicitly forbids one. Project 5 first passes local acceptance (validated against LocalStack), then deploys a temporary protected endpoint in one dedicated course-managed AWS sandbox per student.
2. **Enterprise AWS SDK Mastery (`boto3`)**: From Day 1, students write standard Python AWS SDK code (`boto3`) and CLI scripts (`awslocal`) targeting local emulated AWS services, establishing **API-level** code parity between local development and cloud production. Emulation gives API and behavioral parity only — never performance or authorization parity. See [Emulation Fidelity Boundaries](overview-and-module-map.md#emulation-fidelity-boundaries).
3. **Project-First Pedagogy**: Theory is delivered "Just-In-Time". Students learn by inheriting realistic, messy enterprise codebases with seeded defects and architectural gaps that they must diagnose and fix.
4. **Containerized Engineering**: Every project must run locally via `docker compose up` before review. P5 adds a separately assessed AWS deployment after local acceptance; it does not replace the local path.
5. **High-Touch Support**: Students are supported by rigorous line-by-line code reviews on GitHub Pull Requests and mandatory Loom video client defenses.

---

## 💵 Program Cost (Planning: $470/student)

| Allocation Component | Planning amount | Use |
| :--- | ---: | :--- |
| LocalStack Base license | $270.00 | $45/license/month monthly billing × 6 billing cycles across 22 weeks. |
| Approved LLM API calls | $20.00 | Bounded P5 provider-adapter usage, manual evaluation, and defense traffic. |
| AWS infrastructure cap | $180.00 | Short CPU endpoint, storage, public IPv4, scheduled GPU sessions, variance. ($80 normal target.) |
| **Total per student** | **$470.00** | vs. **$200.00** for the canonical program — a **135% increase**. |

$45/month is LocalStack's **monthly-billing** rate. The widely quoted $39/month requires an annual commitment, which a 5.5-month per-student license cannot use without paying for 6.5 idle months. **Do not quote a figure below $470 until a reduction path is confirmed in writing** — the paths (seat reassignment across cohorts, Hobby-tier eligibility, and the education/OSS program) and the required decisions are enumerated in [LocalStack Licensing and Cost](overview-and-module-map.md#localstack-licensing-and-cost-unresolved). If Project 4's IAM grading requires the Ultimate tier, the license line roughly doubles.

Dropping the live AWS capstone entirely would put this edition at **$290/student** ($270 license + $20 LLM) and forfeit the P5 cloud deployment that graduation criterion 5 requires.

---

## 🛠️ Required Local Environment and Recommended Hardware

The required local environment and recommended hardware support containerized vector databases, LocalStack AWS emulation, and local open-weight LLMs:

* **CPU**: 8-core Modern Processor (Intel i7/i9, AMD Ryzen 7/9, Apple Silicon M1/M2/M3/M4).
* **RAM**: **24 GB minimum, 32 GB strongly recommended.** This edition raises the floor above the canonical program's 16 GB: Project 3 concurrently runs LocalStack (~1–2 GB), vLLM or Ollama, Postgres/pgvector, Redis, Prometheus, Grafana, and Jaeger. 16 GB will thrash during the P3 failure lab.
* **GPU/VRAM**: 8 GB VRAM strongly recommended for local inference. Projects 1–4 provide mock, small-model, or approved local fallback paths rather than a paid-cloud dependency. The $20 API allowance and scheduled AWS GPU access are reserved for P5.
* **OS**: macOS (M-series preferred), Linux, or Windows (WSL2 required).

### Prerequisites Software Stack:
* Docker Desktop or Rancher Desktop (with Docker Compose enabled)
* Python 3.12+
* AWS CLI (`aws`) & `awslocal` wrapper (`pip install localstack awscli-local`)
* A program-issued LocalStack account and license key (students never purchase their own; see [licensing](overview-and-module-map.md#localstack-licensing-and-cost-unresolved))
* Git & GitHub CLI (`gh`)
* VS Code or Cursor IDE

Starter repos set sentinel AWS credentials and route every `boto3` client through a shared factory that injects `endpoint_url`, so a student's real AWS credentials can never be used by accident. See [Local Credential Safety](overview-and-module-map.md#local-credential-safety-required-scaffold-control).

---

## 📅 22-Week Curriculum Roadmap Overview

The 22 weeks are distributed across 5 major enterprise build phases. Each project uses containerized enterprise services and LocalStack AWS emulation with a unique AI FDE grading focus.

| Project | Weeks | Module Topic | Core Focus for FDEs | Workload |
| :--- | :--- | :--- | :--- | :--- |
| **Project 1** | W01–W03 | System Diagnostics & API Scaling | API Diagnostics, LocalStack S3 Telemetry Tracing, LLM Mock Latency | ~67 Hours (22h/wk) |
| **Project 2** | W04–W07 | Data Layer, Vector Search & Hybrid RAG | LocalStack S3 Document Lake (`s3://enterprise-docs`), S3 Event Triggers, Pgvector Data Prep | ~86 Hours (21h/wk) |
| **Project 3** | W08–W12 | Resilience, Microservices & Local LLMs | Docker Compose, Local LLM Serving (vLLM), LocalStack SQS/SNS Queues & Failure Lab | ~96 Hours (19h/wk) |
| **Project 4** | W13–W16 | Zero-Trust Security, Guardrails & Governance | OWASP LLM, LocalStack Secrets Manager/SSM, Guardrails AI, Local IAM Policies, PII Redaction | ~83 Hours (20h/wk) |
| **Project 5** | W17–W22 | Autonomous Multi-Agent Platform & Defense | Advanced RAG, Multi-Agent LangGraph, LocalStack Pre-flight, Ragas Evals, LoRA, protected AWS deployment | ~120 Hours (20h/wk) |

⚠️ **These hours are inherited unchanged from the canonical program and do not account for the LocalStack surface this edition adds** (estimated **+27 hours**, taking the program to ~479 hours / ~21.8 h/wk). Either extend the envelope or displace ~27 hours of existing scope before publishing this table. See [Workload Impact](overview-and-module-map.md#workload-impact-pending-re-cost).

---

## 📖 Project Summaries

### [Project 1: System Diagnostics & API Scaling](project-1.md)
Students diagnose a provided monolith-based reference platform running with LocalStack S3. They trace request paths and AWS SDK (`boto3`) calls across OpenTelemetry/Jaeger, repair observability defects (Prometheus/Grafana), run reproducible load tests, and evaluate the latency impacts of mocked LLM API calls on traditional backend systems. LocalStack appears here as a **traced boundary only** — all capacity and latency conclusions come from the deterministic provider scenario pack and the real Postgres/Redis tier, never from emulated AWS timings.

### [Project 2: Data Layer, Vector Search & Hybrid RAG](project-2.md)
Students build the foundational data layer for AI integration using a LocalStack S3 document lake (`s3://enterprise-docs`). S3 upload events trigger text and table extraction using `Unstructured`, generating local embeddings with `FastEmbed`, tracking job metadata in LocalStack DynamoDB, and indexing hybrid semantic retrieval in `pgvector` and BM25.

### [Project 3: Resilience, Microservices & Local LLM Serving](project-3.md)
Students run local LLM serving with `vLLM` where supported and Ollama as the grading-equivalent local fallback. LocalStack SQS and SNS emulate asynchronous task queues and Dead Letter Queues (DLQs). A deterministic provider emulator and SQS failure script drive circuit breakers, retries, and failure labs without paid cloud traffic.

### [Project 4: Zero-Trust Security, Guardrails & Governance](project-4.md)
Students secure the AI system against the OWASP LLM Top 10 using LocalStack SSM Parameter Store and Secrets Manager for API keys and guardrail configs. They build a STRIDE threat model, evaluate local IAM policies, implement output guardrails (`Guardrails AI`), log CloudWatch audit events, and map educational compliance controls (EU AI Act & HIPAA).

### [Project 5: Autonomous Multi-Agent Platform & Defense](project-5.md)
The capstone. Students build a multi-agent tool flow using `LangGraph` with human-in-the-loop sandboxing. They use `awslocal` to run local AWS pre-flight verification on LocalStack before deploying the accepted stack to a temporary protected AWS endpoint within a $180 infrastructure allocation. They run CI evaluations, calibrate LLM-as-a-judge metrics with `Ragas`, fine-tune a specialized model via LoRA, and present a live cloud defense. The deployment workflow and estimate are defined in [Project 5 AWS Deployment](project-5-aws-deployment.md).

---

## 🛠️ Student Assessment & Code Review Workflow

To mirror real-world engineering standards, pass/fail assessment is highly rigorous and manual:

1. **Continuous Integration (CI) Gates**: Every PR must pass automated CI checks (linting, test coverage, LocalStack integration tests, dependency scanning, and LLM smoke evals) before a human reviews it.
2. **Code Reviews**: Dedicated engineering reviewers conduct line-by-line code reviews on GitHub Pull Requests. Students must address all requested changes to merge their work.
3. **Client Defenses (Loom Videos)**: Projects 1–4 use 5-minute local Loom defenses demonstrating containerized LocalStack integration. Project 5 uses a 15-minute defense of the protected AWS endpoint, local evidence, cost telemetry, and teardown plan.

---

## 🏆 Graduation Criteria

To graduate from the TripleTen AI FDE program, a student must:
1. Successfully complete and merge GitHub Pull Requests for all 5 Projects.
2. Pass all automated CI/CD evaluation pipelines (including LocalStack integration tests).
3. Pass the manual Code Review rubrics (achieving 100% of Must-Have criteria).
4. Deliver passing Client Defense Loom videos for all 5 projects.
5. Successfully deploy the Project 5 Capstone architecture to a temporary protected AWS endpoint, demonstrate the LLM telemetry metrics, and complete the teardown evidence.
