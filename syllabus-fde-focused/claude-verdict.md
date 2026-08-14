I'll start by reading the foundational documents.

# Verdict

| Scope | Verdict |
|---|---|
| **Open-source variant** ([fde-focused-6-projects-opensource.md](syllabus-fde-focused/fde-focused-6-projects-opensource.md)) | **Approve with changes** |
| **LocalStack variant** ([fde-focused-6-projects-localstack.md](syllabus-fde-focused/fde-focused-6-projects-localstack.md)) | **Reject** |
| **Overall** | **Approve with changes** — open-source as the primary path, conditional on the 12 critical findings below |

Neither document is ready to become the production syllabus today. The 6/22/20/440 skeleton is sound and the arithmetic is correct, but both documents are *task maps without an assessment contract*: no Must-Haves, no rubric anchors, no hardware floor, no cloud deployment profile, and no delivery contract for the ~26–28 "supplied" assets on which every determinism claim rests. The open-source variant is fixable by addition. The LocalStack variant additionally (a) writes an unresolved third-party licensing precondition into its own text, (b) reintroduces a performance-fidelity violation this repository already documented and prohibited, (c) creates a real-AWS spend leak, and (d) silently overrides the prior $470/student and +27-hour findings without re-costing.

---

# Critical findings

### C1 — No acceptance criteria, Must-Haves, or rubric anchors exist in either document

- **Severity:** Critical
- **File/line:** [opensource.md:52](syllabus-fde-focused/fde-focused-6-projects-opensource.md:52), [:112](syllabus-fde-focused/fde-focused-6-projects-opensource.md:112), [:172](syllabus-fde-focused/fde-focused-6-projects-opensource.md:172), [:232](syllabus-fde-focused/fde-focused-6-projects-opensource.md:232), [:292](syllabus-fde-focused/fde-focused-6-projects-opensource.md:292), [:354](syllabus-fde-focused/fde-focused-6-projects-opensource.md:354); [localstack.md:61](syllabus-fde-focused/fde-focused-6-projects-localstack.md:61) and parallel lines
- **Project/task:** All 31 tasks
- **Exact issue:** Every project lists "Project evidence" (artifact names) but no pass threshold, no Must-Have table, and no rubric anchor. [AGENTS.md:110](AGENTS.md:110) requires "clear *Must-Have* criteria and *Recommendations*". [projects/project-5-rubric.md](projects/project-5-rubric.md) shows what the standard looks like; nothing equivalent exists for the six-project structure. Both executive summaries claim "common rubric anchors" ([opensource.md:9](syllabus-fde-focused/fde-focused-6-projects-opensource.md:9)) that no task produces or references.
- **Consequence:** Determinism is asserted, not implemented. Two reviewers grading the same discovery record or SoW will differ. The program cannot be authored, piloted, or defended to an accreditation/quality function.
- **Recommended correction:** Add a `### Acceptance evidence` block to every task with 3–5 binary Must-Haves, and a per-project rubric file under `projects/`.
- **Proposed replacement wording** (pattern, Task 2.4): *"**Acceptance evidence (Must-Have):** golden set contains ≥25 queries with labelled relevance; held-out recall@10 ≥ 0.70 and p95 retrieval latency ≤ 800 ms on the supplied fixture set; every miss in the failure table is attributed to exactly one of parsing, chunking, metadata, dense, sparse, or rerank; the recommended improvement cites a measured delta."*
- **Workload effect:** None on student hours. Adds ~60–80 hours of authoring per project to program build.

### C2 — 26–28 "supplied" assets carry the determinism claim, with no delivery contract behind them

- **Severity:** Critical
- **File/line:** `supplied` appears 26× in [opensource.md](syllabus-fde-focused/fde-focused-6-projects-opensource.md) and 28× in [localstack.md](syllabus-fde-focused/fde-focused-6-projects-localstack.md); e.g. [opensource.md:78](syllabus-fde-focused/fde-focused-6-projects-opensource.md:78) "deterministic provider emulator", [:138](syllabus-fde-focused/fde-focused-6-projects-opensource.md:138) "supplied local cross-encoder", [:198](syllabus-fde-focused/fde-focused-6-projects-opensource.md:198) "supplied failure injector", [:268](syllabus-fde-focused/fde-focused-6-projects-opensource.md:268) "supplied flawed AI-generated artifact", [:380](syllabus-fde-focused/fde-focused-6-projects-opensource.md:380) "Course verifier", [:410](syllabus-fde-focused/fde-focused-6-projects-opensource.md:410) "supplied teardown script"
- **Project/task:** Program-wide
- **Exact issue:** [AGENTS.md:108](AGENTS.md:108) states the scenario-pack contract document "was deleted in `cd301ba` and has not been replaced; re-author it before delivery repositories are specced." Both new documents depend on published/held-out scenario packs, a stakeholder bot, six held-out packs, a course verifier, and a per-emulator `FIDELITY.md` — none of which have a contract, owner, or format.
- **Consequence:** Every "deterministic" and "held-out" claim in both documents is currently unbacked. Build cost is unknown and unbudgeted; the two variants cannot be compared on cost because their asset inventories are unpriced.
- **Recommended correction:** Re-author the scenario-pack contract before either document is promoted, and add a `## Supplied-asset inventory` appendix to each variant, one row per asset: asset, owning project, format, determinism guarantee, held-out counterpart.
- **Proposed replacement wording:** *"Program dependency: this syllabus is not authorable until the scenario-pack contract (published cases, held-out grading cases, per-emulator `FIDELITY.md`, verifier report schema) is re-authored. Every item in the supplied-asset inventory must exist and be pinned by version before a cohort is scheduled."*
- **Workload effect:** No student-hour change. Gates the build.

### C3 — No hardware floor is stated, and the Project 4–5 stack will not fit 16 GB

- **Severity:** Critical
- **File/line:** Neither document states RAM, VRAM, disk, or OS requirements. Confirmed: `grep RAM|GB|VRAM` returns only [opensource.md:177](syllabus-fde-focused/fde-focused-6-projects-opensource.md:177), [:181](syllabus-fde-focused/fde-focused-6-projects-opensource.md:181), [:322](syllabus-fde-focused/fde-focused-6-projects-opensource.md:322) — all prose mentions of "hardware", no numbers. [AGENTS.md:24-26](AGENTS.md:24) has the numbers; the focused documents dropped them.
- **Project/task:** P1.2, P3.1, P4.3, P5.3, P5.4 (concurrent stack)
- **Exact issue:** By P5 the declared environment implies, concurrently: FastAPI + worker, PostgreSQL/pgvector, Redis, OpenSearch (JVM, ~2–3 GB), Keycloak (~1 GB), Jaeger/Tempo, Prometheus, Grafana, Arize Phoenix, and Ollama with a quantised 7B model (~5 GB resident). That is ~13–15 GB of container working set before Docker Desktop/WSL2 overhead and the IDE. The LocalStack variant adds a LocalStack container that itself spawns a real OpenSearch JVM.
- **Consequence:** A meaningful fraction of admitted students will hit OOM kills and swap-thrash mid-project, in the two heaviest projects, with no documented remedy. This converts into unbudgeted troubleshooting hours and support load, and silently changes who can pass.
- **Recommended correction:** State a hard floor; define compose profiles so no more than one heavyweight service class runs at a time; provide a hosted fallback.
- **Proposed replacement wording:** *"**Required hardware:** 32 GB RAM (hard minimum 16 GB with the reduced compose profile), 8 CPU cores, 80 GB free disk, macOS/Linux/Windows-with-WSL2. Optional 8 GB VRAM for local vLLM only. Every project ships `compose.core.yaml` (assessed services) and `compose.full.yaml` (optional); the assessed path must run in ≤10 GB. Students below the floor use the program-provided remote dev environment; this never affects grading."*
- **Workload effect:** Removes 6–12 hours of hidden troubleshooting per affected student. Adds program cost for remote environments.

### C4 — Project 6 never defines what is actually deployed to AWS

- **Severity:** Critical
- **File/line:** [opensource.md:366-374](syllabus-fde-focused/fde-focused-6-projects-opensource.md:366); [localstack.md:375-383](syllabus-fde-focused/fde-focused-6-projects-localstack.md:375)
- **Project/task:** 6.2 Protected AWS deployment (18 hours)
- **Exact issue:** P6.2 says "Replace local infrastructure adapters with supplied AWS bindings" but no line states which of the ~10 capstone services deploy to AWS, which are replaced by managed services, which are co-located as containers on the instance, and which are dropped. Keycloak, OpenSearch/pgvector, Phoenix, Prometheus, Grafana, RabbitMQ/SQS, MinIO/S3 and Redis all have different answers with 10× cost consequences.
- **Consequence:** Both the $180 cap and the 18-hour estimate are unfalsifiable. A student who deploys Amazon OpenSearch Service + RDS + ALB reaches ~$120/14 days on managed services alone before compute; a student who co-locates everything needs ≥16 GB (t3.xlarge, ~$56/14 days) rather than the canonical t3.large ($28). Reviewers cannot compare submissions.
- **Recommended correction:** Publish a fixed cloud deployment profile as a table in the Project 6 header, matching [syllabus/project-5-aws-deployment.md:33](syllabus/project-5-aws-deployment.md:33)'s prohibition list.
- **Proposed replacement wording:** *"**Cloud deployment profile (fixed):** one `t3.large` instance runs app, worker, PostgreSQL/pgvector, keyword index, and Caddy. Object storage moves to S3; secrets move to SSM Parameter Store. Reviewer access uses the program-issued token, not Keycloak. Phoenix, Prometheus, and Grafana are not deployed; observability evidence is exported from the local run and from CloudWatch. Students must not create a NAT gateway, load balancer, managed database, managed search domain, second public IPv4 address, or second always-on instance. Any deviation requires written instructor approval before resources start."*
- **Workload effect:** P6.2 becomes achievable in 18 hours only with this profile plus a supplied one-command deploy; otherwise re-estimate to 26–34 hours (see Workload audit).

### C5 — Every cost and runtime control from the repository's own AWS runbook has been dropped, and replaced by a contradiction

- **Severity:** Critical
- **File/line:** [opensource.md:360](syllabus-fde-focused/fde-focused-6-projects-opensource.md:360) ("AWS budget dashboard"), [:370](syllabus-fde-focused/fde-focused-6-projects-opensource.md:370) ("Supplied CloudFormation or OpenTofu templates"), [:372](syllabus-fde-focused/fde-focused-6-projects-opensource.md:372) ("trusted TLS"); identical at [localstack.md:369](syllabus-fde-focused/fde-focused-6-projects-localstack.md:369), [:379](syllabus-fde-focused/fde-focused-6-projects-localstack.md:379), [:381](syllabus-fde-focused/fde-focused-6-projects-localstack.md:381). Compare [syllabus/project-5-aws-deployment.md:39-52](syllabus/project-5-aws-deployment.md:39)
- **Project/task:** 6.1, 6.2, 6.6
- **Exact issue:** The canonical runbook specifies a constrained student role that *cannot* create NAT gateways, load balancers, managed databases, public IPs, or IAM principals; an in-account AWS Budget Action at $144 actual / $162 forecast that stops tagged instances; a GPU booking service with a 4-hour auto-stop and nightly sweep; a program-owned DNS zone with Caddy TLS-ALPN-01; and course-automation teardown. The new documents retain none of it. Worse, [tree:235](syllabus-fde-focused/fde-focused-6-project-tree.md:235) says "Use the provided launch templates" while both syllabi replaced that with "CloudFormation or OpenTofu templates" — IaC execution requires broad create permissions, which directly negates the constrained-role model that makes the cap enforceable. And "Configure trusted TLS" is impossible without a program-owned domain, which no line provides.
- **Consequence:** The $180 cap becomes advisory. A dashboard is a report, not a control. One forgotten g5.xlarge over a weekend is $60; one NAT gateway is $15/14 days; one student on a personal account is a compliance incident. "Trusted TLS" as written is unachievable, so students will ship self-signed certificates and the reviewer-access control fails.
- **Recommended correction:** Restate the canonical controls verbatim in the Project 6 header and replace IaC with launch templates.
- **Proposed replacement wording:** *"**Cost and access controls (program-operated, not student work):** one dedicated AWS Organizations member account per student with a constrained course role limited to the supplied launch templates, approved parameter paths, CloudWatch views, and Session Manager; the role cannot create arbitrary instance types, NAT gateways, load balancers, managed databases, IAM principals, public IPs, or untagged resources. Each account carries an in-account AWS Budget with a $144 actual-cost alert, a $162 forecast alert, and a Budget Action that denies new EC2 provisioning and stops tagged instances. The program owns the capstone DNS zone and issues one hostname per student; the supplied Caddy profile obtains a publicly trusted certificate over TLS-ALPN-01. Teardown is executed by course automation and verified by the course verifier. Students never use personal AWS accounts or payment methods."*
- **Workload effect:** Reduces P6.2 by ~4 hours (no IaC authoring) and removes an unbounded troubleshooting tail.

