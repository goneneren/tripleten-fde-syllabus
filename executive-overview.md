# Executive Overview: Dual-Track Program Methodology

This document outlines the strategic methodology for delivering both the **AI System Engineering (SE)** and **AI Forward Deployed Engineer (FDE)** bootcamp programs. 

By adopting a **Unified Project / Dual-Track Strategy**, TripleTen maximizes operational efficiency, reduces curriculum maintenance overhead, and ensures that instructors only need to master one set of core project codebases.

---

## The Challenge

Developing a 22-week technical bootcamp requires immense effort. Creating six full-scale, enterprise-grade field-delivery engagements with seeded defects, automated grading CI pipelines, and deployment infrastructure is the most expensive part of curriculum design.

The FDE curriculum uses five physical starter repositories across six sequential engagements: Project 6 deploys and hands back the accepted Project 5 release. This preserves reusable platform work without requiring a sixth starter repository.

## The Solution: Unified Projects, Divergent Tasks

Our methodology reuses shared platform foundations where they fit, while allowing the FDE track to have its own six-project field-delivery sequence and task requirements.

FDE students progress through five supplied repository checkpoints. The next project starts from TripleTen's accepted reference checkpoint, so an earlier student defect cannot block later work.

- **System Engineering (SE) Students** are graded on their ability to build robust backend infrastructure (Kubernetes, Kafka, Terraform, CI/CD).
- **Forward Deployed Engineer (FDE) Students** are graded on their ability to deploy applied AI (Docker Compose, deterministic enterprise/provider scenarios, local LLMs, Guardrails, Hybrid RAG, Multi-Agent Workflows, and a bounded AWS capstone deployment).

---

## How It Works in Practice

We map technical concepts into two categories: `[CORE]` (must be implemented to pass) and `[POSITIONING]` (strategic knowledge for interviews, but not a graded implementation requirement).

The FDE program of record is documented in [`syllabus-fde-focused/fde-focused-6-projects-opensource.md`](syllabus-fde-focused/fde-focused-6-projects-opensource.md). Its six engagements are:

| FDE engagement | AI FDE delivery focus |
| :--- | :--- |
| **P1: Client Discovery and System Diagnostics** | Diagnose an unreliable AI-enabled workflow and make a bounded recommendation. |
| **P2: Enterprise Data Integration and Hybrid RAG** | Deliver and defend retrieval over messy enterprise data. |
| **P3: Reliable AI Service Delivery** | Stabilize service behavior through provider failures and changing requirements. |
| **P4: Security, Guardrails and Governance Approval** | Secure a high-value AI workflow and obtain a defensible risk decision. |
| **P5: Bounded Agent Workflow Under Ambiguity** | Build and evaluate one bounded, auditable agent workflow. |
| **P6: AWS Capstone, Adoption and Handback** | Deploy the accepted system temporarily, demonstrate value and safety, hand it back, and tear it down. |

### FDE Delivery Boundary

FDE Projects 1-5 are built, tested, graded, and demonstrated locally with Docker Compose and deterministic scenario packs; they do not expose public endpoints. Project 6 must first pass the same local acceptance path, then students deploy a temporary protected endpoint for a 14-day assessment window in one dedicated course-managed AWS sandbox. The capstone is capped at $180 of AWS infrastructure plus $20 of approved API usage per student; the program provisions no GPU and hands-on fine-tuning is out of scope. The delivery repositories must publish a scenario-pack contract with development and held-out cases and a `FIDELITY.md` for every emulator before cohort delivery.

---

## Business & Operational Benefits for TripleTen

1. **Write Once, Teach Twice**: Curriculum authors build one highly polished enterprise codebase (e.g., a monolith simulating an e-commerce platform). Both programs use it.
2. **Focused Instructor Training**: Tutors and reviewers work from one FDE evidence model across five repository checkpoints and six sequential engagements.
3. **Reduced CI/CD Maintenance**: The automated tests for `pytest`, linting, and security scanning are shared. 
4. **Peer Learning**: SE and FDE students can collaborate in the same Slack/Discord channels. FDEs can help SEs understand the AI components, while SEs can help FDEs debug complex database queries, mirroring a real-world enterprise engineering team.
5. **Agile Iteration**: If a bug is fixed in the Project 2 starter code, the fix immediately benefits students in both programs.

## Summary

The delivery strategy ensures that TripleTen can share platform foundations where appropriate while preserving the FDE program's distinct discovery, implementation, governance, deployment, and handback outcomes.
