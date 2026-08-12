# Codex Review: AI FDE Program Syllabus

## Second-Round Assessment

The first-round fixes are substantial, but not all findings are closed. Two high-severity inconsistencies remain, plus two medium or low readiness gaps.

## Findings

- **High: Program workload now exceeds the stated 440-hour target.** Project 5 was increased to `120` hours ([`project-5.md`](5-projects-22-weeks/project-5.md)), but the project total is now `452.25` hours: P1 `67` + P2 `86.5` + P3 `96` + P4 `82.75` + P5 `120`. This is `12.25` hours over the stated target in [`AGENTS.md`](../AGENTS.md). Weekly pacing also remains uneven: P1 `22.33`, P2 `21.62`, P3 `19.2`, P4 `20.69`, and P5 `17.58` hours per week.

- **High: Project 5 introduces a direct local-first contradiction.** Project 5 now requires deployment to a cloud instance and a live cloud endpoint ([`project-5.md`](5-projects-22-weeks/project-5.md)), while the governing guidance still says every core task must run locally without paid cloud infrastructure ([`AGENTS.md`](../AGENTS.md)). The module map says FDEs operate strictly within Docker Compose ([`overview-and-module-map.md`](5-projects-22-weeks/overview-and-module-map.md)), and the executive overview describes the FDE track as Docker Compose and local-LLM focused ([`executive-overview.md`](../executive-overview.md)). This is a new regression, not merely an unresolved old finding.

- **Medium: Assessment structure improved, but actual rubrics are still absent.** Each project now documents tests, artifacts, and a client defense. However, every project still says its Pass/Fail rubric must be supplied later in `projects/`, while [`projects/README.md`](../projects/README.md) explicitly describes that directory as a placeholder. The repository is more assessment-ready as a blueprint, but not launch-ready as a complete grading package.

- **Medium: Reproducibility is improved but not fully deterministic.** Project 2 now selects `pgvector` and `FastEmbed` as grading defaults ([`project-2.md`](5-projects-22-weeks/project-2.md)), and Project 3 selects vLLM ([`project-3.md`](5-projects-22-weeks/project-3.md)). Project 4 still leaves `Guardrails AI` versus `NeMo Guardrails` to a future scaffold choice ([`project-4.md`](5-projects-22-weeks/project-4.md)), while Project 5 still permits multiple fine-tuning and tracing paths ([`project-5.md`](5-projects-22-weeks/project-5.md)). This is acceptable for planning, but not yet sufficient for reproducible grading.

- **Low: Competitor documents remain weakly sourced.** The unsupported "95% of current enterprise job openings" claim remains in [`program-comparison.md`](../competitors/program-comparison.md), alongside uncited market claims such as "highest-demand" in [`fde-role-benchmark.md`](../competitors/fde-role-benchmark.md). The documents are consistent as positioning material, but not evidence-backed competitive research.

## Resolved Since Round One

- Legacy 11-sprint documents now carry deprecation warnings.
- The `projects/` placeholder and delivery role are documented.
- The `[AI]` taxonomy is now consistent with the root guidance.
- P2 gRPC scope and P2/P3 default tools are clearer.
- Project 5 now explicitly continues from Project 4.
- Project-specific submission and client-defense sections were added.
- Hardware and controlled API-budget guidance was added.

## Review Scope

This second-round review was performed against the clean `main` checkout at commit `3831e26`. No files were modified during the review; this report replaces the prior `codex-review.md` assessment.
