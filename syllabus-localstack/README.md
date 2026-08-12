# AI Forward Deployed Engineer (AI FDE) Syllabus: 5-Project Program (LocalStack Edition)

## 22-Week Bootcamp Program | ~20 Hours / Week Commitment (~452 Hours Total)

---

## 🚀 Program Manifesto & Local-First Philosophy

The **AI Forward Deployed Engineer (AI FDE)** program is designed to build production-ready engineers who can architect, deploy, and evaluate enterprise AI solutions. 

### Key Program Principles:
1. **Local-First Development with LocalStack AWS Emulation & Bounded AWS Capstone**: Projects 1–4 run and are graded locally on the student's machine via **Docker Compose** using open-source containers and **LocalStack AWS Emulation** (S3, SQS, SNS, SSM Parameter Store, Secrets Manager, DynamoDB, and CloudWatch Logs). They do not expose public endpoints; Project 1 explicitly forbids one. Project 5 first passes local acceptance (validated against LocalStack), then deploys a temporary protected endpoint in one dedicated course-managed AWS sandbox per student. For paid LocalStack Pro/Base licensing ($39/month over the 22-week program $\approx$ $214.50 per student), the total per-student program allocation is re-estimated at **$414.50** ($214.50 LocalStack + $180 AWS infrastructure cap + $20 LLM API allowance). If using 100% LocalStack without live AWS deployment, the total per-student budget is **$234.50**.
2. **Enterprise AWS SDK Mastery (`boto3`)**: From Day 1, students write standard Python AWS SDK code (`boto3`) and CLI scripts (`awslocal`) targeting local emulated AWS services, establishing 1:1 code parity between local development and cloud production.
3. **Project-First Pedagogy**: Theory is delivered "Just-In-Time". Students learn by inheriting realistic, messy enterprise codebases with seeded defects and architectural gaps that they must diagnose and fix.
4. **Containerized Engineering**: Every project must run locally via `docker compose up` before review. P5 adds a separately assessed AWS deployment after local acceptance; it does not replace the local path.
5. **High-Touch Support**: Students are supported by rigorous line-by-line code reviews on GitHub Pull Requests and mandatory Loom video client defenses.

---

## 🛠️ Required Local Environment and Recommended Hardware

The required local environment and recommended hardware support containerized vector databases, LocalStack AWS emulation, and local open-weight LLMs:

* **CPU**: 8-core Modern Processor (Intel i7/i9, AMD Ryzen 7/9, Apple Silicon M1/M2/M3/M4).
* **RAM**: 16 GB minimum (32 GB strongly recommended for smooth multi-container orchestration including LocalStack, Postgres/pgvector, Redis, and vLLM/Ollama).
* **GPU/VRAM**: 8 GB VRAM strongly recommended for local inference. Projects 1–4 provide mock, small-model, or approved local fallback paths rather than a paid-cloud dependency. The $20 API allowance and scheduled AWS GPU access are reserved for P5.
* **OS**: macOS (M-series preferred), Linux, or Windows (WSL2 required).

### Prerequisites Software Stack:
* Docker Desktop or Rancher Desktop (with Docker Compose enabled)
* Python 3.12+
* AWS CLI (`aws`) & `awslocal` wrapper (`pip install localstack awscli-local`)
* Git & GitHub CLI (`gh`)
* VS Code or Cursor IDE

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

---

## 📖 Project Summaries

### [Project 1: System Diagnostics & API Scaling](project-1.md)
Students diagnose a provided monolith-based reference platform running with LocalStack S3. They trace request paths and AWS SDK (`boto3`) calls across OpenTelemetry/Jaeger, repair observability defects (Prometheus/Grafana), run reproducible load tests, and evaluate the latency impacts of mocked LLM API calls on traditional backend systems.

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
