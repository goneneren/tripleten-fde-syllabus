# Project Overview: AI Forward Deployed Engineer (AI FDE) Syllabus

## 🎯 Program Vision & Parameters
- **Role Target**: AI Forward Deployed Engineer (AI FDE)
- **Program Duration**: 22 Weeks (440 Hours Total Study & Project Work)
- **Student Commitment**: ~20 Hours / Week
- **Pedagogical Model**: **Project-First & Problem-Driven** (Organized around **5 Major Real-World Enterprise Projects** with Just-In-Time theory)
- **Format**: Asynchronous project-first work combined with live instructor/tutor support, rigorous code reviews, office hours, and client defense.
- **Primary Goal**: Train job-ready AI Forward Deployed Engineers who can bridge production AI (LLMs, RAG, bounded agents, vector search, and evaluation) with enterprise delivery (discovery, APIs, data pipelines, system architecture, security, governance, client delivery, and cloud/container infrastructure).

---

## 💡 TripleTen Project-First Pedagogy & Methodology
Unlike traditional curriculum models that teach theory first and assign a small project at the end, TripleTen's **Project-First Approach** introduces real-world enterprise problems **upfront**. Students learn technical concepts **Just-In-Time (JIT)** as they encounter and solve concrete engineering challenges in their projects.

### Program-Wide Delivery Model & Constraints:
1. **5 Major Projects across 22 Weeks**: Total workload is 440 hours across five sequential field-delivery engagements: 60/80/80/80/140 hours. Project 5 contains Phase 5.A (80 hours) and Phase 5.B (60 hours).
2. **Local-First Development, Bounded AWS Capstone**: Projects 1–4 and Phase 5.A run and are graded entirely locally via **Docker Compose** with deterministic enterprise and provider scenarios. They do not deploy to cloud services or expose public endpoints. Phase 5.B first passes the same local acceptance path, then deploys the instructor-accepted Phase 5.A release to a temporary protected endpoint in one dedicated, course-managed AWS sandbox per student. The per-student program budget is capped at $200: $20 for approved LLM API usage and $180 for AWS infrastructure. The program provisions no AWS GPU; fine-tuning implementation is out of scope.
3. **Clear Pass/Fail Scope & Seeded Defect Labs**: Starter scaffolds include realistic enterprise legacy code, seeded bugs, performance bottlenecks, and architectural gaps that students must diagnose, audit, refactor, and fix.
4. **Reference Program Benchmark**: The FDE curriculum is a distinct five-project field-delivery program. It retains local-first grading and a bounded AWS capstone while using five physical starter repositories: Phase 5.B deploys the instructor-accepted Phase 5.A release tag from Repository 5.

### Required Local Environment and Recommended Hardware
The required local environment and recommended hardware support containerized vector databases and, where hardware allows, local open-weight LLMs:
- **RAM**: 16GB minimum (32GB strongly recommended for smooth multi-container orchestration).
- **GPU/VRAM**: A local GPU is optional and never affects grading. The assessed local inference path is a small quantized model; the deterministic provider emulator is the fallback. The $20 API allowance is split between Phase 5.A evaluation and Phase 5.B endpoint, held-out, and Final Demo Day traffic.
- **OS**: macOS (M-series preferred), Linux, or Windows (WSL2 required).

### Curriculum Content Taxonomy:
- `[CORE]` - Required implementation work that students build, operate, document, and defend.
- `[SUPPORTING]` - Just-in-time theory, lab guides, or practice exercises supporting core tasks.
- `[OPTIONAL]` - Advanced depth or extension topics separated from pass/fail scope.
- `[POSITIONING]` - Strategic, decision-level architecture knowledge (interview-defensible without forcing operational setup overhead).
- `[AI]` - AI Forward Deployed Engineer additions (LLMs, RAG, multi-agent state graphs, guardrails, evaluation, governance, MLOps).

---

## 🏗️ Repository & Delivery Architecture

This planning repository (`c:\repos\tripleten-fde-syllabus`) is the central design blueprint for the five-project curriculum. It specifies curriculum and delivery dependencies; student delivery repositories will be authored separately:

```
Project Delivery Repository Structure (Target Pattern):
├── compose.yaml / docker-compose.yml   # Multi-container orchestration scaffold
├── src/                                # Seeded codebase with real-world architecture gaps & bugs
├── tests/                              # Pytest test suite & automated task gates
├── docs/
│   ├── student/                        # Welcome guide, infra guide, setup & submission workflow
│   ├── instructor/                     # Rubrics, evaluation guide, repository rules
│   └── cms/                            # Sequential task-step authoring sources
└── scripts/                            # CI check scripts & student package bundler
```

---

## 🛠️ What is an AI Forward Deployed Engineer?
An **AI Forward Deployed Engineer (AI FDE)** operates at the intersection of Enterprise Software Engineering, Applied AI/ML, and Solutions Delivery (popularized by companies like Palantir, OpenAI, Anthropic, Scale AI, and Databricks).

