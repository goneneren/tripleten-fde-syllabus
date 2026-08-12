# Project 5 - Autonomous Multi-Agent Platform, LocalStack Pre-Flight & AWS Defense

## Project Description

Students build and defend a complex autonomous AI system using paid/local LLM APIs as the required hands-on path. They implement advanced RAG with PostgreSQL, `pgvector`, keyword search, and cross-encoder reranking; complete a multi-agent LangGraph tool flow with LocalStack S3/SQS integrations; add tool sandboxing and a human checkpoint; execute `awslocal` pre-flight verification scripts against LocalStack; run CI evaluation cases; implement LLM-as-a-judge metrics via Ragas; fine-tune a model via PEFT/LoRA (Unsloth); add cost/latency telemetry; and deploy the locally accepted Docker Compose stack to a temporary protected AWS endpoint as a mandatory capstone requirement.

## Skills

- Define production readiness for an AI-enabled multi-agent system.
- Integrate OpenAI/Anthropic APIs or local models through a provider adapter with request and token limits.
- Build Hybrid RAG with LocalStack S3 document ingestion, PostgreSQL, `pgvector`, keyword search, and cross-encoder reranking.
- Design a multi-agent LangGraph tool flow with LocalStack SQS tool queues, sandboxing, step limits, and a human-in-the-loop checkpoint.
- Write and run `awslocal` pre-flight verification scripts against LocalStack to validate AWS parameter lookups and bucket setups locally prior to AWS deployment.
- Build CI-safe evaluation cases with cached prompt/response fixtures.
- Implement LLM-as-a-judge evaluation pipelines using Ragas.
- Perform PEFT/LoRA fine-tuning for a specialized task using Unsloth.
- Monitor quality signals, cost, latency, failures, and user-visible behavior using Arize Phoenix.
- Deploy the locally accepted Docker Compose stack to a temporary, protected AWS endpoint as a mandatory capstone delivery requirement.
- Apply a production-minded deployment boundary: TLS, application authentication, rate limits, least-privilege IAM access, secrets in AWS SSM Parameter Store outside Git, and a documented teardown.
- Defend model-serving, provider, architecture, safety, cloud deployment, and evaluation trade-offs.

## Tech Setup

- Secured version of the platform extending Project 4.
- Paid LLM API provider adapter for the protected AWS endpoint; vLLM for scheduled local/GPU model-serving evidence.
- LocalStack Base container for local development and `awslocal` pre-flight verification.
- PostgreSQL with `pgvector` plus simple keyword search and local cross-encoder for hybrid retrieval.
- LangGraph scaffold for multi-agent tool-execution flow.
- Tool-execution sandbox, step limits, token budgets, request budgets, and human-in-the-loop checkpoint pattern.
- Evaluation dataset with CI smoke cases, cached fixtures, and larger Ragas evaluation path.
- PEFT/LoRA fine-tuning scaffold (Unsloth) for a narrow specialized task.
- Cost/latency telemetry template and AI observability dashboard scaffold (Arize Phoenix).
- Seeded flawed AI eval artifact, expected-issue list, and review rubric.

## Learning Objectives

- Build an end-to-end AI system that satisfies production acceptance criteria.
- Use LocalStack locally for zero-friction local-to-cloud AWS parity (`awslocal` pre-flight script).
- Implement advanced Hybrid RAG that balances retrieval quality, latency, cost, and safety.
- Prevent prompt injection and unsafe tool execution with concrete controls in a multi-agent setup.
- Calibrate evals (LLM-as-a-Judge, Ragas) so failures are measurable, reproducible, and useful.
- Use PEFT/LoRA to adapt a base model to a specific enterprise domain task.
- Use telemetry to explain quality, cost, latency, and failure behavior across agent state graphs.
- Deploy to AWS within budget, defend the final architecture, rejected alternatives, provider choice, safety controls, eval gaps, cost reports, and remaining risks.

## Theory Topics

- Production definition of done, build kickoff, and final architecture review.
- LocalStack pre-flight validation vs. live AWS provisioning parity.
- Production LLM integration, provider adapters, API reliability.
- Advanced RAG as production architecture, `pgvector`, keyword retrieval, reranking, and grounding.
- Agentic frameworks, state graphs, tool sandboxing, and human oversight.
- Evaluation pipelines, LLM-as-judge calibration, CI smoke gates, cached fixtures, and failure coverage.
- PEFT Fine-Tuning (LoRA) for Specialized Tasks.
- AI observability (Arize Phoenix), cost telemetry, latency telemetry, portfolio readiness, and hostile defense preparation.

## Delivery Limits

- The re-estimated total per-student allocation for the LocalStack edition is $414.50: $214.50 for the 22-week LocalStack Base subscription ($39/mo $\times$ 5.5 mo), $20 maximum for approved LLM API calls, and $180 maximum for AWS infrastructure ($80 normal target). Each student receives one dedicated course-managed AWS sandbox in the fixed region; account, resource, and cost-allocation tags are required.
- The protected endpoint runs on a CPU instance (`t3.large`) for a 14-calendar-day assessment window. A `g4dn.xlarge` GPU is launched only through booked, program-controlled sessions for local model-serving evidence or fine-tuning and is stopped automatically after each session. It is not an always-on six-week host.
- The protected endpoint requires a program-issued hostname with a publicly trusted TLS certificate, per-reviewer authentication tokens, a maximum request body of 128 KiB, and a rate limit of 30 requests per minute per token. Its security group allows public HTTPS only; administration uses Session Manager, not public SSH. Secrets stay in managed SSM parameters or host configuration, never Git.
- The launch templates require IMDSv2, block container access to link-local instance metadata, use a least-privilege instance profile, and restrict application egress to approved provider and required AWS service endpoints. Application logs exclude prompts and secrets; trace/evaluation payloads use synthetic data, retain for at most seven days, and are deleted at teardown.
- The $180 planning estimate, deployment sequence, access model, monitoring, and teardown evidence are defined in [Project 5 AWS Deployment](project-5-aws-deployment.md).
- Default tools are mandatory for grading: `LocalStack` for local AWS pre-flight verification, `vLLM` for scheduled local/GPU model-serving evidence, `Arize Phoenix` for tracing, and `Unsloth` for fine-tuning must be explicitly chosen as single defaults in the repository scaffold.

## Submission & Assessment Criteria

- **Automated Tests**: CI pipeline must pass (LLM smoke evaluation gates, LocalStack pre-flight integration checks).
- **Required Artifacts**: PR containing the LangGraph multi-agent flow, the Ragas evaluation suite, held-out scenario results, LocalStack `awslocal` pre-flight log, protected AWS endpoint URL and access instructions for reviewers, scheduled vLLM evidence, a verifier report, a cost report, and teardown evidence.
- **Client Defense (Capstone)**: A 15-minute live or Loom video defense demonstrating the working application in the cloud, explaining the multi-agent architecture, interpreting the LLM-as-a-judge Ragas metrics, and justifying the model fine-tuning results.
- **Pass/Fail Rubric**: Must be explicitly supplied in the `projects/` directory, defining Must-Have criteria for the defense and evaluation metrics.

## Workload

| Field | Hours |
| :--- | ---: |
| Theory time | 25.5 |
| Local platform, scenario, and evaluation work time | 78.5 |
| AWS deployment, defense, and teardown work time | 16 |
| Workload calc | 120 |
