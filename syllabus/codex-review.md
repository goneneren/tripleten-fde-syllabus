# Codex Review: AI FDE Program Syllabus

## Overall Assessment

The syllabus has a strong, credible project sequence, but it is not yet launch-ready as an operational curriculum. The design is ahead of the delivery specification.

## Major Findings

- **High: Pass/fail assessment is missing from the current syllabus.** The repository requires explicit Must-Have criteria, Recommendations, rubrics, and Loom demonstrations in [`AGENTS.md`](../AGENTS.md), but the five project briefs only say that a rubric must be supplied later, for example [`project-1.md`](5-projects-22-weeks/project-1.md), [`project-3.md`](5-projects-22-weeks/project-3.md), and [`project-5.md`](5-projects-22-weeks/project-5.md). There are no project-specific acceptance tests, required submission artifacts, reviewer criteria, or defense requirements in the current model.

- **High: The local-first, no-paid-cloud-or-GPU-dependency claim conflicts with Projects 4 and 5.** The policy is stated in [`AGENTS.md`](../AGENTS.md), but Project 4 permits paid LLM APIs ([`project-4.md`](5-projects-22-weeks/project-4.md)), and Project 5 explicitly permits paid APIs and cloud notebooks when local VRAM is insufficient ([`project-5.md`](5-projects-22-weeks/project-5.md)). This needs one authoritative learner path.

- **High: The current and legacy syllabus versions are not clearly separated operationally.** The root documentation identifies the 5-project model as current ([`AGENTS.md`](../AGENTS.md)), but the older 11-sprint document still presents itself as the complete AI FDE syllabus ([`based-on-competitors-2w-sprints.md`](based-on-competitors-2w-sprints.md)), and the teaching document still describes 11 two-week sprints as the operating model ([`teaching-and-submission-models.md`](../competitors/teaching-and-submission-models.md)). Readers could reasonably use either document as authoritative.

- **High: The dual-track strategy is described, but not deliverable from this repository.** The executive document promises shared repositories with divergent tasks and grading ([`executive-overview.md`](../executive-overview.md)), while the expected `projects/` directory described in [`AGENTS.md`](../AGENTS.md) does not exist in this checkout. The task matrices and grading differences are therefore strategic claims rather than executable curriculum specifications.

- **Medium: The taxonomy is inconsistent.** [`AGENTS.md`](../AGENTS.md) defines `[AI]`, while the module map uses `[FDE-SPECIFIC]` instead ([`overview-and-module-map.md`](5-projects-22-weeks/overview-and-module-map.md)). The individual project briefs do not consistently use either taxonomy. This makes it difficult to distinguish required work from positioning, supporting material, and optional depth.

- **Medium: Workload totals are correct but phase pacing is uneven.** The five projects total `437.75` hours, which is close to the stated `440`. However, the documented project windows allocate approximately 22.3, 21.6, 24, 20.7, and 15.1 hours per week respectively. Project 5 contains advanced RAG, multi-agent execution, sandboxing, evaluation, fine-tuning, observability, and defense ([`project-5.md`](5-projects-22-weeks/project-5.md)), yet has the lowest weekly allocation.

- **Medium: Cloud deployment and client-delivery competencies are underrepresented.** The role benchmark includes cloud deployment, infrastructure as code, requirements scoping, technical specifications, and client delivery ([`fde-role-benchmark.md`](../competitors/fde-role-benchmark.md)). The current syllabus makes AWS optional or positioning-only ([`project-2.md`](5-projects-22-weeks/project-2.md), [`project-3.md`](5-projects-22-weeks/project-3.md)), and only Project 5 clearly requires a defense ([`project-5.md`](5-projects-22-weeks/project-5.md)). The job-ready FDE claim is stronger than the currently documented evidence of cloud and client-delivery practice.

- **Medium: Tool choices are too variable for reproducible delivery and grading.** The briefs offer alternatives such as FastEmbed or sentence-transformers, Ollama or vLLM, Redpanda or Kafka, Guardrails AI or NeMo, OpenBao or Vault, and paid APIs or local models. Examples appear in [`project-2.md`](5-projects-22-weeks/project-2.md), [`project-3.md`](5-projects-22-weeks/project-3.md), [`project-4.md`](5-projects-22-weeks/project-4.md), and [`project-5.md`](5-projects-22-weeks/project-5.md). Alternatives are reasonable pedagogically, but the default implementation path and equivalence rules need to be explicit.

## What Is Working

- The progression from diagnostics to data, resilience, security, and autonomous systems is coherent.
- The projects use realistic enterprise constraints instead of isolated chatbot exercises.
- Scope controls are good: exactly two defects in Project 1, one failure lab in Project 3, one protected endpoint in Project 4, and one bounded multi-agent flow in Project 5.
- The competitor documents consistently support the intended positioning: enterprise integration, production engineering, evaluation, and client-facing delivery.
- The total workload arithmetic is sound.

## Other Document Review

The executive overview and current module map are broadly consistent about the shared five-project SE/FDE strategy. The competitor and teaching documents are directionally consistent, but they function more like positioning memos than evidence-backed research: many competitor claims have no URLs, dates, or source methodology. The "95% of current enterprise job openings" claim in [`program-comparison.md`](../competitors/program-comparison.md) is especially too precise to leave uncited.

## Review Scope

This review was performed against the clean `main` checkout at commit `18bb7bf`. No existing syllabus or supporting documents were modified during the assessment; this report was saved separately as `codex-review.md`.
