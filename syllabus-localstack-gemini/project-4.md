# Project 4 - Zero-Trust Security, LocalStack SSM/Secrets & AI Governance

## Project Description

Students harden one core platform workflow and add a grounded AI feature using a local model or deterministic provider emulator through a provider adapter. They configure **LocalStack Base** (SSM Parameter Store and Secrets Manager) for secure API key and database credential storage locally, complete one STRIDE threat model (focusing on AI and cloud IAM risks), evaluate local IAM least-privilege policies, apply RBAC to one endpoint, configure one CI security gate, add AI Output Guardrails (`Guardrails AI` with PII redaction and hallucination checks), and log CloudWatch audit events to LocalStack CloudWatch Logs. Educational control mapping covers EU AI Act and HIPAA-style safeguards.

## Skills

- Build and defend a STRIDE threat model for one real platform workflow (emphasizing Prompt Injection, Cloud IAM abuse, and Data Poisoning).
- Store, retrieve, and rotate API Keys and secrets using **LocalStack SSM Parameter Store & Secrets Manager** with `boto3`.
- Write and evaluate local IAM least-privilege JSON policies (`AssumeRole`, S3 bucket policies, KMS key policies) using LocalStack, and state where local evaluation diverges from the real AWS policy engine.
- Apply zero-trust principles, OIDC/RBAC, scopes, and least privilege to one endpoint.
- Configure one CI security gate for secrets (Gitleaks), dependencies (Trivy), or pipeline hardening.
- Defend against OWASP LLM Top 10 vulnerabilities (Prompt Injection, Insecure Output Handling, Sensitive Information Disclosure).
- Add a grounded AI feature with output guardrails (`Guardrails AI`), PII redaction, CloudWatch audit logging, request limits, and token limits.
- Map EU AI Act and HIPAA-style controls as educational engineering evidence.
- Audit an AI-generated threat and compliance draft for missing controls, overclaims, and weak reasoning.

## Tech Setup

- Secured version of the platform from Projects 1–3.
- Docker Compose scaffold with **LocalStack Base** (SSM Parameter Store, Secrets Manager, IAM, and CloudWatch Logs services).
- Dex or Keycloak dev-mode container with seeded users, roles, and token examples.
- OIDC/RBAC middleware scaffold for one endpoint.
- Python `boto3` integration with LocalStack for SSM parameter resolution (`ssm.get_parameter`) and secret retrieval (`secretsmanager.get_secret_value`).
- Local IAM policy test scripts verifying least-privilege access rules locally, each annotated with the AWS policy-engine features it does **not** exercise.
- Shared `boto3` client factory with sentinel credentials and injected `endpoint_url`, carried forward from Projects 1–3.
- CI security checks such as Gitleaks, Trivy, dependency scanning, or gated deployment.
- Local LLM or deterministic provider-emulator adapter, with Guardrails AI scaffold.
- PII redaction scaffold, request audit log stream pushing to LocalStack CloudWatch Logs, and request/token controls.
- STRIDE template, compliance-control matrix, security review template, and audit-evidence template.
- Seeded flawed AI STRIDE/compliance artifact, expected-issue list, and review rubric.

## Learning Objectives

- Identify realistic threats across users, cloud pipelines, local secrets, and AI features (OWASP LLM Top 10 & STRIDE).
- Manage API keys and credentials using LocalStack SSM Parameter Store and Secrets Manager instead of raw `.env` files or hardcoded strings.
- Evaluate IAM least-privilege policies locally using `boto3` and LocalStack, and articulate why a local pass is necessary but not sufficient evidence of correct authorization.
- Implement identity, access, and secrets controls without production cloud identity cluster overhead.
- Add one CI security check that fails unsafe changes early.
- Protect LLM API calls with PII redaction, LocalStack CloudWatch audit logging, prompt injection mitigation, and cost/request limits.
- Translate EU AI Act and HIPAA-style requirements into educational control mapping and simulated audit evidence.
- Defend privacy, security, cloud IAM, and governance trade-offs in a grounded AI feature.

## Theory Topics

- Threat modeling, STRIDE for AI, zero-trust architecture, and trust boundaries.
- Secrets management, safe runtime configuration, LocalStack SSM Parameter Store & Secrets Manager.
- AWS IAM basics: Principals, Actions, Resources, Least-Privilege JSON Policies, and `AssumeRole`.
- Identity, access control, OIDC, RBAC, scopes, and least privilege.
- Pipeline security, dependency scanning, secret scanning, and deployment gates.
- Compliance by design, simulated audit evidence, redaction, BAA boundaries, and safeguards.
- EU AI Act classification, transparency, human oversight, and control mapping.
- AI governance, CloudWatch audit logging, grounded AI risks, and technical communication.
- OWASP LLM Top 10: Prompt Injection Mitigation & Red-Teaming.
- Output Guardrails (`Guardrails AI` default), Hallucination Checks & PII Redaction.

## Delivery Limits

- Compliance work is educational control mapping, not legal readiness or certification.
- Production AWS Vault or enterprise IAM cluster operations are not required; LocalStack SSM/Secrets Manager provides the local emulation layer.
- **IAM evaluation is approximate and must be taught as such.** LocalStack does not fully replicate the AWS policy engine across condition keys, resource policies, permission boundaries, and SCPs. A policy that passes locally can behave differently in AWS. Students must accompany each policy with a short note naming what local evaluation did not verify; the rubric grades policy *reasoning and least-privilege intent*, not the emulator's allow/deny verdict alone. Presenting a local pass as production-ready authorization is a rubric failure. Real-AWS authorization behavior is first observed in Project 5 via the course verifier and least-privilege instance profile.
- **Open tier dependency:** LocalStack Base advertises *basic* IAM policy enforcement; *advanced* IAM policy testing is an Ultimate feature. This project grades `AssumeRole`, S3 bucket policies, and KMS key policies, which may exceed "basic". Verify against the current LocalStack feature matrix before the cohort is priced — if Ultimate is required, the per-student license line roughly doubles. If only Base is available, reduce the graded IAM scope to policy authoring and reasoning and drop enforcement-verdict grading rather than silently grading against an unsupported feature.
- Sentinel credentials and the injected `endpoint_url` are mandatory; bypassing the client factory is a CI failure. The Gitleaks gate this project configures must also cover the LocalStack license credential.
- No cloud deployment or public endpoint is permitted; the graded AI path uses the local model or deterministic provider emulator with LocalStack. Paid provider use is an ungraded extension and does not consume the Project 5 API allowance.
- Students complete one STRIDE workflow, protect one RBAC endpoint, retrieve secrets via LocalStack SSM/Secrets Manager, configure one CI security gate, and add one grounded AI guardrail boundary.
- Default tools are mandatory for grading: `Guardrails AI` must be explicitly chosen as the single default in the final repository scaffold (`NeMo Guardrails` permitted as fallback only).
- The identity dev setup, LocalStack parameter initializer, STRIDE template, compliance matrix, security gate scaffold, grounded AI adapter, flawed AI artifact, expected issues, and rubric must be provided before launch.

## Workload

| Field | Hours |
| :--- | ---: |
| Theory time | 20.75 |
| Project work time | 62 |
| Workload calc | 82.75 |

⚠️ **Pending re-cost.** These hours are inherited from the canonical program. This edition adds an estimated **+6 hours** (SSM Parameter Store, Secrets Manager, IAM policy evaluation, CloudWatch Logs). At 82.75 hours across 4 weeks this is 20.7 h/wk. See [Workload Impact](overview-and-module-map.md#workload-impact-pending-re-cost).
