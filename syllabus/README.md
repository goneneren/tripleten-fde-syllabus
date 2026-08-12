# AI Forward Deployed Engineer (AI FDE) Syllabus: 5-Project Program

## 22-Week Bootcamp Program | ~20 Hours / Week Commitment (~452 Hours Total)

---

## 🚀 Program Manifesto & Local-First Philosophy

The **AI Forward Deployed Engineer (AI FDE)** program is designed to build production-ready engineers who can architect, deploy, and evaluate enterprise AI solutions. 

### Key Program Principles:
1. **Local-First Development, Bounded AWS Capstone**: Projects 1-4 run and are graded locally on the student's machine via **Docker Compose** using open-source tools and deterministic enterprise/provider scenarios. They do not deploy to cloud services or expose public endpoints; Project 1 explicitly forbids one. Project 5 first passes local acceptance, then deploys a temporary protected endpoint in one dedicated course-managed AWS sandbox per student. The total allocation is capped at $200 per student: $20 for approved LLM API calls and $180 for AWS infrastructure.
2. **Project-First Pedagogy**: Theory is delivered "Just-In-Time". Students learn by inheriting realistic, messy enterprise codebases with seeded defects and architectural gaps that they must diagnose and fix.
3. **Containerized Engineering**: Every project must run locally via `docker compose up` before review. P5 adds a separately assessed AWS deployment after local acceptance; it does not replace the local path.
4. **High-Touch Support**: Students are supported by rigorous line-by-line code reviews on GitHub Pull Requests and mandatory Loom video client defenses.

---

## 🛠️ Required Local Environment and Recommended Hardware

The required local environment and recommended hardware support containerized vector databases and, where hardware allows, local open-weight LLMs:

* **CPU**: 8-core Modern Processor (Intel i7/i9, AMD Ryzen 7/9, Apple Silicon M1/M2/M3/M4).
* **RAM**: 16 GB minimum (32 GB strongly recommended for smooth multi-container orchestration).
* **GPU/VRAM**: 8 GB VRAM strongly recommended for local inference. Projects 1-4 provide mock, small-model, or approved local fallback paths rather than a paid-cloud dependency. The $20 API allowance and scheduled AWS GPU access are reserved for P5.
* **OS**: macOS (M-series preferred), Linux, or Windows (WSL2 required).

### Prerequisites Software Stack:
* Docker Desktop or Rancher Desktop (with Docker Compose enabled)
* Python 3.12+
* Git & GitHub CLI (`gh`)
* VS Code or Cursor IDE

---

## 📅 22-Week Curriculum Roadmap Overview

The 22 weeks are distributed across 5 major enterprise build phases. Each project uses the exact same starter repositories as the System Engineering track, but with a unique AI grading focus.

| Project | Weeks | Module Topic | Core Focus for FDEs | Workload |
| :--- | :--- | :--- | :--- | :--- |
| **Project 1** | W01–W03 | System Diagnostics & API Scaling | API Diagnostics, LLM Mock Latency, Observability | ~67 Hours (22h/wk) |
| **Project 2** | W04–W07 | Data Layer, Vector Search & Hybrid RAG | Unstructured ETL, Chunking, Pgvector Data Prep | ~86 Hours (21h/wk) |
| **Project 3** | W08–W12 | Resilience, Microservices & Local LLMs | Docker Compose, Local LLM Serving (vLLM), API Resiliency | ~96 Hours (19h/wk) |
| **Project 4** | W13–W16 | Zero-Trust Security, Guardrails & Governance | OWASP LLM, Guardrails, PII Redaction, Prompt Injection Defense | ~83 Hours (20h/wk) |
| **Project 5** | W17–W22 | Autonomous Multi-Agent Platform & Defense | Advanced RAG, Multi-Agent LangGraph, Ragas Evals, LoRA, protected AWS deployment | ~120 Hours (20h/wk) |

---

## 📖 Project Summaries

### [Project 1: System Diagnostics & API Scaling](project-1.md)
Students diagnose a provided monolith-based reference platform. They trace request paths, repair observability defects (Prometheus/Grafana), run reproducible load tests, and evaluate the latency impacts of mocked LLM API calls on traditional backend systems.

### [Project 2: Data Layer, Vector Search & Hybrid RAG](project-2.md)
Students build the foundational data layer for AI integration. They extract text and tables from enterprise documents using `Unstructured`, generate local embeddings with `FastEmbed`, and implement hybrid semantic retrieval using `pgvector` and BM25.

### [Project 3: Resilience, Microservices & Local LLM Serving](project-3.md)
Students run local LLM serving with `vLLM` where supported and Ollama as the grading-equivalent local fallback. A deterministic provider emulator drives circuit breakers, retries, and the simulated failure lab without paid API traffic.

### [Project 4: Zero-Trust Security, Guardrails & Governance](project-4.md)
Students secure the AI system against the OWASP LLM Top 10. They build a STRIDE threat model, implement output guardrails (`Guardrails AI`), configure PII redaction, and map educational compliance controls (EU AI Act & HIPAA).

### [Project 5: Autonomous Multi-Agent Platform & Defense](project-5.md)
The capstone. Students build a multi-agent tool flow using `LangGraph` with human-in-the-loop sandboxing. They run CI evaluations, calibrate LLM-as-a-judge metrics with `Ragas`, fine-tune a specialized model via LoRA, and deploy the locally accepted stack to a temporary protected AWS endpoint within a $180 infrastructure allocation. The deployment workflow and estimate are defined in [Project 5 AWS Deployment](project-5-aws-deployment.md).
