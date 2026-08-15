Both files are substantially rewritten. I re-verified the arithmetic and diffed them: P1 and P6 are now byte-identical between variants, and divergence is confined to three adapter implementations. Nearly every blocker from the prior review is closed.

## 1. Headline grades

| | Open-source | LocalStack |
|---|:--:|:--:|
| **Overall program grade** | **A−** | **B+** |
| Design quality (ignoring external dependencies) | A− | A− |
| Launch readiness | B− | C+ |

The LocalStack grade is capped by its own line 38 (unresolved Hobby-terms confirmation), not by design quality. Both share one gating constraint: every rubric, floor, and supplied asset named in "Production-readiness dependencies" is still unbuilt.

## 2. Summary evaluation matrix

| Evaluated dimension | OS | LS | Assessment |
|---|:--:|:--:|---|
| **Pacing & workload (440h)** | A− | B+ | Arithmetic exact on all six projects and the total. Hidden hours genuinely removed — preflight at admission, pinned reduced profiles, supplied scaffolds, 5 recordings instead of ~11. Residual risk sits in three tasks, not across the program. |
| **Internal consistency** | A | A | No contradictions between summary tables, delivery contract, task bodies, and workload table. The `fde-focused-6-project-tree.md` file is now stale against both. |
| **Technical relevance (2026)** | A | A | OTel/Tempo, pgvector+FTS hybrid with RRF and cross-encoder rerank, circuit breaker + DLQ, STRIDE/OWASP-LLM, LangGraph, deterministic evals, IMDSv2/least privilege, ports & adapters. Correctly *excludes* fine-tuning and K8s — matches the 0-of-41-postings evidence. |
| **FDE field competencies** | A | A | Four discovery reps, SoW with exclusions, two change-control reps, incident comms, executive decision, adoption, handback, teardown, playbook, context-switch inject, and now undocumented-legacy integration. Only the live drill is missing. |
| **Local-first ergonomics** | A− | B+ | 16 GB floor, 10 GB container budget, ≤3B quantized model, emulator fallback, admission preflight. Genuinely engineered rather than asserted. LS carries one more container plus a third-party account. |
| **AI integration rigor** | A | A | AI is treated as an untrusted component: schema validation, step/token/tool budgets, human checkpoint, audit trail, injection controls, output validation. Judge and Ragas are explicitly kept out of CI with variance reported — this is better than most industry practice. |
| **Assessment determinism** | A− | A− | Fixed transcripts, checkpoint-triggered injects, published floors, chatbot demoted to unassessed. Docked because the floors and rubric anchors do not exist yet, and 6.5's accept/reject decision has no published derivation rule (6.3 does). |
| **Evidence & acceptance design** | B+ | B+ | Floors added in 2.4, 3.3, 5.2 and thresholds in 6.3. P1, P4, 6.4 and 6.5 still have named artifacts but no pass condition. Largest remaining authoring gap. |
| **Repository & continuity** | A | A | The checkpoint model is the strongest single addition: it kills defect propagation, caps integration hours, protects grading integrity, and keeps five physical repos — preserving the dual-track economics. One consequence is unstated (see §5). |
| **Cloud & budget governance** | A | A | Fixed profile, prohibited-resource list, constrained role and templates, budget actions, supplied DNS/TLS/SSM, automated teardown, verifier, $80 target inside a $180 cap with one remediation, endpoint by end of Week 20, 3-day SLA, no GPU. Now tighter than the canonical runbook on window logic. |
| **Claim honesty / governance** | A | A | Explicit evidence boundary, per-row "what this does not prove", fidelity notes in 2.2/3.2/4.3, pressure inject in 4.5. Exemplary discipline. |
| **Tooling economy** | A− | B+ | Removed OpenSearch, OpenBao, DynamoDB, KMS, IAM, SNS, Lambda/EventBridge/API Gateway, GPU, and every either/or fork. LS keeps a container whose payoff shrank: SDK code now lives inside supplied adapters, so students barely write AWS calls. |
| **Cross-variant parity** | A | A | ~27 of 31 tasks identical; P1 and P6 byte-identical; skills lines now differ correctly where tools differ. |
| **Admission gate** | B | B | Added async behavior, unfamiliar-codebase debugging, written communication, preflight. Still no production-history bar despite the market's four-year median and "shipped at scale, verified at intake". |
| **Portfolio & career value** | A− | A− | Five named artifacts, public index, sanitized repo, reference architecture, playbook. Docked for the reference-code point and the ungraded demo day. |
| **Marketing-claim safety** | A | A | "Multi-Agent" gone, fine-tuning out of scope, status header present, no placement or salary language. Safe to hand to marketing with the evidence boundary attached. |
| **Production-authoring readiness** | B− | C+ | Dependencies honestly listed at line 23 — and all of them are unbuilt: scenario-pack contract, asset inventory, six rubrics, FIDELITY set, pinned images, verifier schema, five starter repos with reference solutions. `AGENTS.md` and `executive-overview.md` still describe a 5-project program. |

## 3. Per-project grades