An AI FDE must be able to:
1. **Understand Enterprise Business Logic & Needs**: Scope client problems and translate domain requirements into concrete technical architectures.
2. **Build & Integrate Production AI Systems**: Implement modern LLM pipelines, RAG architectures, multi-agent frameworks, fine-tuned models, and vector stores.
3. **Ship Enterprise-Grade Software**: Write clean, testable code, dockerize services, build robust APIs (REST/gRPC), set up CI/CD, and handle security, governance, and cloud deployment.
4. **Evaluate & Audit AI Systems**: Measure accuracy, hallucination, latency, throughput, token cost, and safety/security vulnerabilities (OWASP for LLMs).
5. **Manage Delivery & Client Iteration**: Work directly with stakeholders, conduct technical scoping, handle edge cases in messy enterprise data, and deliver production-ready software solutions.

---

## 📋 Syllabus Evolution & Versions

1. **TripleTen Five-Project, 22-Week Open-Source Version (Program of Record)**:
   - Documented in [`syllabus-fde-focused-5-projects/fde-focused-5-projects-opensource.md`](syllabus-fde-focused-5-projects/fde-focused-5-projects-opensource.md).
   - Five sequential field-delivery projects with problem-driven JIT learning maps. Project 5 contains a local build-and-acceptance phase (5.A) and a bounded AWS deployment-and-Demo-Day phase (5.B).
2. **LocalStack Alternative (Under Evaluation)**:
   - Documented in [`syllabus-fde-focused-5-projects/fde-focused-5-projects-localstack.md`](syllabus-fde-focused-5-projects/fde-focused-5-projects-localstack.md).
   - It is not the program of record and must not be adopted until its licensing and delivery constraints are resolved.
3. **Superseded Six-Project Source Edition (Historical)**:
   - Retained unchanged under [`syllabus-fde-focused/`](syllabus-fde-focused/) for comparison and review history.
   - Any embedded program-of-record status in those preserved snapshots is superseded by this file and the five-project edition above.

---

## 📁 Repository Structure
```
tripleten-fde-syllabus/
├── AGENTS.md                           # Project context, rules, and sitemap
├── competitors/                        # Competitor analysis & benchmark reports
│   ├── fde-role-benchmark.md           # Analysis of Palantir/OpenAI/Scale FDE job specs & expectations
│   ├── competitor-curriculums.md       # Analysis of existing AI / SE / ML Bootcamps
│   └── teaching-and-submission-models.md # Analysis of teaching methodologies & submission workflows
├── syllabus-fde-focused-5-projects/    # Current five-project curriculum and review record
│   ├── fde-focused-5-projects-opensource.md # Program of record
│   └── fde-focused-5-projects-localstack.md # Alternative under evaluation
├── syllabus-fde-focused/               # Superseded six-project source and historical evaluation record
│   ├── fde-focused-6-projects-opensource.md # Preserved source snapshot
│   ├── fde-focused-6-projects-localstack.md # Preserved alternative snapshot
│   ├── fde-focused-6-project-tree.md   # Task tree and evidence map
│   └── *-evaluation.md / *-verdict.md  # Historical evaluation artifacts
├── reference/                          # Saved role-research source material
├── executive-overview.md               # Shared-delivery strategy and program boundary
└── docs/                               # Supporting research and working artifacts
```

---

## 🤖 Guidelines for AI Assistants & Contributors
- **Adhere to the Project-First Philosophy**: Always ground theoretical topics in concrete project tasks and real-world problem scenarios.
- **Maintain the Delivery Boundary**: Projects 1–4 and Phase 5.A must run and pass locally using Docker Compose; none may expose a public endpoint. Phase 5.B must deploy only the instructor-accepted Phase 5.A release through the required temporary protected AWS profile. Do not add cloud requirements to Projects 1–4 or Phase 5.A, require a GPU, or add hands-on fine-tuning.
- **Keep the Capstone Budget Bounded**: Treat $200 as the total per-student allocation: $20 maximum for approved LLM API calls and $180 maximum for AWS. The delivery contract must define the fixed deployment profile, access controls, security baseline, verification evidence, and teardown process before student repositories are built.
- **Provide Deterministic Local Scenarios Before Launch**: Delivery repositories must implement a published and held-out scenario-pack contract covering each project's emulator: published development cases, held-out grading cases, and a per-emulator `FIDELITY.md` stating what the emulator does and does not reproduce. Do not treat an optional paid API or an external cloud service as a fallback for Projects 1–4 or Phase 5.A.
- **Treat the LocalStack Edition as Unadopted**: The Open-Source curriculum is canonical. Do not make LocalStack mandatory, add student-owned paid-service dependencies, or represent emulator fidelity as real-AWS evidence until the alternative's licensing and delivery constraints are formally resolved.
- **Enforce High-Touch Quality**: Ensure grading rubrics contain clear *Must-Have* criteria and *Recommendations*. Projects 1–4 and Phase 5.A require Instructor Presentation / Review recordings; Phase 5.B provides formative instructor support and culminates in the required Final Demo Day.
