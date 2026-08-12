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
- [Positioning] Deploy the Docker Compose stack to a basic cloud instance (e.g., AWS EC2) as an optional capstone delivery requirement.
- Defend model-serving, provider, architecture, safety, and evaluation trade-offs.

## Tech Setup

- Secured version of the platform extending Project 4.
- Paid LLM API provider adapter or local inference engine (vLLM default).
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

- GPU access is strictly limited; fine-tuning tasks use highly optimized small-parameter models (e.g., Qwen/Llama 3B via Unsloth) or run on provided cloud notebooks if local VRAM is insufficient.
- Required retrieval is `pgvector` plus keyword search AND cross-encoder reranking.
- Students implement one bounded multi-agent LangGraph flow.
- CI evals are limited to smoke cases with cached fixtures; larger LLM-as-judge evals run manually.
- The starter repo, `pgvector` setup, provider adapter, LangGraph scaffold, tool sandbox template, eval fixtures, fine-tuning script, telemetry template, flawed AI artifact, expected issues, and rubric must be provided before launch.
- Default tools are mandatory for grading: `vLLM` for model serving, `Arize Phoenix` for tracing, and `Unsloth` for fine-tuning must be explicitly chosen as the single defaults in the final repository scaffold.

## Submission & Assessment Criteria

- **Automated Tests**: CI pipeline must pass (LLM smoke evaluation gates).
- **Required Artifacts**: PR containing the LangGraph multi-agent flow, the Ragas evaluation suite, and a live endpoint URL pointing to the cloud-deployed instance.
- **Client Defense (Capstone)**: A 15-minute live or Loom video defense demonstrating the working application in the cloud, explaining the multi-agent architecture, interpreting the LLM-as-a-judge Ragas metrics, and justifying the model fine-tuning results.
- **Pass/Fail Rubric**: Must be explicitly supplied in the `projects/` directory, defining Must-Have criteria for the defense and evaluation metrics.

## Workload

| Field | Hours |
| :--- | ---: |
| Theory time | 25.5 |
| Project work time | 94.5 |
| Workload calc | 120 |
