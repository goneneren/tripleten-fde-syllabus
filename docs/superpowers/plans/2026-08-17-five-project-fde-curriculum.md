# Five-Project AI FDE Curriculum Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Create open-source and LocalStack five-project curriculum editions that combine the current Projects 5 and 6 as phases 5.A and 5.B, require Instructor Presentation / Review after Projects 1–4 and at the Phase 5.A gate, and culminate in a required Final Demo Day after instructor-supported Phase 5.B preparation.

**Architecture:** Copy the two normative six-project curriculum documents into a new version folder, then make structure-only curriculum edits in the copies. Preserve Projects 1–4 and all technical delivery boundaries while consolidating the capstone, placing the Project 5 instructor review at the Phase 5.A deployment gate, making Phase 5.B preparation formative, and converting the optional demo-day reference into a required Final Demo Day before teardown. Update the repository governance documents to adopt the five-project edition while preserving the six-project sources unchanged.

**Tech Stack:** Markdown, PowerShell, ripgrep, Git diff validation.

**Spec:** `docs/superpowers/specs/2026-08-17-five-project-fde-curriculum-design.md`

## Global Constraints

- Preserve the original `syllabus-fde-focused/` folder unchanged.
- Create the new edition only under `syllabus-fde-focused-5-projects/`.
- Preserve exactly 22 weeks, 440 hours, five physical repositories, and 31 tasks.
- Preserve Project hours as 60, 80, 80, 80, and 140; Phase 5.A is 80 hours and Phase 5.B is 60 hours.
- Preserve the $20 approved LLM API cap, $180 AWS cap, local-first boundary, protected AWS endpoint, no-GPU rule, and no hands-on fine-tuning rule.
- Use the exact labels `Instructor Presentation / Review` and `Final Demo Day`.
- Use `Final Demo Day` as the sole name for the capstone event.
- Five Instructor Presentation / Review recordings are required: Projects 1–4 and Phase 5.A. Final Demo Day is the separate Project 5 culmination after Phase 5.B.
- Final Demo Day is required, uses a 20-minute demonstration plus up to 10 minutes of questions, occurs by day 12 of the endpoint window, and precedes teardown by day 14.
- Phase 5.B may include formative instructor assistance but no additional graded defense or instructor review.
- Do not copy historical evaluation/verdict files or the superseded project tree into the new version folder.
- Preserve explicitly supplied `*-review.md` files as non-normative working artifacts.

---

### Task 1: Create the parallel edition from the normative sources

**Files:**
- Create: `syllabus-fde-focused-5-projects/fde-focused-5-projects-opensource.md`
- Create: `syllabus-fde-focused-5-projects/fde-focused-5-projects-localstack.md`
- Read: `syllabus-fde-focused/fde-focused-6-projects-opensource.md`
- Read: `syllabus-fde-focused/fde-focused-6-projects-localstack.md`

**Interfaces:**
- Consumes: the two normative focused six-project curriculum documents.
- Produces: two independent five-project copies with unchanged source content before structural edits.

- [ ] **Step 1: Record source hashes before copying**

Run:

```powershell
Get-FileHash syllabus-fde-focused\fde-focused-6-projects-opensource.md, syllabus-fde-focused\fde-focused-6-projects-localstack.md -Algorithm SHA256
```

Expected: two SHA-256 hashes to compare again after implementation.

- [ ] **Step 2: Create the new folder and direct copies**

Run:

```powershell
New-Item -ItemType Directory -Path syllabus-fde-focused-5-projects
Copy-Item -LiteralPath syllabus-fde-focused\fde-focused-6-projects-opensource.md -Destination syllabus-fde-focused-5-projects\fde-focused-5-projects-opensource.md
Copy-Item -LiteralPath syllabus-fde-focused\fde-focused-6-projects-localstack.md -Destination syllabus-fde-focused-5-projects\fde-focused-5-projects-localstack.md
```

Expected: the new directory contains two byte-identical curriculum copies under their five-project filenames.

- [ ] **Step 3: Verify copy parity before editing**

Run:

```powershell
git diff --no-index -- syllabus-fde-focused\fde-focused-6-projects-opensource.md syllabus-fde-focused-5-projects\fde-focused-5-projects-opensource.md
git diff --no-index -- syllabus-fde-focused\fde-focused-6-projects-localstack.md syllabus-fde-focused-5-projects\fde-focused-5-projects-localstack.md
```

Expected: both commands produce no diff.

