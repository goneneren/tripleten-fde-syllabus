Executive Verdict

READY AFTER REQUIRED FIXES

The mechanical redesign is sound and verifies cleanly: 5 top-level projects, 2 phases, 31 tasks, 440 hours summing to 60/80/80/80/(80+60) in both editions, headings structurally identical across editions, and syllabus-fde-focused/ byte-unchanged against HEAD. Projects 1–4 were not rewritten — the diff is exactly one added line each.

But the redesign is not yet educationally honest about assessment load or operationally executable in Weeks 20–22. Three classes of defect survive:

The consolidation deleted the graded-recording contract instead of replacing it, so the program's assessment count is now undefined while five new required events were added.
Task 5.A.5 was renamed but not rewritten — it still reads as a dual-audience project closeout, so Project 5 still reads as two projects at its seam.
Renumbering made a previously-true LocalStack delivery rule factually false.

Plus a governance blocker outside the two documents: AGENTS.md and executive-overview.md still mandate six projects and name the six-project file as program of record, while the new file also declares itself program of record.

Blocking and Required Findings
P0-1 — Two documents both claim "program of record"; governing rules file mandates six projects
File and line: fde-focused-5-projects-opensource.md:3 vs AGENTS.md:7,17,18,20,25,69-70,86-94,100 and executive-overview.md:11,13,17,30,43,50
Current wording: New OS doc: > **Status: program of record.** — AGENTS.md:69–70: "TripleTen Six-Project, 22-Week Open-Source Version (Program of Record): Documented in syllabus-fde-focused/fde-focused-6-projects-opensource.md". AGENTS.md:100: "Projects 1-5 must run and pass locally… Project 6 must pass locally before its required, temporary protected AWS deployment." AGENTS.md:25: "$20 API allowance is split between Project 5 evaluation and Project 6 endpoint/defense traffic."
Why defective: Two live program-of-record declarations. Worse, AGENTS.md is the contributor/AI rules file — it would actively instruct future work to restore six projects and to keep Projects 1–5 local (which under the new numbering forbids Phase 5.B's AWS deployment). executive-overview.md:30 points external stakeholders at the six-project file. The user constraint protects syllabus-fde-focused/, not these two files.
Minimal correction: At adoption, update AGENTS.md lines 7, 17, 18, 20, 25, 69–74, 86–94, 100–101 and executive-overview.md lines 11, 13, 17, 30, 43, 50 to the five-project structure, and demote the six-project file to "superseded source edition."
P0-2 — LocalStack edition forbids the AWS CLI that Phase 5.B requires
File and line: fde-focused-5-projects-localstack.md:41, contradicted by :437 and :443
Current wording: ":41 — Projects 2–5 use only awslocal; plain AWS CLI is not used… a CI gate rejects SDK clients constructed outside that factory." Meanwhile ":437 — [Tools] …AWS CLI, ECR, EC2, S3, SQS/DLQ, SSM Parameter Store…" and ":443 — Demonstrate and handle at least one real-AWS policy-denial, throttling, consistency, or network-reachability failure."
Why defective: In the six-project edition "Projects 2–5" correctly excluded Project 6. Under the new numbering, Project 5 contains Phase 5.B, so the rule now bans the exact tooling Task 5.B.2 mandates — and the named CI gate would reject the Phase 5.B adapters. This is precisely the semantic breakage a search-and-replace pass cannot catch: the string never changed, its truth value did.
Minimal correction: ":41 — Projects 2–4 and Phase 5.A use only awslocal; plain AWS CLI is not used in the local stages. Phase 5.B uses the real AWS CLI and supplied AWS adapters, and the local-endpoint CI gate does not apply to the Phase 5.B configuration."
P1-3 — The graded-recording contract was deleted, not replaced
File and line: OS:56-57 / LS:66-67, replacing six-project OS:57 / LS:67
Current wording: Removed sentence: "Five graded recordings are required: the Project 2 SoW defense, Project 4 executive risk decision, Project 5 technical defense, and Project 6 technical and executive defenses. Each is a single take of at most 10 minutes; production polish is not assessed. Other defenses are written." Nothing replaced it — the two new bullets describe IPR and Final Demo Day only.
Why defective: The approved plan (Task 6, Step 2) explicitly required replacement with a contract distinguishing the five IPR closeouts, the 5.A gate, 5.B evidence, and Final Demo Day, and warned against "double-counting one recording when it satisfies both a defense and its project review." Instead the whole contract vanished. The program still requires recordings at OS:199, 326, 396, 461–463 — now five recorded defenses plus five IPRs plus Final Demo Day, with no cap on length, no rule on recorded vs written, and no statement of the total. This is the single largest honesty gap: the announced "five projects" is satisfied while assessment volume silently grew and became uncountable.
Minimal correction: Restore a bullet after OS:57 / LS:67: "Six graded recordings are required: the Project 2 SoW defense (which is Project 2's Instructor Presentation / Review), the Project 4 executive risk decision (which is Project 4's Instructor Presentation / Review), the Phase 5.A technical acceptance-gate defense, the Phase 5.B technical and executive defenses (which together constitute Project 5's Instructor Presentation / Review), and Final Demo Day. Each is a single take of at most 10 minutes; production polish is not assessed. The Project 1 and Project 3 Instructor Presentations / Reviews and all other defenses are written."
P1-4 — Task 5.B.5's Instructor Presentation / Review duplicates the two defenses inside the same 6-hour task
File and line: OS:461-465 / LS:471-475
Current wording: ":461 — Record a technical defense covering architecture, controls, evaluations, operations, cost, and residual risks. :462 — Record an executive defense covering value, adoption status, limitations, and next investment. … :465 — [Instructor Presentation / Review] Present the architecture, controls, evaluations, operations, cost, value, adoption status, limitations, residual risks, and next investment recommendation."
Why defective: The IPR content list is the exact set-union of the two bullets three lines above it. Within 6 hours a student now produces four overlapping presentations (technical defense, executive defense, scenario-inject response, IPR) of the same evidence. This is not a differentiated review — it is the same deliverable counted twice, which the plan explicitly prohibited.
Minimal correction: Replace :465 with: "[Instructor Presentation / Review] The recorded technical and executive defenses together constitute Project 5's Instructor Presentation / Review. The instructor applies the published Project 5 Must-Haves and Recommendations to that evidence and records feedback and the final project acceptance decision. No additional presentation is produced."
P1-5 — Projects 2 and 4 gained a second closeout event instead of reframing the existing one
File and line: OS:199-200 and OS:326-328 / LS:209-210, 336-338
Current wording: ":199 — Record the graded SoW defense… :200 — [Instructor Presentation / Review] Present the outcomes, exclusions, assumptions, estimate, acceptance criteria, and scope-change decision." Same pattern at :326/:328 for the executive risk defense.
Why defective: Plan Task 3, Steps 2 and 4 said to frame the existing recorded defense as the IPR. The implementation appended a distinct bullet, so both tasks now read as two separate events covering identical content inside unchanged 10-hour and 8-hour budgets. Task 4.5 at 8 hours already carries an executive brief, a recorded defense, a pressure inject, and a decision record.
Minimal correction: ":200 — [Instructor Presentation / Review] The recorded SoW defense is Project 2's Instructor Presentation / Review; the instructor applies the published Must-Haves and Recommendations to it and records feedback and an accepted or remediation-required decision." Mirror at :328 for the executive risk defense.
P1-6 — Final Demo Day was added to Task 5.B.6 with no hours added and nothing removed
File and line: OS:467-478 / LS:477-488, against six-project OS:456-465
Current wording: The task remains "(8 hours)" and retains all five original bullets (teardown verification, final cost/acceptance/risk evidence, sensitive-data separation, sanitized repo + reference architecture + playbook + product-feedback record, portfolio index) while gaining ":472 — Complete the required Final Demo Day… Demonstrate the end-to-end workflow, business value, architecture, authority and safety boundaries, evaluation evidence, AWS operations, cost, limitations, and next recommendation" and ":473 — Record the demonstration evidence…".
Why defective: The spec authorises IPR to fit "within its existing final-task hours" because it reuses existing artifacts. Final Demo Day is a new required deliverable with its own evidence template (:471), its own API traffic allocation (:61), and a nine-topic end-to-end demonstration against a live endpoint. Absorbing it into an unchanged 8-hour task that must also complete verified teardown of eight resource classes is not credible. This is the one place the approved 140-hour envelope is materially oversubscribed.
Minimal correction: Rebalance inside Phase 5.B's fixed 60 hours — reduce Task 5.B.5 to 4 hours (justified once P1-4 removes the duplicate presentation) and raise Task 5.B.6 to 10 hours. Hours per phase and per project are unchanged.
P1-7 — A "remediation-required" outcome was introduced at four project closeouts with no time, schedule, or deadline
File and line: OS:56, 136, 200, 265, 328 / LS:66, 146, 210, 275, 338
Current wording: ":56 — The instructor records feedback, the acceptance decision, and any allowed remediation inside the project's existing hours." Each closeout: "records feedback and an accepted or remediation-required decision."
Why defective: The six-project edition used "remediation" only in the AWS context, where it is explicitly bounded by budget, endpoint window, and a one-deployment limit (OS:407, 408, 444). The redesign introduces a new failure state at every project boundary while asserting it consumes no additional hours — yet the schedule is a fully-allocated 20 h/week with no slack week, and Projects 2–5 begin from a TripleTen reference reset that discards the student's code anyway. As written, "remediation-required" has no defined consequence.
Minimal correction: Add to the OS:56 / LS:66 bullet: "A remediation-required decision requires the student to resubmit the affected evidence artifacts within the published resubmission window; it does not reopen implementation work, because the next project begins from TripleTen's reference checkpoint. Remediation at the Phase 5.A gate must complete before the Week 20 AWS provisioning deadline."
P1-8 — The Phase 5.A → 5.B release gate names no acceptance authority and no artifact-identity check
File and line: OS:398, 420, 425 / LS:408, 430, 435
Current wording: ":398 — Produce the accepted release tag required before Phase 5.B can provision AWS resources. :420 — Pass the local gate before provisioning cloud resources. :425 — Deploy the tagged, locally accepted release through the fixed course-managed AWS profile."
Why defective: "Accepted" is used passively throughout — no actor issues the acceptance, and nothing binds the artifact deployed in 5.B.2 to the tag produced in 5.A.5. Phase 5.B's output is checked by a named "Course verifier" with a published schema (:439); Phase 5.A's gate has a schema promised in production-readiness dependencies (:23) but no verifier and no authority in the task itself. Since "it is the same accepted release" is the load-bearing claim of the entire consolidation, an unenforceable gate means Project 5 is two projects joined by an assertion.
Minimal correction: Amend :398 to "Obtain the instructor's recorded Phase 5.A acceptance decision against the published acceptance-gate schema and produce the signed, immutable release tag. Phase 5.B may not provision AWS resources until that decision is recorded." Amend :425 to "…and confirm through the supplied verifier that the deployed image is built from the accepted Phase 5.A tag."
P1-9 — Weeks 20–22 contain no scheduled slot for Final Demo Day relative to the reviewer window and remediation
File and line: OS:407, 444, 472 / LS:417, 454, 482
Current wording: ":407 — 14 consecutive days of reviewer access beginning at the first verified endpoint, which must occur by the end of Week 20 so review, one remediation, and teardown remain inside the 22-week program. Reviewer turnaround is three business days. :444 — one instructor-approved remediation deployment is permitted before automated teardown. :472 — Complete the required Final Demo Day while the protected endpoint is available."
Why defective: Weeks 20–22 is 21 days. An endpoint first verified at the end of Week 20 consumes all 14 reviewer days through the end of Week 22. The six-project edition packed review + one remediation + teardown into that tail; the new edition inserts a further required event and places it only "while the protected endpoint is available" — the same interval, with no ordering rule. If a reviewer verdict arrives at day 10–13 and the student exercises the one permitted remediation deployment, Final Demo Day and verified teardown collide with the window close. The FDD-before-teardown ordering is correct everywhere; the FDD-within-the-window scheduling is undefined.
Minimal correction: Add to :407 / :417: "Final Demo Day must be held no later than day 12 of the 14-day reviewer window and after any instructor-approved remediation deployment, so that verified teardown completes before the window closes."
P1-10 — Task 5.A.5 still reads as an independent project closeout
File and line: OS:389-396 / LS:399-406
Current wording: Retitled to "Change control and technical acceptance gate," but the body is unchanged from six-project Task 5.5: ":391 — [Summary] Revise the solution under pressure and defend it to technical and business audiences. :392 — [Skills] …technical defense, executive storytelling, adoption-risk communication. :396 — Record the graded technical defense and submit a written executive brief covering value, limitations, adoption risk, and the next investment decision."
Why defective: The approved spec (line 35) requires 5.A.5 to be "a required technical phase-gate defense… not presented as a sixth project closeout." Only the heading and one appended bullet changed. A dual-audience defense with an executive brief on value/adoption/next-investment is a project closeout — and its content list nearly matches 5.B.5's recorded executive defense ("value, adoption status, limitations, and next investment," :462). This is the strongest remaining signal that Project 5 is two projects wearing one heading, and it is exactly the failure mode the review was asked to hunt.
Minimal correction: ":391 — [Summary] Revise the solution under pressure and pass the technical acceptance gate that authorises the deployment phase. :392 — [Skills] Change control, impact analysis, technical defense, evaluation-gap disclosure, deployment-readiness reasoning. :396 — Record the graded technical defense and submit a short written readiness memo covering evaluation gaps, deferred work, and deployment risks. The engagement's executive value case is presented once, in Phase 5.B."
Non-Blocking Findings
P2
#	File:line	Finding
P2-1	OS:61 / LS:71	The unchanged $15 Phase 5.B allocation must now additionally fund "Final Demo Day traffic." The $20/$180 caps are respected, but the sub-allocation absorbed a new live end-to-end demonstration with no revalidation note. Recommend adding Final Demo Day to the pre-launch cost validation named at :408.
P2-2	OS:398, 444, 464, 465	Four distinct meanings of "acceptance" inside one project: the 5.A local gate acceptance, the 5.B.3 accept/conditional-accept/reject verdict, the 5.B.5 simulated client acceptance, and the 5.B.5 "final project acceptance decision." Recommend distinct terms (gate acceptance / verifier verdict / simulated client acceptance / project grade).
P2-3	OS:23, 56	"five project rubrics with binary Must-Haves" plus a separate 5.A gate schema and 5.B verifier schema. But :56 says the IPR uses "its published Must-Haves," and 5.A's gate has none named. Recommend stating that the Project 5 rubric publishes separate Phase 5.A and Phase 5.B Must-Have sets.
P2-4	syllabus-fde-focused-5-projects/gemini-review.md	A third-party evaluation artifact sits in the normative edition folder, violating spec version-boundary lines 11–14 and plan Task 1 Step 4 ("exactly the two new curriculum Markdown files; no evaluation, verdict, or tree artifact"). Move it to syllabus-fde-focused/ alongside the other verdict files.
P2-5	OS:136 vs OS:117-126	Project 1's IPR ("Present the diagnosis, repair evidence, ADR, unresolved risks, and next recommendation") substantially restates Task 1.4's "recommendation playback." Lower-stakes than P1-5 because 1.4 is not a graded recording, but worth differentiating.
P3
#	File:line	Finding
P3-1	OS:336, 344, 404 / LS:346, 354, 414	Project 5 and Phase 5.A both use **Schedule:**; Phase 5.B uses **Phase schedule:**. Two identically-labelled Schedule fields in nested scopes. Use **Phase schedule:** for 5.A.
P3-2	OS:56	"Every project ends with a required Instructor Presentation / Review" — but Project 5's IPR is Task 5.B.5, followed by 5.B.6 (Final Demo Day + teardown). Reword to "Every project includes a required Instructor Presentation / Review at its closeout."
P3-3	OS:338	Project 5's evidence list flattens local artifacts (audit trail, evaluation report) and real-cloud artifacts (protected endpoint, verifier report) with no evidence-boundary note of the kind Project 4 carries at :276.
Requirement-by-Requirement Audit
#	Approved constraint	Result	Evidence	Location
1	Exactly five projects, 22 weeks, 440 hours	PASS	grep -c "^## Project " = 5 in both; task-hour regex sums to 440 in both	OS:45, 491; LS:55, 501
2	Allocations 60/80/80/80/140	PASS	Summed per section: 60/80/80/80/(80+60)	OS:484-491; LS:494-501
3	5.A = 80 h, 5.B = 60 h	PASS	Task sums 5.A=80, 5.B=60; workload rows explicit	OS:344, 404, 489-490; LS:354, 414, 499-500
4	Five physical starter repositories	PASS	Checkpoint table collapsed to 5 rows; row 5 spans both phases	OS:67-73; LS:77-83
5	Projects 1–4 and Phase 5.A local-only	PASS	"Projects 1–4 and Phase 5.A are locally runnable and graded; no public endpoint or cloud deployment is allowed."	OS:9, 51; LS:9, 61
6	Phase 5.B retains bounded AWS contract	PASS	Fixed profile, prohibited resources, cloud boundary, budget, access/cleanup all carried verbatim	OS:405-409; LS:415-419
7	Required Instructor Presentation / Review after every project	PASS (with P1-4, P1-5)	Contract bullet plus IPR at Tasks 1.5, 2.5, 3.5, 4.5, 5.B.5	OS:56, 136, 200, 265, 328, 465
8	5.A defense is a capstone gate, not a sixth project review	FAIL	5.A.5 still says "defend it to technical and business audiences," lists "executive storytelling," and requires an executive brief on value/adoption risk/next investment	OS:391-396; LS:401-406 → P1-10
9	Final Demo Day required, endpoint available, precedes teardown	PASS	Correct order at every occurrence: contract, Project 5 summary, Phase 5.B intro, task title, task bullets	OS:57, 334, 402, 410, 467, 472-474; LS:67, 344, 412, 420, 477, 482-484
10	Six-project sources unchanged	PASS	git diff --stat HEAD -- syllabus-fde-focused/ returns empty; git status --short shows only docs/ and syllabus-fde-focused-5-projects/ as untracked	repo state
11	No GPU, no hands-on fine-tuning	PASS	"The program provisions no AWS GPU. Fine-tuning implementation is out of scope"; carried in 5.A.3 and 3.1	OS:62, 377; LS:72, 387
12	$20 LLM API and $180 AWS unchanged	PASS (with P2-1)	"$20 for approved LLM APIs and $180 for AWS"; "$180 maximum for AWS… target at most $80"	OS:9, 61, 408; LS:9, 71, 418
13	Added presentations fit within existing hours	FAIL	Task 5.B.6 keeps 8 hours and all five original closeout bullets while gaining a nine-topic Final Demo Day and its evidence recording	OS:467-478; LS:477-488 → P1-6
14	No stale Project 6 / six-project / optional-Demo-Day / six-rubric language	PASS	Scan for six-project|six sequential|six project rubrics|Project 6|Task 6\.|optional and ungraded|sixth project matches nothing in either curriculum file (only in the stray gemini-review.md)	both files
15	No wording conflicts with AGENTS.md	FAIL	AGENTS.md mandates six projects and names the six-project file as program of record while the new file also claims it	AGENTS.md:17-20, 69-70, 100 → P0-1
16	No overstatement of local/emulated evidence	PASS	Fidelity citations, "state what local evidence does not prove," migration-delta "one failure mode that local evidence could not prove," Project 4 evidence boundary all preserved	OS:60, 167, 232, 276, 307, 431; LS:43, 70, 177, 242, 286, 317, 441
17	Assessment counts / grading language agree across sections	FAIL	The graded-recording contract was deleted without replacement	OS:56-57; LS:66-67 → P1-3
18	Task numbering and repository lineage agree	PASS	31 tasks, 5.A.1–5.A.5 and 5.B.1–5.B.6, Repository 5 across both phases, no stale "this project" inside Project 5	OS:348-467; LS:358-477
Cross-Edition Consistency

Structural parity is the strongest part of this redesign. diff of all #–#### headings between the two new editions returns exactly three expected differences: the H1 title, ### Open-source delivery stack vs ### LocalStack delivery stack, and the LocalStack-only ### LocalStack adoption and fidelity boundary.

Dimension	Result
Project structure	Identical — 5 top-level projects, same titles, same week/hour rows (OS:38-45 ≡ LS:48-55)
Phase structure	Identical — ### Phase 5.A / ### Phase 5.B with matching intros and evidence lists (OS:340-346, 400-410 ≡ LS:350-356, 410-420)
Task numbering and hours	Identical — 31 tasks, same numbers, same titles, same hour values; both sum to 440 with the same per-section split
Instructor reviews	Identical — same five IPR bullets, same wording (OS:136, 200, 265, 328, 465 ≡ LS:146, 210, 275, 338, 475)
Final Demo Day	Identical — same contract bullet, same task title, same bullets, same evidence ordering
Repository model	Identical five-row checkpoint table with the same row-5 phrasing (OS:67-73 ≡ LS:77-83)
Cloud transition	Identical Phase 5.B profile, prohibited resources, cloud boundary, budget, and access/cleanup text
Legitimate differences	MinIO→LocalStack S3, RabbitMQ→LocalStack SQS/DLQ, Compose secrets→LocalStack SSM, awslocal tooling, the conditional-adoption/fidelity boundary section, and Phase 5.A's "carried-forward LocalStack S3/SQS/SSM adapters" (LS:355). All pre-existing and correctly preserved.
Illegitimate drift	One: LS:41 (P0-2). The LocalStack edition alone acquired an internal contradiction, because it alone contains a rule keyed to the old project numbering.

No structural drift. The only cross-edition problem is a content contradiction unique to LocalStack.

Content-Preservation Audit

Projects 1–4 preserved except for the approved review additions — YES. The unified diff against both six-project sources shows exactly four content additions across Projects 1–4: one [Instructor Presentation / Review] bullet appended to Tasks 1.5, 2.5, 3.5, and 4.5. Every other line in Projects 1–4 is byte-identical in both editions, including all task titles, hour values, Summary/Skills/Tools lines, evidence lists, floors, and the Project 4 evidence boundary. No unintended rewrite.

Former Project 5 content retained under 5.A — YES, with one caveat. All five tasks, all hours (12/10/24/18/16 = 80), all Summary/Skills/Tools lines, and all body bullets carried across verbatim. Additions: the phase heading, "and accepted release tag" in Phase evidence (OS:346), the release-tag bullet (OS:398), and the task-title change at 5.A.5. Caveat: the retention is too complete — 5.A.5's dual-audience body should have been narrowed to a gate (P1-10).

Former Project 6 content retained under 5.B — YES. All six tasks, all hours (8/18/12/8/6/8 = 60), the full fixed cloud profile, prohibited-resource list, cloud boundary, budget, and access/cleanup bullets carried verbatim. Task 6.1's title lost "kickoff" (appropriate — it is no longer a project start). Tasks 6.5 and 6.6 gained IPR and Final Demo Day content.

Requirements lost or materially changed:

Item	Status
Graded-recording contract, incl. "single take of at most 10 minutes" and "Other defenses are written"	LOST — deleted with no replacement (P1-3). This is the only outright content loss in the redesign.
Repository checkpoint row 6 ("Student's accepted Project 5 capstone release tag")	CHANGED, ACCEPTABLE — folded into row 5. The substantive property (5.B starts from the student's own accepted tag, not a reference reset) survives at OS:73 and OS:52.
Project-6-level "Project summary" heading	CHANGED, ACCEPTABLE — replaced by the Phase 5.B intro paragraph; no content dropped.
"demo-day participation is optional and ungraded"	CHANGED, INTENDED — correctly inverted per the approved constraint.
Task 5.B.6 scope	MATERIALLY CHANGED — Final Demo Day added without an hour increase (P1-6).
Adoption Recommendation

The five-project edition can replace the six-project edition as the program of record, but not in its current state. The architecture is right — one continuous capstone in one repository with a local gate feeding a bounded cloud phase is a more honest description of the engagement than two artificially separated projects, and the numeric envelope holds exactly. What is missing is that four of the seams were renamed rather than rewritten, and the assessment contract was deleted rather than rebuilt.

Required before adoption — ten corrections:

P0-1 — Update AGENTS.md (lines 7, 17, 18, 20, 25, 69–74, 86–94, 100–101) and executive-overview.md (lines 11, 13, 17, 30, 43, 50) to the five-project structure; demote the six-project file to a superseded source edition so only one document claims program-of-record status.
P0-2 — Fix fde-focused-5-projects-localstack.md:41 so the awslocal-only rule and its CI gate scope to Projects 2–4 and Phase 5.A, and explicitly exempt Phase 5.B.
P1-3 — Restore a graded-recording contract at OS:57 / LS:67 stating the total count, which events are recorded versus written, the single-take 10-minute cap, and that a defense doubling as its project review is counted once.
P1-4 — Rewrite the Task 5.B.5 IPR bullet so the recorded technical and executive defenses are Project 5's review, rather than a fourth presentation of the same content.
P1-5 — Rewrite the Task 2.5 and Task 4.5 IPR bullets to frame the existing recorded defenses as those projects' reviews.
P1-6 — Rebalance Phase 5.B's fixed 60 hours (5.B.5 → 4 h, 5.B.6 → 10 h) so Final Demo Day is funded.
P1-7 — Define what "remediation-required" costs and when it is due, including at the Phase 5.A gate against the Week 20 provisioning deadline.
P1-8 — Name the Phase 5.A acceptance authority and require the verifier to confirm the deployed image derives from the accepted tag.
P1-9 — Pin Final Demo Day to a stated day inside the 14-day reviewer window, after any remediation deployment and before verified teardown.
P1-10 — Narrow Task 5.A.5 to a technical gate: drop the business-audience framing, "executive storytelling," and the value/adoption/next-investment executive brief, so the engagement's executive case is made once, in Phase 5.B.

Items 4, 5, and 10 are what convert this from a renumbered six-project program into a genuine five-project one; item 3 is what makes its assessment load honest; items 6 and 9 are what make Weeks 20–22 executable. The P2 and P3 items are worth folding into the same editing pass but should not gate adoption.