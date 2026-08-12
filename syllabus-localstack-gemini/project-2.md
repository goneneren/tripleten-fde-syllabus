# Project 2 - Data Layer, Vector Search, LocalStack S3 Lake & Hybrid RAG

## Project Description

Students evolve the reference platform to support AI document ingestion and hybrid retrieval using LocalStack S3 (`s3://enterprise-docs`) and PostgreSQL (`pgvector`). They extend REST endpoints, build an event-driven ingestion pipeline that triggers on LocalStack S3 upload events, extract text and tables using `Unstructured`, generate dense vector embeddings using `FastEmbed`, track document metadata in LocalStack DynamoDB, and store/query hybrid vectors in `pgvector`. Traditional backend architecture (Redis caching, gRPC boundaries) is implemented but shifted to a supporting/positioning focus, emphasizing the production data prep needed for enterprise RAG systems.

## Skills

- Design REST APIs with clear resources, status codes, versioning, and evolution paths.
- Upload enterprise raw documents (PDFs, HTML) to LocalStack S3 (`s3://enterprise-docs`) using Python `boto3`.
- Build event-driven ingestion pipelines handling S3 notifications to trigger text and table parsing via `Unstructured.io`.
- Track ingestion pipeline job states, retries, and document metadata in LocalStack DynamoDB.
- Generate dense vector embeddings locally using `FastEmbed` (sentence-transformers as fallback).
- Implement hybrid retrieval combining `pgvector` (dense vector search) and BM25 (sparse keyword search).
- Use simulated read replicas and Redis caching while explaining lag, freshness, and cache invalidation.
- Compare GraphQL, NoSQL, partitioning, and managed cloud data services (S3, OpenSearch, DynamoDB) at a decision level.
- Audit an AI-generated repository or migration change for correctness and architectural risk.

## Tech Setup

- Opinionated REST/gRPC starter repo extended from Project 1.
- Docker Compose scaffold with PostgreSQL (including `pgvector`), Redis, and **LocalStack Base** (S3 and DynamoDB services).
- Python `boto3` integration with LocalStack endpoint overrides (`endpoint_url="http://localstack:4566"`).
- S3 Bucket initializer script (`awslocal s3 mb s3://enterprise-docs`) and DynamoDB table schema initializer, re-runnable on every `docker compose up` because state persistence is not assumed.
- Shared `boto3` client factory with sentinel credentials and injected `endpoint_url`, carried forward from Project 1, plus the CI gate that fails on clients constructed outside it.
- Database connection pooling, migration tooling, repository layer, and test harness.
- API contract tests and integration tests for document upload, extraction, idempotency, vector indexing, and cache freshness.
- Deterministic enterprise-data scenario pack with messy documents, duplicate IDs, slow listings, and held-out grading cases.
- Seeded flawed AI migration or repository artifact, expected-issue list, and review rubric.

## Learning Objectives

- Design APIs and data ingestion contracts that remain stable as AI document processing evolves.
- Build event-driven document ingestion workflows utilizing LocalStack S3 and `Unstructured.io`.
- Store document metadata in LocalStack DynamoDB and semantic vectors in PostgreSQL `pgvector`.
- Implement a hybrid search data layer combining dense vector similarity with sparse BM25 keyword matching.
- Explain cloud storage vs. relational vector database trade-offs and cache invalidation mechanics.
- Justify when NoSQL (DynamoDB), GraphQL, partitioning, sharding, or managed vector databases are appropriate without building all of them.
- Review AI-assisted database implementations for hidden data corruption and decomposition defects.

## Theory Topics

- REST design, API versioning, and API evolution.
- Cloud Object Storage patterns (AWS S3 / LocalStack S3 bucket notification architectures).
- AI-Native Development, Data Preparation, and Document Chunking Strategies.
- Relational production patterns, migrations, repositories, `pgvector`, and transaction boundaries.
- NoSQL key-value & document patterns (LocalStack DynamoDB for job tracking).
- Local Embedding Models (FastEmbed default, sentence-transformers fallback).
- Hybrid Retrieval (Dense Vector + BM25 Sparse Search).
- Data replication, read replicas, Redis caching, cache invalidation, and freshness.
- gRPC, protobufs, service boundaries, and DDD (Positioning).

## Delivery Limits

- Raw PostgreSQL WAL or physical streaming replication is not required.
- Students implement unstructured parsing from LocalStack S3, DynamoDB tracking, and hybrid search; additional complex microservice splits are optional.
- Default tools are mandatory for grading: `LocalStack S3` for object storage, `pgvector` for vector storage, `FastEmbed` for local embeddings, and `LocalStack DynamoDB` for metadata tracking. Alternatives are only permitted as un-graded optional extensions.
- NoSQL deep dives, GraphQL, partitioning, sharding, and gRPC implementation are decision-level only unless scaffolded.
- No cloud deployment or public endpoint is permitted; all S3 and DynamoDB calls execute against LocalStack inside Docker Compose. Sentinel credentials and the injected `endpoint_url` are mandatory; bypassing the client factory is a CI failure.
- Retrieval quality, chunking, and correctness are graded from the scenario pack. **Ingestion throughput and S3/DynamoDB latency are not graded and must not appear as evidence** — emulated storage timings are not transferable. Idempotency, retry, and job-state correctness are graded on behavior, not speed.
- This is the first project in which students write `boto3` service logic themselves; Project 1 provides it pre-built.
- The starter repo must provide LocalStack initialization, the `boto3` client factory and its CI gate, database plumbing, migration tooling, tests, flawed AI artifact, expected issues, and rubric before launch.

## Submission & Assessment Criteria

- **Automated Tests**: CI pipeline must pass (LocalStack S3 upload tests, Unstructured extraction ETL tests, vector retrieval unit tests).
- **Required Artifacts**: PR containing the LocalStack S3 event-handler pipeline script and the hybrid search API endpoint.
- **Client Defense**: A 5-minute Loom video demonstrating the upload of a messy PDF to LocalStack S3, processing via `Unstructured`, and executing a successful hybrid search query against `pgvector`.
- **Pass/Fail Rubric**: Must be explicitly supplied in the `projects/` directory, defining Must-Have criteria for chunking logic and S3 integration.

## Workload

| Field | Hours |
| :--- | ---: |
| Theory time | 22.5 |
| Project work time | 64 |
| Workload calc | 86.5 |

⚠️ **Pending re-cost.** These hours are inherited from the canonical program. This edition adds an estimated **+8 hours** (S3 document lake, S3 event notifications, DynamoDB job-state tracking) — the largest increase of any project. At 86.5 hours across 4 weeks this is already 21.6 h/wk. See [Workload Impact](overview-and-module-map.md#workload-impact-pending-re-cost).
