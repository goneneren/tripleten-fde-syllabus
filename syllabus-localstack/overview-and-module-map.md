# AI FDE Project Module Map (22 Week Program - LocalStack Edition)

This module map adapts the 5 shared enterprise projects specifically for the **AI Forward Deployed Engineer (AI FDE)** role, integrating **LocalStack Base** ($39/month subscription) into the local Docker Compose runtime across Projects 1–4, and bridging to the Project 5 AWS Capstone.

**Core Concept: Same Repository, AWS SDK Local Parity**
FDE students use containerized starter repositories running LocalStack (`localstack/localstack`) alongside PostgreSQL/pgvector, Redis, and AI serving engines. Students write production Python AWS SDK code (`boto3`) and CLI commands (`awslocal`) locally. **Projects 1–4 operate strictly within `docker-compose` with $0 cloud spend; Project 5 deploys that locally accepted stack to a temporary protected AWS endpoint under the documented $180 infrastructure cap.**

### Program Comparison: AI FDE vs. System Engineering (LocalStack Edition)

| Project | Shared Starter Repo | SE Focus (Core) | AI FDE Focus (Core) |
| :--- | :--- | :--- | :--- |
| **P1: Diagnostics & Scaling** | Monolith, Prom/Grafana, Load Tester | Traces, DB Bottlenecks, Load Testing | API Diagnostics, LocalStack S3 telemetry tracing, LLM latency scenarios, Observability |
| **P2: Polyglot Data Tier** | Postgres, Redis, LocalStack, Auth | gRPC boundaries, Redis replication, Idempotency | LocalStack S3 Document Lake (`s3://enterprise-docs`), S3 event notifications, DynamoDB tracking, Pgvector Data Prep |
| **P3: Operations & Resilience** | K8s (`kind`), CI/CD, Event Bus, LocalStack | Terraform/OpenTofu, Kafka, Chaos Lab | Docker Compose, LocalStack SQS/SNS Queues, DLQs, local vLLM/Ollama serving, AWS SDK Retries/Circuit Breakers |
| **P4: Security & Compliance** | IAM, LocalStack Secrets, LLM Adapter | K8s Secrets, RBAC, CI Security Gates | OWASP LLM, LocalStack SSM Parameter Store & Secrets Manager, Guardrails AI, CloudWatch Logs audit, PII Redaction |
| **P5: Autonomous AI System** | RAG, LangGraph, Telemetry, LocalStack | Basic RAG, CI Smoke Evals, Telemetry | Advanced RAG, Multi-Agent LangGraph, LocalStack `awslocal` Pre-flight checks, LLM-as-a-Judge, Fine-Tuning, protected AWS deployment |

## Labels

- `[CORE]` - Required FDE project work students build, operate, document, or defend using Docker Compose and LocalStack. P5 also includes its documented temporary protected AWS deployment after local acceptance.
- `[SUPPORTING]` - Just-in-time theory or practice that supports the core FDE work.
- `[OPTIONAL]` - Useful extension or deeper review.
- `[POSITIONING]` - Strategic knowledge (marketing-visible, architectural evaluation) without forcing implementation. Infrastructure like K8s or live Terraform modules falls here for FDEs until P5.
- `[AI]` - Modules specifically added or required for the AI FDE track (e.g., Fine-tuning, Guardrails, Evaluation, LocalStack AWS SDK adapters).

## 22-Week AI FDE Syllabus Structure (LocalStack Edition)

```text
Projects/
├── Project 1: System Diagnostics & API Scaling (Weeks 1-3)
│   ├── Chapter 1.1 How Systems Fit Together [CORE]
│   ├── Chapter 1.2 Monolith vs Microservices [CORE]
│   ├── Chapter 1.3 Meet the Reference Platform (Docker Compose & LocalStack S3) [CORE]
│   ├── Chapter 2.1 Reasoning About Scale [CORE]
│   ├── Chapter 2.2 Finding API Bottlenecks [CORE]
│   ├── Chapter 14.1 LLM Fundamentals for Engineers [CORE]
│   ├── AWS SDK (boto3) connection pooling & local request tracing [CORE]
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
│   ├── Local IAM Policy Evaluation (boto3 AssumeRole, S3 Bucket Policies) [CORE]
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
