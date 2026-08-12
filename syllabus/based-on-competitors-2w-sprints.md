> [!WARNING]
> **DEPRECATED: LEGACY 11-SPRINT MODEL**
> This document describes an older, competitor-based 11-sprint curriculum model. 
> The authoritative, current curriculum model is the **5-Project Project-First Syllabus** located in [`AGENTS.md`](../AGENTS.md) and [`5-projects-22-weeks/overview-and-module-map.md`](5-projects-22-weeks/overview-and-module-map.md).

# AI Forward Deployed Engineer (AI FDE) Syllabus
## 22-Week Bootcamp Program | ~20 Hours / Week Commitment (~440 Hours Total)

---

## 🚀 Program Manifesto & Local-First Philosophy

The **AI Forward Deployed Engineer (AI FDE)** program is designed to build production-ready engineers who can architect, deploy, and evaluate enterprise AI solutions. 

### Key Program Principles:
1. **Local-First & 100% Open Source**: All development is performed on the student's local machine using **Docker containers** and open-source software (Ollama/vLLM, PostgreSQL/Pgvector, Qdrant, MinIO, Redis, Arize Phoenix, LangGraph). There are no mandatory cloud subscriptions or proprietary API paywalls required to complete the curriculum.
2. **Containerized Engineering**: Every sprint project must be fully containerized via `docker-compose.yml`. If it doesn't run with `docker compose up`, it doesn't pass code review.
3. **Sprint-Based Asynchronous Pacing**: Organized into **11 Two-Week Sprints**. Each sprint requires ~40 hours of effort (~20 hours/week) comprising interactive theory, local lab exercises, and a client-simulated sprint project.
4. **High-Touch Support**: Students are supported by live weekly instructor office hours, asynchronous 24/7 tutor assistance on Discord/Slack, and rigorous line-by-line code reviews on GitHub Pull Requests.

---

## 🛠️ Required Hardware & Local Environment Setup

### Recommended Minimum Hardware:
* **CPU**: 8-core Modern Processor (Intel i7/i9, AMD Ryzen 7/9, Apple Silicon M1/M2/M3/M4).
* **RAM**: 16 GB minimum (32 GB recommended for running multiple Docker containers alongside local LLM inference).
* **Storage**: 100 GB free SSD space (for Docker images, local vector DBs, and local open-weights LLMs).
* **GPU (Optional but Recommended)**: NVIDIA GPU with 8GB+ VRAM or Apple Silicon unified memory (for accelerating local vLLM / Ollama models). CPU execution via Ollama/vLLM quantizations (GGUF/Q4) is fully supported for all sprints.

### Prerequisites Software Stack (Sprint 0 Setup):
* Docker Desktop or Rancher Desktop (with Docker Compose enabled)
* Python 3.12+ & `uv` / `poetry` dependency manager
* Git & GitHub CLI (`gh`)
* VS Code or Cursor IDE
* Ollama (for running local open-weights models like `llama3.3`, `qwen2.5-coder`, and `nomic-embed-text`)

---

## 📅 22-Week Master Curriculum Roadmap Overview