- [ ] **Step 4: Confirm the new folder contains only normative editions**

Run:

```powershell
rg --files syllabus-fde-focused-5-projects
```

Expected: exactly two normative curriculum files matching `fde-focused-5-projects-*.md`. Explicitly supplied `*-review.md` working artifacts may coexist; no copied historical evaluation, verdict, or tree artifact is introduced.

### Task 2: Convert program-level structure to five projects

**Files:**
- Modify: `syllabus-fde-focused-5-projects/fde-focused-5-projects-opensource.md`
- Modify: `syllabus-fde-focused-5-projects/fde-focused-5-projects-localstack.md`

**Interfaces:**
- Consumes: the copied six-project summaries, program contracts, and repository checkpoint tables.
- Produces: five-project program metadata shared by both editions.

- [ ] **Step 1: Update titles, status language, and executive summaries**

Change `Six-Project` to `Five-Project` in each title and describe Projects 1–4 as local engagements followed by Project 5 phases 5.A and 5.B. Keep the open-source edition as program of record and LocalStack as an unadopted alternative.

- [ ] **Step 2: Replace the project summary table**

Use five rows with these exact allocations:

```text
Project 1: Weeks 1–3, 60 hours
Project 2: Weeks 4–7, 80 hours
Project 3: Weeks 8–11, 80 hours
Project 4: Weeks 12–15, 80 hours
Project 5: Weeks 16–22, 140 hours
Total: 22 weeks, 440 hours, five sequential field-delivery engagements
```

Describe Project 5 as building and locally accepting the bounded workflow in 5.A, then deploying, handing back, demonstrating, and tearing down the same accepted release in 5.B.

- [ ] **Step 3: Update the program delivery contract**

Replace six-project language with five-project language. State that Repository 5 spans both phases, Phase 5.A produces the accepted release tag, and Phase 5.B deploys that exact tag. Replace the six-project rubric dependency with five project rubrics plus explicit Phase 5.A gate and Phase 5.B verifier requirements.

- [ ] **Step 4: Define the recurring assessment contract**

Add that Projects 1–4 end with a required `Instructor Presentation / Review` and Project 5 receives its review at the end of Phase 5.A as the deployment gate. State that presentation evidence, instructor feedback, acceptance status, and bounded evidence resubmission are recorded inside existing hours.

- [ ] **Step 5: Define required Final Demo Day**

State that `Final Demo Day` is required for program completion, is held at the end of Phase 5.B while the endpoint is available, and is followed by teardown. Remove every statement that demo-day participation is optional or ungraded enrichment.

- [ ] **Step 6: Collapse the repository checkpoint table**

Keep five rows. Row 5 must name Repository 5, its TripleTen reference checkpoint through Project 4, the Phase 5.A accepted release gate, and reuse of the same repository/release in Phase 5.B.

- [ ] **Step 7: Run program-level stale-language checks**

Run:

```powershell
$curriculumFiles = @('syllabus-fde-focused-5-projects\fde-focused-5-projects-opensource.md','syllabus-fde-focused-5-projects\fde-focused-5-projects-localstack.md')
rg -n "Six-Project|six sequential|six project rubrics|\| 6 \| Repository 5|Projects 1–5 run locally|Project 6" $curriculumFiles
```

Expected: no stale six-project structural statements. Any historical comparison explicitly labeled as history must be reviewed manually rather than accepted automatically.

### Task 3: Add Instructor Presentation / Review to Projects 1–4

**Files:**
- Modify: `syllabus-fde-focused-5-projects/fde-focused-5-projects-opensource.md`
- Modify: `syllabus-fde-focused-5-projects/fde-focused-5-projects-localstack.md`

**Interfaces:**
- Consumes: existing closing Tasks 1.5, 2.5, 3.5, and 4.5 and their evidence artifacts.
- Produces: four explicit project-closeout instructor reviews per edition without changing project hours.

- [ ] **Step 1: Extend Task 1.5**

Add `Instructor Presentation / Review` to the diagnostic handoff using the repair, evidence packet, ADR, workflow trace, unresolved risks, and next recommendation. Require recorded instructor feedback and either evidence acceptance or bounded evidence resubmission within the existing 10 hours.

- [ ] **Step 2: Extend Task 2.5**

Frame the existing recorded SoW defense as Project 2's `Instructor Presentation / Review`. Require review of outcomes, exclusions, assumptions, estimate, acceptance criteria, and scope-change decision within the existing 10 hours.