### C6 — Three mutually inconsistent GPU positions; P5 defers LoRA to a Project 6 that never authorizes it

- **Severity:** Critical
- **File/line:** [opensource.md:322](syllabus-fde-focused/fde-focused-6-projects-opensource.md:322) and [localstack.md:331](syllabus-fde-focused/fde-focused-6-projects-localstack.md:331) ("Any AWS GPU execution is deferred to Project 6"); [opensource.md:353](syllabus-fde-focused/fde-focused-6-projects-opensource.md:353) ("4–8 GPU hours"); [opensource.md:374](syllabus-fde-focused/fde-focused-6-projects-opensource.md:374) / [tree:238](syllabus-fde-focused/fde-focused-6-project-tree.md:238) (GPU permitted "only for approved model-serving evidence"); [tree:204](syllabus-fde-focused/fde-focused-6-project-tree.md:204) (LoRA "may be attempted in a scheduled GPU session"); [syllabus/project-5-aws-deployment.md:26](syllabus/project-5-aws-deployment.md:26) (40 GPU hours, $21) and [projects/project-5-rubric.md:9](projects/project-5-rubric.md:9) (vLLM session is a **Must-Have**)
- **Project/task:** 5.3, 6.2
- **Exact issue:** P5.3 defers LoRA to Project 6. No Project 6 task mentions fine-tuning; P6.2 restricts GPU to "model-serving evidence". So the deferral points nowhere. Separately, the allowance moved from 40 hours (canonical, required) to "4–8 hours" (new, optional, recommended-pilot) with no rationale, no ledger, no booking mechanism, no acceptance evidence, no rubric line, and no hours allocated in any task.
- **Consequence:** An unassessed, unowned, cost-bearing feature sits in the highest-risk project. Students will ask for it; instructors have no basis to grant or refuse; and the repository's rubric of record still demands it as a Must-Have.
- **Recommended correction:** Delete the GPU and PEFT/LoRA thread entirely from both variants and update [projects/project-5-rubric.md](projects/project-5-rubric.md). The evidence is decisive: the role brief records that fine-tuning appears in **zero of 41 postings** and states plainly that it "is a different profession" (`Forward Deployed Engineer — the role, explained_files/saved_resource.html`, "The job does not" / "Weak fit ML engineer" sections). There is no market cost to removal and a large operational saving.
- **Proposed replacement wording:** Replace [opensource.md:353](syllabus-fde-focused/fde-focused-6-projects-opensource.md:353) with *"**GPU boundary:** none. The program provisions no GPU. The deployed endpoint is CPU- and API-backed. Model-weight selection, quantisation, and serving trade-offs are assessed as a written architecture decision, not as a provisioned session."* Replace the final bullet of 5.3 with *"Fine-tuning is out of scope. Students must be able to explain, in the Project 5 technical defense, why prompt design, retrieval, and tool constraints are the correct levers for this workflow and when fine-tuning would instead be justified."*
- **Workload effect:** Removes 4–8 unbudgeted student hours, removes the booking service and quota-management operating cost, and removes $4–60 of variance from the AWS cap.

### C7 — The 14-day window, the 3-week project, asynchronous review turnaround, and mandatory teardown are mutually incompatible

- **Severity:** Critical
- **File/line:** [opensource.md:351](syllabus-fde-focused/fde-focused-6-projects-opensource.md:351), [:362](syllabus-fde-focused/fde-focused-6-projects-opensource.md:362), [:384](syllabus-fde-focused/fde-focused-6-projects-opensource.md:384); [localstack.md:360](syllabus-fde-focused/fde-focused-6-projects-localstack.md:360), [:371](syllabus-fde-focused/fde-focused-6-projects-localstack.md:371), [:393](syllabus-fde-focused/fde-focused-6-projects-localstack.md:393)
- **Project/task:** 6.1, 6.3, 6.6
- **Exact issue:** Project 6 spans 21 days. The cloud window is 14 days. Assessment is asynchronous, so reviewer turnaround consumes part of that window. P6.3 requires remediation "inside the endpoint, assessment window, and budget". Nothing defines what happens when a student fails acceptance with the window expired and teardown mandatory: there is no re-deploy authorisation, no remediation reserve inside the $180, and no second-window policy.
- **Consequence:** The most common real outcome — conditional-accept requiring a fix — has no compliant path. Instructors will improvise, students will either exceed the cap or fail on an administrative technicality, and the "mandatory teardown" claim will be broken in practice.
- **Recommended correction:** Anchor the window, publish a review SLA, and reserve budget for exactly one re-deploy.
- **Proposed replacement wording:** *"**Assessment window:** 14 consecutive days of reviewer access, beginning at first verified endpoint, which must occur no later than the end of week 21. Reviewer turnaround is 3 business days. One instructor-approved remediation redeployment is permitted inside the same window or as a single 5-day extension; it draws on a $40 remediation reserve inside the $180 cap (normal target $70, reserve $40, contingency $70). A second window requires program approval and is treated as a resubmission."*
- **Workload effect:** Adds ~2 hours to 6.1 (planning against a published SLA); prevents an unbounded tail.

### C8 — P5/P6 repository continuity is asserted but structurally undefined

- **Severity:** Critical
- **File/line:** [opensource.md:39](syllabus-fde-focused/fde-focused-6-projects-opensource.md:39), [:288](syllabus-fde-focused/fde-focused-6-projects-opensource.md:288), [:318](syllabus-fde-focused/fde-focused-6-projects-opensource.md:318); [localstack.md:48](syllabus-fde-focused/fde-focused-6-projects-localstack.md:48), [:297](syllabus-fde-focused/fde-focused-6-projects-localstack.md:297), [:327](syllabus-fde-focused/fde-focused-6-projects-localstack.md:327); [tree:181-182](syllabus-fde-focused/fde-focused-6-project-tree.md:181)
- **Project/task:** 5.3, 6.2
- **Exact issue:** "Project 5 creates the capstone repository" contradicts 5.3's "Reuse Project 2 retrieval" and the capstone's dependence on P3 resilience and P4 security controls. Nowhere do the documents state whether P1–P4 are one evolving repository or four separate starters. Both readings break something: four repositories means P5 must integrate three foreign codebases (unbudgeted, 10–20 hours); one evolving repository means P1 created the capstone, not P5, and the stated contract is false.
- **Consequence:** The single largest unpriced task in the program. It also creates a grading hole: a student who failed P4's controls carries an insecure capstone into a deployed, reviewer-accessible endpoint, with no inter-project remediation gate defined.
- **Recommended correction:** Declare one continuous repository, rename the P5 milestone, and add a remediation gate.
- **Proposed replacement wording:** Replace the contract bullet with *"One student repository spans Projects 1–6. Each project extends it on a new branch and merges after acceptance; the supplied scaffold for each project arrives as an upstream merge, not a new clone. Project 5 produces the **capstone release tag**; Project 6 deploys, accepts, hands back, and tears down that tagged release. Any Project 4 control that did not pass must be remediated and re-verified before the Project 6 local gate; a deployed endpoint may not carry a failed security control."*
- **Workload effect:** Removes 10–20 hours of hidden integration work from P5; adds ~2 hours of remediation to the P6.1 local gate.

### C9 — LocalStack: the document writes an unresolved licensing precondition into its own terms, and silently overrides the prior $470 / +27-hour findings

- **Severity:** Critical (LocalStack variant)
- **File/line:** [localstack.md:25](syllabus-fde-focused/fde-focused-6-projects-localstack.md:25), [:26](syllabus-fde-focused/fde-focused-6-projects-localstack.md:26), [:7](syllabus-fde-focused/fde-focused-6-projects-localstack.md:7). Compare [syllabus-localstack-gemini/README.md:29-31](syllabus-localstack-gemini/README.md:29) and [syllabus-localstack-gemini/overview-and-module-map.md:66-83](syllabus-localstack-gemini/overview-and-module-map.md:66)
- **Project/task:** Program-wide
- **Exact issue:** Line 25 instructs the reader to obtain written confirmation that mandatory use in a *paid* program is compatible with Hobby terms, "If it is not, use the open-source program variant." A production syllabus cannot ship with its own foundation conditional. Separately, the prior evaluation of this exact approach concluded **$470/student** (a 135% increase) precisely because Hobby eligibility was unresolved, and **+27 hours** of added surface that "cannot simply be absorbed", with an explicit instruction: *"Do not publish per-project hour tables from this edition until Option A or B is chosen."* The new document resolves the cost by asserting student-owned Hobby accounts and resolves the workload by not mentioning it — the hour table at [localstack.md:427-435](syllabus-fde-focused/fde-focused-6-projects-localstack.md:427) is identical to the open-source one.
- **Consequence:** Both blockers that stopped the previous LocalStack edition remain open, now invisible. Line 26 ("TripleTen does not distribute tokens") also makes a third-party account a graded dependency with no defined fallback for a student whose signup, token, or eligibility fails.
- **Recommended correction:** Do not promote this variant until written confirmation exists and the +27 hours are displaced with a documented per-project trade. Add a fallback path.
- **Proposed replacement wording:** *"**Status: conditional alternative, not the production syllabus.** Promotion requires (a) written confirmation from LocalStack that mandatory use by students in a paid program is permitted on the tier assumed here, or a program-purchased licence line added to the per-student cost; (b) a per-project displacement of the ~27 hours this variant adds, published in the hour table; and (c) a documented open-source fallback that any student may use without penalty if their account or token is unavailable. Until all three land, quote the open-source variant."*
- **Workload effect:** +27 hours unaccounted; must be displaced or the envelope extended to ~21.8 h/week.

### C10 — LocalStack: Project 1 grades performance diagnosis against emulated metrics, violating the fidelity rule this repository already documented

- **Severity:** Critical (LocalStack variant)
- **File/line:** [localstack.md:60](syllabus-fde-focused/fde-focused-6-projects-localstack.md:60), [:87](syllabus-fde-focused/fde-focused-6-projects-localstack.md:87), [:88-90](syllabus-fde-focused/fde-focused-6-projects-localstack.md:88). Compare [syllabus-localstack-gemini/overview-and-module-map.md:49](syllabus-localstack-gemini/overview-and-module-map.md:49)
- **Project/task:** 1.3 Diagnose and repair the seeded failure (18 hours)
- **Exact issue:** Task 1.3's tool list adds "LocalStack CloudWatch APIs" to a task whose activities are "Run one bounded load and provider-latency scenario" and "Identify the first supported bottleneck". The prior fidelity analysis states: *"No performance conclusions may be drawn from emulated services… This constraint falls hardest on Project 1, whose entire subject is empirical performance diagnosis."* The new document reintroduces exactly that. Compounding it: P1 adds LocalStack S3 and CloudWatch to the environment and `awslocal` to the tool list, yet **no P1 activity bullet uses S3 or CloudWatch for anything** — [localstack.md:78](syllabus-fde-focused/fde-focused-6-projects-localstack.md:78) only says "Run … LocalStack … locally", and the `[Skills]` line at [:86](syllabus-fde-focused/fde-focused-6-projects-localstack.md:86) is byte-identical to the open-source version, naming no AWS skill.
- **Consequence:** In the program's first three weeks the LocalStack variant adds a container, a CLI, and a metrics surface that produce zero assessed learning, while inviting students to draw performance conclusions from a local process. Students learn a wrong inference habit in the exact skill P1 exists to build.
- **Recommended correction:** Remove LocalStack entirely from Project 1 in this variant.
- **Proposed replacement wording:** Line 60 → *"**Local environment:** Docker Compose, FastAPI, PostgreSQL, Redis, OpenTelemetry, Prometheus, Grafana, and Jaeger or Tempo. LocalStack is not introduced until Project 2; no performance or bottleneck conclusion in this program may be drawn from an emulated AWS service."* Line 87 → remove "LocalStack CloudWatch APIs".
- **Workload effect:** −2 hours of hidden setup in P1; recovers the +2 the prior analysis attributed to P1.

### C11 — LocalStack: "AWS CLI or `awslocal`" plus a missing enforcement control creates a real-AWS spend and credential leak

