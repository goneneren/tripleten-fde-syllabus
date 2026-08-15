# Comprehensive Curriculum Evaluation: AI Forward Deployed Engineer (6-Project, 22-Week Program)

## 1. Executive Evaluation Summary

Following the latest revisions to [`fde-focused-6-projects-opensource.md`](file:///c:/repos/tripleten-fde-syllabus/syllabus-fde-focused/fde-focused-6-projects-opensource.md) and [`fde-focused-6-projects-localstack.md`](file:///c:/repos/tripleten-fde-syllabus/syllabus-fde-focused/fde-focused-6-projects-localstack.md), both proposals have evolved from conceptual blueprints into **exceptionally mature, enterprise-grade curriculum specifications**.

### Key Architectural Improvements in this Revision:
1. **Repository Checkpoint & Reset Model:** Introducing physical starter repositories across Projects 1–5 with TripleTen reference baselines prevents defect cascading while preserving students' client-facing decision artifacts.
2. **Ports and Adapters Architecture:** Conformance-tested ports (`ObjectStore`, `JobQueue`, `SecretProvider`, `ModelProvider`) ensure the Project 6 AWS transition in Task 6.2 is a genuine configuration and adapter swap rather than a destructive code refactoring.
3. **Realistic Local Hardware Bounds:** Capping container memory to a 10 GB budget, standardizing on sub-3B parameter local LLMs (Ollama), and retaining PostgreSQL Full-Text Search (FTS) eliminates the OOM risks of running heavy OpenSearch/Java containers on 16 GB student laptops.
4. **Disciplined Security & LocalStack Scope:** Removing unenforced LocalStack IAM/KMS exercises and pinning Keycloak for OIDC/RBAC ensures students learn verifiable security without "security theater."
5. **Air-Tight Cloud Economics & Boundary:** Eliminating the GPU distraction from Project 6 and bounding compute to a single `t3.large` instance with Caddy, S3, SQS, and SSM anchors the deployment cost to ~$80 (well below the $180 ceiling) with a strict 14-day window and automated teardown.

---

## 2. Master Evaluation Matrix (Extended Dimensions)

| Evaluated Dimension | Open-Source Grade | LocalStack Grade | Detailed Evaluator Feedback |
|---|:---:|:---:|---|
| **1. Pacing & Workload (440h / 22 Wks)** | **A+** | **A** | Perfectly calibrated at exactly 20 hrs/week. Redistributing Project 1 (14h repair / 12h framing / 10h handoff) and bounding video recordings to five 10-minute single-take submissions prevents runaway student hours. |
| **2. FDE Role & Industry Alignment** | **A+** | **A+** | Hits the exact 2026 enterprise FDE mandate: discovery under ambiguity, legacy system triage, defensive client integration, SLO-driven reliability, STRIDE threat modeling, bounded agent state-graphs, and dual-room defenses. |
| **3. Field-Delivery & Stakeholder Rigor** | **A+** | **A+** | Rare among AI programs: treats client discovery, SoW negotiation, mid-sprint change control, and operational handoff as equal first-class citizens alongside code deliverables. |
| **4. Local-First Ergonomics & Hardware** | **A+** | **A** | **OS:** Near-zero friction with standard Docker containers (MinIO, RabbitMQ, Postgres, Keycloak). <br>**LocalStack:** Highly refined via `awslocal` & client factory, but LocalStack startup overhead slightly trails native containers. |
| **5. AI Integration, Evals & Safety Rigor** | **A+** | **A+** | AI is treated as an untrusted, stochastic component requiring input guardrails, PII redaction, schema validation, step/token budgets, deterministic CI smoke tests, and manual judged eval calibration. |
| **6. Cloud Transition & Cost Safety** | **A** | **A+** | **LocalStack:** Edge in AWS API familiarity (`boto3`/`awslocal`). <br>**Both:** Flawless cloud boundaries—single `t3.large`, prohibited resource lists, automated teardown script, and strict $180 cap with ~$80 target. |
| **7. Assessment Determinism & Scalability** | **A+** | **A+** | Fully asynchronous, deterministic grading: fixed transcripts, timed injects, published acceptance floors, and held-out scenario packs eliminate reviewer improvisation and guarantee grading consistency. |
| **8. Portfolio & Career Value** | **A+** | **A+** | Produces five high-signal portfolio artifacts (diagnostic trace, legacy client spec, unhappy-path resilience suite, judged eval report, bounded agent audit log) that qualify 3–5+ YOE engineers for Senior AI/FDE roles. |
| **OVERALL PROGRAM GRADE** | **A+ (98/100)** | **A (94/100)** | **The Open-Source variant is launch-ready as the primary program of record.** LocalStack is a high-value drop-in alternative pending licensing confirmation. |

---

## 3. Project-by-Project Evaluation and Report Card

```
========================================================================================
PROJECT REPORT CARD OVERVIEW
========================================================================================
Project 1: Client Discovery and System Diagnostics       [Grade: A+]  (60 Hours / W1-3)
Project 2: Enterprise Data Integration and Hybrid RAG   [Grade: A+]  (80 Hours / W4-7)
Project 3: Reliable AI Service Delivery                 [Grade: A]   (80 Hours / W8-11)
Project 4: Security, Guardrails and Governance Approval [Grade: A+]  (80 Hours / W12-15)
Project 5: Bounded Agent Workflow Under Ambiguity       [Grade: A+]  (80 Hours / W16-19)
Project 6: AWS Capstone, Adoption and Handback          [Grade: A]   (60 Hours / W20-22)
========================================================================================
```

---

### Project 1: Client Discovery and System Diagnostics (Weeks 1–3 / 60h)
* **Grade:** **A+**
* **Primary Objective:** Diagnose an unreliable existing AI system and frame an evidence-backed recommendation before writing code.
* **Key Strengths:**
  * **Anti-Greenfield Start:** Forces the engineer to orient inside an unfamiliar codebase with OpenTelemetry, Prometheus, and Grafana.
  * **Balanced Hours:** Allocating 14h to discovery, 14h to repair, and 22h to framing/handoff/ADRs establishes the FDE delivery mindset on day one.
  * **Asynchronous Stakeholder Simulation:** Role cards and fixed transcripts simulate ambiguous client requirements deterministically.

---

### Project 2: Enterprise Data Integration and Hybrid RAG (Weeks 4–7 / 80h)
* **Grade:** **A+**
* **Primary Objective:** Build an auditable document ingestion and hybrid retrieval pipeline over messy enterprise fixtures.
* **Key Strengths:**
  * **Scope Protection:** Excluding OCR engines and unbounded document types keeps the focus on deduplication, metadata normalization, and chunking strategies.
  * **Pragmatic Retrieval Architecture:** Dense pgvector + PostgreSQL full-text search (FTS) with reciprocal-rank fusion and cross-encoder reranking avoids the memory bloat of standalone OpenSearch clusters.
  * **SoW Defense Deliverable:** Closes with Task 2.5, where students record a 10-minute defense rejecting scope creep while defining explicit acceptance criteria.

---

### Project 3: Reliable AI Service Delivery (Weeks 8–11 / 80h)
* **Grade:** **A**
* **Primary Objective:** Stabilize an AI service against upstream provider latency, rate limits, outages, and messy legacy backends.
* **Key Strengths:**
  * **Defensive Legacy Integration:** Task 3.1 introduces an undocumented legacy emulator with stale fields and hidden rate limits, teaching real-world enterprise fault tolerance.
  * **Practical Resilience:** Pinned circuit-breaker-with-fallback and dead-letter queue (DLQ) patterns backed by a deterministic chaos/failure injector.
  * **Mid-Sprint Change Negotiation:** Task 3.4 forces students to triage an urgent Project 2 client escalation against active reliability tasks, modeling true field multi-tenancy.

---

### Project 4: Security, Guardrails and Governance Approval (Weeks 12–15 / 80h)
* **Grade:** **A+**
* **Primary Objective:** Implement an end-to-end security boundary (OIDC/RBAC, prompt injection defense, PII redaction, CI scanning) and obtain executive sign-off.
* **Key Strengths:**
  * **No "Security Theater":** Uses preconfigured Keycloak for real OIDC/RBAC token validation and file-mounted Compose / SSM secrets.
  * **Inspectable Evidence Boundary:** Task 4.4 requires linking STRIDE risks directly to automated test evidence, highlighting what local tests *do and do not* prove about cloud key custody.
  * **Adversarial Evaluation:** Students audit a flawed AI-generated compliance artifact for overclaims and omissions before facing a timed executive pressure inject.

---

### Project 5: Bounded Agent Workflow Under Ambiguity (Weeks 16–19 / 80h)
* **Grade:** **A+**
* **Primary Objective:** Turn a vague automation request into an auditable LangGraph state-machine with strict step/token limits and human-in-the-loop checkpoints.
* **Key Strengths:**
  * **Bounded Autonomy:** Rejects generic "autonomous agent" hype in favor of structured state graphs, tool schema validation, and complete audit logging.
  * **Deterministic CI Evals:** Bit-reproducible CI smoke tests gate merging; manual Ragas / LLM-as-judge scoring is calibrated on a fixed 20-case sample without holding CI hostage.
  * **Dual-Room Defense:** Separates the technical defense (safety boundaries, eval gaps) from the executive brief (ROI, adoption risk, deferred capabilities).

---

### Project 6: AWS Capstone, Adoption and Handback (Weeks 20–22 / 60h)
* **Grade:** **A**
* **Primary Objective:** Deploy the tagged Project 5 release to a secure AWS sandbox, verify client acceptance, deliver an enablement workshop, and verify teardown.
* **Key Strengths:**
  * **Guaranteed Budget Ceiling:** By locking the deployment to a single `t3.large` host (running Caddy reverse-proxy, application, and Postgres) with managed S3/SQS/SSM, standard AWS cost is ~$80, comfortably below the $180 cap.
  * **Clear Operational Gates:** Producing the verified endpoint by the end of Week 20 guarantees a 14-day reviewer window with a 3-business-day review SLA.
  * **Field Playbook & Teardown Verification:** Concludes with an auditable teardown checklist and a reusable discovery-to-handback playbook for the student's portfolio.

---

## 4. Variant Comparison: Open-Source vs. LocalStack

| Dimension | Open-Source Variant (`opensource.md`) | LocalStack Variant (`localstack.md`) | Strategic Takeaway |
|---|---|---|---|
| **Local Infrastructure** | MinIO, RabbitMQ, Docker Compose Secrets, Keycloak. | LocalStack (S3, SQS, SSM), Keycloak. | **Parity Achieved:** Both use Keycloak and Postgres FTS. |
| **Local Memory Footprint** | ~5.5 GB container RAM (very light). | ~7.2 GB container RAM (LocalStack runtime overhead). | Open-source provides higher headroom on 16 GB laptops. |
| **Licensing / Operational Risk** | **Zero Risk:** 100% permissive open-source licenses. | **Medium Risk:** Depends on LocalStack Hobby ToS compliance in commercial programs. | Open-Source is the safe default for immediate launch. |
| **AWS Cloud Translation** | Swaps `ObjectStore` & `JobQueue` adapters for AWS S3/SQS. | Replaces `awslocal` endpoints and sentinel keys with real AWS. | LocalStack gives slight syntax muscle-memory; OS teaches cleaner architectural separation. |
| **Recommended Program Role** | **Primary Program of Record (Canonical)** | **Approved Technical Fallback / Alternative** | Adopt OS for Cohort 1; keep LocalStack aligned as an interchangeable track. |

---

## 5. Final Production Readiness Verdict

### **Verdict:** **APPROVE FOR PRODUCTION**

Both syllabi have successfully resolved the prior architectural, workload, and economic risks. The 6-project, 22-week structure is cohesive, academically rigorous, and extraordinarily aligned with enterprise demand for AI Forward Deployed Engineers.

### Immediate Next Steps for Curriculum Production:
1. **Promote Open-Source to Program of Record:** Update [`AGENTS.md`](file:///c:/repos/tripleten-fde-syllabus/AGENTS.md) and [`syllabus/README.md`](file:///c:/repos/tripleten-fde-syllabus/syllabus/README.md) to adopt `fde-focused-6-projects-opensource.md` as the canonical curriculum.
2. **Build Seed Scaffolds with Strict Ports:** Ensure repository 1 through 5 starter codebases implement the conformance-tested `ObjectStore`, `JobQueue`, `SecretProvider`, and `ModelProvider` interfaces.
3. **Publish the Scenario-Pack Contract:** Finalize the deterministic role cards, fixed transcripts, and timed injects for all six projects prior to cohort onboarding.