| Sprint | Weeks | Module Topic | Core Open-Source Stack | Project Deliverable |
| :--- | :--- | :--- | :--- | :--- |
| **Sprint 1** | W01–W02 | Enterprise Python & Async APIs | Python 3.12, FastAPI, Pydantic, Pytest | Containerized Enterprise REST API Service |
| **Sprint 2** | W03–W04 | Local Data Infrastructure & Storage | Docker Compose, PostgreSQL, Redis, MinIO | Local Data Ingestion & Storage Pipeline |
| **Sprint 3** | W05–W06 | Unstructured Data Ingestion & ETL | Unstructured.io, PDFMiner, DuckDB | Enterprise Multi-Format Document Processor |
| **Sprint 4** | W07–W08 | Embeddings & Hybrid Vector Search | Qdrant (Docker), Pgvector, FastEmbed | Local Hybrid Vector & BM25 Search Engine |
| **Sprint 5** | W09–W10 | Local LLM Serving & Structured Generation | Ollama, Instructor, PydanticAI | Local LLM Microservice with Strict Schema Enforcement |
| **Sprint 6** | W11–W12 | Advanced RAG Architectures & Context Eng. | LlamaIndex / LangChain, Cohere ReRank (local), Ragas | Enterprise Knowledge Base RAG with Citation Tracing |
| **Sprint 7** | W13–W14 | Autonomous Agents & Function Calling | LangGraph, Local Tool Bindings, SQLite | Stateful Multi-Step Autonomous Task Agent |
| **Sprint 8** | W15–W16 | Multi-Agent Orchestration & Enterprise Workflows | AutoGen / LangGraph, Human-in-the-Loop | Multi-Agent Customer Support & Operations System |
| **Sprint 9** | W17–W18 | Local High-Throughput Serving & Fine-Tuning | vLLM, Hugging Face PEFT, LoRA/QLoRA, Unsloth | Fine-Tuned Local Domain Model & Inference Engine |
| **Sprint 10** | W19–W20 | LLMOps, Observability & Security Guardrails | Arize Phoenix, Guardrails AI, OWASP LLM Top 10 | Monitored & Red-Teamed Enterprise AI Gateway |
| **Sprint 11** | W21–W22 | Final Enterprise Capstone & Client Defense | Complete Local Docker Stack, OpenAPI, Loom | End-to-End Enterprise Forward Deployment Capstone |

---

## 📖 Sprint-by-Sprint Detailed Modules & Project Specifications

---

### Sprint 1 (Weeks 1–2): Enterprise Python & Async API Engineering

* **Focus**: Transitioning from scripts to modular, production-grade Python services with strict type safety, asynchronous execution, and RESTful API standards.
* **Weekly Time Allocation**: 10h Theory & Exercises / 10h Sprint Project per week.

#### Learning Objectives:
* Master Python 3.12+ advanced features: dataclasses, type hints, context managers, generators, and async/await (`asyncio`).
* Build high-performance REST APIs using **FastAPI** and **Pydantic v2**.
* Implement structured logging (JSON format using `structlog`), custom middleware, CORS, and dependency injection.
* Containerize Python services cleanly using multi-stage `Dockerfile`s and non-root security principles.

#### Local Docker Stack:
* `Dockerfile` for Python FastAPI App (multi-stage build with `uv`/`poetry`)

#### Sprint 1 Project Prompt:
> **Enterprise Microservice for Client Telemetry Ingestion**  
> Build a containerized FastAPI web microservice that accepts high-frequency telemetry events from enterprise clients, validates incoming payloads against Pydantic schemas, handles asynchronous batch processing, logs structured event metrics, and provides health-check (`/healthz`, `/readyz`) endpoints.

#### Submission Requirements & Rubric:
1. Modular directory structure (`src/api`, `src/core`, `src/services`, `tests`).
2. Automated unit and integration tests using `pytest` and `httpx` (>80% coverage).
3. `Dockerfile` that builds and runs cleanly under non-root user.
4. OpenAPI (`/docs`) auto-generated documentation.

---

### Sprint 2 (Weeks 3–4): Local Data Infrastructure & Storage Systems

* **Focus**: Setting up reproducible, multi-container local data infrastructure for enterprise persistence.
* **Weekly Time Allocation**: 10h Theory & Exercises / 10h Sprint Project per week.

#### Learning Objectives:
* Write clean, maintainable `docker-compose.yml` configurations with service dependencies, healthchecks, custom networks, and named persistent volumes.
* Interact with relational databases using **PostgreSQL** and async ORMs (**SQLAlchemy 2.0** / **SQLModel** / **asyncpg**).
* Utilize **Redis** for in-memory caching, rate-limiting, and state management.
* Deploy **MinIO** locally as an S3-compatible enterprise object store for documents and blob data.

#### Local Docker Stack:
* `postgres:16-alpine`, `redis:7-alpine`, `minio/minio` + `minio/mc` (client container)

#### Sprint 2 Project Prompt:
> **Local Enterprise Object & Metadata Repository Pipeline**  
> Build a multi-container data pipeline using Docker Compose. The system must ingest enterprise raw documents into MinIO object storage, generate relational metadata records in PostgreSQL, cache frequent lookup queries in Redis, and expose a FastAPI management interface.