- **Severity:** Critical (LocalStack variant)
- **File/line:** [localstack.md:77](syllabus-fde-focused/fde-focused-6-projects-localstack.md:77), [:137](syllabus-fde-focused/fde-focused-6-projects-localstack.md:137), [:147](syllabus-fde-focused/fde-focused-6-projects-localstack.md:147), [:27](syllabus-fde-focused/fde-focused-6-projects-localstack.md:27), [:7](syllabus-fde-focused/fde-focused-6-projects-localstack.md:7). Compare [syllabus-localstack-gemini/overview-and-module-map.md:55-62](syllabus-localstack-gemini/overview-and-module-map.md:55)
- **Project/task:** 1.2, 2.2, 2.3
- **Exact issue:** Line 7 claims "no real AWS account … is used" and line 27 covers sentinel credentials and not mounting `~/.aws`. But the prior analysis specified four controls, and the new document keeps only two — it omits the **shared client factory** and the **CI lint gate that fails when a boto3 client is constructed outside it**, which are the only *enforcing* controls. Offering "AWS CLI" as an alternative to `awslocal` makes the failure trivially reachable: a student with real credentials on the host and one missing `--endpoint-url` calls real AWS and bills their own card.
- **Consequence:** The "$0 local spend / no real AWS account" claim is unenforced from week 1. Worst case is a student's personal card charged during a paid course — a support and reputational incident, not merely a budget variance.
- **Recommended correction:** Drop plain AWS CLI, and restate all four controls.
- **Proposed replacement wording:** Replace `AWS CLI or `awslocal`` with `` `awslocal` (plain AWS CLI is not used in Projects 1–5) `` in all three tool lists, and extend line 27: *"Compose sets sentinel credentials and a sentinel region for every service. A shared client factory is the only sanctioned way to construct an AWS SDK client and injects `endpoint_url` from configuration. A CI gate fails the build when an SDK client is constructed outside that factory. Starter repositories ship no AWS profile references and never mount the host credential directory."*
- **Workload effect:** Neutral for students; adds a scaffold requirement to every LocalStack starter repository.

### C12 — Project 5 is titled "Multi-Agent" and explicitly forbids building a multi-agent system

- **Severity:** Critical
- **File/line:** [opensource.md:284](syllabus-fde-focused/fde-focused-6-projects-opensource.md:284) vs [:319](syllabus-fde-focused/fde-focused-6-projects-opensource.md:319); [localstack.md:293](syllabus-fde-focused/fde-focused-6-projects-localstack.md:293) vs [:328](syllabus-fde-focused/fde-focused-6-projects-localstack.md:328); [tree:178](syllabus-fde-focused/fde-focused-6-project-tree.md:178) vs [tree:199-200](syllabus-fde-focused/fde-focused-6-project-tree.md:199)
- **Project/task:** Project 5, Task 5.3
- **Exact issue:** The title, both program summary tables ([opensource.md:30](syllabus-fde-focused/fde-focused-6-projects-opensource.md:30)) and the tree all say "Multi-Agent". Task 5.3 says "Build one bounded multi-step tool flow rather than a general agent platform" and 5.3's summary says "one auditable workflow". The program teaches a single bounded state graph — correctly, and defensibly. It does not teach multi-agent systems.
- **Consequence:** An unsupportable claim embedded in the project name, which will propagate verbatim into landing pages and graduate CVs, and will collapse in the first technical interview that asks about agent-to-agent coordination. It also invites students to over-build against the task's own instruction.
- **Recommended correction:** Rename the project in both documents, the tree, and the summary tables.
- **Proposed replacement wording:** *"Project 5 — Bounded Agent Workflow Under Ambiguity"*, engagement outcome *"Build and evaluate one bounded, auditable agent workflow with an enforced authority boundary."*
- **Workload effect:** None.

### C13 — "Deterministic" assessment is contradicted by stakeholder bots, student-defined acceptance criteria, and "respond live"

- **Severity:** Critical
- **File/line:** [opensource.md:9](syllabus-fde-focused/fde-focused-6-projects-opensource.md:9) and [:58](syllabus-fde-focused/fde-focused-6-projects-opensource.md:58) ("stakeholder bot"); [:121](syllabus-fde-focused/fde-focused-6-projects-opensource.md:121) + [:150](syllabus-fde-focused/fde-focused-6-projects-opensource.md:150), [:199](syllabus-fde-focused/fde-focused-6-projects-opensource.md:199), [:311](syllabus-fde-focused/fde-focused-6-projects-opensource.md:311) (student-defined criteria then graded against them); [tree:259](syllabus-fde-focused/fde-focused-6-project-tree.md:259) ("Respond **live** to changed constraints") vs [opensource.md:403](syllabus-fde-focused/fde-focused-6-projects-opensource.md:403) (recorded, asynchronous); [:404](syllabus-fde-focused/fde-focused-6-projects-opensource.md:404) ("Obtain a simulated accept, conditional-accept, or reject decision"). Same lines in the LocalStack variant.
- **Project/task:** 1.1, 2.1/2.4, 3.3, 5.2, 4.5, 6.5
- **Exact issue:** Three separate breaks. (a) An LLM-driven "stakeholder bot" is by construction non-deterministic; it cannot coexist with a determinism guarantee. (b) In 2.1→2.4, 3.3 and 5.2 the student *defines* the acceptance criteria, SLO, and acceptance conditions, and is then assessed against them — a self-set bar produces non-comparable grades and rewards low ambition. (c) The tree requires a live response in 6.5 while both syllabi make it recorded; nothing states which governs.
- **Consequence:** The program's central differentiator — deterministic, asynchronous, comparable assessment — does not hold as written. Reviewer variance will be the dominant grade signal in exactly the field-competency tasks the program is selling.
- **Recommended correction:** Fix the bot's role, floor the self-set criteria, and settle live-vs-recorded deliberately.
- **Proposed replacement wording:** (a) Line 9 → *"…using role cards, fixed transcripts, timed injects with published trigger conditions, evidence templates, recorded defenses, and published rubric anchors. An optional stakeholder chatbot is provided for unassessed practice only; no graded evidence may originate from it."* (b) Add to each affected task: *"Student-defined criteria must meet or exceed the published floor for this project; the grade is awarded against the floor and against the justification for any criterion set above it."* (c) See I-10 below for the recommended hybrid.
- **Workload effect:** None on hours; substantial on rubric authoring.

### C14 — The six-project structure invalidates the repository's stated program contract and shared-repository economics, and neither document says so

- **Severity:** Critical
- **File/line:** [AGENTS.md:5](AGENTS.md:5), [:17](AGENTS.md:17), [:20](AGENTS.md:20), [:75-100](AGENTS.md:75), [:109](AGENTS.md:109); [executive-overview.md:11-19](executive-overview.md:11); both new documents carry no status header. `git status` shows `syllabus-fde-focused/` untracked.
- **Project/task:** Program governance
- **Exact issue:** [AGENTS.md](AGENTS.md) is the repository's authority and states 5 projects, ~452 hours, Project 5 as the AWS capstone, `syllabus/` as canonical, and `syllabus-localstack-gemini/` as unadopted. `syllabus-fde-focused/` appears nowhere in the sitemap. More materially, [executive-overview.md:15-19](executive-overview.md:15) makes the whole build economically viable by **reusing the same 5 SE starter repositories** across the SE and FDE tracks; the current SE version of record is `v05-5-projects-22-weeks-local-and-aws-simplified` (5 projects — SE moved *away* from its `v02-6-projects-22-weeks`). A 6-project FDE track has no sixth SE counterpart and re-themes P1 as discovery, so the shared-repo strategy breaks. `executive-overview.md` also still lists Fine-Tuning as FDE P5 core.
- **Consequence:** Three competing programs of record with no precedence rule. Adopting either new document silently doubles curriculum build and reviewer-training cost relative to the documented plan, and that cost increase is nowhere quantified in the very documents proposing it.
- **Recommended correction:** Add a status header to both new documents, and resolve the dual-track question before authoring.
- **Proposed replacement wording:** Prepend to each: *"**Status: candidate proposal, not the program of record.** The program of record remains `syllabus/` (5 projects, ~452 hours) per AGENTS.md until this document is adopted. Adoption requires: an updated AGENTS.md; a decision on the Unified Project / Dual-Track strategy in executive-overview.md, which assumes five shared SE/FDE starter repositories and does not accommodate a sixth; and a re-cost of curriculum build and reviewer training against that decision."*
- **Workload effect:** None on students. Blocks authoring until resolved.

---

# Important findings

### I-1 — Task 1.2 at 10 hours is the program's first and worst underestimate

- **Severity:** Important
- **File/line:** [opensource.md:64-72](syllabus-fde-focused/fde-focused-6-projects-opensource.md:64); [localstack.md:73-81](syllabus-fde-focused/fde-focused-6-projects-localstack.md:73)
- **Project/task:** 1.2 (10 hours)
- **Exact issue:** Ten hours covers, in week 1: first `docker compose up` of 8–9 services on Windows/WSL2 or macOS, multi-gigabyte image pulls, port conflicts, orienting in an unfamiliar codebase, and following one request end-to-end through code, logs, Prometheus metrics, and a distributed trace — four observability tools, at least two of which most senior backend engineers have not used. Meanwhile 1.1, a document-production task, gets 14 hours.
- **Consequence:** The whole cohort runs late in week 1, which is where retention is decided.
- **Recommended correction:** Rebalance and add a Week 0.
- **Proposed replacement wording:** Move 4 hours from 1.1 to 1.2 (1.1 → 10 h, 1.2 → 14 h) and add *"**Week 0 — Environment and toolchain onboarding (10 hours, unassessed):** verify hardware against the floor, install and validate the toolchain, pre-pull all pinned images and the local embedding and inference models, run the supplied smoke check, and open a support ticket if the smoke check fails."*
- **Workload effect:** Net +10 hours of honest, front-loaded time; removes 6–12 hours of hidden mid-project troubleshooting.

### I-2 — Task 4.3 at 30 hours is the most likely task to fail outright

- **Severity:** Important
- **File/line:** [opensource.md:254-262](syllabus-fde-focused/fde-focused-6-projects-opensource.md:254); [localstack.md:263-271](syllabus-fde-focused/fde-focused-6-projects-localstack.md:263)
- **Project/task:** 4.3 (30 hours)
- **Exact issue:** Thirty hours covers: Keycloak realm/client/role/mapper configuration plus OIDC token validation in FastAPI; prompt-injection handling; output validation; PII redaction (Presidio pulls spaCy models and needs tuning); audit logging; a secrets-management change; a CI security gate across Semgrep, Trivy and Gitleaks; and testing against both published and held-out attack scenarios. Keycloak alone routinely costs a first-timer 6–10 hours. The LocalStack variant adds SSM, Secrets Manager and a KMS exercise ([localstack.md:270](syllabus-fde-focused/fde-focused-6-projects-localstack.md:270)) at the same 30 hours.
- **Consequence:** Realistic cost is 36–45 hours (open-source) and 42–52 (LocalStack) — a 6–22 hour overrun in a 20 h/week project.
- **Recommended correction:** Supply the identity layer fully configured and assess only integration and controls.
- **Proposed replacement wording:** *"The Keycloak realm, clients, roles, and token mappers are supplied pre-configured and are not student work; students integrate token validation and role checks at one endpoint. The CI security gate is supplied as a pinned workflow; students configure its policy and triage its findings."*
- **Workload effect:** −8 to −10 hours in 4.3, bringing it inside 30.

### I-3 — Task 6.2 at 18 hours cannot absorb a first real AWS deployment

- **Severity:** Important
- **File/line:** [opensource.md:366-374](syllabus-fde-focused/fde-focused-6-projects-opensource.md:366); [localstack.md:375-383](syllabus-fde-focused/fde-focused-6-projects-localstack.md:375)
- **Project/task:** 6.2 (18 hours)
- **Exact issue:** Eighteen hours covers ECR image build and push (including cross-architecture builds from Apple Silicon), template deployment, TLS and DNS, reviewer authentication, rate and request limits, IMDSv2, least-privilege instance profile, egress control, tags, secrets, and bringing a multi-service stack up on one instance. Every debugging hour simultaneously burns AWS spend and the 14-day window.
- **Consequence:** 26–34 hours realistically; the overrun lands in the final three weeks with cost and window coupled to it.
- **Recommended correction:** Ship a one-command deploy and make the student's assessed work the verification and the decisions, not the plumbing.
- **Proposed replacement wording:** *"The program supplies `scripts/deploy.sh`, which builds, pushes, provisions from the fixed launch template, and starts the stack; it must succeed in under 30 minutes from a clean account. Students are assessed on the pre-flight checklist, the verifier report, the control decisions and their justification, and the cost record — not on authoring infrastructure."*
- **Workload effect:** Keeps 6.2 inside 18 hours; shifts ~10 hours to program build.

### I-4 — Task 2.3 at 24 hours is tight, and tighter in the LocalStack variant

