# AI FDE Project Module Map (22 Week Program)

This module map adapts the 5 shared enterprise projects (used across both SE and FDE tracks) specifically for the **AI Forward Deployed Engineer (AI FDE)** role. 

**Core Concept: Same Repository, Different Focus**
FDE students use the exact same starter repositories and environments as SE students. However, the grading scope is shifted: heavy backend infrastructure (Kubernetes, Kafka, Terraform) is relegated to `[POSITIONING]` (decision-level knowledge), while applied AI, containerization, and evaluation are elevated to `[CORE]` required implementations. **Projects 1-4 operate strictly within `docker-compose` instead of local Kubernetes (`kind`); Project 5 deploys that locally accepted stack to a temporary protected AWS endpoint under the documented $180 infrastructure cap.**

### Program Comparison: AI FDE vs. System Engineering

| Project | Shared Starter Repo | SE Focus (Core) | AI FDE Focus (Core) |
| :--- | :--- | :--- | :--- |
| **P1: Diagnostics & Scaling** | Monolith, Prom/Grafana, Load Tester | Traces, DB Bottlenecks, Load Testing | API Diagnostics, deterministic latency scenarios, Observability |
| **P2: Polyglot Data Tier** | Postgres, Redis, gRPC, Auth | gRPC boundaries, Redis replication, Idempotency | Unstructured ETL, enterprise-data scenarios, Pgvector Data Prep |
| **P3: Operations & Resilience** | K8s (`kind`), CI/CD, Event Bus | Terraform/OpenTofu, Kafka, Chaos Lab | Docker Compose, local serving, provider-emulator resilience (Retries) |
| **P4: Security & Compliance** | IAM, Secrets, LLM Adapter | K8s Secrets, RBAC, CI Security Gates | OWASP LLM, provider-emulator guardrails, PII Redaction |
| **P5: Autonomous AI System** | RAG, LangGraph, Telemetry | Basic RAG, CI Smoke Evals, Telemetry | Advanced RAG, Multi-Agent LangGraph, LLM-as-a-Judge, Fine-Tuning, protected AWS deployment |

## Labels

- `[CORE]` - Required FDE project work students build, operate, document, or defend using Docker Compose. P5 also includes its documented temporary protected AWS deployment after local acceptance.
- `[SUPPORTING]` - Just-in-time theory or practice that supports the core FDE work.
- `[OPTIONAL]` - Useful extension or deeper review.
- `[POSITIONING]` - Strategic knowledge (marketing-visible, architectural evaluation) without forcing implementation. Infrastructure like K8s or Terraform falls here for FDEs.
- `[AI]` - Modules specifically added or required for the AI FDE track (e.g., Fine-tuning, Guardrails, Evaluation).

## 22-Week AI FDE Syllabus Structure

