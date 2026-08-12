# Codex Review: PR1 P5 Cloud Capstone

## Review Scope

Reviewed branch `feature/p5-cloud-capstone` at commit `0f3a0df` against `origin/main` at `a41d2dd`. PR1 changes four documentation files and contains no executable code or automated tests.

## Findings

- **High: The local-first policy remains internally contradictory.** PR1 changes the headline policy to require a cloud capstone ([`AGENTS.md`](../AGENTS.md)), but the existing contributor rule still says every core task must run locally without paid cloud infrastructure or GPU dependencies ([`AGENTS.md`](../AGENTS.md)). The syllabus README also retains the rule that every core project path runs locally ([`README.md`](README.md)). The PR needs one authoritative definition of the local/cloud boundary.

- **High: The `$200` budget is double-allocated.** PR1 assigns it to the six-week EC2 deployment ([`project-5.md`](project-5.md)), while the hardware policy still describes the same budget as an external API fallback ([`AGENTS.md`](../AGENTS.md)). Project 5 also permits OpenAI/Anthropic APIs ([`project-5.md`](project-5.md)). The PR does not provide a cost model or clarify whether API usage is separately funded.

- **High: The public endpoint has no documented security baseline.** PR1 requires deploying a multi-agent tool system to the public web ([`AGENTS.md`](../AGENTS.md), [`project-5.md`](project-5.md)), but does not specify mandatory TLS, authentication, network restrictions, rate limits, secret handling, abuse controls, data retention, or teardown requirements. This is especially important because the system executes tools and exposes model-backed behavior.

- **Medium: The cloud-capstone change is not propagated to the module map or executive overview.** PR1 updates `AGENTS.md`, the syllabus README, Project 5, and the teaching document, but the Project 5 section in [`overview-and-module-map.md`](overview-and-module-map.md) does not list cloud deployment, and [`executive-overview.md`](../executive-overview.md) still describes the FDE track primarily as Docker Compose and local-LLM delivery.

- **Medium: Defense duration is inconsistent.** The general teaching document says every project requires a 3-5 minute Loom ([`teaching-and-submission-models.md`](../competitors/teaching-and-submission-models.md)), while Project 5 requires a 15-minute defense ([`project-5.md`](project-5.md)). PR1 adds a Project 5 public-cloud exception but does not update the duration rule.

- **Medium: Student cloud operations are underspecified.** PR1 names `AWS EC2 g4dn.xlarge` but does not define the AWS account model, region, quota process, IAM permissions, deployment procedure, persistent storage, endpoint lifecycle, monitoring, or automatic shutdown. Without those details, a six-week live deployment is not yet a reproducible student workflow.

- **Low: The root sitemap still references the removed legacy sprint file.** This is not introduced by PR1, but the branch still leaves the stale path in [`AGENTS.md`](../AGENTS.md) while PR1 modifies that file.

## What PR1 Does Well

- It makes the intended Project 5 cloud-capstone direction explicit instead of leaving it as optional positioning.
- It separates local delivery for Projects 1-4 from the cloud deployment requirement for Project 5.
- It identifies a concrete deployment target and allocates a program budget for the capstone environment.
- It updates the client-demo guidance to require the live public endpoint for Project 5.

## Verdict

**Request changes.** Resolve the policy and budget contradictions, define the minimum public-cloud security and operations baseline, and propagate the final cloud-capstone contract through all authoritative syllabus documents before merging.