- [ ] **Step 3: Extend Task 3.5**

Add `Instructor Presentation / Review` to the incident and operational handoff using SLO evidence, failure response, stakeholder communication, runbook, and remaining risks within the existing 12 hours.

- [ ] **Step 4: Extend Task 4.5**

Frame the executive risk decision as Project 4's `Instructor Presentation / Review`. Require review of value, threat evidence, controls, residual risks, evidence boundaries, and go/conditional-go/no-go recommendation within the existing 8 hours.

- [ ] **Step 5: Verify all four closeouts in both editions**

Run:

```powershell
$curriculumFiles = @('syllabus-fde-focused-5-projects\fde-focused-5-projects-opensource.md','syllabus-fde-focused-5-projects\fde-focused-5-projects-localstack.md')
rg -n -A 12 "^### Task (1\.5|2\.5|3\.5|4\.5)" $curriculumFiles
```

Expected: every matched closing task explicitly contains `Instructor Presentation / Review`; project hours remain 60/80/80/80.

### Task 4: Merge current Projects 5 and 6 into capstone phases

**Files:**
- Modify: `syllabus-fde-focused-5-projects/fde-focused-5-projects-opensource.md`
- Modify: `syllabus-fde-focused-5-projects/fde-focused-5-projects-localstack.md`

**Interfaces:**
- Consumes: current Project 5 content, current Project 6 content, and Repository 5 release-gate relationship.
- Produces: one 140-hour Project 5 with phases 5.A and 5.B and 11 preserved tasks.

- [ ] **Step 1: Create the Project 5 parent section**

Use one top-level heading for Project 5 and state its schedule as Weeks 16–22 / 140 hours. Summarize the continuous capstone journey from ambiguous workflow discovery through local acceptance, protected AWS deployment, adoption, handback, Final Demo Day, and teardown.

- [ ] **Step 2: Convert current Project 5 to Phase 5.A**

Add the phase heading `Phase 5.A — Bounded Agent Workflow Under Ambiguity`, preserve its 80 hours, and rename Tasks 5.1–5.5 to Tasks 5.A.1–5.A.5. Update references so Task 5.A.5 produces the required accepted release gate for Phase 5.B.

- [ ] **Step 3: Convert current Project 6 to Phase 5.B**

Add the phase heading `Phase 5.B — AWS Deployment, Adoption and Handback`, preserve its 60 hours, and rename Tasks 6.1–6.6 to Tasks 5.B.1–5.B.6. Replace references to `Project 6` with `Phase 5.B` or `the capstone deployment phase` while preserving all cloud controls, budgets, SLAs, access, acceptance, and teardown requirements.

- [ ] **Step 4: Update intra-capstone references**

Replace “Project 5 release”/“Project 6 deployment” relationships with “Phase 5.A accepted release”/“Phase 5.B deployment.” Preserve Repository 5 throughout and state that business logic does not change during the adapter/configuration transition.

- [ ] **Step 5: Verify phase and task numbering**

Run:

```powershell
$curriculumFiles = @('syllabus-fde-focused-5-projects\fde-focused-5-projects-opensource.md','syllabus-fde-focused-5-projects\fde-focused-5-projects-localstack.md')
rg -n "^## Project|^### Phase 5\.[AB]|^#### Task 5\.[AB]\." $curriculumFiles
```

Expected per edition: five top-level projects, two level-3 Project 5 phases, five level-4 5.A task headings, and six level-4 5.B task headings. Projects 1–4 retain level-3 task headings in both editions.

### Task 5: Add the Phase 5.A review, Phase 5.B instructor support, and required Final Demo Day

**Files:**
- Modify: `syllabus-fde-focused-5-projects/fde-focused-5-projects-opensource.md`
- Modify: `syllabus-fde-focused-5-projects/fde-focused-5-projects-localstack.md`

**Interfaces:**
- Consumes: Phase 5.A technical gate, Phase 5.B acceptance evidence, protected endpoint, existing defense and teardown tasks.
- Produces: the fifth Instructor Presentation / Review at the Phase 5.A gate, formative instructor-supported Final Demo Day preparation in Phase 5.B, and the required capstone Final Demo Day.

- [ ] **Step 1: Make Task 5.A.5 the Instructor Presentation / Review and enforceable technical gate**

Retitle Task 5.A.5 `Instructor Presentation / Review and technical acceptance gate (16 hours)`. Remove the dual-room executive closeout language; focus the recording on workflow boundaries, evaluation gaps, deployment readiness, and a short readiness memo. Require the instructor's recorded decision against the Phase 5.A gate, an immutable tag, commit SHA, and image digest before Phase 5.B can provision AWS.