#### Submission Requirements & Rubric:
1. Single `docker-compose up` command orchestrating FastAPI, Postgres, Redis, and MinIO.
2. Database migrations handled via **Alembic**.
3. Redis caching layer reducing database query overhead.
4. Comprehensive `README.md` with environment configuration instructions.

---

### Sprint 3 (Weeks 5–6): Unstructured Enterprise Data Ingestion & ETL

* **Focus**: Ingesting, parsing, cleaning, and transforming messy real-world enterprise documents (PDFs, DOCX, HTML, scanned tables).
* **Weekly Time Allocation**: 10h Theory & Exercises / 10h Sprint Project per week.

#### Learning Objectives:
* Extract text, tables, and images from complex document types using open-source tools (**Unstructured.io**, **pdfplumber**, **PyPDF**).
* Implement text normalization, layout detection, header/footer removal, and table extraction into structured JSON/Markdown.
* Use **DuckDB** and **Pandas** for rapid in-memory processing of structured tabular metadata.
* Design idempotent ETL pipelines that handle file corruption, encoding bugs, and missing data gracefully.

#### Local Docker Stack:
* Ingestion Worker container running `unstructured` and `DuckDB`

#### Sprint 3 Project Prompt:
> **Enterprise Document Parsing & Normalization Engine**  
> Build a local document ingestion worker that monitors an input directory in MinIO, extracts text and layout structures from complex enterprise PDFs/scans, converts tabular data into clean Markdown tables, normalizes metadata, and saves structured JSON chunks into PostgreSQL.

#### Submission Requirements & Rubric:
1. Ingestion pipeline capable of processing multi-page PDFs with embedded tables.
2. Robust error handling for corrupt files with failed job status logging in Postgres.
3. Automated test suite asserting parsing accuracy across sample messy documents.

---

### Sprint 4 (Weeks 7–8): Local Vector Stores, Embeddings & Hybrid Search

* **Focus**: Understanding vector geometry, embedding generation, dense vs. sparse retrieval, and hybrid keyword-vector search engines.
* **Weekly Time Allocation**: 10h Theory & Exercises / 10h Sprint Project per week.

#### Learning Objectives:
* Generate local vector embeddings using **FastEmbed** or **Sentence-Transformers** (`all-MiniLM-L6-v2`, `bge-small-en-v1.5`, `nomic-embed-text`).
* Deploy and query open-source vector databases: **Qdrant** (local Docker) and **PostgreSQL with Pgvector extension**.
* Implement chunking strategies: Fixed-size, Recursive Character, Sentence Boundary, and Semantic Chunking with overlap tuning.
* Build **Hybrid Search engines** combining dense vector cosine similarity with sparse keyword retrieval (**BM25**) and Reciprocal Rank Fusion (RRF).

#### Local Docker Stack:
* `qdrant/qdrant:latest`, `pgvector/pgvector:pg16`

#### Sprint 4 Project Prompt:
> **Local Hybrid Vector Search & Retrieval Engine**  
> Build a local search service containerized with Qdrant and Pgvector. The engine must ingest parsed document chunks, compute dense embeddings locally, generate BM25 sparse indices, and expose a unified `/search` endpoint returning hybrid search results weighted by RRF.

#### Submission Requirements & Rubric:
1. Docker Compose setup including Qdrant and Pgvector.
2. Configurable chunking pipeline supporting recursive and semantic chunking.
3. Hybrid search implementation combining BM25 and vector search with benchmark comparison tests.

---

### Sprint 5 (Weeks 9–10): Local LLM Serving & Structured Generation

* **Focus**: Running open-weights LLMs on local hardware and enforcing strict structured JSON outputs for enterprise integration.
* **Weekly Time Allocation**: 10h Theory & Exercises / 10h Sprint Project per week.

