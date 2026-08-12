# AI Forward Deployed Engineer (AI FDE) Syllabus: 5-Project Program

## 22-Week Bootcamp Program | ~20 Hours / Week Commitment (~452 Hours Total)

---

## 🚀 Program Manifesto & Local-First Philosophy

The **AI Forward Deployed Engineer (AI FDE)** program is designed to build production-ready engineers who can architect, deploy, and evaluate enterprise AI solutions. 

### Key Program Principles:
1. **Local-First Development, Cloud-Native Capstone**: Projects 1-4 run entirely locally on the student's machine via **Docker Compose** using open-source tools (Ollama/vLLM, PostgreSQL/Pgvector, Redis, LangGraph, Arize Phoenix) to ensure rapid iteration and zero unexpected costs. However, for the Project 5 Capstone, a $200 budget per student is allocated to provision a live cloud instance (e.g., an AWS EC2 GPU instance) and deploy their final multi-agent architecture to the public web.
2. **Project-First Pedagogy**: Theory is delivered "Just-In-Time". Students learn by inheriting realistic, messy enterprise codebases with seeded defects and architectural gaps that they must diagnose and fix.
3. **Containerized Engineering**: Every core required project path runs locally via `docker-compose`. If it doesn't run with `docker compose up`, it doesn't pass code review.
4. **High-Touch Support**: Students are supported by rigorous line-by-line code reviews on GitHub Pull Requests and mandatory Loom video client defenses.

---

## 🛠️ Required Hardware & Local Environment Setup

Due to the focus on local deployment of open-weight LLMs (Ollama/vLLM) and containerized vector databases, students must meet the following hardware minimums:

* **CPU**: 8-core Modern Processor (Intel i7/i9, AMD Ryzen 7/9, Apple Silicon M1/M2/M3/M4).
* **RAM**: 16 GB minimum (32 GB strongly recommended for smooth multi-container orchestration).
* **GPU/VRAM**: 8 GB VRAM minimum for local inference. (If local VRAM is insufficient, students will rely on the $200 external API budget or provided cloud notebooks).
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
| **Project 5** | W17–W22 | Autonomous Multi-Agent Platform & Defense | Advanced RAG, Multi-Agent LangGraph, Ragas Evals, LoRA | ~120 Hours (20h/wk) |

---

## 📖 Project Summaries

### [Project 1: System Diagnostics & API Scaling](project-1.md)
Students diagnose a provided monolith-based reference platform. They trace request paths, repair observability defects (Prometheus/Grafana), run reproducible load tests, and evaluate the latency impacts of mocked LLM API calls on traditional backend systems.

### [Project 2: Data Layer, Vector Search & Hybrid RAG](project-2.md)
Students build the foundational data layer for AI integration. They extract text and tables from enterprise documents using `Unstructured`, generate local embeddings with `FastEmbed`, and implement hybrid semantic retrieval using `pgvector` and BM25.

### [Project 3: Resilience, Microservices & Local LLM Serving](project-3.md)
Students deploy local LLM inference engines (`vLLM` or `Ollama`) within a strictly `docker-compose` orchestrated environment. They implement circuit breakers and retry logic to gracefully handle LLM API timeouts and failures, proving resiliency through a simulated failure lab.

### [Project 4: Zero-Trust Security, Guardrails & Governance](project-4.md)
Students secure the AI system against the OWASP LLM Top 10. They build a STRIDE threat model, implement output guardrails (`Guardrails AI`), configure PII redaction, and map educational compliance controls (EU AI Act & HIPAA).

### [Project 5: Autonomous Multi-Agent Platform & Defense](project-5.md)
The capstone. Students build a multi-agent tool flow using `LangGraph` with human-in-the-loop sandboxing. They run CI evaluations, calibrate LLM-as-a-judge metrics with `Ragas`, fine-tune a specialized model via LoRA, and deploy the full stack to a live cloud instance (AWS EC2).

---

## 🛠️ Student Assessment & Code Review Workflow

To mirror real-world engineering standards, pass/fail assessment is highly rigorous and manual:

1. **Continuous Integration (CI) Gates**: Every PR must pass automated CI checks (linting, test coverage, dependency scanning, and LLM smoke evals) before a human reviews it.
2. **Code Reviews**: Dedicated engineering reviewers conduct line-by-line code reviews on GitHub Pull Requests. Students must address all requested changes to merge their work.
3. **Client Defenses (Loom Videos)**: For every project, students must record a 5-15 minute Loom video acting as a "Forward Deployed Engineer" presenting their solution, demonstrating the working code, and explaining their architectural trade-offs to a simulated enterprise client.

---

## 🏆 Graduation Criteria

To graduate from the TripleTen AI FDE program, a student must:
1. successfully complete and merge GitHub Pull Requests for all 5 Projects.
2. Pass all automated CI/CD evaluation pipelines.
3. Pass the manual Code Review rubrics (achieving 100% of Must-Have criteria).
4. Deliver passing Client Defense Loom videos for all 5 projects.
5. Successfully deploy the Project 5 Capstone architecture to the cloud and defend the LLM telemetry metrics.
