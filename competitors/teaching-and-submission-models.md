# Analysis: Bootcamp Teaching Methodology & Student Submission Workflow

## Executive Summary
This document analyzes teaching methodologies, student operational workflows, code submission pipelines, and instructor support models across modern technical bootcamps. It highlights how TripleTen's signature model operates and adapts it for the 22-Week **AI Forward Deployed Engineer (AI FDE)** program.

---

## 1. Teaching Methodology Comparison

| Component | Asynchronous + Platform Model (TripleTen Style) | Live Lecture Model (General Assembly) | Cohort / Masterclass Model (Maven / CoRise) |
| :--- | :--- | :--- | :--- |
| **Pacing** | Bi-weekly Sprints (Self-paced within sprint boundaries) | Fixed schedule (e.g. 7pm-10pm Mon/Wed + Sat) | Scheduled weekly live sessions |
| **Learning Content** | Interactive text/code platform, short videos, code tasks | Live Zoom lectures & code-alongs | Recorded videos + live guest workshops |
| **Student Support** | Tutors on Discord/Slack (24/7 SLA), Live Office Hours | Live instructors during class, TAs post-class | Community Q&A, mentor office hours |
| **Evaluation** | Human Code Reviews on GitHub/Platform with strict rubrics | Homework submissions, pass/fail capstones | Project presentations & peer review |
| **Flexibility** | High (ideal for 20h/week working adults) | Low (rigid attendance) | Medium |

---

## 2. TripleTen-Style Operational Model for AI FDE

### A. The 2-Week Sprint Cycle
The 22-week program is divided into **11 Sprints** (2 weeks per sprint = 40 hours total effort per sprint).

```
Week 1 (Days 1–7)                        Week 2 (Days 8–14)
+------------------------------------+   +------------------------------------+
| Sprint Kickoff & Platform Reading  |   | Project Build & Initial Submission |
| - Interactive lessons & micro-tasks|   | - Push code to GitHub              |
| - Practice tasks in web container  |   | - Submit PR for Code Review        |
| - Mid-sprint live workshop/office  |   | - Iterative revision fixes         |
|   hours with Senior Instructors    |   | - Sprint Retrospective & Approval  |
+------------------------------------+   +------------------------------------+
```

### B. Instructor & Support Roles
1. **Tutors / Senior Instructors**:
   - Provide technical support on Discord/Slack.
   - Host live weekly office hours, live Q&A, and technical deep-dives (e.g., "Debugging RAG Latency" or "Setting up vLLM on AWS").
2. **Code Reviewers (Industry Practitioners)**:
   - Provide rigorous, professional line-by-line code reviews on GitHub Pull Requests.
   - Grade against standardized criteria: *Must-Have Requirements* (blocking approval) and *Recommendations/Best Practices* (non-blocking advice).
   - Guarantee turn-around within 24–48 hours.
3. **Community & Program Managers**:
   - Monitor student engagement, handle extensions, track progress, and host soft-skill & client presentation workshops.

---

## 3. Student Workflow & Submission Pipeline

For an **AI Forward Deployed Engineer** program, submissions must simulate real-world software engineering and client delivery:

```
[Student Workspace]
       |
       v
1. Develop Locally (VS Code / Cursor / Docker / Pytest)
       |
       v
2. Push Branch to GitHub Repository
       |
       v
3. Create Pull Request & Fill PR Template (Architecture diagram, test results, Loom video link)
       |
       v
4. Submit PR Link to TripleTen LMS / Platform
       |
       +---> [Automated CI Check] (GitHub Actions: Linting, Pytest, Security scan)
       |
       v
5. Code Reviewer Assigned -> Line-by-Line Code Review
       |
       +---> APPROVED? ---------> Sprint Completed 🎉
       |
       +---> REVISIONS NEEDED? -> Student fixes code -> Resubmits -> Re-review (up to 3 iterations)
```

### Required Submission Artifacts for AI FDE Projects
Every sprint project submission must contain:
1. **Codebase**: Modular Python packages (not single 1,000-line notebooks), `requirements.txt` / `pyproject.toml`, `Dockerfile`, `.env.example`.
2. **Automated Tests**: Pytest coverage for core utilities, tool parsing, API endpoints, and evaluation metrics.
3. **System Documentation (`README.md`)**: System architecture overview, setup instructions, API specs (OpenAPI/Swagger), cost & performance benchmarks.
4. **Client-Facing Video Walkthrough (Loom, 3–5 min)**:
   - Students present their solution as if pitching or delivering to an enterprise client stakeholder (demonstrates communication, technical scoping, and live system demonstration).

---

## 4. Grading & Evaluation Rubric Framework

Code reviews use a dual-tier rubric format:

### 1. Requirements (Must-Have for Pass)
* **Functionality**: Meets all functional user stories (e.g., RAG pipeline returns accurate chunks, agent handles tool errors gracefully).
* **Code Architecture**: Modular separation of concerns (API routes separated from business logic, prompts, and database connection logic).
* **Error Handling & Security**: No hardcoded API keys, graceful handling of API rate limits/timeouts, PII sanitization.
* **Testing & Dockerization**: `docker compose up` builds cleanly; test suite passes without errors.

### 2. Recommendations (Nice-to-Have / Senior Level)
* **Optimization**: Latency reduction techniques (streaming responses, prompt compression, async execution).
* **Observability**: Structured JSON logging, OpenTelemetry integration, tracing with LangSmith/Phoenix.
* **Documentation & Polish**: Exceptionally clear architecture diagrams (Mermaid.js) and professional client video walkthroughs.