- **Severity:** Important
- **File/line:** [opensource.md:134-142](syllabus-fde-focused/fde-focused-6-projects-opensource.md:134); [localstack.md:143-151](syllabus-fde-focused/fde-focused-6-projects-localstack.md:143)
- **Project/task:** 2.3 (24 hours)
- **Exact issue:** pgvector index and distance-operator choice, OpenSearch index mapping and analyzer setup, hybrid fusion (reciprocal-rank or weighted, which is a tuning rabbit hole), CPU cross-encoder reranking with its latency implications, authorization-metadata propagation, API versioning and migrations. The LocalStack variant adds OpenSearch domain creation through the emulator, which is slow and adds a second failure surface.
- **Consequence:** 28–34 hours realistically.
- **Recommended correction:** Supply the fusion function and the index mappings; assess the parameter choices and the evidence.
- **Proposed replacement wording:** *"Reciprocal-rank fusion, the OpenSearch index mapping, and the cross-encoder wrapper are supplied. Students choose and justify `k`, candidate depth, fusion weights, and the rerank cut-off, and must show the latency cost of each choice."*
- **Workload effect:** −5 hours in 2.3.

### I-5 — Roughly eleven recorded defenses are required and none are budgeted

- **Severity:** Important
- **File/line:** [opensource.md:98](syllabus-fde-focused/fde-focused-6-projects-opensource.md:98), [:102](syllabus-fde-focused/fde-focused-6-projects-opensource.md:102), [:158](syllabus-fde-focused/fde-focused-6-projects-opensource.md:158), [:208](syllabus-fde-focused/fde-focused-6-projects-opensource.md:208), [:218](syllabus-fde-focused/fde-focused-6-projects-opensource.md:218), [:278](syllabus-fde-focused/fde-focused-6-projects-opensource.md:278), [:338](syllabus-fde-focused/fde-focused-6-projects-opensource.md:338), [:390](syllabus-fde-focused/fde-focused-6-projects-opensource.md:390), [:400-403](syllabus-fde-focused/fde-focused-6-projects-opensource.md:400)
- **Project/task:** 1.5, 2.5, 3.4, 3.5, 4.5, 5.5 (×2), 6.4, 6.5 (×3)
- **Exact issue:** Recording a 10–15 minute technical defense with slides or a screen walkthrough, then re-recording it because the first take was poor, is 1.5–2.5 hours each. Nothing in the hour estimates names this.
- **Consequence:** 12–18 unbudgeted hours program-wide, concentrated in the communication tasks that already have the least implementation slack.
- **Recommended correction:** Reduce to five graded recordings, cap length, supply a template and a recording guide, and state the time cost in each task.
- **Proposed replacement wording:** *"Graded recordings are limited to five across the program: 2.5 (SoW defense), 4.5 (executive risk decision), 5.5 (technical), 6.5 (technical), 6.5 (executive). Each is capped at 10 minutes, single take, using the supplied slide template; production polish is not assessed. All other defenses are written."*
- **Workload effect:** −8 to −12 hours program-wide.

### I-6 — The admission gate is weaker than the program and weaker than the market

- **Severity:** Important
- **File/line:** [opensource.md:9](syllabus-fde-focused/fde-focused-6-projects-opensource.md:9); [localstack.md:9](syllabus-fde-focused/fde-focused-6-projects-localstack.md:9); [tree:18](syllabus-fde-focused/fde-focused-6-project-tree.md:18)
- **Project/task:** Admission
- **Exact issue:** The gate tests "Python, Git, REST APIs, SQL and relational databases, Docker, debugging, and basic cloud concepts". The program then requires async Python concurrency (deadlines, retries, circuit breakers, queue consumers), multi-container orchestration on a 32 GB-class machine, reading unfamiliar instrumented codebases, and roughly 40% written stakeholder-grade English. None of those are tested. The role brief is explicit that the engineering gate is *"Years of production engineering — 'shipped at scale', not demos"* with a market median of four years, *"Verified at intake"* — and there is no production-history requirement in the gate at all.
- **Consequence:** The program admits students it cannot carry, and its own marketing position ("not entry-level") is unenforced.
- **Recommended correction:** Add four gate components.
- **Proposed replacement wording:** *"Admission requires: (1) evidence of ≥3 years professional production software engineering, with one shipped system the candidate can walk through in a 20-minute interview; (2) a timed practical covering async Python, an unfamiliar instrumented FastAPI codebase, SQL, and a Docker Compose failure to diagnose; (3) a written exercise — a one-page recommendation from ambiguous notes, assessed on structure and audience fit; (4) a hardware and toolchain check against the stated floor. Candidates whose only evidence is coursework, notebooks, or prototypes are not admitted."*
- **Workload effect:** None on hours; materially reduces the attrition and support load implied by I-1 to I-4.

### I-7 — The program produces four of the role brief's five artefacts; the legacy-integration artefact is missing

- **Severity:** Important
- **File/line:** [opensource.md:128-132](syllabus-fde-focused/fde-focused-6-projects-opensource.md:128) (supplied parser, supplied fixtures); no equivalent task anywhere
- **Project/task:** Project 2 (or a new 3.x)
- **Exact issue:** The role brief's five auditable artefacts are a traced workflow, an agent with an audit trail, unhappy-path hardening, an eval suite, and *"An integration into legacy. Against an undocumented system with real permissions and limits, not a clean sandbox."* The program delivers the first four well. The fifth does not exist: P2 works from a supplied robust parser over supplied fixtures with OCR explicitly out of scope, which is precisely a clean sandbox.
- **Consequence:** Graduates lack the artefact that most directly answers the market's central doubt, and the program's own commercial logic — five checkable public things standing in for client history — is 80% delivered.
- **Recommended correction:** Add a legacy-integration task, funded from the cuts in the Tooling audit.
- **Proposed replacement wording:** Add **Task 3.6 — Undocumented legacy integration (10 hours)**: *"Integrate against the supplied legacy service, which has no documentation, an inconsistent response schema, an undocumented rate limit, a stale field that must be ignored, and a permission model that denies two of the five operations the client believes are available. Produce a written interface specification derived from observed behaviour, a defensive client with schema tolerance and backoff, a table of the limits and permissions you discovered and how, and a decision record for each behaviour you chose to work around rather than fix."*
- **Workload effect:** +10 hours to Project 3, offset by the tooling removals below.

### I-8 — No public portfolio, reference architecture, or demo-day output

- **Severity:** Important
- **File/line:** [opensource.md:406-414](syllabus-fde-focused/fde-focused-6-projects-opensource.md:406) (playbook is internal); no visibility statement anywhere
- **Project/task:** 6.6
- **Exact issue:** The role brief states the commercial mechanism plainly: *"manufacture auditable evidence: a client component in every project, public reference architectures, a demo day"* and *"Five public, working things beat any testimonial we could print."* Neither document states repository visibility, requires a public write-up, or schedules a demo day. P6.6 produces a playbook with no audience.
- **Consequence:** The program builds the evidence and then does not publish it, forfeiting the only differentiator its target audience will accept.
- **Recommended correction:** Add a publication requirement to 6.6 with sensitive-content rules already implied by that task.
- **Proposed replacement wording:** *"Publish the sanitised capstone repository, a reference-architecture write-up, and the discovery-to-handback playbook to a public portfolio, using synthetic data only and with all scenario role-card content removed. Present the engagement at the cohort demo day. The portfolio index links all five artefacts."*
- **Workload effect:** +4 hours in 6.6 (reduce 6.5 by 2 under I-5 to hold 60).

### I-9 — Nothing simulates parallel clients or context switching

- **Severity:** Important
- **File/line:** Program structure: six strictly sequential single-client engagements
- **Project/task:** Program-wide
- **Exact issue:** The role brief names context switching as the job — *"I work with 10–15 clients in parallel"* — lists it as the 4th-most-cited pain (6 of 14 threads), and flags candidates who *"want deep focus on one problem for weeks"* as the profile that "will be miserable regardless". The program is six consecutive months of exactly that.
- **Consequence:** Graduates are unrehearsed in the single most-cited day-to-day reality, and the program cannot honestly claim to prepare them for it.
- **Recommended correction:** Overlap one engagement without adding hours.
- **Proposed replacement wording:** Add to the delivery contract: *"One overlap is required: a Project 2 client escalation arrives during Project 3 weeks 9–10 as a timed inject. Students triage it against their Project 3 commitments, respond to the Project 2 stakeholder, and record the trade-off. Six hours of Project 3's Task 3.4 allocation cover this; no new hours are added."*
- **Workload effect:** Neutral (reallocates within 3.4).

### I-10 — Facilitation and live-response skills are claimed but assessed only asynchronously

- **Severity:** Important
- **File/line:** [opensource.md:237](syllabus-fde-focused/fde-focused-6-projects-opensource.md:237) ("workshop facilitation") vs [:238](syllabus-fde-focused/fde-focused-6-projects-opensource.md:238) ("asynchronous workshop injects"); [tree:146](syllabus-fde-focused/fde-focused-6-project-tree.md:146) ("Facilitate a simulated workshop") and [tree:252](syllabus-fde-focused/fde-focused-6-project-tree.md:252) ("Facilitate a simulated enablement session with resistant or skeptical users") vs [opensource.md:393](syllabus-fde-focused/fde-focused-6-projects-opensource.md:393) ("Respond to skeptical-user questions through a deterministic recorded simulation")
- **Project/task:** 4.1, 6.4, 6.5
- **Exact issue:** Facilitation is a real-time skill — reading a room, interrupting a derail, closing a decision. It cannot be evidenced by analysing injects. The role brief's four required rehearsals are explicitly live: *"A discovery sprint with a live stakeholder who withholds information, changes their mind, and controls a budget"* and *"The live interview drill — narrating a solution while the constraints keep changing. The exact format candidates report failing."*
- **Consequence:** The program's async design removes the exact rehearsal the market tests and candidates report failing, while still claiming the skill. This is the sharpest tension between the pedagogy and the target role.
- **Recommended correction:** Keep grading async and deterministic; add two required-but-ungraded live drills.
- **Proposed replacement wording:** Amend the delivery contract: *"Grading is asynchronous and deterministic. Two live drills are required for completion but are not graded and produce no rubric score: a 45-minute discovery sprint with a live stakeholder who withholds information and changes priorities (Project 1), and a 30-minute constraints-change drill in the live-interview format (Project 6). Both are attendance-and-participation gates; the assessable evidence remains the written and recorded artefacts."* Change 4.1's skill to "workshop design and synthesis" and 6.4's to "enablement material design".
- **Workload effect:** +2 hours total; requires instructor scheduling capacity for two sessions per student.

### I-11 — Eleven (open-source) to thirteen (LocalStack) either/or tool choices break determinism

- **Severity:** Important
- **File/line:** [opensource.md:51](syllabus-fde-focused/fde-focused-6-projects-opensource.md:51), [:68](syllabus-fde-focused/fde-focused-6-projects-opensource.md:68), [:78](syllabus-fde-focused/fde-focused-6-projects-opensource.md:78), [:148](syllabus-fde-focused/fde-focused-6-projects-opensource.md:148), [:188](syllabus-fde-focused/fde-focused-6-projects-opensource.md:188), [:198](syllabus-fde-focused/fde-focused-6-projects-opensource.md:198), [:258](syllabus-fde-focused/fde-focused-6-projects-opensource.md:258), [:370](syllabus-fde-focused/fde-focused-6-projects-opensource.md:370), [:380](syllabus-fde-focused/fde-focused-6-projects-opensource.md:380); plus [localstack.md:77](syllabus-fde-focused/fde-focused-6-projects-localstack.md:77), [:137](syllabus-fde-focused/fde-focused-6-projects-localstack.md:137), [:147](syllabus-fde-focused/fde-focused-6-projects-localstack.md:147)
- **Project/task:** Program-wide
- **Exact issue:** "Jaeger or Tempo", "Toxiproxy or supplied failure injector", "Tenacity or supplied resilience library", "Presidio or supplied redactor", "notebooks or supplied reporting script", "CloudFormation or OpenTofu", "Secrets Manager or SSM", "Cost Explorer or supplied budget report", "transcript or stakeholder bot", "AWS CLI or awslocal", "Ollama or optional local vLLM".
- **Consequence:** Each fork doubles the instructor support surface and the number of environments the verifier must handle, and makes submissions non-comparable — the opposite of the determinism claim.
- **Recommended correction:** Pin one of each in the assessed path; list the alternative as optional exploration only.
- **Proposed replacement wording:** Add to the delivery contract: *"The assessed toolchain is pinned to exactly one implementation per capability: Tempo for traces, the supplied failure injector, the supplied resilience library, the supplied redactor, the supplied reporting script, the supplied launch templates, SSM Parameter Store, the supplied budget report, fixed transcripts, `awslocal`, and Ollama. Named alternatives are optional exploration and are never assessed."*
- **Workload effect:** −4 to −6 hours of student decision and setup overhead; large reduction in support cost.

