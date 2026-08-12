# Project 5 - Autonomous Multi-Agent Platform & Defense

## Project Description

Students build and defend a complex autonomous AI system using paid/local LLM APIs as the required hands-on path. They implement advanced RAG with PostgreSQL, `pgvector`, keyword search, and cross-encoder reranking; complete a multi-agent LangGraph tool flow; add sandboxing and a human checkpoint; run CI evaluation cases; implement LLM-as-a-judge metrics via Ragas; fine-tune a model via PEFT/LoRA (FDE specific); and add cost/latency telemetry. 

## Skills

- Define production readiness for an AI-enabled multi-agent system.
- Integrate OpenAI/Anthropic APIs or local models through a provider adapter with request and token limits.
- Build Hybrid RAG with PostgreSQL, `pgvector`, keyword search, and cross-encoder reranking.
- Design a multi-agent LangGraph tool flow with sandboxing, step limits, and a human-in-the-loop checkpoint.
- Build CI-safe evaluation cases with cached prompt/response fixtures.
- Implement LLM-as-a-judge evaluation pipelines using Ragas.
- Perform PEFT/LoRA fine-tuning for a specialized task.
- Monitor quality signals, cost, latency, failures, and user-visible behavior using Arize Phoenix.
- Deploy the locally accepted Docker Compose stack to a temporary, protected AWS endpoint as a mandatory capstone delivery requirement.
- Apply a production-minded deployment boundary: TLS, application authentication, rate limits, least-privilege access, secrets outside Git, and a documented teardown.
- Defend model-serving, provider, architecture, safety, and evaluation trade-offs.

## Tech Setup

- Secured version of the platform extending Project 4.
- Paid LLM API provider adapter for the protected AWS endpoint; vLLM for scheduled local/GPU model-serving evidence.
- PostgreSQL with `pgvector` plus simple keyword search and local cross-encoder for hybrid retrieval.
- LangGraph scaffold for multi-agent tool-execution flow.
- Tool-execution sandbox, step limits, token budgets, request budgets, and human-in-the-loop checkpoint pattern.
- Evaluation dataset with CI smoke cases, cached fixtures, and larger Ragas evaluation path.
- PEFT/LoRA fine-tuning scaffold (Unsloth) for a narrow specialized task.
- Cost/latency telemetry template and AI observability dashboard scaffold (Arize Phoenix).
- Seeded flawed AI eval artifact, expected-issue list, and review rubric.

## Learning Objectives

- Build an end-to-end AI system that satisfies production acceptance criteria.
- Implement advanced Hybrid RAG that balances retrieval quality, latency, cost, and safety.
- Prevent prompt injection and unsafe tool execution with concrete controls in a multi-agent setup.
- Calibrate evals (LLM-as-a-Judge, Ragas) so failures are measurable, reproducible, and useful.
- Use PEFT/LoRA to adapt a base model to a specific enterprise domain task.
- Use telemetry to explain quality, cost, latency, and failure behavior across agent state graphs.
- Defend the final architecture, rejected alternatives, provider choice, safety controls, eval gaps, and remaining risks.

## Theory Topics

- Production definition of done, build kickoff, and final architecture review.
- Production LLM integration, provider adapters, API reliability.
- Advanced RAG as production architecture, `pgvector`, keyword retrieval, reranking, and grounding.
- Agentic frameworks, state graphs, tool sandboxing, and human oversight.
- Evaluation pipelines, LLM-as-judge calibration, CI smoke gates, cached fixtures, and failure coverage.
- PEFT Fine-Tuning (LoRA) for Specialized Tasks.
- AI observability (Arize Phoenix), cost telemetry, latency telemetry, portfolio readiness, and hostile defense preparation.

## Delivery Limits

- The total per-student allocation is $200: $20 maximum for approved LLM API calls and $180 maximum for AWS. Each student receives one dedicated course-managed AWS sandbox in the fixed region; account, resource, and cost-allocation tags are required.
- The protected endpoint runs on a CPU instance for a 14-calendar-day assessment window. A `g4dn.xlarge` GPU is launched only through booked, program-controlled sessions for local model-serving evidence or fine-tuning and is stopped automatically after each session. It is not an always-on six-week host.
- The protected endpoint requires a program-issued hostname with a publicly trusted TLS certificate, per-reviewer authentication tokens, a maximum request body of 128 KiB, and a rate limit of 30 requests per minute per token. Its security group allows public HTTPS only; administration uses Session Manager, not public SSH. Secrets stay in managed parameters or host configuration, never Git.
- The launch templates require IMDSv2, block container access to link-local instance metadata, use a least-privilege instance profile, and restrict application egress to approved provider and required AWS service endpoints. Application logs exclude prompts and secrets; trace/evaluation payloads use synthetic data, retain for at most seven days, and are deleted at teardown.
- The $180 planning estimate, deployment sequence, access model, monitoring, and teardown evidence are defined in [Project 5 AWS Deployment](project-5-aws-deployment.md). Prices are planning assumptions and must be refreshed in AWS Pricing Calculator before each cohort.
- GPU access is strictly limited; fine-tuning tasks use highly optimized small-parameter models (e.g., Qwen/Llama 3B via Unsloth) in the scheduled GPU sessions. Local VRAM is not a prerequisite for P1-P4.
- Required retrieval is `pgvector` plus keyword search AND cross-encoder reranking.
- Students implement one bounded multi-agent LangGraph flow.
- CI evals are limited to smoke cases with cached fixtures; larger LLM-as-judge evals run manually.
- The starter repo, `pgvector` setup, provider adapter, LangGraph scaffold, tool sandbox template, eval fixtures, fine-tuning script, telemetry template, flawed AI artifact, expected issues, and rubric must be provided before launch.
- Default tools are mandatory for grading: `vLLM` for scheduled local/GPU model-serving evidence, `Arize Phoenix` for tracing, and `Unsloth` for fine-tuning must be explicitly chosen as the single defaults in the final repository scaffold. The protected AWS endpoint is API-backed by design.

## Submission & Assessment Criteria

- **Automated Tests**: CI pipeline must pass (LLM smoke evaluation gates).
- **Required Artifacts**: PR containing the LangGraph multi-agent flow, the Ragas evaluation suite, held-out scenario results, the protected AWS endpoint URL and access instructions for reviewers, scheduled vLLM evidence, a verifier report, a cost report, and teardown evidence.
- **Client Defense (Capstone)**: A 15-minute live or Loom video defense demonstrating the working application in the cloud, explaining the multi-agent architecture, interpreting the LLM-as-a-judge Ragas metrics, and justifying the model fine-tuning results.
- **Pass/Fail Rubric**: Must be explicitly supplied in the `projects/` directory, defining Must-Have criteria for the defense and evaluation metrics.

## Workload

| Field | Hours |
| :--- | ---: |
| Theory time | 25.5 |
| Local platform, scenario, and evaluation work time | 78.5 |
| AWS deployment, defense, and teardown work time | 16 |
| Workload calc | 120 |