```text
Projects/
├── Project 1: System Diagnostics & API Scaling (Weeks 1-3)
│   ├── Chapter 1.1 How Systems Fit Together [CORE]
│   ├── Chapter 1.2 Monolith vs Microservices [CORE]
│   ├── Chapter 1.3 Meet the Reference Platform (Docker Compose) [CORE]
│   ├── Chapter 2.1 Reasoning About Scale [CORE]
│   ├── Chapter 2.2 Finding API Bottlenecks [CORE]
│   ├── Chapter 14.1 LLM Fundamentals for Engineers [CORE]
│   ├── AI-generated capacity notebook audited for LLM latency & rate limits [AI]
│   ├── Deterministic provider latency scenario [CORE]
│   ├── Chapter 2.3 Observability First Principles [CORE]
│   ├── Chapter 9.1 Metrics & Dashboards (Prometheus/Grafana) [CORE]
│   └── Chapter 17.1 C4 Diagrams & ADRs [SUPPORTING]
├── Project 2: Data Layer, Vector Search & Hybrid RAG (Weeks 4-7)
│   ├── Chapter 3.1 REST Done Right (FastAPI) [CORE]
│   ├── Chapter 3.2 API Versioning & Evolution [SUPPORTING]
│   ├── Chapter 4.1 gRPC & Protobufs [POSITIONING]
│   ├── Chapter 4.2 Service Boundaries & DDD [SUPPORTING]
│   ├── Chapter 16.1 AI-Native Development & Data Prep [CORE]
│   ├── Chapter 5.1 Relational Data & pgvector at Production Level [CORE]
│   ├── Chapter 6.1 Replication & Read Replicas [POSITIONING]
│   ├── Chapter 6.3 Caching with Redis [CORE]
│   ├── Unstructured Data Extraction & Document Chunking [AI]
│   ├── Local Embedding Generation (FastEmbed) [AI]
│   ├── Hybrid Retrieval Systems (pgvector + BM25) [AI]
│   ├── Enterprise-data scenario pack and held-out retrieval case [CORE]
│   └── Chapter 18.1 Use Case & Architecture [SUPPORTING]
├── Project 3: Resilience, Microservices & Local LLM Serving (Weeks 8-12)
│   ├── Chapter 7.1 Docker Deeply & Docker Compose Orchestration [CORE]
│   ├── Chapter 7.2 Kubernetes Core [POSITIONING]
│   ├── Chapter 8.1 Terraform Fundamentals [POSITIONING]
│   ├── Chapter 8.2 CI/CD Pipelines [CORE]
│   ├── Chapter 9.3 Alerting SLOs & the Failure Lab [CORE]
│   ├── Chapter 10.2 Partial-Failure Patterns & LLM API Retries [CORE]
│   ├── Chapter 11.2 Kafka at Working Level [POSITIONING]
│   ├── Local LLM Model Serving: vLLM via Docker [AI]
│   ├── LLM Provider Adapters, Rate Limits, and Circuit Breakers [AI]
│   ├── Deterministic provider-emulator failure lab [CORE]
│   └── Chapter 19.1 Deploy & Observe (Local LLM API Endpoint) [CORE]
├── Project 4: Zero-Trust Security, Guardrails & Governance (Weeks 13-16)
│   ├── Chapter 12.1 Threat Modeling & Zero-Trust (STRIDE for AI) [CORE]
│   ├── Chapter 12.2 Identity, Access & RBAC [CORE]
│   ├── Chapter 12.3 Secrets Management (API Keys) [CORE]
│   ├── Chapter 13.1 Securing the Pipeline [CORE]
│   ├── Chapter 13.2 Compliance by Design (EU AI Act & HIPAA) [CORE]
│   ├── Chapter 16.3 AI Governance [CORE]
│   ├── OWASP LLM Top 10: Prompt Injection Mitigation & Red-Teaming [AI]
│   ├── Output Guardrails, Hallucination Checks & PII Redaction [AI]
│   ├── Provider-emulator prompt-injection and PII scenarios [CORE]
│   └── Chapter 17.3 Technical Communication [SUPPORTING]
└── Project 5: Autonomous Multi-Agent Platform & Defense (Weeks 17-22)
    ├── Chapter 18.2 Production Definition of Done [CORE]
    ├── Chapter 14.3 RAG as Production Architecture [CORE]
    ├── Cross-Encoder Reranking [CORE]
    ├── Chapter 15.1 Agentic Frameworks (LangGraph / CrewAI) [CORE]
    ├── Autonomous Agent State Graphs & Tool Execution Sandboxing [CORE]
    ├── Human-in-the-Loop Oversight & State Management [AI]
    ├── Chapter 15.2 Evaluation Pipelines [CORE]
    ├── CI Smoke Evaluation Gates (Cached Fixtures) [CORE]
    ├── Held-out enterprise and provider scenario evaluation [CORE]
    ├── LLM-as-Judge Calibration & Ragas Metrics [AI]
    ├── PEFT Fine-Tuning (LoRA) for Specialized Tasks [AI]
    ├── Chapter 15.3 AI Observability (Arize Phoenix / Tracing) [CORE]
    ├── Bounded AWS Deployment, Cost Controls, and Teardown Evidence [CORE]
    ├── Chapter 20.2 Final Architecture Review [CORE]
    └── Chapter 20.3 Portfolio & Employment Readiness [OPTIONAL]
```
