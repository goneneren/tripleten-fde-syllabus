Claude’s review is materially stronger and more implementation-aware than Gemini’s. It finds several genuine production-readiness gaps that the earlier reviews missed. However, some conclusions are overstated or conflict with already-decided program constraints.

## Combined verdict

- Open-source variant: **Approve as the primary candidate, with substantial pre-production work**
- LocalStack variant: **Retain as a conditional alternative**, but simplify it significantly
- Neither version is ready for production authoring yet
- The six-project/440-hour structure remains credible only after removing tools, supplying scaffolds, and explicitly defining the delivery infrastructure

Claude says there are “12 critical findings” but actually lists 14. Of those:

- 10 are valid or substantially valid.
- 3 are partially valid.
- 1 contains an overstated conclusion.

## Critical findings assessment

| Finding | Decision | Analysis |
|---|---|---|
| C1: Missing Must-Haves and rubrics | **Accept as production gate** | The documents are program maps, so 3–5 Must-Haves do not necessarily belong inside every task section. Separate project rubrics are preferable, but they must exist before authoring or piloting. |
| C2: Missing supplied-asset contract | **Accept—launch blocker** | This is explicitly acknowledged in `AGENTS.md`. Scenario packs, stakeholder materials, emulators, fixtures, verifier schemas, and fidelity files need an inventory and contract. |
| C3: Missing hardware floor | **Accept** | Also identified by Gemini. Add assessed/reduced Compose profiles, explicit memory ceilings, pinned images, and a tested ≤3B quantized inference path. Do not promise a hosted fallback without costing it. |
| C4: Undefined AWS deployment profile | **Accept—launch blocker** | P6 cannot be costed or completed in 18 hours without naming exactly what runs in AWS and what remains local or is removed. |
| C5: Canonical AWS controls dropped | **Accept—launch blocker** | The focused documents should inherit the existing constrained role, launch templates, budget actions, DNS, TLS, auto-stop, sweep, and automated teardown controls. |
| C6: GPU/LoRA contradiction | **Accept** | The role artifact verifies fine-tuning appears in zero of 41 postings. Hands-on LoRA should be removed. |
| C7: 14-day remediation ambiguity | **Accept** | Define when the window starts, reviewer SLA, exactly one remediation path, and its budget reserve. |
| C8: Repository continuity undefined | **Accept the problem** | The exact solution requires a product decision: one continuous repository, or five physical repositories with P5/P6 sharing the fifth. |
| C9: LocalStack licensing and +27 hours | **Partially accept** | Licensing remains conditional. However, the old +27-hour estimate came from a broader LocalStack variant and cannot automatically be applied to this narrower version. A fresh displacement audit is needed. |
| C10: LocalStack in P1 performance diagnosis | **Accept** | Remove LocalStack from P1. No performance conclusion should be based on an AWS emulator. Introduce LocalStack in P2. |
| C11: Plain AWS CLI leak risk | **Accept—security blocker** | P1–P5 should use only `awslocal`, sentinel credentials, a central client factory, explicit endpoint injection, and a CI gate preventing direct SDK construction. |
| C12: “Multi-Agent” title mismatch | **Accept** | Rename it to **Bounded Agent Workflow Under Ambiguity**. The project intentionally teaches one auditable state graph, not agent-to-agent coordination. |
| C13: Determinism contradictions | **Accept most of it** | Graded work should use fixed transcripts and published floors. Stakeholder bots should be unassessed practice. The old ASCII tree is stale and should no longer be treated as authoritative. |
| C14: Six projects conflict with repository governance | **Partially accept** | Both documents need candidate-status headers. But six assessment projects do not necessarily require six physical repositories or double the build cost—P5 and P6 already share one repository. The delivery-repository mapping must be decided explicitly. |

## Strong consensus between Gemini and Claude

Both reviewers independently found these issues:

1. The local runtime needs a tested resource profile.
2. The P6 transition needs explicit adapters and a fixed deployment architecture.
3. LoRA/GPU is orphaned and weakly justified.
4. P4’s identity/security scaffold must be preconfigured.
5. P6 needs automated cost and teardown controls.
6. The tooling surface is too broad.
7. The LocalStack variant requires stronger fidelity and licensing boundaries.

These are the highest-confidence changes.

## Tooling cuts I recommend

Both variants should remove or simplify:

- OpenSearch → PostgreSQL full-text search with supplied configuration.
- OpenBao → supplied development secrets scaffold plus Gitleaks.
- PEFT/LoRA → remove hands-on work entirely.
- GPU → remove from required and optional student infrastructure.
- Multiple “A or B” tool paths → one pinned assessed tool; alternatives are unassessed.
- Ragas in CI → deterministic metrics in CI; Ragas only on a fixed manual sample.

LocalStack should additionally remove:

- LocalStack from P1.
- DynamoDB from P2.
- KMS and IAM exercises from P4.
- SNS unless it has assessed learning evidence.
- Lambda, EventBridge, and API Gateway from the program-level list because no task uses them.
- LocalStack CloudWatch from P5 unless a task explicitly assesses it.

The simplified LocalStack surface becomes:

- P2: S3
- P3: SQS and DLQ
- P4: SSM Parameter Store or Secrets Manager
- P5: reuse the same interfaces without adding new AWS services
- P6: real AWS migration and fidelity-delta evidence

That is much more defensible than discarding LocalStack outright.

## Additional Claude findings worth adopting

- Add one legacy-integration experience, but fold it into P3 rather than adding a new 10-hour task:
  - undocumented schema;
  - hidden rate limit;
  - partial permissions;
  - defensive client;
  - discovered-interface document.

- Add a public, sanitized portfolio artifact in P6.

- Add one parallel-client escalation during P3 to exercise context switching.

- Separate deterministic evaluation from Ragas/LLM judging.

- Add an explicit Project 4 evidence boundary: design and integration evidence, not production security certification.

- Allocate the API allowance:
  - `$5` for fixed P5 evaluation;
  - `$15` for P6 endpoint, held-out scenarios, and defense traffic;
  - program-issued metered key;
  - no personal payment method.

- Add a migration-delta artifact in P6:
  - local service;
  - AWS counterpart;
  - configuration difference;
  - missing local IAM/resource policy;
  - one AWS-only failure mode;
  - evidence that it was handled.

## Findings I would not apply as written

### Mandatory Week 0

Claude proposes an additional mandatory 10-hour Week 0. That breaks the declared 440-hour envelope unless it becomes a pre-admission environment check. Better:

- Hardware and toolchain check during admission.
- Pre-pull pinned images before Week 1.
- Task 1.2 includes the assessed runtime orientation.
- No hidden 23rd week.

### Required three years of experience

The market evidence supports a senior audience, but “≥3 years” is a product/admissions policy decision—not a curriculum correction. The practical gate should test production debugging, async Python, Docker, written reasoning, and codebase orientation regardless of calendar years.

### Two mandatory live drills

This conflicts with the already-selected asynchronous, scalable assessment model. A better boundary:

- Grading stays asynchronous and deterministic.
- Live drills are optional or delivered through existing office hours.
- If TripleTen wants them required, instructor capacity must be explicitly funded and scheduled.

### Exact AWS cost figures

Claude’s cost structure is useful, but the instance prices are time-sensitive. Do not copy them without refreshing the AWS calculator and running a real sandbox pilot. The canonical $80 normal target remains the current internal planning reference.

### Five genuine adapter swaps in P6

Five student-authored migrations will not fit 18 hours. Students should implement narrow interfaces and conformance tests earlier, then use supplied AWS adapters in P6 while producing and defending the migration-delta record.

## Recommended implementation order

1. Add candidate-status headers and designate the Markdown versions as normative over the old tree.
2. Decide the physical repository model.
3. Remove LoRA/GPU and rename Project 5.
4. Add hardware/resource profiles and pin one assessed tool per capability.
5. Reduce the open-source and LocalStack service surfaces.
6. Add the portable integration contract and conformance tests.
7. Define the fixed P6 cloud profile and restore canonical AWS controls.
8. Define the 14-day review and remediation path.
9. Add the supplied-asset inventory and scenario-pack contract.
10. Create six separate project rubrics with Must-Haves and Recommendations.
11. Add legacy integration, context switching, portfolio publication, and migration-delta evidence without increasing 440 hours.
12. Recalculate both variants after the cuts.

## Decisions needed before editing

Three choices materially affect the rewrite:

1. Repository model:
   - one continuous student repository across P1–P6; or
   - five physical repositories, with P5 and P6 sharing repository 5.

2. GPU:
   - my recommendation is **remove all student AWS GPU and hands-on fine-tuning requirements**.

3. Live simulations:
   - my recommendation is **keep all grading asynchronous and deterministic; offer live drills only through optional instructor sessions**.

No files were modified during this review.