### I-12 — Several services do not earn their learning cost

- **Severity:** Important
- **File/line:** OpenSearch: [opensource.md:15](syllabus-fde-focused/fde-focused-6-projects-opensource.md:15), [:138](syllabus-fde-focused/fde-focused-6-projects-opensource.md:138). OpenBao: [:17](syllabus-fde-focused/fde-focused-6-projects-opensource.md:17), [:258](syllabus-fde-focused/fde-focused-6-projects-opensource.md:258), used for one bullet at [:261](syllabus-fde-focused/fde-focused-6-projects-opensource.md:261). RabbitMQ: [:16](syllabus-fde-focused/fde-focused-6-projects-opensource.md:16), [:191](syllabus-fde-focused/fde-focused-6-projects-opensource.md:191) ("only where … requires"). LocalStack DynamoDB: [localstack.md:14](syllabus-fde-focused/fde-focused-6-projects-localstack.md:14) vs [:139](syllabus-fde-focused/fde-focused-6-projects-localstack.md:139). LocalStack KMS/IAM: [:17](syllabus-fde-focused/fde-focused-6-projects-localstack.md:17), [:270](syllabus-fde-focused/fde-focused-6-projects-localstack.md:270), [:28](syllabus-fde-focused/fde-focused-6-projects-localstack.md:28). Lambda/EventBridge/API Gateway: [:16](syllabus-fde-focused/fde-focused-6-projects-localstack.md:16)
- **Project/task:** 2.3, 3.2, 4.3
- **Exact issue:** OpenSearch is a 2–3 GB JVM service used by one task, for BM25 that Postgres full-text search provides adequately in a hybrid-retrieval teaching context. OpenBao is a full secrets platform for one configuration change. RabbitMQ is declared as core environment then made conditional. DynamoDB is described as optional at line 14 and mandated at line 139 — a direct contradiction — and adds a second data model for no FDE outcome when Postgres is already present. KMS "exercised through the assessed API subset" against an emulator produces no verifiable security outcome. IAM APIs are declared while enforcement is explicitly not graded — teaching a non-outcome. Lambda, EventBridge, and API Gateway appear in the stack list and in **zero tasks** (verified by grep).
- **Consequence:** Roughly 20–30 hours of setup and concept load across both variants buying little or no assessable learning, plus the RAM pressure behind C3.
- **Recommended correction:** Remove OpenSearch (use Postgres FTS with a supplied `tsvector` configuration), remove OpenBao (use the supplied secrets scaffold plus Gitleaks), make RabbitMQ/SQS required with one assessed DLQ evidence artefact or remove it, remove DynamoDB, KMS and IAM from the LocalStack variant, and delete Lambda/EventBridge/API Gateway from line 16.
- **Workload effect:** −8 hours (OpenSearch), −5 (OpenBao), −6 (DynamoDB/KMS/IAM), −2 (orphan services). Funds I-7 and I-8.

### I-13 — Ragas judged by a local model cannot produce the deterministic CI evidence the task requires

- **Severity:** Important
- **File/line:** [opensource.md:328-332](syllabus-fde-focused/fde-focused-6-projects-opensource.md:328); [localstack.md:337-341](syllabus-fde-focused/fde-focused-6-projects-localstack.md:337)
- **Project/task:** 5.4 (18 hours)
- **Exact issue:** The task requires "deterministic CI smoke evaluations using cached fixtures" and Ragas in the same 18 hours. Ragas' quality metrics are themselves LLM-judged; run against local Ollama they are noisy run-to-run, and run against a hosted model they consume the $20 allowance that Project 6 needs. Five surfaces (Ragas, Phoenix, OpenTelemetry, Pytest, judge worksheet) sit in one task.
- **Consequence:** Students will produce unstable numbers and cannot tell instability from regression — the opposite of the lesson. Determinism claim fails at the one task that most depends on it.
- **Recommended correction:** Split deterministic from judged evaluation explicitly.
- **Proposed replacement wording:** *"CI evaluation uses the supplied deterministic metric script (exact-match, schema validity, tool-sequence conformance, recall@k, refusal and escalation rates) over cached fixtures; it must be bit-reproducible. Ragas and the LLM-as-judge sample are used once, manually, on a fixed 20-case sample, and their variance across three runs must be reported alongside their scores. Neither may gate CI. Phoenix is used for trace inspection only."*
- **Workload effect:** −4 hours in 5.4 and removes an unbudgeted API-spend path.

### I-14 — The LocalStack variant drops "explain remaining gaps" from Task 4.3

- **Severity:** Important
- **File/line:** [opensource.md:262](syllabus-fde-focused/fde-focused-6-projects-opensource.md:262) vs [localstack.md:271](syllabus-fde-focused/fde-focused-6-projects-localstack.md:271)
- **Project/task:** 4.3
- **Exact issue:** Open-source: "Test published and held-out attack and data-leakage scenarios; **explain remaining gaps**." LocalStack: the same sentence with the gap-explanation clause replaced by the IAM caveat. The residual-gap reasoning is silently lost in the variant that most needs it.
- **Consequence:** An unintended learning-outcome divergence in a security task, in the direction of weaker evidence discipline.
- **Recommended correction / wording:** Restore the clause: *"…; explain remaining gaps. Application authorization is graded; LocalStack IAM policy enforcement is not, and no local result may be presented as evidence of AWS authorization behaviour."*
- **Workload effect:** Neutral.

### I-15 — The LocalStack variant adds assessed work to Tasks 5.3 and 4.3 without adding hours

- **Severity:** Important
- **File/line:** [localstack.md:329](syllabus-fde-focused/fde-focused-6-projects-localstack.md:329) (SQS async tool path, 24 h — same as [opensource.md:320](syllabus-fde-focused/fde-focused-6-projects-opensource.md:320)); [localstack.md:270](syllabus-fde-focused/fde-focused-6-projects-localstack.md:270) (SSM/Secrets Manager move plus KMS exercise, 30 h — same as [opensource.md:261](syllabus-fde-focused/fde-focused-6-projects-opensource.md:261) "one secrets improvement")
- **Project/task:** 4.3, 5.3
- **Exact issue:** Two tasks gained deliverables in the LocalStack variant and neither gained an hour. This is the same defect the prior LocalStack analysis identified ("Every project gained an AWS service surface and a second SDK; no project gained an hour") and it has recurred unchanged.
- **Consequence:** The LocalStack variant's 440 total is arithmetically valid and substantively false.
- **Recommended correction:** Either remove the additions (preferred, per I-12) or publish per-project displacement. Do not publish the hour table unchanged.
- **Workload effect:** +6 to +10 hours unaccounted in P4/P5 alone.

### I-16 — Every `[Skills]` line is byte-identical across the two variants

- **Severity:** Important
- **File/line:** All 31 `[Skills]` lines; the diff shows zero changes to any of them
- **Project/task:** All
- **Exact issue:** The LocalStack variant demonstrably teaches AWS SDK client construction, endpoint and credential configuration, and AWS service-contract usage; the open-source variant teaches AMQP broker semantics, S3-compatible object storage, and Vault-family secret operations. Neither is reflected in any skills line.
- **Consequence:** The skills taxonomy — the thing rubrics and marketing will be generated from — does not describe either program, and the parity claim cannot be checked against it.
- **Recommended correction:** Rewrite the skills line for every task where the tool line differs between variants (1.2, 1.3, 2.2, 2.3, 3.2, 4.3, 5.3, 5.4, 6.2), naming the actual competency.
- **Workload effect:** None on students.

### I-17 — Tree-to-syllabus drift on five substantive points

- **Severity:** Important
- **File/line:** [tree:109](syllabus-fde-focused/fde-focused-6-project-tree.md:109) vs [opensource.md:181](syllabus-fde-focused/fde-focused-6-projects-opensource.md:181); [tree:117](syllabus-fde-focused/fde-focused-6-project-tree.md:117); [tree:85](syllabus-fde-focused/fde-focused-6-project-tree.md:85); [tree:235](syllabus-fde-focused/fde-focused-6-project-tree.md:235) vs [opensource.md:370](syllabus-fde-focused/fde-focused-6-projects-opensource.md:370); [tree:259](syllabus-fde-focused/fde-focused-6-project-tree.md:259) vs [opensource.md:403](syllabus-fde-focused/fde-focused-6-projects-opensource.md:403)
- **Exact issue:** (a) The tree makes vLLM the primary path with a "grading-equivalent Ollama fallback"; both syllabi make Ollama the common path. "Grading-equivalent" is also false for Project 3, which grades latency and SLO behaviour under load — vLLM and Ollama have materially different throughput profiles. (b) Kafka/Redpanda appear in the tree as optional extensions and in neither syllabus. (c) Cache freshness and replication appear in the tree's 2.3 and in neither syllabus. (d) Launch templates became CloudFormation/OpenTofu (see C5). (e) "Respond live" became recorded (see C13).
- **Consequence:** No document is authoritative; three sources will be cited selectively during authoring.
- **Recommended correction:** Designate one document as normative and regenerate the tree from it. Delete "grading-equivalent": *"Ollama is the assessed path for every learner. Local vLLM is optional exploration; because its throughput and latency profile differs materially from Ollama's, no SLO, load, or latency evidence may be produced from a vLLM run."*
- **Workload effect:** None.

### I-18 — Local-to-AWS migration realism is inverted between the variants, and neither is priced

