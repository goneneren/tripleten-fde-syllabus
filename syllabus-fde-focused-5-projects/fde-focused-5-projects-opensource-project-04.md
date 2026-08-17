# Project 04 — Security, Guardrails and Governance Approval

## #

- 4

## Project

- Security, Guardrails and Governance Approval

## Project description 

- Students secure one high-value AI workflow and make the result inspectable by engineering, security, compliance, and business stakeholders. They select proportionate controls, implement one bounded security boundary, test it against held-out attacks, and obtain a documented go, conditional-go, or no-go decision without overstating what educational evidence proves.

## Skills

- Facilitate security discovery, reconcile stakeholder conflicts, map sensitive data and decision rights, and assign accountable risk owners.
- Create a STRIDE threat model with trust boundaries, abuse cases, prompt-injection analysis, and proportionate control selection.
- Integrate OIDC/RBAC, prompt and output controls, PII redaction, audit logging, Compose secrets, and a deterministic CI security gate.
- Test published and held-out attack/data-leakage scenarios and explain remaining gaps.
- Map risks, controls, tests, evidence, owners, residual risks, and human-oversight triggers in an inspectable control matrix.
- Translate technical risk for executives and facilitate an accountable decision while defending evidence boundaries.

## Tech setup

- Preconfigured development-mode Keycloak realm, FastAPI OIDC/RBAC scaffold, and file-mounted Docker Compose secrets.
- Supplied redactor, prompt/output guardrail boundary, audit log, deterministic attack scenarios, and Pytest.
- Pinned CI security workflow with Semgrep, Trivy, and Gitleaks.
- OpenTelemetry, stakeholder role cards, data-flow and STRIDE templates, OWASP LLM guidance, risk register, control matrix, and decision records.
- Supplied flawed AI-generated threat/compliance artifact for adversarial review and timed executive pressure inject.

## Learning Objectives

- Identify actors, sensitive data, trust boundaries, decision rights, risk tolerance, and accountable owners for one high-value workflow.
- Select the smallest proportionate control set based on material abuse cases and reject unnecessary complexity.
- Protect one endpoint and one AI boundary with identity, authorization, injection handling, output validation, redaction, auditability, and secret hygiene.
- Use deterministic CI and held-out scenarios to verify controls and disclose what the evidence does not prove.
- Detect overclaims and omissions in AI-generated governance artifacts and define residual risk and human oversight.
- Present value, risk, controls, remaining exposure, owners, conditions, and review date in the graded executive decision.

## Theory topics

- Security and governance discovery, risk ownership, treatment choices, decision rights, and stakeholder conflict reconciliation.
- STRIDE, assets, actors, trust boundaries, abuse cases, prompt injection, unsafe output handling, and control selection.
- OIDC, RBAC, least privilege, prompt/output guardrails, PII redaction, audit logging, secrets management, and CI security.
- Adversarial review, AI-output verification, evidence mapping, residual risk, limitations, and human-oversight design.
- Executive risk translation, accountability, go/conditional-go/no-go decisions, and boundary defense.
- Legal and compliance frameworks as engineering-control mapping rather than audit, certification, or legal advice.

## Delivery Limits

- Starts from TripleTen's reference solution to Project 3 in Repository 4; earlier student defects do not propagate.
- Runs and is graded locally against development services and supplied attacks; no cloud deployment or public endpoint is allowed.
- The project implements one bounded workflow security boundary, not production identity, key-custody, or security-platform operations.
- Evidence demonstrates educational control design and integration only; it does not prove production hardening, an audit, certification, or legal compliance.
- Each control-matrix entry must state both what its evidence proves and what it does not prove about AWS or production operation.
- The assessed path uses the supplied Keycloak, Compose-secret, redactor, CI, and security-scanner configurations.
- The executive risk defense is the project's single graded Instructor Presentation / Review recording.

## Theory time (25% allocation)

- 20
- Hours: 20

## Project work time (75% allocation)

- 60
- Hours: 60

## Workload calc

- Formula: `=I6+J6`
- Calculated total: 80 hours
- Allocation basis: 25% theory time and 75% project work time from the canonical project estimate.

Source: `syllabus-fde-focused-5-projects/fde-focused-5-projects-opensource.md`