| Project | OS | LS | Verdict |
|---|:--:|:--:|---|
| **P1 — Discovery & Diagnostics** | A− | A− | Now identical across variants (LocalStack correctly deferred to P2). Strong discovery framing. But 1.2 stayed at 10 h while 1.3 was *cut* 18→14, so the project now runs 36 h of writing (1.1+1.4+1.5) against 24 h of hands-on. Defensible for a client-half-focused program; still the tightest technical onramp. |
| **P2 — Data & Hybrid RAG** | A | A− | Excellent scope discipline. Supplied fusion and cross-encoder wrappers de-risk 2.3, and 2.3's "justify candidate depth, fusion parameters, rerank cut-off with measured effects" converts the saved time into better learning. |
| **P3 — Reliable AI Service** | A− | A− | Best *content* in the program — legacy integration, resilience, SLO lab, incident comms, and the context-switch inject. But 3.1 at 18 h now absorbs what was previously proposed as a standalone 10-hour task **on top of** runtime setup and provider abstraction. **Highest overrun risk in the program.** |
| **P4 — Security & Governance** | A | A− | The 30-hour task is now realistic: preconfigured Keycloak realm, supplied redactor, supplied pinned CI workflow. The evidence boundary at line 274/284 is the single best-written paragraph in either document. |
| **P5 — Bounded Agent** | A | A | Evaluation design is the standout: bit-reproducible CI, judge and Ragas manual-only with three-run variance. One real risk — a ≤3B quantized model is unreliable at structured tool calling, which is exactly what 5.3 builds. |
| **P6 — AWS Capstone & Handback** | A | A | Byte-identical across variants. Fixed profile, prohibited resources, migration-delta record, and a required real-AWS failure demonstration. Two tight spots: 6.5 at 6 h covers three recordings; 6.6 at 8 h covers five deliverables. |

## 4. What moved since the last review

| Prior blocker | Status |
|---|:--|
| No rubrics / Must-Haves | Partially — declared as a build dependency; floors exist in 3 of 31 tasks |
| No hardware floor | **Closed** — lines 15–19 |
| No P6 cloud profile | **Closed** — fixed profile + prohibited list |
| Cost controls dropped | **Closed** — constrained role, budget actions, automated teardown |
| GPU contradiction | **Closed** — no GPU provisioned, fine-tuning out of scope |
| 14-day window vs 3-week project | **Closed** — endpoint by end of Week 20, 3-day SLA, one remediation |
| P5/P6 repo continuity | **Closed** — checkpoint model |
| LocalStack ToS | Bounded, not closed — conditional status + no-penalty fallback |
| LocalStack P1 fidelity violation | **Closed** — LocalStack deferred to P2 |
| Real-AWS spend leak | **Closed** — `awslocal` only, client factory, CI gate |
| "Multi-Agent" claim | **Closed** — renamed |
| Determinism vs bots / self-set criteria | **Closed** — fixed transcripts, published floors |
| Missing legacy-integration artifact | **Closed** — Task 3.1 |
| No portfolio output | **Closed** — Task 6.6 |
| No context-switching rep | **Closed** — Task 3.4 |
| Tool excess | **Closed** — ~10 services removed |
| Ragas non-determinism | **Closed** — manual, variance-reported, non-gating |

## 5. Ten remaining gaps, ranked

1. **Rubrics and floors don't exist.** P1, P4, 6.4 and 6.5 have artifacts with no pass condition. Everything else is now blocked behind this.
2. **Task 3.1 is overloaded at 18 h** — runtime + provider abstraction + legacy discovery + derived spec + defensive client. Split it, or move 4 h from 3.3.
3. **Admission has no production-history bar.** Add "≥3 years professional production engineering with one shipped system walked through in interview."
4. **≤3B model vs LangGraph tool calling.** Make the deterministic emulator the *assessed* agent path in P5 and Ollama optional there, or the agent lesson teaches model weakness rather than design.
5. **The deployed capstone is largely TripleTen reference code** (repo 5 starts from the P4 reference). Correct for grading; must be stated explicitly for the portfolio and licensing story.
6. **Live rehearsal still optional** (line 58/68) — the role brief names the live constraints-change drill as the exact format candidates report failing.
7. **6.5 at 6 h for three recordings** and **6.6 at 8 h for five deliverables** are the two tightest allocations left.
8. **6.2's required real-AWS failure demonstration needs a seeded scenario** — students hold a constrained role and cannot manufacture a policy denial. Add it to the supplied-asset inventory.
9. **`fde-focused-6-project-tree.md` is stale** against both documents (old hours, old P5 name, GPU language).
10. **`AGENTS.md` and `executive-overview.md` still describe a 5-project, 452-hour program** with fine-tuning in P5 core.

## 6. Recommendation

**Open-source is the primary.** It now teaches slightly *more* than LocalStack, not less: line 231 asks students to distinguish RabbitMQ delivery semantics from the AWS adapter, and its P6 involves three genuine adapter swaps rather than an endpoint-URL change — at the same cost, with no third-party dependency.

**Keep LocalStack as the documented conditional alternative.** Its design is now equal, but its differentiator has shrunk: with SDK clients confined to supplied adapters, students get AWS API exposure they largely don't write. That is a thin return for a licensing condition and an extra container.

**Before authoring:** resolve the program-of-record question (items 9–10), then build the rubrics and floors (item 1). Everything else on the list is a 30-minute edit.

Want me to save this evaluation — and/or the earlier full review — under `syllabus-fde-focused/`? Your earlier `claude-verdict.md` request was interrupted by the model switch, so nothing was written.