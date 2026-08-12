# Analysis: Bootcamp Teaching Methodology & Student Submission Workflow

## Executive Summary
This document analyzes teaching methodologies, student operational workflows, code submission pipelines, and instructor support models across modern technical bootcamps. It highlights how TripleTen's signature model operates and adapts it for the 22-Week **AI Forward Deployed Engineer (AI FDE)** 5-Project program.

---

## 1. Teaching Methodology Comparison

| Component | Asynchronous + Platform Model (TripleTen Style) | Live Lecture Model (General Assembly) | Cohort / Masterclass Model (Maven / CoRise) |
| :--- | :--- | :--- | :--- |
| **Pacing** | 5 Project Phases (Self-paced within phase boundaries) | Fixed schedule (e.g. 7pm-10pm Mon/Wed + Sat) | Scheduled weekly live sessions |
| **Learning Content** | Project-First (JIT Theory), interactive lessons, seeded repos | Live Zoom lectures & code-alongs | Recorded videos + live guest workshops |
| **Student Support** | Tutors on Discord/Slack (24/7 SLA), Live Office Hours | Live instructors during class, TAs post-class | Community Q&A, mentor office hours |
| **Evaluation** | Human Code Reviews on GitHub PRs & Client Defense (Loom) | Homework submissions, pass/fail capstones | Project presentations & peer review |
| **Flexibility** | High (ideal for 20h/week working adults) | Low (rigid attendance) | Medium |

---

## 2. TripleTen-Style Operational Model for AI FDE

### A. The 5-Project Build Cycle
The 22-week program eschews traditional isolated weekly sprints in favor of **5 Major Enterprise Projects** mapped across the 22 weeks. Students learn Just-In-Time (JIT) theory as they encounter concrete problems in their scaffolded enterprise codebases.

1. **Project 1: System Diagnostics & API Scaling** (Weeks 1-3)
2. **Project 2: Data Layer, Vector Search & Hybrid RAG** (Weeks 4-7)
3. **Project 3: Resilience, Microservices & Local LLM Serving** (Weeks 8-12)
4. **Project 4: Zero-Trust Security, Guardrails & Governance** (Weeks 13-16)
5. **Project 5: Autonomous Multi-Agent Platform & Defense** (Weeks 17-22)

### B. Instructor & Support Roles
1. **Tutors / Senior Instructors**:
   - Provide technical support on Discord/Slack.
   - Host live weekly office hours, live Q&A, and technical deep-dives (e.g., "Debugging RAG Latency" or "Setting up vLLM locally via Docker Compose").
2. **Code Reviewers (Industry Practitioners)**:
   - Provide rigorous, professional line-by-line code reviews on GitHub Pull Requests for every project phase.
   - Grade against standardized criteria defined in `projects/` directory.
   - Guarantee turn-around within 24–48 hours.
3. **Community & Program Managers**:
   - Monitor student engagement, handle extensions, track progress, and host soft-skill & client presentation workshops.

---

## 3. Student Workflow & Submission Pipeline

For an **AI Forward Deployed Engineer** program, submissions must simulate real-world software engineering and client delivery using the **Seeded Codebase** model:

```
[Student Workspace]
       |
       v
1. Clone Seeded Enterprise Repo & Develop Locally (Docker Compose / Pytest)
       |
       v
2. Push Branch to GitHub Repository
       |
       v
3. Create Pull Request & Fill PR Template (Architecture diagram, test results, Loom video link)
       |
       v
4. For Project 5 only: after the open PR has a green CI run and local acceptance evidence, deploy the protected AWS endpoint for the 14-day assessment window; record verifier, cost, and teardown evidence
       |
       v
5. Submit PR Link to TripleTen LMS / Platform
       |
       +---> [Automated CI Check] (GitHub Actions: Linting, Pytest, Security scan)
       |
       v
6. Code Reviewer Assigned -> Line-by-Line Code Review
       |
       +---> APPROVED? ---------> Project Phase Completed 🎉
       |
       +---> REVISIONS NEEDED? -> Student fixes code -> Resubmits -> Re-review (up to 3 iterations)
```

### Required Submission Artifacts for AI FDE Projects
Every project submission must contain:
1. **Codebase**: Modular Python packages (not single 1,000-line notebooks), Docker Compose configurations for local-first testing, `.env.example`.
2. **Automated Tests**: Pytest coverage for core utilities, tool parsing, API endpoints, and evaluation metrics (CI smoke tests).
3. **System Documentation (`README.md`)**: System architecture overview, setup instructions, cost & performance telemetry basics.
4. **Client-Facing Video Walkthrough (Loom)**:
   - Students present their solution as if pitching or delivering to an enterprise client stakeholder (demonstrates communication, technical scoping, and live system demonstration).
   - Projects 1-4 use a 5-minute local demonstration. They do not expose public endpoints; Project 1 explicitly forbids one.
   - *For Project 5*, the 15-minute capstone defense must demonstrate the temporary protected AWS endpoint, cost telemetry, and teardown plan; reviewer access is supplied separately and the endpoint is not an unauthenticated public demo.

---

## 4. Grading & Evaluation Rubric Framework

Code reviews use a dual-tier rubric format strictly evaluating the `[CORE]` required implementations, treating infrastructure like K8s or Terraform as `[POSITIONING]` (decision-level knowledge).

### 1. Requirements (Must-Have for Pass)
* **Functionality**: Meets all functional user stories in the project brief (e.g., local LLM serving with vLLM, hybrid RAG with pgvector/FastEmbed, LangGraph tool execution).
* **Code Architecture**: Modular separation of concerns within the seeded monolith.
* **Error Handling & Security**: No hardcoded API keys, graceful handling of API rate limits/timeouts (circuit breakers), OWASP LLM mitigation.
* **Testing & Dockerization**: `docker compose up` builds cleanly locally; test suite passes without errors.
* **Scenario Resilience**: Required behavior passes published local scenario packs; held-out packs are evaluated by the course grader.
* **P5 Deployment, Cost, and Teardown**: For Project 5 only, the course verifier confirms the protected endpoint, required security controls, cost tags, 14-day assessment window, scheduled GPU controls, and complete teardown. An unapproved cost overrun or incomplete teardown remains incomplete until the instructor remediates it; it does not create a student payment obligation.

### 2. Recommendations (Nice-to-Have / Senior Level)
* **Optimization**: Latency reduction techniques (streaming responses, prompt compression, async execution).
* **Observability**: Structured JSON logging, tracing with Arize Phoenix, cost/latency telemetry.
* **Documentation & Polish**: Exceptionally clear architecture diagrams (Mermaid.js) and professional client video walkthroughs.