- [ ] **Step 2: Convert Task 5.B.5 to formative Final Demo Day preparation**

Retitle it `Final Demo Day preparation and instructor support (6 hours)`. Remove the separate technical and executive defenses. Use the task to assemble accepted evidence, prepare the run sheet, rehearse the protected-endpoint demonstration, and receive optional formative instructor feedback without transferring artifact ownership.

- [ ] **Step 3: Convert Task 5.B.6 to Final Demo Day and closeout**

Retitle it `Final Demo Day, teardown, portfolio and reusable field playbook (8 hours)`. Require a 20-minute end-to-end demonstration plus up to 10 minutes of questions covering workflow, value, architecture, authority and safety boundaries, evaluation, AWS operation, cost, limitations, and next recommendation. Schedule it after approved remediation and by day 12, record event evidence, then verify teardown by day 14.

- [ ] **Step 4: Remove optional-demo language**

Replace `demo-day participation is optional and ungraded` with an explicit statement that Final Demo Day is required for program completion and is the culmination of Project 5 rather than a sixth project.

- [ ] **Step 5: Verify required event terminology**

Run:

```powershell
$curriculumFiles = @('syllabus-fde-focused-5-projects\fde-focused-5-projects-opensource.md','syllabus-fde-focused-5-projects\fde-focused-5-projects-localstack.md')
rg -n -i "Instructor Presentation / Review|Final Demo Day|demo-day participation is optional" $curriculumFiles
```

Expected per edition: five Instructor Presentation / Review recordings at Projects 1–4 and Phase 5.A, formative instructor support in Task 5.B.5, a required Final Demo Day requirement and task, and no optional-demo statement.

### Task 6: Reconcile workload, recordings, and edition parity

**Files:**
- Modify: `syllabus-fde-focused-5-projects/fde-focused-5-projects-opensource.md`
- Modify: `syllabus-fde-focused-5-projects/fde-focused-5-projects-localstack.md`

**Interfaces:**
- Consumes: completed five-project structure in both editions.
- Produces: aligned workload and assessment contracts with no hidden extra hours.

- [ ] **Step 1: Replace workload verification tables**

Use:

```text
Project 1: 3 weeks x 20 = 60 hours
Project 2: 4 weeks x 20 = 80 hours
Project 3: 4 weeks x 20 = 80 hours
Project 4: 4 weeks x 20 = 80 hours
Project 5: 7 weeks x 20 = 140 hours
  Phase 5.A: 4 weeks x 20 = 80 hours
  Phase 5.B: 3 weeks x 20 = 60 hours
Program: 22 weeks x 20 = 440 hours
```

- [ ] **Step 2: Reconcile assessment counts**

Replace the existing recording sentence with a contract naming exactly five Instructor Presentation / Review recordings: Projects 1–4 and Phase 5.A. State that the Project 2 and Project 4 defenses are their reviews, not extra recordings; Task 5.B.5 is formative preparation; Final Demo Day is a separate required program event.

- [ ] **Step 3: Compare structural headings between editions**

Run:

```powershell
rg "^(#|##|###|####) " syllabus-fde-focused-5-projects\fde-focused-5-projects-opensource.md
rg "^(#|##|###|####) " syllabus-fde-focused-5-projects\fde-focused-5-projects-localstack.md
```

Expected: identical project, phase, task, workload, and assessment heading structure; only stack-specific content differs.

- [ ] **Step 4: Compare task-hour totals**

Run this read-only check once per new edition by assigning its path to `$curriculumPath`:

```powershell
$curriculumPath = 'syllabus-fde-focused-5-projects\fde-focused-5-projects-opensource.md'
$taskRows = [regex]::Matches((Get-Content -Raw $curriculumPath), '(?m)^#{3,4} Task (?<task>[1-5](?:\.[1-5]|\.[AB]\.[1-6])) .* \((?<hours>\d+) hours\)\r?$') | ForEach-Object { [pscustomobject]@{ Task = $_.Groups['task'].Value; Hours = [int]$_.Groups['hours'].Value } }
$taskRows.Count
($taskRows | Measure-Object Hours -Sum).Sum
$taskRows | Group-Object { if ($_.Task -match '^5\.A\.') { '5.A' } elseif ($_.Task -match '^5\.B\.') { '5.B' } else { $_.Task.Split('.')[0] } } | ForEach-Object { [pscustomobject]@{ Section = $_.Name; Hours = ($_.Group | Measure-Object Hours -Sum).Sum } }
```