#### Learning Objectives:
* Deploy and manage open-source LLMs locally using **Ollama** (`llama3.3:8b`, `qwen2.5:7b`, `mistral:7b`).
* Master local model parameter tuning: temperature, top_p, repeat_penalty, system prompts, and context length adjustment.
* Enforce deterministic JSON output extraction from LLMs using **Instructor** and **PydanticAI** with retry logic.
* Implement native LLM **Function Calling / Tool Use** schemas locally.

#### Local Docker Stack:
* `ollama/ollama:latest` container volume-mapped to local model weights

#### Sprint 5 Project Prompt:
> **Local Enterprise Data Extraction & API Service**  
> Create a microservice powered by local Ollama models. The service takes unstructured enterprise customer emails/tickets, executes structured schema extraction via Instructor/Pydantic, validates output schemas (extracting urgency, customer ID, sentiment, and action items), and retries automatically on schema failure.

#### Submission Requirements & Rubric:
1. 100% local execution using Ollama without external API dependencies.
2. Strict schema extraction validation with zero invalid JSON fallback failures.
3. Pytest suite evaluating extraction accuracy against a benchmark dataset of tickets.

---

### Sprint 6 (Weeks 11–12): Advanced RAG Architectures & Context Engineering

* **Focus**: Architecting production-grade Retrieval-Augmented Generation (RAG) systems with query transformation, re-ranking, and hallucination evaluation.
* **Weekly Time Allocation**: 10h Theory & Exercises / 10h Sprint Project per week.

#### Learning Objectives:
* Master RAG orchestration frameworks: **LlamaIndex** and **LangChain**.
* Implement advanced RAG techniques: Query Rewriting, Hypothetical Document Embeddings (HyDE), Parent-Child Chunking, and Sentence Window Retrieval.
* Integrate local **Cross-Encoder Re-rankers** (`bge-reranker-base` / FlashRank) to boost retrieval precision.
* Implement citation tracing (linking generated answer claims directly to source chunk IDs).
* Evaluate RAG performance using open-source evaluation metrics via **Ragas** (Faithfulness, Answer Relevance, Context Recall).

#### Local Docker Stack:
* Qdrant, Ollama, FastAPI RAG Service

#### Sprint 6 Project Prompt:
> **Enterprise Knowledge Base RAG Assistant with Citation & Eval**  
> Build an enterprise RAG assistant that answers employee policy/technical questions from internal company documents. The engine must perform query expansion, retrieve relevant chunks via hybrid search, re-rank results using FlashRank/Cross-Encoder, generate responses with exact file/page citations via Ollama, and include an automated Ragas evaluation suite.

#### Submission Requirements & Rubric:
1. End-to-end local RAG pipeline with sub-3-second response latency.
2. Verified citation mapping accuracy for every generated answer statement.
3. Automated Ragas evaluation script reporting Faithfulness and Context Recall scores.

---

### Sprint 7 (Weeks 13–14): Autonomous Agents & Tool Execution

* **Focus**: Building single-agent stateful decision-making systems capable of planning, executing local tools, and handling unexpected tool errors.
* **Weekly Time Allocation**: 10h Theory & Exercises / 10h Sprint Project per week.

#### Learning Objectives:
* Understand agentic design patterns: ReAct (Reasoning + Acting), Plan-and-Solve, and Reflection.
* Build stateful agent graphs using **LangGraph**.
* Create custom Python tool bindings (database queries, local file operations, web scraping, arithmetic calculators).
* Implement state persistence, memory checkpointing, and error-recovery loops.

#### Local Docker Stack:
* FastAPI, Ollama, SQLite / Postgres checkpoint persistence

#### Sprint 7 Project Prompt:
> **Autonomous Enterprise Database & File Operations Agent**  
> Build an autonomous ReAct agent using LangGraph connected to a local Ollama LLM. The agent accepts natural language analytical requests (e.g., "Summarize top 5 sales in Postgres and save a plot into MinIO"), formulates execution plans, executes local SQL/file tools, self-corrects broken SQL queries, and persists execution state.

#### Submission Requirements & Rubric:
1. Stateful LangGraph execution flow with loop protection and retry mechanisms.
2. At least 3 custom tools (SQL execution, file writing, data summary).
3. Demonstration of agent self-healing when given an intentionally flawed initial query.

