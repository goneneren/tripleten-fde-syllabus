# Project 5 Capstone Rubric

## Must-Have Criteria

| Area | Pass evidence |
| :--- | :--- |
| Local acceptance | The open PR has a green CI run, `docker compose up` succeeds, and the required local tests pass before AWS deployment. |
| Scenario resilience | The submission passes published scenario packs and the course grader's held-out enterprise/provider packs. |
| Model-serving evidence | The student supplies evidence from one scheduled vLLM session and documents the provider choice for the API-backed protected endpoint. |
| Protected endpoint | The course verifier confirms the program-issued hostname, publicly trusted TLS, reviewer authentication, 128 KiB request limit, 30 requests/minute/token limit, HTTPS-only ingress, and no public SSH. |
| Cloud security | The course verifier confirms required tags, IMDSv2, blocked container access to link-local metadata, least-privilege instance profile, approved application egress, secrets outside Git, and synthetic-only trace/evaluation data with seven-day retention. |
| Cost control | The course verifier confirms the dedicated sandbox, active cost-allocation tags, $144 actual-cost alert, $162 forecast alert, booked GPU shutdown control, and spend at or below the $20 API and $180 AWS caps. |
| Teardown | Within 14 calendar days of first reviewer access, the student and course automation remove instances, volumes, public IPv4, reviewer tokens, parameters, traces, and endpoint records. The verifier records completion timestamps. |
| Defense | The 15-minute defense demonstrates the protected endpoint, local and held-out scenario results, security controls, telemetry, cost report, model-serving evidence, and teardown plan. |

## Verification Model

Screenshots alone do not satisfy a cloud control. Before launch, the course platform must provide a read-only verifier role or automated verifier that produces an attached report for every listed cloud control.

An unapproved cost overrun or incomplete teardown is an incomplete submission until instructor remediation and verifier confirmation. The course-managed account remains the program's billing responsibility; students are not asked to use personal payment methods.
