# Claude Review: AI FDE Syllabus (v2) & Cross-Document Consistency

## Objective Review — Program Syllabus (v2: `5-projects-22-weeks/`, the current target)

### 🔴 Structural issue: hours-per-week budget doesn't match the week allocations

[overview-and-module-map.md](5-projects-22-weeks/overview-and-module-map.md) assigns week ranges; each `project-N.md` has its own **Workload** table. At the stated ~20h/week commitment, expected hours = weeks × 20. Actual vs. expected:

| Project | Weeks | Expected (20h/wk) | Actual workload | Delta |
|---|---|---:|---:|---:|
| P1 Diagnostics | 3 | 60 | 67 | +7 (+12%) |
| P2 Data/RAG | 4 | 80 | 86.5 | +6.5 (+8%) |
| P3 Resilience/LLM Serving | 4 | 80 | 96 | **+16 (+20%)** |
| P4 Security/Guardrails | 4 | 80 | 82.75 | +3.4% |
| P5 Multi-Agent Capstone | 7 | 140 | 105.5 | **−34.5 (−25%)** |
| **Total** | 22 | 440 | 437.75 | ~on target |

The program-level total (~440h) checks out only because P5's deficit cancels the other four's surplus. That's masking the real problem: **P5 — the capstone, gating project, and by far the densest scope** (hybrid RAG + reranking, multi-agent LangGraph + sandboxing + HITL, Ragas/LLM-as-judge evals, PEFT/LoRA fine-tuning, cost/latency telemetry, *and* the final defense) — runs at only ~15h/week against a 20h/week commitment, while the simplest project (P1) runs *over* budget. This is backwards: the hardest, highest-stakes project has the least time pressure relief, and it's the one where "fine-tune a model" alone is a notoriously unpredictable time sink for beginners. Treat this as the single biggest risk to program completion rates.

### 🟡 Tech-stack claims vs. actual project content

[AGENTS.md](../AGENTS.md) and the legacy syllabus both advertise the stack as *"Ollama/vLLM, PostgreSQL/Pgvector, **Qdrant**, Redis, **MinIO**, LangGraph, Arize Phoenix."* Grepping all five `project-N.md` files shows **neither Qdrant nor MinIO is mentioned once.** pgvector is the only vector store actually specified anywhere in the current-target syllabus. Either the stack claim is stale (drop Qdrant/MinIO) or a project is missing the task that was supposed to use them.

### 🟡 Internal ambiguity: is gRPC Core or Positioning in Project 2?

[project-2.md](5-projects-22-weeks/project-2.md) labels gRPC "(Positioning)" in Theory Topics, but Tech Setup provisions "preconfigured `protoc` build scripts... and **one gRPC extension point**" — that reads as hands-on implementation work, not decision-level knowledge. Similar (milder) ambiguity in [project-3.md](5-projects-22-weeks/project-3.md), where Redpanda/Kafka is "(Positioning)" but tied to "the selected resilience pattern" in Tech Setup. Worth clarifying whether these are graded builds or read-only scaffolds.

### 🟡 Project 5 breaks the "evolving platform" continuity narrative

P2 ("extended from Project 1"), P3 ("services from earlier projects"), and P4 ("secured version of the platform from Projects 1-3") each explicitly build on the prior project's codebase. [project-5.md](5-projects-22-weeks/project-5.md) just says "capstone starter repository" — no stated continuity from P1-P4. That undercuts the exact differentiator [program-comparison.md](../competitors/program-comparison.md) claims ("forces students to maintain and upgrade the same infrastructure across 22 weeks").

### 🟢 What's actually solid

- The five `project-N.md` briefs are internally consistent with each other in template (Skills → Tech Setup → Objectives → Theory → Delivery Limits → Workload) and with [executive-overview.md](../executive-overview.md)'s CORE/POSITIONING split per project — no contradictions found there.
- `[CORE]`/`[POSITIONING]` tagging is applied consistently and does real work bounding scope (e.g., explicitly punting Kubernetes/Terraform/Kafka to positioning-only for FDEs, consistently, across P3-4 and the module map).
- Docker-Compose-only constraint is honestly enforced in every Delivery Limits section (no doc quietly requires cloud/K8s).

---

## Consistency Check — Other Documents

| Finding | Detail |
|---|---|
| **Superseded doc has no deprecation notice** | [based-on-competitors-2w-sprints.md](based-on-competitors-2w-sprints.md) reads as a complete, live 22-week/11-sprint program (its own hardware reqs, graduation criteria, rubrics) with no banner marking it superseded. Only [AGENTS.md](../AGENTS.md) frames it as "Version 1." Anyone opening that file directly could mistake it for the current program. |
| **Hardware/setup requirements gap** | Minimum RAM/CPU/GPU and prerequisite software stack exist *only* in the superseded v1 doc. None of the v2 files (`overview-and-module-map.md`, `project-1..5.md`) restate this, even though v2 is what's actually meant to ship — the accessibility info got dropped in the v1→v2 rewrite. |
| **`projects/` folder documented but absent** | AGENTS.md's repo structure diagram lists a `projects/` directory ("Starter code specs, seeded defects, & rubric definitions") that doesn't exist in the repo. Understandable for a planning repo, but it's aspirational structure presented as current fact. |
| **Competitor/positioning docs are mutually consistent** | [fde-role-benchmark.md](../competitors/fde-role-benchmark.md), [competitor-curriculums.md](../competitors/competitor-curriculums.md), [program-comparison.md](../competitors/program-comparison.md), and [executive-overview.md](../executive-overview.md) all agree on terminology, tech choices, and the CORE/POSITIONING split per project — no contradictions across these four. |

---

**Bottom line:** the biggest fix worth prioritizing is P5's hours/week mismatch — either shorten P5's week window (freeing weeks for P1-P3, which are all over-budget) or increase P5's workload hours to match its actual scope. Second priority: reconcile the Qdrant/MinIO stack claim with what the projects actually build, and add a deprecation header to the v1 syllabus so it can't be mistaken for current.
