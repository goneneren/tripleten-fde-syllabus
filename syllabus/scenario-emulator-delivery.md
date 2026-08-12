# Scenario Emulator Delivery Contract

## Purpose

The delivery repositories use deterministic scenario emulators to make Projects 1-4 fully local, role-realistic, and gradeable without paid APIs or student cloud resources. Project 5 local acceptance uses the same scenarios before the separate protected AWS deployment.

This planning repository does not implement emulator images. The required images, scenarios, tests, and grader integration must exist in the student delivery repositories before the affected project launches.

## Required v1 Components

### Enterprise Emulator

The enterprise emulator exposes local customer-system surfaces that expand across the program:

- P1-P2: messy documents, duplicate identifiers, slow listings, and malformed source files.
- P2: deeply nested records with optional fields and synthetic PII in free-text fields.
- P3-P4: token expiry, `429` responses with `Retry-After`, and partial-write outcomes.
- P5: delayed analytics queries, result truncation, and stale-read behavior.

### Provider Emulator

The provider emulator exposes an OpenAI/Anthropic-shaped local API with deterministic latency, rate limits, malformed tool calls, truncated streams, refusals, outages, and token accounting. It is the required CI and failure-lab provider for Projects 3-4 and the default no-cost path for local Project 5 development. It does not replace the bounded real API use required in the protected Project 5 AWS endpoint.

## Scenario-Pack Rules

- Scenario packs are declarative, versioned files: request matchers plus named fault directives.
- Given the same image version, pack version, and seed, behavior must be identical locally and in CI.
- Students receive published development packs. The course grader runs held-out packs that exercise the same public contract but are not distributed to students.
- Each emulator ships a `FIDELITY.md` describing its supported behavior, deliberate simplifications, version date, and escalation path for emulator defects.
- Emulator images are pinned, have their own test suite, and support the program's required operating systems before launch.

## Scope Boundary

The scenario suite emulates customer data-plane and provider failure behavior. It must not be the source of truth for IAM, security-group, quota, cost, TLS, or other cloud security semantics. Project 5 validates those controls in AWS. GPU fine-tuning and the scheduled vLLM demonstration also remain real bounded workloads.

`emu-aws` (LocalStack plus OpenTofu) is a later `[SUPPORTING]` or `[POSITIONING]` lab, not a v1 prerequisite and never a pass/fail substitute for real AWS security controls.

## Launch Preconditions

For every project using an emulator, the delivery repository must ship:

1. The pinned Docker image and one-command local Compose profile.
2. Published scenario packs, held-out grading packs, deterministic seeds, and expected outcomes.
3. Emulator tests, `FIDELITY.md`, and an instructor escalation procedure.
4. Rubric assertions tying required learner behavior to scenario outcomes.

For P5, the course verifier additionally confirms the separate AWS security, cost, and teardown contract in [`projects/project-5-rubric.md`](../projects/project-5-rubric.md).
