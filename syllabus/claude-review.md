# Claude Review: AI FDE Syllabus (v2) & Cross-Document Consistency

_Round 2 — reviewed against commit `3831e26` ("fix: resolve claude and codex review findings for syllabus launch-readiness"), which addressed round-1 findings from this file and from `codex-review.md`._

## ✅ Confirmed resolved from Round 1

| Round 1 finding | Status |
|---|---|
| Qdrant/MinIO claimed but never used | Removed from [AGENTS.md](../AGENTS.md)'s stack list — now matches what the project briefs actually build |
| gRPC Core/Positioning ambiguity (P2) | Fixed — Tech Setup now explicitly says "read-only scaffold... Positioning-level for FDEs" |
| P5 missing platform continuity | Fixed — Tech Setup now says "Secured version of the platform extending Project 4" |
| `[FDE-SPECIFIC]` vs `[AI]` taxonomy drift | Fixed — module map now uses `[AI]` throughout, matches AGENTS.md |
| v1 legacy syllabus mistaken for current | Fixed — deprecation banners added to both [based-on-competitors-2w-sprints.md](based-on-competitors-2w-sprints.md) and [teaching-and-submission-models.md](../competitors/teaching-and-submission-models.md) |
| Hardware/setup gap in v2 docs | Fixed — new "Hardware & System Prerequisites" section in AGENTS.md |
| P5's hours/week under-allocation (Round 1's top finding) | **Well fixed** — P5 moved from 7wk/105.5h (−25% vs. budget) to 6wk/120h, now *exactly* on budget. P3 also improved from +20% over to −4% (gained a week). |

## 🔴 New issue introduced by the fix itself: total hours claim now stale

P5's workload bump (105.5h → 120h, +14.5h) wasn't propagated to the program-level total. AGENTS.md still says *"22 Weeks (~440 Hours Total)"* / *"~438-440 hours."* Actual sum is now:

67 + 86.5 + 96 + 82.75 + 120 = **452.25h** (~2.8% over the stated ceiling)

Easy fix, but currently wrong.

## 🔴 New issue: the P5 cloud-deployment fix breaks the program's own "local-first" promise

To address a "cloud deployment underrepresented" finding, [project-5.md](5-projects-22-weeks/project-5.md) added this as a **Skill**:
> "Deploy the Docker Compose stack to a basic cloud instance (e.g., AWS EC2) as a **final capstone delivery requirement**."

That's an unconditional mandatory-cloud requirement — not a fallback like P2's optional AWS RDS checkpoint. It directly contradicts:
- AGENTS.md's own Guidelines section (unchanged): *"Maintain Local-First Compatibility: **Every core required project task must run locally**... without requiring paid cloud infrastructure."*
- The marketed differentiator repeated in [executive-overview.md](../executive-overview.md) and [program-comparison.md](../competitors/program-comparison.md): *"no mandatory cloud subscriptions."*
- It's also not reflected anywhere in the [overview-and-module-map.md](5-projects-22-weeks/overview-and-module-map.md) chapter list for Project 5.

This over-corrects: it trades one finding for a contradiction with a bigger, more load-bearing program claim. Making EC2 deployment optional/positioning (mirroring how P2 handles AWS RDS) would satisfy "cloud is represented" without breaking the local-first guarantee.

## 🟡 Uneven follow-through: "pin a default tool" fix applied inconsistently

- **P2**: pins pgvector/FastEmbed in Delivery Limits — but the Skills bullet above it still reads "FastEmbed **or** sentence-transformers," text not synced.
- **P3**: pins vLLM in Delivery Limits — but Skills and Tech Setup still list "vLLM / Ollama" as an undifferentiated pair.
- **P4**: doesn't actually name a tool — just says one "must be explicitly chosen" later. Weaker than P2/P3, defers rather than resolves.
- **P5**: untouched — still offers OpenAI/Anthropic-or-local, vLLM/Ollama, *and* Unsloth/HuggingFace as open alternatives, in the one project where reproducible grading matters most.

## 🟡 Partial fix: rubric gap is more honestly labeled, not closed

All 5 projects now have a "Submission & Assessment Criteria" section (good — concrete PR artifacts, Loom format, defense length). But every one of them ends with *"Pass/Fail Rubric: must be explicitly supplied in the `projects/` directory"* — i.e., the actual Must-Have grading criteria still don't exist; they're just now explicitly flagged as pending instead of silently absent. The new [projects/README.md](../projects/README.md) is a placeholder describing what will go there, not the rubric itself.

## 🟢 Untouched, still open (low urgency)

- [program-comparison.md](../competitors/program-comparison.md)'s uncited "95% of current enterprise job openings" stat.

---

**Bottom line:** the pacing fix (P5 hours) was the best outcome of this round — it's now exact. The two things to fix next: sync the ~440h total in AGENTS.md to the new 452.25h actual, and roll back P5's mandatory-EC2 requirement to optional/positioning so it stops contradicting the program's own local-first claim.
