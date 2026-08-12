# Project 4 - Zero-Trust Security, Guardrails & Governance

## Project Description

Students harden one core platform workflow and add a narrow grounded AI feature using a local model or deterministic provider emulator through a provider adapter. They complete one STRIDE threat model (focusing on AI risks), apply RBAC to one endpoint, configure one CI security gate, make one secrets-management improvement, add AI Output Guardrails (PII redaction, hallucination checks), and produce educational control mapping for EU AI Act and HIPAA-style safeguards. A paid provider path is optional and ungraded until Project 5.

## Skills

- Build and defend a STRIDE threat model for one real platform workflow (emphasizing Prompt Injection and Data Poisoning).
- Apply zero-trust principles, OIDC/RBAC, scopes, and least privilege to one endpoint.
- Manage API Keys and secrets securely.
- Configure one CI security gate for secrets, dependencies, or pipeline hardening.
- Defend against OWASP LLM Top 10 vulnerabilities (Prompt Injection, Insecure Output Handling).
- Add a grounded AI feature with output guardrails, PII redaction, audit logging, request limits, and token limits.
- Map EU AI Act and HIPAA-style controls as educational engineering evidence.
- Audit an AI-generated threat and compliance draft for missing controls, overclaims, and weak reasoning.

## Tech Setup

- Secured version of the platform from Projects 1-3.
- Dex or Keycloak dev-mode container with seeded users, roles, and token examples.
- OIDC/RBAC middleware scaffold for one endpoint.
- Kubernetes Secrets plus OpenBao or Vault dev server for secrets-management concepts (Positioning).
- CI security checks such as Gitleaks, Trivy, dependency scanning, or gated deployment.
- Local LLM or deterministic provider-emulator adapter, with Guardrails AI scaffold.
- PII redaction scaffold, request audit log, prompt/response fixture cache, and request/token controls.
- STRIDE template, compliance-control matrix, security review template, and audit-evidence template.
- Seeded flawed AI STRIDE/compliance artifact, expected-issue list, and review rubric.

## Learning Objectives

- Identify realistic threats across users, pipelines, and AI features (OWASP LLM).
- Implement identity, access, and secrets controls without production identity-cluster operations.
- Add one security check that fails unsafe changes early.
- Protect LLM API calls with redaction, logging, prompt injection mitigation, and cost/request limits.
- Translate EU AI Act and HIPAA-style requirements into educational control mapping and simulated audit evidence.
- Defend privacy, security, and governance trade-offs in a grounded AI feature.
- Produce a security and simulated compliance package that an engineering reviewer can inspect.

## Theory Topics

- Threat modeling, STRIDE for AI, zero-trust architecture, and trust boundaries.
- Identity, access control, OIDC, RBAC, scopes, and least privilege.
- Secrets management and safe runtime configuration.
- Pipeline security, dependency scanning, secret scanning, and deployment gates.
- Compliance by design, simulated audit evidence, redaction, BAA boundaries, and safeguards.
- EU AI Act classification, transparency, human oversight, and control mapping.
- AI governance, grounded AI risks, security gaps, and technical communication.
- OWASP LLM Top 10: Prompt Injection Mitigation & Red-Teaming.
- Output Guardrails, Hallucination Checks & PII Redaction.

## Delivery Limits

- Compliance work is educational control mapping, not legal readiness or certification.
- Production Vault or Keycloak operations are not required.
- No cloud deployment or public endpoint is permitted; the graded AI path uses the local model or deterministic provider emulator. Paid provider use is an ungraded extension and does not use the Project 5 API allowance.
- Students complete one STRIDE workflow, protect one RBAC endpoint, configure one CI security gate, make one secrets improvement, and add one grounded AI guardrail boundary.
- Default tools are mandatory for grading: `Guardrails AI` must be explicitly chosen as the single default in the final repository scaffold (`NeMo Guardrails` permitted as fallback only).
- Any optional paid-provider experiment must have request/token limits, cached fixtures, and audit logging.
- The identity dev setup, STRIDE template, compliance matrix, security gate scaffold, grounded AI adapter, flawed AI artifact, expected issues, and rubric must be provided before launch.

## Submission & Assessment Criteria

- **Automated Tests**: CI pipeline must pass (Gitleaks, dependency scanning, guardrail unit tests).
- **Required Artifacts**: PR containing the RBAC implementation, the Guardrails AI configuration, and the completed STRIDE threat model.
- **Client Defense**: A 5-minute Loom video demonstrating a prompt injection attempt being successfully blocked and redacted by the AI guardrails.
- **Pass/Fail Rubric**: Must be explicitly supplied in the `projects/` directory, defining Must-Have criteria for the STRIDE threat model and guardrail accuracy.

## Workload

| Field | Hours |
| :--- | ---: |
| Theory time | 20.75 |
| Project work time | 62 |
| Workload calc | 82.75 |