---

### Sprint 8 (Weeks 15–16): Multi-Agent Orchestration & Enterprise Workflows

* **Focus**: Coordinating multiple specialized autonomous agents into complex collaborative enterprise workflows with human-in-the-loop oversight.
* **Weekly Time Allocation**: 10h Theory & Exercises / 10h Sprint Project per week.

#### Learning Objectives:
* Design multi-agent topologies: Supervisor/Router, Hierarchical Teams, and Sequential Pipelines using **LangGraph** or **CrewAI**.
* Implement inter-agent message passing, shared state graphs, and task handoffs.
* Integrate **Human-in-the-Loop (HITL)** approval breakpoints before critical actions (e.g., database writes, client email generation).
* Manage context window expansion and summarize conversation state between multi-agent steps.

#### Local Docker Stack:
* Multi-Agent Service, Redis state cache, Ollama local model server

#### Sprint 8 Project Prompt:
> **Multi-Agent Customer Support & Issue Escalation System**  
> Build a multi-agent system comprising 3 specialized agents: (1) Triage & Intent Classifier Agent, (2) Technical RAG Investigator Agent, and (3) Customer Response Writer Agent. The workflow routes incoming issues, investigates internal knowledge bases, drafts responses, and pauses for Human Manager Approval before final dispatch.

#### Submission Requirements & Rubric:
1. Multi-agent state graph built cleanly in LangGraph or CrewAI.
2. Verified human-in-the-loop breakpoint mechanism for sensitive steps.
3. Full execution trace logging showing agent state transitions and tool calls.

---

### Sprint 9 (Weeks 17–18): Local High-Throughput Model Serving & Fine-Tuning

* **Focus**: Maximizing local inference throughput using vLLM and fine-tuning open-source models for domain-specific tasks using PEFT/LoRA.
* **Weekly Time Allocation**: 10h Theory & Exercises / 10h Sprint Project per week.

#### Learning Objectives:
* Deploy high-throughput local inference servers using **vLLM** (PagedAttention, continuous batching, OpenAI-compatible API endpoint).
* Understand parameter-efficient fine-tuning (**PEFT**) techniques: **LoRA** and **QLoRA**.
* Prepare instruction-tuning datasets (JSONL format, prompt-response formatting) using **Unsloth** or **Hugging Face TRL**.
* Fine-tune a lightweight base model (e.g., `Llama-3.2-3B` or `Qwen2.5-3B`) on a specialized domain dataset and export GGUF / Adapter weights.

#### Local Docker Stack:
* `vllm/vllm-openai:latest` container (or Ollama custom ModelFile loading LoRA adapter)

#### Sprint 9 Project Prompt:
> **Domain-Specific Fine-Tuned Model & vLLM Serving Pipeline**  
> Prepare an instruction fine-tuning dataset for a enterprise domain (e.g., medical report translation or specialized code formatting). Fine-tune a 3B parameter open-source model using QLoRA/Unsloth, convert the adapter weights, serve the fine-tuned model locally via vLLM Docker container, and benchmark throughput (tokens/sec) vs. base model.

#### Submission Requirements & Rubric:
1. Reproducible fine-tuning script (`train.py`) and formatted dataset validator.
2. Docker container serving the fine-tuned model via OpenAI-compatible API.
3. Benchmark report comparing accuracy and tokens/sec latency against the un-tuned base model.

---

### Sprint 10 (Weeks 19–20): LLMOps, Observability & Security Guardrails

* **Focus**: Monitoring LLM applications in production, tracking cost/latency/quality metrics, and protecting systems against prompt injection and security vulnerabilities.
* **Weekly Time Allocation**: 10h Theory & Exercises / 10h Sprint Project per week.

#### Learning Objectives:
* Implement open-source LLM tracing and observability using **Arize Phoenix** or **MLflow** via OpenTelemetry.
* Trace complete RAG and Agent execution graphs: latency per node, prompt/completion token usage, intermediate steps.
* Implement input and output security guardrails using **Guardrails AI** / **NeMo Guardrails** / regex validators.
* Audit and defend systems against **OWASP LLM Top 10** vulnerabilities (Prompt Injection, Insecure Output Handling, Data Poisoning, Sensitive Information Disclosure).

