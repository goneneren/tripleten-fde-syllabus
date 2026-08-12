# Claude Review: AI FDE Syllabus (v2) & Cross-Document Consistency

_Round 4 — reviewed [PR #1](https://github.com/goneneren/tripleten-fde-syllabus/pull/1) ("feat: implement P5 cloud capstone pivot"), which resolves the round-3 cloud-deployment self-contradiction by making P5's cloud deploy unambiguously mandatory (rather than optional)._

## ✅ Confirmed resolved by PR #1

| Round 3 finding | Status |
|---|---|
| P5's "make cloud optional" fix was self-contradictory (Skills said optional, Submission Criteria + README Graduation Criteria said mandatory) | Fixed by picking a direction: cloud deploy is now unambiguously **mandatory**. AGENTS.md's Program Principle, `syllabus/README.md`'s principles/summary, and `project-5.md`'s Skills bullet all now agree with each other and with the Submission Criteria/Graduation Criteria that already assumed mandatory. |

## 🔴 New: AGENTS.md now contradicts itself directly

PR #1 rewrote the Program Principle (renamed "Local-First Development, Cloud-Native Capstone") to make P5's AWS EC2 GPU instance mandatory, but left the **Guidelines for AI Assistants & Contributors** section untouched:
> *"Maintain Local-First Compatibility: Every core required project task must run locally using Docker Compose without requiring paid cloud infrastructure or GPU dependencies."*

Before this PR the tension was soft (P5 said "optional"). Now it's a hard contradiction in the same file — one section mandates paid cloud GPU infra for a core project, the next says no core task can require that. Same class of miss as the dead legacy-syllabus reference below: a principle gets amended but the guideline derived from it doesn't.

## 🟡 New: the $200 budget now has two conflicting jobs

- **AGENTS.md / README Hardware Prerequisites** (unchanged by the PR): the $200 is framed as a general fallback "if local VRAM is insufficient" — implicitly available whenever a student's machine can't run local inference (e.g., Project 3's vLLM serving).
- **New Program Principle + `project-5.md` Delivery Limits** (added by the PR): the $200 is *"primarily allocated to provision a live cloud instance... to host this capstone project for the duration of the 6-week build."*

If Project 5 primarily claims the pool, a student who needed the fallback earlier (P1-P4) may have nothing left. The PR doesn't reconcile which claim on the same $200 wins.

## 🟡 New: budget math is tight to the point of unrealistic

A `g4dn.xlarge` (T4 GPU) instance run continuously for the stated "6-week build" costs roughly $0.526/hr × ~1,008 hrs ≈ **$530** on-demand — well past the $200 allocated. The number only works if students stop/start the instance around their ~20h/week active hours (~$65-90 + storage), but nothing in the docs instructs that, and "host this capstone project for the duration of the 6-week build" reads as always-on. Worth an explicit start/stop instruction or a smaller instance size before this ships to real students.

## 🔴 Still open: AGENTS.md's dead reference to the deleted legacy syllabus

Flagged after the reorg (round 3), still unfixed and untouched by this PR. [AGENTS.md](../AGENTS.md) still says (in "Syllabus Evolution & Versions") and repeats in its repo-structure diagram: `syllabus/based-on-competitors-2w-sprints.md` — that file was deleted in the reorg commit. Both references are dead links.

## 🟡 Still open: default-tool fix never propagated to README prose

[syllabus/README.md](README.md)'s Project 3 summary still reads *"deploy local LLM inference engines (`vLLM` or `Ollama`)"* — presenting them as equal alternatives again. This contradicts both the roadmap table directly above it in the same file (correctly shows "vLLM" only) and [project-3.md](project-3.md)'s own pinned default. Untouched by PR #1 since it only targeted the P5 cloud pivot.

## 🟢 Low-priority nits (cosmetic, not urgent)

- `overview-and-module-map.md`'s Project 5 chapter list still has no entry for cloud deployment/AWS EC2 — out of sync now that it's mandatory, but this gap predates PR #1 and wasn't in its scope.
- README's roadmap table hours/week column is slightly off: Project 2 shows "21h/wk" (86.5h ÷ 4wk ≈ 21.6), Project 4 shows "20h/wk" (82.75h ÷ 4wk ≈ 20.7).
- [projects/README.md](../projects/README.md) is still just a placeholder — every project's "Pass/Fail Rubric" line still defers to a rubric file that doesn't exist yet.
- [codex-review.md](codex-review.md) in this same directory is now stale — it was written against pre-PR1 `c79ea82` and still describes P5 cloud deploy as "optional," so its top finding no longer applies post-merge.

---

**Bottom line:** PR #1 correctly resolves the round-3 self-contradiction by committing to "mandatory," and that choice is now consistent everywhere it needs to be *within the syllabus docs*. What it missed is the ripple effect one level up: AGENTS.md's own Guidelines section still bans what the Program Principle right above it now requires, and the $200 budget is described as serving two different, possibly incompatible purposes. Both are one- or two-line fixes, not a redesign.
