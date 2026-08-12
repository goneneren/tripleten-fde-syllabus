# Project Overview: AI Forward Deployed Engineer (AI FDE) Syllabus

## 🎯 Program Vision & Parameters
- **Role Target**: AI Forward Deployed Engineer (AI FDE)
- **Program Duration**: 22 Weeks (~452 Hours Total Study & Project Work)
- **Student Commitment**: ~20 Hours / Week
- **Pedagogical Model**: **Project-First & Problem-Driven** (Organized around **5 Major Real-World Enterprise Projects** with Just-In-Time theory)
- **Format**: Asynchronous project-first work combined with live instructor/tutor support, rigorous code reviews, office hours, and client defense.
- **Primary Goal**: Train job-ready AI Forward Deployed Engineers who can bridge production AI (LLMs, RAG, Agents, Vector DBs, Fine-Tuning) with enterprise deployment (APIs, data pipelines, system architecture, security, evaluation, client delivery, and cloud/container infrastructure).

---

## 💡 TripleTen Project-First Pedagogy & Methodology
Unlike traditional curriculum models that teach theory first and assign a small project at the end, TripleTen's **Project-First Approach** introduces real-world enterprise problems **upfront**. Students learn technical concepts **Just-In-Time (JIT)** as they encounter and solve concrete engineering challenges in their projects.

### Program-Wide Delivery Model & Constraints:
1. **5 Major Projects across 22 Weeks**: Total workload calculated at ~452 hours across 5 sequential build phases.
2. **Local-First Development, Bounded AWS Capstone**: Projects 1-4 run and are graded entirely locally via **Docker Compose** with deterministic enterprise and provider scenarios. They do not deploy to cloud services or expose public endpoints; Project 1 explicitly forbids one. Project 5 first passes the same local acceptance path, then deploys a temporary protected endpoint in one dedicated, course-managed AWS sandbox per student. The per-student program budget is capped at $200: $20 for approved LLM API usage and $180 for AWS infrastructure. The AWS GPU is scheduled for bounded model-serving or fine-tuning sessions; it is never an always-on six-week host.
3. **Clear Pass/Fail Scope & Seeded Defect Labs**: Starter scaffolds include realistic enterprise legacy code, seeded bugs, performance bottlenecks, and architectural gaps that students must diagnose, audit, refactor, and fix.
4. **Reference Program Benchmark**: Aligned with TripleTen's 5-Project Systems Engineering project-first structure and local-first grading paradigm located at [`C:\repos\tripleten-systemengineering-projects\projects\v05-5-projects-22-weeks-local-and-aws-simplified`](file:///C:/repos/tripleten-systemengineering-projects/projects/v05-5-projects-22-weeks-local-and-aws-simplified). The FDE track intentionally diverges only by adding the bounded mandatory Project 5 AWS capstone.

### Required Local Environment and Recommended Hardware
The required local environment and recommended hardware support containerized vector databases and, where hardware allows, local open-weight LLMs:
- **RAM**: 16GB minimum (32GB strongly recommended for smooth multi-container orchestration).
- **GPU/VRAM**: 8GB VRAM is strongly recommended for local inference. It is not a Project 1-4 cloud fallback requirement: those projects provide mock, small-model, or approved local fallback paths. The $20 API allowance is reserved for Project 5; scheduled AWS GPU sessions are reserved for Project 5 model-serving or fine-tuning work.
- **OS**: macOS (M-series preferred), Linux, or Windows (WSL2 required).

### Curriculum Content Taxonomy:
- `[CORE]` - Required implementation work that students build, operate, document, and defend.
- `[SUPPORTING]` - Just-in-time theory, lab guides, or practice exercises supporting core tasks.
- `[OPTIONAL]` - Advanced depth or extension topics separated from pass/fail scope.
- `[POSITIONING]` - Strategic, decision-level architecture knowledge (interview-defensible without forcing operational setup overhead).
- `[AI]` - AI Forward Deployed Engineer additions (LLMs, RAG, multi-agent state graphs, guardrails, evaluation, governance, MLOps).

---

## 🏗️ Repository & Delivery Architecture

This planning repository (`c:\repos\tripleten-fde-syllabus`) serves as the central design blueprint for the 5-project curriculum. Actual student delivery repositories follow the project-delivery architecture benchmarked in early project alphas (e.g., [`C:\repos\tripleten-systemengineering-project-1`](file:///C:/repos/tripleten-systemengineering-project-1)):

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

1. **TripleTen 5-Project, 22-Week Project-First Version (Current Target)**:
   - Documented in [`syllabus/`](file:///c:/repos/tripleten-fde-syllabus/syllabus/).
   - 5 major real-world enterprise projects with problem-driven JIT learning maps.

---

## 📁 Repository Structure
```
tripleten-fde-syllabus/
├── AGENTS.md                           # Project context, rules, and sitemap
├── competitors/                        # Competitor analysis & benchmark reports
│   ├── fde-role-benchmark.md           # Analysis of Palantir/OpenAI/Scale FDE job specs & expectations
│   ├── competitor-curriculums.md       # Analysis of existing AI / SE / ML Bootcamps
│   └── teaching-and-submission-models.md # Analysis of teaching methodologies & submission workflows
├── syllabus/                           # Core 22-week curriculum design
│   ├── README.md                       # Program principles, roadmap, and graduation criteria
│   ├── overview-and-module-map.md      # 5-Project module map, hours calculation, and JIT roadmap
│   ├── project-1.md                    # Project 1 Brief: System Diagnostics & Enterprise API Scaling
│   ├── project-2.md                    # Project 2 Brief: Data Layer, Vector Search & Hybrid RAG
│   ├── project-3.md                    # Project 3 Brief: Resilience, Microservices & Local LLM Serving
│   ├── project-4.md                    # Project 4 Brief: Zero-Trust Security, Guardrails & Governance
│   ├── project-5.md                    # Project 5 Brief: Autonomous Multi-Agent Platform & Defense
│   ├── project-5-aws-deployment.md     # P5 AWS estimate, deployment workflow, and teardown contract
│   └── scenario-emulator-delivery.md   # Required local scenario-emulator delivery contract
└── projects/                           # Starter code specs, seeded defects, & rubric definitions
    ├── README.md                       # Delivery-artifact inventory and launch prerequisites
    └── project-5-rubric.md             # P5 local, cloud, cost, and teardown Must-Haves
```

---

## 🤖 Guidelines for AI Assistants & Contributors
- **Adhere to the Project-First Philosophy**: Always ground theoretical topics in concrete project tasks and real-world problem scenarios.
- **Maintain the Delivery Boundary**: Projects 1-4 must run and pass locally using Docker Compose; Project 1 must not expose a public endpoint. Project 5 must pass locally before its required, temporary protected AWS deployment. Do not add cloud requirements to Projects 1-4 or turn the P5 GPU into an always-on service.
- **Keep the Capstone Budget Bounded**: Treat $200 as the total per-student allocation: $20 maximum for approved LLM API calls and $180 maximum for AWS. Use the estimate, access controls, security baseline, and teardown process in [`syllabus/project-5-aws-deployment.md`](syllabus/project-5-aws-deployment.md).
- **Provide Deterministic Local Scenarios Before Launch**: Delivery repositories must implement the published and held-out scenario-pack contract in [`syllabus/scenario-emulator-delivery.md`](syllabus/scenario-emulator-delivery.md). Do not treat an optional paid API or an external cloud service as a fallback for Projects 1-4.
- **Enforce High-Touch Quality**: Ensure grading rubrics contain clear *Must-Have* criteria and *Recommendations*, alongside Loom video client demonstration requirements.