- **Severity:** Important
- **File/line:** [opensource.md:371](syllabus-fde-focused/fde-focused-6-projects-opensource.md:371) vs [localstack.md:380](syllabus-fde-focused/fde-focused-6-projects-localstack.md:380); both at 18 hours
- **Project/task:** 6.2
- **Exact issue:** The open-source variant's migration is five genuine adapter swaps (MinIO→S3, RabbitMQ→SQS, OpenBao→Secrets Manager, keyword tier, identity) — which is exactly the work an FDE does — but it is handed over as "supplied AWS bindings", removing the learning, and still costed at 18 hours. The LocalStack variant's migration is an endpoint-URL and credential swap, which is cheap but teaches almost nothing, and it omits every real failure mode: IAM role and resource policies (never exercised, explicitly ungraded), KMS key policies, VPC and security-group reachability, throttling and 429 handling, and eventual consistency. Both variants therefore state the migration too simply, which is the "API availability implies parity" implication the LocalStack fidelity boundary at [:29](syllabus-fde-focused/fde-focused-6-projects-localstack.md:29) exists to prevent — contradicted 350 lines later by line 380.
- **Consequence:** The one place either variant's local-infrastructure choice pays off is the one place the program has the least time, and neither variant converts it into assessed learning.
- **Recommended correction:** Add an explicit assessed migration-delta artefact to 6.2 in both variants.
- **Proposed replacement wording:** *"Produce a migration-delta record: for every local service, name its AWS counterpart, the configuration that changed, the IAM or resource policy the local environment did not require, and one failure mode that only appears in AWS (throttling, eventual consistency, policy denial, or network reachability). Demonstrate at least one such failure occurring and being handled. Local evidence may not be cited as evidence of AWS performance, durability, or authorization behaviour."*
- **Workload effect:** +4 hours in 6.2 (fund from I-3's supplied deploy script).

### I-19 — Security and governance evidence limits are stated in one task and nowhere else

- **Severity:** Important
- **File/line:** [opensource.md:231](syllabus-fde-focused/fde-focused-6-projects-opensource.md:231) (dev-mode Keycloak and OpenBao), [:280](syllabus-fde-focused/fde-focused-6-projects-opensource.md:280); [localstack.md:240](syllabus-fde-focused/fde-focused-6-projects-localstack.md:240), [:270](syllabus-fde-focused/fde-focused-6-projects-localstack.md:270), [:289](syllabus-fde-focused/fde-focused-6-projects-localstack.md:289)
- **Project/task:** Project 4, 4.4, 4.5
- **Exact issue:** Controls are built on development-mode identity, development-mode secrets, an emulated KMS, and ungraded IAM. The only place this is acknowledged is 4.5's "Respond to pressure to describe educational evidence as production certification" — a good instinct, but it is a rehearsal, not a stated boundary. The project title is "Governance **Approval**" and its evidence list includes "executive decision" with no scope qualifier.
- **Consequence:** Graduates and marketing will overstate what a green control matrix built on dev-mode services demonstrates.
- **Recommended correction:** Add an evidence-limits line to the Project 4 header and require it in the control matrix.
- **Proposed replacement wording:** *"**Evidence boundary:** all controls are implemented against development-mode identity and secret stores and emulated key management. Evidence demonstrates control *design and integration*, not production hardening, key custody, or authorization enforcement. Every row of the control matrix must state what its test does and does not prove. No artefact from this project may be described as a security assessment, audit, or certification."*
- **Workload effect:** +1 hour in 4.4.

### I-20 — The $20 LLM allowance is unallocated, unmetered, and has no custody model

- **Severity:** Important
- **File/line:** [opensource.md:7](syllabus-fde-focused/fde-focused-6-projects-opensource.md:7), [:352](syllabus-fde-focused/fde-focused-6-projects-opensource.md:352), [:362](syllabus-fde-focused/fde-focused-6-projects-opensource.md:362); [localstack.md:7](syllabus-fde-focused/fde-focused-6-projects-localstack.md:7), [:361](syllabus-fde-focused/fde-focused-6-projects-localstack.md:361)
- **Project/task:** 5.4, 6.1, 6.2, 6.3
- **Exact issue:** The cap appears three times and is never allocated. No project owns it, no model is named, no token ceiling is set, no metering is specified, and there is no custody statement (program-issued key with a hard provider-side limit versus a student's own account). Meanwhile 5.4's Ragas and LLM-as-judge work and Project 6's API-backed endpoint both plausibly draw on it.
- **Consequence:** Either an unpriced overrun or a student paying with a personal card — which [syllabus/project-5-aws-deployment.md:15](syllabus/project-5-aws-deployment.md:15) explicitly forbids for AWS and should equally forbid here.
- **Recommended correction / wording:** *"**Approved API allowance ($20 total):** $5 for Project 5 manual evaluation and judge calibration; $15 for Project 6 endpoint operation, held-out scenario runs, and defense traffic. Projects 1–4 use no hosted API. The program issues one metered key per student on the named approved model with a provider-side hard spend limit; students never use personal accounts or payment methods. Exceeding the allowance stops the key and requires instructor approval to resume."*
- **Workload effect:** None.

---

# Minor findings

| # | File/line | Issue | Correction |
|---|---|---|---|
| M1 | [opensource.md:78](syllabus-fde-focused/fde-focused-6-projects-opensource.md:78) vs [tree:42](syllabus-fde-focused/fde-focused-6-project-tree.md:42) | Tree says "Run one **deterministic** load and provider-latency scenario"; both syllabi say "one **bounded** load" — the determinism qualifier is lost on the load scenario. | Restore: "one bounded, deterministic load and provider-latency scenario". |
| M2 | [opensource.md:51](syllabus-fde-focused/fde-focused-6-projects-opensource.md:51) vs [:111](syllabus-fde-focused/fde-focused-6-projects-opensource.md:111), [:171](syllabus-fde-focused/fde-focused-6-projects-opensource.md:171), [:291](syllabus-fde-focused/fde-focused-6-projects-opensource.md:291) | Redis is in P1 and then silently absent from P2, P3 and P5 environments, though the repository is continuous. | State per-project environments as *deltas* on a continuous stack, or list carried-forward services explicitly. |
| M3 | [opensource.md:352](syllabus-fde-focused/fde-focused-6-projects-opensource.md:352) | "normal delivery should target materially below the ceiling" is unquantified, where [syllabus/project-5-aws-deployment.md:31](syllabus/project-5-aws-deployment.md:31) gives a specific $80 target. | State the number: "normal target $70; $40 remediation reserve; $70 contingency; $180 hard cap." |
| M4 | [opensource.md:353](syllabus-fde-focused/fde-focused-6-projects-opensource.md:353) | "recommended pilot allowance" is planning language inside a student-facing contract. | Remove with the GPU thread (C6); otherwise state a hard per-student ledger. |
| M5 | [localstack.md:29](syllabus-fde-focused/fde-focused-6-projects-localstack.md:29) | "Each project publishes its assessed subset and known limitations" — no project's evidence list contains a `FIDELITY.md`, and no task allocates time to reading it. | Add `FIDELITY.md` to every project's "Project evidence" line and require students to cite it in the P4 control matrix and the P6 migration-delta record. |
| M6 | [localstack.md:26](syllabus-fde-focused/fde-focused-6-projects-localstack.md:26) | "Students create and control individual accounts and tokens" — never states whether a token is actually required for the assessed service subset, or what a student does if signup is unavailable in their region. | Specify: which services need a token, and the open-source fallback for any student who cannot obtain one. |
| M7 | [opensource.md:9](syllabus-fde-focused/fde-focused-6-projects-opensource.md:9) | "basic cloud concepts" in the admission gate is untestable as written. | Replace with a named, checkable competency (e.g. "can explain IAM roles, VPC subnets, and object versus block storage, and has deployed at least one service to a public cloud"). |
| M8 | [opensource.md:404](syllabus-fde-focused/fde-focused-6-projects-opensource.md:404), [:281](syllabus-fde-focused/fde-focused-6-projects-opensource.md:281) | "Obtain a simulated accept, conditional-accept, or reject decision" never says who issues it or against what rule, so the outcome is reviewer judgment. | Publish decision rules mapping evidence thresholds to each outcome, so the decision is derived rather than opined. |
| M9 | [opensource.md:20](syllabus-fde-focused/fde-focused-6-projects-opensource.md:20) | "students are not asked to build a general cloud platform" is a negative scope statement; the positive boundary is never given. | State what students *do* build in AWS (the fixed profile from C4). |
| M10 | [tree:269](syllabus-fde-focused/fde-focused-6-project-tree.md:269) | A stray `|` after Task 6.6 breaks the ASCII tree's indentation. | Remove. |
| M11 | [executive-overview.md:39](executive-overview.md:39) | Still lists "Fine-Tuning" as FDE P5 core, contradicting both new documents and the 0-of-41-postings evidence. | Remove when C6 is applied. |

---

# Cross-variant parity audit

| Project/task | Open-source outcome | LocalStack outcome | Equivalent | Required correction |
|---|---|---|---|---|
| Contract / fidelity framing | Portable-interface reasoning; must explain translation limits ([:41](syllabus-fde-focused/fde-focused-6-projects-opensource.md:41)) | Explicit fidelity boundary; may not claim performance/IAM/durability parity ([:22-29](syllabus-fde-focused/fde-focused-6-projects-localstack.md:22), [:50](syllabus-fde-focused/fde-focused-6-projects-localstack.md:50)) | **No** — LS is stronger here | Port an equivalent boundary section to the open-source variant covering MinIO≠S3, RabbitMQ≠SQS, dev-Keycloak≠Cognito |
| 1.2 Runtime orientation | 8 services; no AWS surface | +LocalStack container, +`awslocal`/AWS CLI, but zero assessed AWS activity ([:78](syllabus-fde-focused/fde-focused-6-projects-localstack.md:78)) | **No** | Remove LocalStack from P1 (C10) |
| 1.3 Seeded failure diagnosis | Real metric/trace sources | +LocalStack CloudWatch as a metrics source in a performance-diagnosis task ([:87](syllabus-fde-focused/fde-focused-6-projects-localstack.md:87)) | **No** — LS is a fidelity violation | Remove; add the no-performance-conclusions rule (C10) |
| 2.2 Ingestion | MinIO object storage; Postgres state | LocalStack S3 + **mandated** DynamoDB state ([:139](syllabus-fde-focused/fde-focused-6-projects-localstack.md:139)), contradicting [:14](syllabus-fde-focused/fde-focused-6-projects-localstack.md:14) | **No** — LS adds a data model | Remove DynamoDB; use Postgres for state in both |
| 2.3 Hybrid retrieval | Real OpenSearch BM25 — real ranking and analyzer behaviour | "assessed LocalStack OpenSearch API subset" ([:148](syllabus-fde-focused/fde-focused-6-projects-localstack.md:148)) | **No** | Standardise both on Postgres FTS (I-12); state the BM25 limitation identically |
| 3.2 Provider resilience | RabbitMQ: exchanges, routing, ack/nack, DLX | SQS: polling, visibility timeout, at-least-once, DLQ; +SNS decoratively ([:200](syllabus-fde-focused/fde-focused-6-projects-localstack.md:200)) | **No** — different concepts, LS simpler | Pin one required async concept set and one assessed DLQ evidence artefact for both; drop SNS |
| 4.3 Secrets | "one secrets improvement" via OpenBao | "Move one secret into SSM or Secrets Manager, exercise KMS" — two extra deliverables at the same 30 h ([:270](syllabus-fde-focused/fde-focused-6-projects-localstack.md:270)) | **No** | Remove KMS; equalise to one assessed secret migration plus Gitleaks in both |
| 4.3 Residual gaps | "explain remaining gaps" ([:262](syllabus-fde-focused/fde-focused-6-projects-opensource.md:262)) | Clause dropped ([:271](syllabus-fde-focused/fde-focused-6-projects-localstack.md:271)) | **No** | Restore (I-14) |
| 4.x Authorization enforcement | Keycloak dev-mode RBAC at the app layer | Same, plus IAM APIs whose enforcement is explicitly ungraded ([:28](syllabus-fde-focused/fde-focused-6-projects-localstack.md:28)) | **No** — LS teaches a non-outcome | Remove IAM from the LS stack; treat it as a P6 real-AWS topic in both |
| 5.3 Agent implementation | LangGraph + retrieval + limits (24 h) | Same + "use LocalStack SQS for the … asynchronous tool path" (24 h) ([:329](syllabus-fde-focused/fde-focused-6-projects-localstack.md:329)) | **No** — extra work, same hours | Remove the SQS requirement or add 3 hours and displace them |
| 5.4 Eval and observability | Ragas + Phoenix + OTel | Same + LocalStack CloudWatch APIs ([:337](syllabus-fde-focused/fde-focused-6-projects-localstack.md:337)) with no activity using them | **No** | Remove the orphan CloudWatch entry; apply I-13 to both |
| 6.2 Migration work | Five real adapter swaps, "supplied AWS bindings" (18 h) | Endpoint-URL and credential swap (18 h) | **No** — same hours, very different work and learning | Add the migration-delta artefact to both (I-18); re-cost |
| 1.1, 1.4, 1.5, 2.1, 2.4, 2.5, 3.1, 3.3, 3.4, 3.5, 4.1, 4.2, 4.4, 4.5, 5.1, 5.2, 5.5, 6.1, 6.3, 6.4, 6.5, 6.6 | Identical text | Identical text | **Yes** (21 of 31 tasks) | None |
| Declared-but-unused services | None | Lambda, EventBridge, API Gateway in the stack list; zero tasks ([:16](syllabus-fde-focused/fde-focused-6-projects-localstack.md:16)) | **No** | Delete from line 16 |
| `[Skills]` taxonomy | Unchanged | Byte-identical to open-source across all 31 tasks | **No** — parity is asserted, not described | Rewrite skills lines wherever tool lines differ (I-16) |

**Net:** 21 of 31 tasks are genuinely equivalent. Ten diverge, and **all ten divergences favour the open-source variant** on either fidelity, hour honesty, or learning value. The two documents are not currently pedagogically equivalent, and the divergence is not confined to the infrastructure path.

---

# Workload audit

**Stated arithmetic — verified correct in all three documents.**

| Project | Task sum | Weeks × 20 | Match |
|---|---:|---:|:--:|
| P1 | 14+10+18+10+8 = 60 | 60 | ✓ |
| P2 | 12+20+24+14+10 = 80 | 80 | ✓ |
| P3 | 18+20+18+12+12 = 80 | 80 | ✓ |
| P4 | 12+18+30+12+8 = 80 | 80 | ✓ |
| P5 | 12+10+24+18+16 = 80 | 80 | ✓ |
| P6 | 8+18+12+8+8+6 = 60 | 60 | ✓ |
| **Program** | **440** | **440** | ✓ |

The arithmetic is sound. The estimates are not.

**Realistic re-estimate**

| Project | Stated | Realistic (OS) | Realistic (LS) | Principal driver |
|---|---:|---:|---:|---|
| P1 | 60 | 72–80 | 76–84 | 1.2 first-run orchestration and 4-tool observability in 10 h (I-1) |
| P2 | 80 | 92–100 | 98–108 | 2.3 hybrid fusion and CPU reranking; 2.2 held-out re-runs |
| P3 | 80 | 88–94 | 90–96 | 3.1 Ollama/model pulls; 3.2 async recovery path |
| P4 | 80 | 96–108 | 102–116 | 4.3 (I-2) — the single worst task |
| P5 | 80 | 92–100 | 96–106 | 5.4 Ragas/Phoenix (I-13); cross-project integration (C8) |
| P6 | 60 | 80–95 | 78–92 | 6.2 first real deployment (I-3); recordings |
| **Total** | **440** | **520–577** | **540–602** | **+18% to +37%** |

**Hidden hours, none of which appear as a task**

| Hidden work | OS | LS |
|---|---:|---:|
| Week-0 environment, toolchain, WSL2/Docker, hardware remediation | 8–12 | 10–14 |
| Image pulls, embedding and inference model downloads, first-run waits | 4–6 | 5–8 |
| Recorded defenses and retakes (≈11 recordings) | 12–18 | 12–18 |
| Cross-project integration into the P5 capstone (if multi-repo) | 10–20 | 10–20 |
| Code-review response cycles across six submissions | 8–12 | 8–12 |
| LocalStack surface (prior analysis: +27, unchanged in the new doc) | — | 25–30 |
| **Total hidden** | **42–68** | **70–102** |

**What must be removed or scaffolded to hold 440**

| Action | Reference | Δ hours |
|---|---|---:|
| Remove OpenSearch; use Postgres FTS with a supplied configuration | I-12 | −8 |
| Remove OpenBao; supplied secrets scaffold + Gitleaks | I-12 | −5 |
| Remove GPU and PEFT/LoRA thread entirely | C6 | −6 |
| Supply Keycloak realm and CI workflow fully configured | I-2 | −9 |
| Supply RRF, index mappings, cross-encoder wrapper | I-4 | −5 |
| Supply one-command AWS deploy script | I-3 | −10 |
| Replace Ragas-in-CI with a supplied deterministic metric script | I-13 | −4 |
| Pin one tool per capability (eliminate 11–13 either/or forks) | I-11 | −5 |
| Pre-built, pre-pulled pinned images; reduced compose profiles | C3 | −8 |
| Reduce graded recordings from ~11 to 5 | I-5 | −10 |
| **Subtotal removed/scaffolded** | | **−70** |
| Add Task 3.6 undocumented legacy integration | I-7 | +10 |
| Add public portfolio and demo day to 6.6 | I-8 | +4 |
| Add migration-delta artefact to 6.2 | I-18 | +4 |
| Add two live drills | I-10 | +2 |
| **Net change to assessed hours** | | **−50** |

**Conclusion.** With every scaffolding action above applied, the open-source variant lands near 470–500 realistic hours against a 440 nominal envelope. Close the remaining gap by adding an unassessed **Week 0 (10 hours)** and rebalancing P1 (1.1 → 10 h, 1.2 → 14 h), and by cutting ~20 hours of Project 4 breadth — Project 4 remains the least defensible allocation at 80 hours with a 30-hour implementation task. The **LocalStack variant cannot hold 440 at all** without publishing the ~27-hour displacement its predecessor document explicitly required and this one omits.

---

# Tooling audit

### Open-source variant

| Category | Items |
|---|---|
| **Required (assessed)** | Docker Compose, Python, FastAPI, PostgreSQL + pgvector, Redis, Alembic, Pytest, MinIO, supplied PDF/HTML parser, local embedding model, supplied cross-encoder, Ollama, LangGraph, Pydantic, OpenTelemetry, Prometheus, Grafana, one tracing backend, k6, Semgrep, Trivy, Gitleaks, Git/PR, AWS CLI (P6 only) |
| **Should be supplied / pre-configured** | Keycloak realm+clients+roles (I-2); CI security workflow; provider emulator; failure injector; resilience library; PII redactor; RRF + index mappings + cross-encoder wrapper (I-4); deterministic metric script (I-13); scenario packs ×6 published + ×6 held-out; flawed AI artefact; course verifier; teardown script; launch templates; DNS zone + Caddy TLS profile (C5); pre-built pinned images (C3); `deploy.sh` (I-3) |
| **Optional (never assessed)** | local vLLM, notebooks, Toxiproxy, OpenTofu, Cost Explorer UI, stakeholder chatbot (unassessed practice only, C13) |
| **Should be removed** | OpenSearch (I-12), OpenBao (I-12), all 11 either/or forks reduced to one each (I-11), GPU/PEFT thread (C6), RabbitMQ unless made required with assessed DLQ evidence |
| **Fidelity / hardware risks** | No stated hardware floor (C3); MinIO≠S3 (no bucket policies, no versioning semantics, no consistency behaviour), RabbitMQ≠SQS (different delivery semantics), dev-mode Keycloak≠production OIDC, dev-mode OpenBao≠production secret custody — **none of these is stated anywhere**, unlike the LocalStack variant which does state its boundary. CPU cross-encoder reranking latency will dominate P2.3 on low-end hardware. |

### LocalStack variant

| Category | Items |
|---|---|
| **Required (assessed)** | Everything above, plus LocalStack, `awslocal`, AWS SDK (boto3), LocalStack S3, SQS + DLQ, SSM Parameter Store, Secrets Manager, and selected CloudWatch APIs |
| **Should be supplied / pre-configured** | All of the above, plus: deterministic LocalStack initialisation scripts (line 28 assumes them), the shared AWS client factory and the CI lint gate that enforces it (C11), and a per-project `FIDELITY.md` (M5) |
| **Optional (never assessed)** | Same as open-source |
| **Should be removed** | DynamoDB (contradiction at [:14](syllabus-fde-focused/fde-focused-6-projects-localstack.md:14) vs [:139](syllabus-fde-focused/fde-focused-6-projects-localstack.md:139)); KMS (no verifiable outcome against an emulator); IAM APIs (enforcement ungraded); SNS (decorative); Lambda, EventBridge, API Gateway (**zero tasks** — verified); plain AWS CLI (C11); LocalStack from P1 entirely (C10); LocalStack OpenSearch (I-12) |
| **Fidelity / hardware risks** | Highest-risk stack in either document. Emulated performance must never ground a conclusion — violated in P1.3 (C10). IAM policy evaluation is approximate and ungraded, so the security project's authorization learning is app-layer only. LocalStack's OpenSearch provider starts a real JVM search process inside an already-oversubscribed container budget (C3). Third-party account, token and ToS dependency with no fallback (C9, M6). Real-AWS spend leak via plain AWS CLI plus missing enforcement controls (C11). |

---

# AWS budget and GPU assessment

**Is $180 achievable? Yes — with roughly 2× headroom, but only if the controls in C4 and C5 are restated. As written, it is not enforceable.**

Planning estimate for one 14-day window, `us-east-1` Linux on-demand, under the fixed profile recommended in C4:

| Item | Assumption | Amount |
|---|---|---:|
| Application host | `t3.large`, 336 h @ ~$0.0832 | $28 |
| Application host (16 GB alternative) | `t3.xlarge`, 336 h @ ~$0.1664 | *$56* |
| gp3 volume | 40 GiB retained 21 days | $3 |
| Public IPv4 | 1 address, 336 h @ $0.005 | $2 |
| ECR | capped storage and retention | $1 |
| CloudWatch logs | capped retention, synthetic payloads | $3 |
| Secrets/SSM | 2 parameters | $1 |
| **Normal target (t3.large profile)** | | **≈$38** |
| Contingency: data transfer, metering lag, price variance | | $32 |
| **Recommended normal target** | | **$70** |
| **Remediation reserve — one re-deploy (C7)** | | **$40** |
| **Unallocated headroom** | | **$70** |
| **Hard cap** | | **$180** |

This aligns with the repository's own $80 normal target at [syllabus/project-5-aws-deployment.md:31](syllabus/project-5-aws-deployment.md:31) and is comfortable — *provided* the capstone fits one t3.large. Under the six-project scope it may not: the P5 capstone carries a keyword search tier, an identity service, and a tracing UI on top of the application, database and worker. Hence C4's requirement to publish a fixed profile that drops Phoenix, Prometheus, Grafana and Keycloak from the cloud deployment.

**The overrun paths the documents leave open**

| Path | 14-day cost | Blocked by C4/C5? |
|---|---:|---|
| NAT gateway | +$15 plus data | Yes, once the prohibition list is restated |
| Application Load Balancer | +$8 plus LCU | Yes |
| Amazon OpenSearch Service `t3.small.search` | +$12 | Yes |
| Amazon OpenSearch Service `r5.large.search` | +$60 | Yes |
| RDS `db.t3.medium` Multi-AZ | +$46 | Yes |
| `t3.xlarge` instead of `t3.large` | +$28 | Requires the fixed profile |
| Teardown missed by 16 days | +$40–70 | Only by course-automation teardown |
| Second full deployment after a failed review | +$38–56 | Only by the C7 remediation reserve |
| Forgotten `g5.xlarge` over a weekend (60 h @ $1.006) | +$60 | Only by a 4-hour auto-stop and nightly sweep |

Any two of these together exhaust the cap. All of them were controlled in [syllabus/project-5-aws-deployment.md:41-43](syllabus/project-5-aws-deployment.md:41) and none are controlled in the new documents, whose sole cost mechanism is "AWS budget dashboard" ([opensource.md:360](syllabus-fde-focused/fde-focused-6-projects-opensource.md:360)).

**The 14-day window.** Incompatible with a 21-day project under asynchronous review with mandatory teardown (C7). Recommended precise boundary: *14 consecutive days of reviewer access, beginning at first verified endpoint, which must occur no later than the end of week 21; reviewer turnaround 3 business days; one instructor-approved remediation redeployment inside the same window or a single 5-day extension, drawing on the $40 reserve; a second window is a resubmission requiring program approval.*

**The protected endpoint.** "Configure trusted TLS" ([opensource.md:372](syllabus-fde-focused/fde-focused-6-projects-opensource.md:372)) is unachievable without a program-owned domain. Restate the canonical model: program-owned DNS zone, one hostname per student, supplied Caddy profile with TLS-ALPN-01, HTTPS-only ingress, no public SSH, Session Manager for administration, a unique reviewer token scoped to the window, 30 requests/minute, 128 KiB bodies.

**GPU: recommend zero hours.** The 4–8 hour allowance is optional, unassessed, hour-less, ledger-less, rubric-less, and points at a deliverable (LoRA) that Project 6 never authorises (C6). Against that, the role brief records fine-tuning in **zero of 41 postings**. If the program nonetheless retains a GPU: cap at 6 hours per student on `g4dn.xlarge` (~$3.20), hard ledger, program-initiated start only, mandatory 4-hour in-account stop action, nightly sweep, temporary disks deleted per session, and one assessed evidence artefact with a rubric line. Otherwise remove it and recover the operating cost, the quota-management risk, and $4–60 of variance.

---

# FDE role evaluation

Assessed against the role brief's five artefacts and four rehearsals, assuming the critical findings are fixed. "Defensible" means a graduate could survive a hostile technical interview on it.

| Competency | Evidence produced | Verdict |
|---|---|---|
| **Discovery** | 1.1 discovery record, 2.1 data discovery, 4.1 security discovery, 5.1 workflow discovery — four distinct discovery reps with conflicting stakeholders. Matches the brief's "traced workflow" artefact and "teach domain discovery, never the domains." | **Strong.** The program's best-designed competency. Weakened only by C13 (bot non-determinism) and I-10 (async-only). |
| **Scoping and SoW** | 2.5 full SoW with exclusions; 5.2 value hypothesis with rollback and override conditions; 3.4 and 5.5 change control with impact analysis. Both scope *rejection* reps are explicit ("Defend what will not be built"). | **Strong.** Directly matches the brief's "scoping defence: estimate it, cut scope out loud, and hold the line." |
| **Stakeholder management** | Stakeholders across six projects: domain, data owner, compliance, security, engineering, business, executive, resistant users. | **Adequate, structurally limited.** All simulations are single-client, sequential, and asynchronous. No parallel-client rep (I-9), no live rep (I-10), and "facilitation" is claimed but never performed. |
| **Delivery under ambiguity** | 5.1 vague brief with an assumption log; 3.4 and 5.5 mid-flight requirement changes; timed injects throughout. | **Adequate.** Ambiguity is scripted and therefore bounded — which is the necessary price of determinism, but it means the graduate has rehearsed *responding* to ambiguity, not *sitting in* it. |
| **Technical ownership** | Repaired seeded failure with before/after evidence; ADRs; runbooks; six end-to-end submissions. | **Strong**, conditional on C8. If the repository is not continuous, "end to end" is not demonstrated. |
| **Production AI integration** | Hybrid retrieval with reranking and authorization propagation; provider adapter; resilience patterns; bounded LangGraph flow with schema validation, budgets, and a human checkpoint; audit trail. | **Strong.** This matches four of the brief's five artefacts, including "unhappy-path hardening" and "an agent with an audit trail". **Missing: "an integration into legacy … against an undocumented system with real permissions and limits"** (I-7) — the fifth artefact does not exist. |
| **Evaluation and observability** | Golden query set; retrieval metrics with error attribution; agent scenario set covering success, refusal, escalation and recovery; CI smoke evals; trace and cost analysis; judge calibration. | **Strong** once I-13 is applied. Without it, the CI numbers are unstable and the lesson inverts. Fully matches the brief's "eval suite … a before-and-after that proves behaviour instead of asserting it." |
| **Security and governance** | STRIDE model; app-layer OIDC/RBAC; prompt-injection and output controls; PII redaction; audit logging; CI gates; control matrix; residual-risk register; adversarial review of a flawed AI artefact; executive risk decision. | **Adequate but must be bounded.** Built on dev-mode identity and secrets, emulated key management, and (LocalStack) explicitly ungraded IAM. The *reasoning* is defensible; the *hardening* is not. Requires I-19's evidence boundary. |
| **Adoption and handback** | Operator runbook, user guidance, escalation map, known-limitations register, enablement simulation, post-launch measures, reusable playbook, product feedback. | **Strong on paper.** 6.4 has 8 hours for five deliverables plus a recorded enablement session — the thinnest allocation relative to scope in the program. |
| **Technical and executive defense** | 4.5 executive risk decision; 5.5 dual-room; 6.5 dual-room plus a constraints-change inject. Three separate two-audience reps. | **Strong in design, weakest in format.** The brief names *"The live interview drill — narrating a solution while the constraints keep changing. The exact format candidates report failing."* The program converts precisely this to a recorded response ([opensource.md:403](syllabus-fde-focused/fde-focused-6-projects-opensource.md:403)) — removing the one rehearsal the market demonstrably tests. I-10's hybrid fixes it at a cost of 2 hours. |

**Overall:** the program would produce defensible evidence for eight of ten competencies and four of the brief's five artefacts. The two structural gaps are the legacy-integration artefact (I-7) and the live-format rehearsals (I-10). Both are cheap to fix and both are load-bearing for the market's stated hiring bar — two-thirds of postings want prior customer-facing work as proof, which is exactly what these artefacts and rehearsals are manufactured to substitute for.

---

# Action plan

Ten highest-priority edits, in implementation order.

1. **Add a status header to both documents** — top of [opensource.md](syllabus-fde-focused/fde-focused-6-projects-opensource.md) and [localstack.md](syllabus-fde-focused/fde-focused-6-projects-localstack.md), before "## Executive summary". Insert the C14 wording declaring them candidate proposals, naming the AGENTS.md 5-project/452-hour program of record and the executive-overview.md five-shared-repository dependency as prerequisites for adoption. *Nothing else should be authored until this decision is made.*
2. **Publish the Project 6 cloud deployment profile and restate the cost controls** — the "## Project 6" header block of both documents ([opensource.md:350-354](syllabus-fde-focused/fde-focused-6-projects-opensource.md:350), [localstack.md:359-363](syllabus-fde-focused/fde-focused-6-projects-localstack.md:359)). Insert the C4 fixed-profile paragraph and the C5 controls paragraph verbatim, and change "Supplied CloudFormation or OpenTofu templates" to "supplied launch templates" at [:370](syllabus-fde-focused/fde-focused-6-projects-opensource.md:370) / [:379](syllabus-fde-focused/fde-focused-6-projects-localstack.md:379). Add the C7 window wording and the M3 budget split.
3. **Delete the GPU and PEFT/LoRA thread** — [opensource.md:353](syllabus-fde-focused/fde-focused-6-projects-opensource.md:353), [:322](syllabus-fde-focused/fde-focused-6-projects-opensource.md:322), [:374](syllabus-fde-focused/fde-focused-6-projects-opensource.md:374); [localstack.md:362](syllabus-fde-focused/fde-focused-6-projects-localstack.md:362), [:331](syllabus-fde-focused/fde-focused-6-projects-localstack.md:331), [:383](syllabus-fde-focused/fde-focused-6-projects-localstack.md:383); [tree:204-205](syllabus-fde-focused/fde-focused-6-project-tree.md:204), [tree:238](syllabus-fde-focused/fde-focused-6-project-tree.md:238). Apply the C6 replacement wording. Update [projects/project-5-rubric.md:9](projects/project-5-rubric.md:9) and [executive-overview.md:39](executive-overview.md:39) to match.
4. **State the hardware floor and add Week 0** — new subsection after each executive summary. Insert the C3 wording, then add the I-1 Week-0 block and rebalance P1 (1.1 → 10 h at [opensource.md:54](syllabus-fde-focused/fde-focused-6-projects-opensource.md:54), 1.2 → 14 h at [:64](syllabus-fde-focused/fde-focused-6-projects-opensource.md:64), and the LocalStack equivalents).
5. **Declare the single continuous repository and the capstone release tag** — the "## Program delivery contract" bullet at [opensource.md:39](syllabus-fde-focused/fde-focused-6-projects-opensource.md:39) / [localstack.md:48](syllabus-fde-focused/fde-focused-6-projects-localstack.md:48). Apply the C8 wording, including the Project 4 remediation gate before the Project 6 local gate.
6. **Fix the determinism contract** — [opensource.md:9](syllabus-fde-focused/fde-focused-6-projects-opensource.md:9) / [localstack.md:9](syllabus-fde-focused/fde-focused-6-projects-localstack.md:9) (stakeholder bot → unassessed practice), then add the acceptance-floor sentence from C13 to Tasks 2.4, 3.3 and 5.2, add the I-11 pinned-toolchain bullet to the delivery contract, and add the I-10 live-drill paragraph. Reconcile [tree:259](syllabus-fde-focused/fde-focused-6-project-tree.md:259) with [opensource.md:403](syllabus-fde-focused/fde-focused-6-projects-opensource.md:403).
7. **Cut the tool surface** — remove OpenSearch from [opensource.md:15](syllabus-fde-focused/fde-focused-6-projects-opensource.md:15), [:111](syllabus-fde-focused/fde-focused-6-projects-opensource.md:111), [:138-139](syllabus-fde-focused/fde-focused-6-projects-opensource.md:138) and the LocalStack equivalents; remove OpenBao from [:17](syllabus-fde-focused/fde-focused-6-projects-opensource.md:17), [:231](syllabus-fde-focused/fde-focused-6-projects-opensource.md:231), [:258](syllabus-fde-focused/fde-focused-6-projects-opensource.md:258); in the LocalStack variant remove DynamoDB ([:14](syllabus-fde-focused/fde-focused-6-projects-localstack.md:14), [:120](syllabus-fde-focused/fde-focused-6-projects-localstack.md:120), [:137](syllabus-fde-focused/fde-focused-6-projects-localstack.md:137), [:139](syllabus-fde-focused/fde-focused-6-projects-localstack.md:139)), KMS and IAM ([:17](syllabus-fde-focused/fde-focused-6-projects-localstack.md:17), [:240](syllabus-fde-focused/fde-focused-6-projects-localstack.md:240), [:267](syllabus-fde-focused/fde-focused-6-projects-localstack.md:267), [:270](syllabus-fde-focused/fde-focused-6-projects-localstack.md:270)), SNS ([:200](syllabus-fde-focused/fde-focused-6-projects-localstack.md:200)), and delete Lambda, EventBridge and API Gateway from [:16](syllabus-fde-focused/fde-focused-6-projects-localstack.md:16).
8. **Add acceptance evidence to all 31 tasks** — apply the C1 pattern task by task. Author `projects/project-N-rubric.md` for N=1..6 on the model of [projects/project-5-rubric.md](projects/project-5-rubric.md). Add the I-19 evidence boundary to the Project 4 header and the M8 decision rules to Tasks 4.5, 6.3 and 6.5.
9. **Close the two FDE-competency gaps** — add Task 3.6 (I-7 wording, 10 hours) to Project 3 in both documents and adjust P3's total; add the I-8 publication requirement and the I-18 migration-delta artefact to Task 6.6 / 6.2; add the I-9 overlap bullet to the delivery contract. Rewrite the `[Skills]` lines for Tasks 1.2, 1.3, 2.2, 2.3, 3.2, 4.3, 5.3, 5.4 and 6.2 per I-16.
10. **Resolve or shelve the LocalStack variant** — replace [localstack.md:22-29](syllabus-fde-focused/fde-focused-6-projects-localstack.md:22) with the C9 conditional-status wording; remove LocalStack from Project 1 entirely (C10, lines 60, 77, 78, 87); replace "AWS CLI or `awslocal`" with `awslocal` at lines 77, 137 and 147 and add the four-part credential-safety control from C11; restore the dropped clause at line 271 (I-14); and either remove the added work at lines 270 and 329 or publish the ~27-hour displacement per project (C9, I-15). Do not republish its hour table until that displacement is in it.

---

# Recommendation

**Primary version: the open-source variant.** Not because it is complete — it is not — but because every one of its defects is an omission that can be added, whereas the LocalStack variant's defects include a legal precondition it cannot resolve itself, a fidelity violation this repository had already identified and prohibited, a real-money credential leak in week 1, and two silently-overridden findings ($470/student and +27 hours) from the prior evaluation of the same approach. Ten of the eleven substantive parity divergences favour the open-source path on fidelity, hour honesty, or learning value.

The decisive argument is structural: LocalStack's advertised benefit — a cheap, realistic local-to-AWS migration — is realised in exactly one 18-hour task at the very end of the program, while its cost is paid in all five local projects (an extra container, an extra SDK, an extra CLI, an extra failure surface, ~27 unbudgeted hours, and a third-party account dependency). And the benefit it does deliver is the wrong one: an endpoint-URL swap teaches less about real migration than the open-source variant's five genuine adapter swaps, which is what forward-deployed engineers actually do. LocalStack optimises the one thing the program should keep hard.

**Retain the alternative — yes, but demote it.** Keep [fde-focused-6-projects-localstack.md](syllabus-fde-focused/fde-focused-6-projects-localstack.md) as a documented conditional alternative with the C9 status header, for two reasons: its fidelity-boundary section ([:22-29](syllabus-fde-focused/fde-focused-6-projects-localstack.md:22), [:50](syllabus-fde-focused/fde-focused-6-projects-localstack.md:50)) is better than anything in the open-source document and should be ported across immediately; and if a future enterprise partnership or a LocalStack education agreement changes the licensing and cost picture, the design work is preserved. Do not maintain it in parallel — it will drift, as the `[Skills]` lines already have.

**Before production authoring starts, five things must be resolved.** Each is a decision, not an edit, and none can be made inside these documents:

1. **Program of record.** Five projects at 452 hours ([AGENTS.md:5](AGENTS.md:5)) or six at 440? Both cannot be canonical, and the six-project structure breaks the five-shared-repository economics that [executive-overview.md:15-19](executive-overview.md:15) relies on for the entire build. Whoever owns that trade must price it before a single task is authored.
2. **The supplied-asset build.** Roughly 26–28 assets, including six held-out scenario packs and a course verifier, with no contract — and [AGENTS.md:108](AGENTS.md:108) records that the contract document was deleted and never replaced. Re-author it, then inventory and price the assets. Nothing about either variant's cost or timeline is knowable until this exists.
3. **The hardware and environment floor.** 32 GB, 16 GB with a reduced profile, or a program-provided remote environment. This decision determines who can be admitted, what the compose profiles look like, and how much of the hidden 42–68 hours the program absorbs rather than the student.
4. **The Project 6 cloud profile and control plane.** Which services deploy, on what instance, with the constrained role, Budget Action, DNS zone and automated teardown from [syllabus/project-5-aws-deployment.md](syllabus/project-5-aws-deployment.md) restated. Until this exists, "$180 maximum" is a hope. With it, the realistic bill is ~$70 and the cap has genuine headroom.
5. **Live versus asynchronous assessment.** The determinism claim and the role brief's four rehearsals pull in opposite directions, and the tree and the syllabi already disagree ([tree:259](syllabus-fde-focused/fde-focused-6-project-tree.md:259) vs [opensource.md:403](syllabus-fde-focused/fde-focused-6-projects-opensource.md:403)). The recommended hybrid — deterministic async grading plus two required, ungraded live drills — costs two student hours and instructor scheduling capacity. That capacity has to be committed, or the program should stop claiming the facilitation and live-narration skills.

One further caution on marketing, since it follows directly from the source material rather than from these documents: the program cannot safely claim multi-agent systems (C12), production security hardening (I-19), production AWS operations experience, or fine-tuning capability. It also should not claim placement or salary outcomes — the role brief is explicit that salary-as-promise and unnamed testimonials lose this audience instantly, and that the market label itself covers four different jobs. What the program *can* claim, once the fixes above land, is five publicly checkable artefacts and a documented method — which the same brief identifies as the only currency this audience accepts.

Happy to turn this into a shareable artifact page, or to draft the exact replacement text for any of the ten action-plan items.