#### Local Docker Stack:
* `arize-phoenix` container, Guardrails gateway proxy container, FastAPI App

#### Sprint 10 Project Prompt:
> **Monitored & Secured Enterprise AI API Gateway**  
> Build a production API gateway wrapping local RAG/Agent services. The gateway must intercept incoming requests, scan for prompt injection attempts using local guardrails, redact PII (personally identifiable information), send OpenTelemetry traces to an Arize Phoenix container, and block unsafe model responses.

#### Submission Requirements & Rubric:
1. Docker Compose setup including Arize Phoenix observability server.
2. Active prompt injection detection blocking malicious red-team inputs.
3. Live Phoenix dashboard screenshot/export showing multi-node execution traces.

---

### Sprint 11 (Weeks 21–22): Final Enterprise Capstone & Client Defense

* **Focus**: Integrating all program competencies into a complete, containerized enterprise AI solution delivered with professional client documentation and live defense.
* **Weekly Time Allocation**: 20h Project Build & Client Delivery per week.

#### Learning Objectives:
* Architect end-to-end enterprise systems combining Data ETL, Hybrid RAG, Multi-Agent Workflows, Security Guardrails, and Observability.
* Complete enterprise technical scoping, API specification documentation, and client handoff guides.
* Present technical solution architecture to senior engineers/instructors acting as enterprise client stakeholders.

#### Local Docker Stack:
* Complete single-command `docker-compose.yml` orchestrating FastAPI, Postgres, Pgvector/Qdrant, Ollama/vLLM, MinIO, Redis, and Arize Phoenix.

#### Capstone Project Choices (Select 1):
1. **Enterprise Financial Audit & Compliance Agent System**: Autonomous multi-agent pipeline parsing quarterly corporate filings, extracting financial metrics, checking compliance rules, generating audit reports with full citations.
2. **Healthcare Clinical Knowledge Base & Triage Assistant**: HIPAA-compliant local RAG & Agent system processing clinical notes, sanitizing PII, cross-referencing medical guidelines, and generating preliminary triage recommendations with doctor approval workflow.
3. **Automated Enterprise Codebase Refactoring & Vulnerability Scanner**: Multi-agent developer tool scanning local repositories, identifying OWASP security vulnerabilities, generating unit tests, and drafting pull requests with refactored code.

#### Capstone Submission Requirements & Final Defense Rubric:
1. **GitHub Repository**: Production-grade modular codebase with complete automated test suite (`pytest`).
2. **One-Command Deployment**: `docker compose up --build` launches the complete ecosystem cleanly on a fresh machine.
3. **System Architecture Document (`README.md`)**: Complete Mermaid.js diagrams, API specifications, data flow diagrams, and threat model.
4. **Client Video Walkthrough & Live Defense (Loom / Live Zoom)**: A 5–7 minute professional client demonstration detailing technical decisions, trade-offs, security measures, and live system capabilities.

---

## 🛠️ Student Assessment & Code Review Workflow

Every sprint follows a structured submission and review process on GitHub:

```
Step 1: Student creates feature branch on local repo
Step 2: Student completes local development & verifies `docker compose up`
Step 3: Student runs automated test suite (`pytest`)
Step 4: Student opens Pull Request (PR) on GitHub using standard template
Step 5: Automated GitHub Actions CI runs linting & unit tests
Step 6: Assigned Code Reviewer conducts line-by-line code review (24-48h SLA)
Step 7: Student addresses review feedback and pushes revision commits
Step 8: Code Reviewer approves PR -> Sprint marked COMPLETE!
```

---

## 🏆 Graduation Criteria

To receive the **AI Forward Deployed Engineer (AI FDE)** Certificate of Completion, students must:
1. Pass all **11 Sprint Projects** by meeting 100% of the *Must-Have Requirements* in each sprint rubric.
2. Maintain a containerized, working GitHub portfolio for all 11 projects.
3. Successfully complete and defend the **Final Enterprise Capstone Project** in Sprint 11.