Repeat with `$curriculumPath = 'syllabus-fde-focused-5-projects\fde-focused-5-projects-localstack.md'`. Expected per edition: task count 31; total 440; section totals Project 1 = 60, Project 2 = 80, Project 3 = 80, Project 4 = 80, Phase 5.A = 80, and Phase 5.B = 60.

### Task 7: Adopt the five-project edition in repository governance

**Files:**
- Modify: `AGENTS.md`
- Modify: `executive-overview.md`
- Preserve unchanged: `syllabus-fde-focused/`

**Interfaces:**
- Consumes: the approved five-project delivery and assessment contract.
- Produces: one unambiguous program-of-record declaration and contributor rules that match the five-project edition.

- [ ] **Step 1: Update AGENTS.md**

Replace active six-project counts, allocations, boundaries, paths, and Project 6 references with five projects, `60/80/80/80/140`, and the Phase 5.A/5.B boundary. Point the program of record and LocalStack alternative to `syllabus-fde-focused-5-projects/`. Mark `syllabus-fde-focused/` as a preserved superseded source whose embedded status labels are overridden by `AGENTS.md`.

- [ ] **Step 2: Update executive-overview.md**

Replace six-engagement descriptions with five engagements, combine the former P5/P6 rows, link the five-project program of record, and describe the Phase 5.A instructor gate, Phase 5.B formative support, Final Demo Day, and teardown boundary.

- [ ] **Step 3: Verify governance alignment**

Run:

```powershell
rg -n "six sequential engagements|Projects 1-5|Project 6|fde-focused-6-projects-opensource" AGENTS.md executive-overview.md
```

Expected: no active six-project delivery rule or stale program-of-record link. Explicitly labeled historical references are allowed only in `AGENTS.md`'s superseded-source entry.

### Task 8: Run final acceptance verification

**Files:**
- Verify: `syllabus-fde-focused-5-projects/fde-focused-5-projects-opensource.md`
- Verify: `syllabus-fde-focused-5-projects/fde-focused-5-projects-localstack.md`
- Verify unchanged: `syllabus-fde-focused/fde-focused-6-projects-opensource.md`
- Verify unchanged: `syllabus-fde-focused/fde-focused-6-projects-localstack.md`

**Interfaces:**
- Consumes: completed five-project editions and Task 1 source hashes.
- Produces: evidence that the new edition meets the design without changing the six-project source.

- [ ] **Step 1: Verify counts and required language**

Run read-only checks for each edition and confirm:

```text
Top-level projects = 5
Phase headings under Project 5 = 2
Task headings = 31
Instructor Presentation / Review recordings = 5 (Projects 1–4 and Phase 5.A)
Final Demo Day = required
Program hours = 440
```

- [ ] **Step 2: Scan for prohibited and stale language**

Run:

```powershell
$curriculumFiles = @('syllabus-fde-focused-5-projects\fde-focused-5-projects-opensource.md','syllabus-fde-focused-5-projects\fde-focused-5-projects-localstack.md')
rg -n -i "six-project|six sequential|^## Project 6|^### Task 6\.|optional and ungraded|six project rubrics" $curriculumFiles
```

Expected: no matches.

- [ ] **Step 3: Verify original source hashes**

Run:

```powershell
Get-FileHash syllabus-fde-focused\fde-focused-6-projects-opensource.md, syllabus-fde-focused\fde-focused-6-projects-localstack.md -Algorithm SHA256
```

Expected: hashes exactly match those recorded in Task 1 Step 1.

- [ ] **Step 4: Run Markdown and whitespace checks**

Run:

```powershell
git diff --check
rg -n "T[B]D|TO[D]O|FIX[M]E" syllabus-fde-focused-5-projects\fde-focused-5-projects-opensource.md syllabus-fde-focused-5-projects\fde-focused-5-projects-localstack.md
```

Expected: `git diff --check` succeeds and the marker scan has no matches.

- [ ] **Step 5: Review final Git scope**

Run:

```powershell
git status --short
git diff --stat
```

Expected: the approved design/plan artifacts, `AGENTS.md`, `executive-overview.md`, and the two normative files under `syllabus-fde-focused-5-projects/` are changed. User-supplied review artifacts may remain untracked in the new folder; the original focused folder is unchanged.
