# Executive Overview: Dual-Track Program Methodology

This document outlines the strategic methodology for delivering both the **AI System Engineering (SE)** and **AI Forward Deployed Engineer (FDE)** bootcamp programs. 

By adopting a **Unified Project / Dual-Track Strategy**, TripleTen maximizes operational efficiency, reduces curriculum maintenance overhead, and ensures that instructors only need to master one set of core project codebases.

---

## The Challenge

Developing a 22-week technical bootcamp requires immense effort. Creating 5 full-scale, enterprise-grade projects with seeded defects, automated grading CI pipelines, and deployment infrastructure is the most expensive part of curriculum design.

If the SE and FDE programs were completely separate, we would need to maintain 10 massive repositories, train our code reviewers on 10 different codebases, and maintain 10 separate automated grading pipelines.

## The Solution: Unified Projects, Divergent Tasks

Our methodology solves this by **reusing the exact same 5 project starter repositories** for both programs, but differentiating the programs strictly through **Task Requirements and Grading Rubrics**.

Both SE and FDE students clone the identical GitHub repository (e.g., `tripleten-systemengineering-project-1`). 

- **System Engineering (SE) Students** are graded on their ability to build robust backend infrastructure (Kubernetes, Kafka, Terraform, CI/CD).
- **Forward Deployed Engineer (FDE) Students** are graded on their ability to deploy applied AI (Docker Compose, deterministic enterprise/provider scenarios, local LLMs, Guardrails, Hybrid RAG, Multi-Agent Workflows, and a bounded AWS capstone deployment).

---

## How It Works in Practice

We map technical concepts into two categories: `[CORE]` (must be implemented to pass) and `[POSITIONING]` (strategic knowledge for interviews, but not a graded implementation requirement).

Here is how the 5 shared projects are adapted for each student persona:

| Project Repository | SE Track (Backend Infrastructure Focus) | AI FDE Track (Applied AI Focus) |
| :--- | :--- | :--- |
| **P1: Diagnostics & Scaling** | **Core:** Distributed Traces, Database Bottlenecks, Load Testing. | **Core:** API Diagnostics, deterministic latency scenarios, Observability. |
| **P2: Polyglot Data Tier** | **Core:** gRPC service boundaries, Redis replication, Idempotency. | **Core:** Unstructured Document ETL, enterprise-data scenarios, Pgvector Data Prep. |
| **P3: Operations & Resilience** | **Core:** Local Kubernetes (`kind`), Terraform/OpenTofu, Kafka, Chaos Lab. | **Core:** Docker Compose, local serving, provider-emulator resiliency (Retries). |
| **P4: Security & Compliance** | **Core:** Kubernetes Secrets, RBAC, CI Security Gates. | **Core:** OWASP LLM, provider-emulator guardrails, PII Redaction. |
| **P5: Autonomous AI System** | **Core:** Basic RAG, CI Smoke Evals, Telemetry. | **Core:** Advanced RAG, Multi-Agent LangGraph, LLM-as-a-Judge, Fine-Tuning, protected AWS deployment. |

### FDE Delivery Boundary

FDE Projects 1-4 are built, tested, graded, and demonstrated locally with Docker Compose and deterministic scenario packs; they do not expose public endpoints, and Project 1 explicitly forbids one. Project 5 must first pass the same local acceptance path, then students deploy a temporary protected endpoint for a 14-day assessment window in one dedicated course-managed AWS sandbox. The P5 deployment is capped at $180 of AWS infrastructure plus $20 of approved API usage per student, with scheduled GPU sessions rather than an always-on GPU service. The delivery-repository contract for local scenarios — published development cases, held-out grading cases, and a per-emulator `FIDELITY.md` — is specified per project in the [project briefs](syllabus/) and awaits re-authoring as a standalone contract document.

---

## Business & Operational Benefits for TripleTen

1. **Write Once, Teach Twice**: Curriculum authors build one highly polished enterprise codebase (e.g., a monolith simulating an e-commerce platform). Both programs use it.
2. **Unified Instructor Training**: Tutors and code reviewers only need to understand the architecture, data models, and edge cases of 5 projects, not 10. They simply evaluate different rubric items based on the student's track.
3. **Reduced CI/CD Maintenance**: The automated tests for `pytest`, linting, and security scanning are shared. 
4. **Peer Learning**: SE and FDE students can collaborate in the same Slack/Discord channels. FDEs can help SEs understand the AI components, while SEs can help FDEs debug complex database queries, mirroring a real-world enterprise engineering team.
5. **Agile Iteration**: If a bug is fixed in the Project 2 starter code, the fix immediately benefits students in both programs.

## Summary

The Unified Project Strategy ensures that TripleTen delivers two distinct, highly specialized, and marketable 22-week bootcamps (SE and FDE) while incurring the curriculum maintenance cost of only a single program. 
