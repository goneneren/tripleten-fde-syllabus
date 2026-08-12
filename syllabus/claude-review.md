# Claude Review: AI FDE Syllabus (v2) & Cross-Document Consistency

_Round 3 — reviewed against commit `c79ea82` ("fix: resolve round 2 review findings: hours, local-first, default tools, claims"), which addressed round-2 findings from this file._

## ✅ Confirmed resolved this round

| Round 2 finding | Status |
|---|---|
| ~440h total was stale after P5's workload bump | Fixed — AGENTS.md, [syllabus/README.md](README.md), and both competitor docs now consistently say **~452h** (matches actual sum: 67+86.5+96+82.75+120=452.25) |
| Uneven "pin a default tool" fixes (P2/P3/P4/P5) | Fixed — every project's Skills/Tech Setup/Theory Topics/Delivery Limits now consistently name a default + fallback (FastEmbed, vLLM, Guardrails AI, Unsloth) within its own file |
| Uncited "95% of enterprise job openings" stat | Softened to "the majority of" in [program-comparison.md](../competitors/program-comparison.md) |

## 🔴 Still open: P5's "make cloud optional" fix is incomplete and now self-contradictory

[project-5.md](project-5.md)'s Skill bullet now reads: *"[Positioning] Deploy... to a basic cloud instance... as an **optional** capstone delivery requirement"* — "optional requirement" is a contradiction in terms on its own. Worse, nothing downstream was updated to match "optional":
- Same file's **Submission & Assessment Criteria** still requires *"a live endpoint URL pointing to the cloud-deployed instance"* and a defense *"demonstrating the working application in the cloud."*
- [syllabus/README.md](README.md)'s **Graduation Criteria** (bullet 5, untouched) still says students must *"successfully deploy the Project 5 Capstone architecture to the cloud and defend the LLM telemetry metrics."*

So the doc now disagrees with itself: one line calls cloud deployment optional/positioning, three other places still gate submission/graduation on it. This is the same underlying tension from round 2, just relocated rather than resolved.

## 🔴 Still open: AGENTS.md's dead reference to the deleted legacy syllabus

Flagged after the reorg, still unfixed. [AGENTS.md](../AGENTS.md) still says (in "Syllabus Evolution & Versions") and repeats in its repo-structure diagram: `syllabus/based-on-competitors-2w-sprints.md` — that file was deleted in the reorg commit. Both references are dead links.

## 🟡 New: default-tool fix didn't propagate to README prose

[syllabus/README.md](README.md)'s Project 3 summary still reads *"deploy local LLM inference engines (`vLLM` or `Ollama`)"* — presenting them as equal alternatives again. This contradicts both the roadmap table directly above it in the same file (correctly shows "vLLM" only) and [project-3.md](project-3.md)'s own pinned default. The fix landed in the project brief but not in the README that summarizes it.

## 🟢 Low-priority nits (cosmetic, not urgent)

- README's roadmap table hours/week column is slightly off: Project 2 shows "21h/wk" (86.5h ÷ 4wk ≈ 21.6), Project 4 shows "20h/wk" (82.75h ÷ 4wk ≈ 20.7).
- [projects/README.md](../projects/README.md) is still just a placeholder — every project's "Pass/Fail Rubric" line still defers to a rubric file that doesn't exist yet. Not a regression, just still unwritten.

---

**Bottom line:** the two structural fixes (hours total, tool defaults) landed cleanly. The cloud-deployment question is the one that keeps almost getting fixed — pick one answer (mandatory-with-fallback, or fully optional/positioning) and make it consistent across project-5.md's Skills/Submission Criteria *and* the README's Graduation Criteria in the same pass. The AGENTS.md dead link is a one-line delete that's been carried over twice now.
