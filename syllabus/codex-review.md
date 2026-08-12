# Codex Review: AI FDE Program Syllabus

## Current Assessment

The reorganized syllabus is substantially improved. The 452-hour total and most current project defaults are now aligned, but several consistency and launch-readiness issues remain.

## Findings

- **High: Project 5 cloud deployment remains mandatory in assessment.** The Project 5 skill marks cloud deployment as optional/positioning ([`project-5.md`](project-5.md)), but its required artifacts still demand a live cloud endpoint and its defense must demonstrate the application in the cloud ([`project-5.md`](project-5.md)). The main README also requires successful cloud deployment for graduation ([`README.md`](README.md)). This remains inconsistent with the local-first core policy in [`AGENTS.md`](../AGENTS.md).

- **High: Root guidance references a removed legacy file.** The repository no longer contains `syllabus/based-on-competitors-2w-sprints.md`, but [`AGENTS.md`](../AGENTS.md) still references it in the syllabus history and repository sitemap. This creates a stale path for anyone following the documented version history.

- **Medium: The companion review report contains broken links after reorganization.** [`claude-review.md`](claude-review.md) still links to the removed `5-projects-22-weeks/` directory and to the removed legacy sprint file. Its findings are also historical snapshots and do not reflect the current optional-cloud wording or pinned tool changes.

- **Medium: The actual grading rubrics are still missing.** The project briefs document submission artifacts and assessment structure, but still defer the Must-Have rubrics to the `projects/` directory ([`project-1.md`](project-1.md), [`project-5.md`](project-5.md)). [`projects/README.md`](../projects/README.md) remains a placeholder rather than an actual grading package.

- **Medium: Project 2 fallback wording is contradictory.** Its Skills and Theory sections describe `sentence-transformers` as a fallback ([`project-2.md`](project-2.md)), but Delivery Limits say alternatives are only permitted as ungraded optional extensions ([`project-2.md`](project-2.md)). A hardware-constrained fallback cannot simultaneously be outside graded scope without an explicit grading rule.

- **Low: Competitor claims remain uncited.** The precise "95% of current enterprise job openings" claim was softened to "the majority," but the competitor documents still provide no sources or methodology for market claims ([`program-comparison.md`](../competitors/program-comparison.md)). The documents are consistent as positioning material, but not evidence-backed competitive research.

## Resolved Since Previous Round

- The program-level workload now consistently reports approximately 452 hours.
- Project 5 cloud deployment is marked optional in its Skills section.
- Default tools are now pinned for the main grading paths: `pgvector`/`FastEmbed`, vLLM, Guardrails AI, Arize Phoenix, and Unsloth.
- The syllabus files are now organized directly under `syllabus/`, with [`README.md`](README.md) as the entry point.
- Legacy sprint content was removed from the active file inventory.
- Project 5 continuity from Project 4 and the project-specific assessment sections are documented.

## Review Scope

This review was performed against the clean `main` checkout at commit `c79ea82`. No files were modified during the review; this report replaces the prior `codex-review.md` assessment.
