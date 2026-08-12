# Project 2 - Data Layer, Vector Search & Hybrid RAG

## Project Description

Students evolve the reference platform to support AI data ingestion and hybrid retrieval using an opinionated starter repo. They extend REST behavior, implement Unstructured data extraction pipelines, build local embeddings, and configure a hybrid search vector database (pgvector). Traditional backend architecture (gRPC, Redis caching) is implemented but shifted to a supporting/positioning focus, emphasizing the data prep needed for RAG systems.

## Skills

- Design REST APIs with clear resources, status codes, versioning, and evolution paths.
- Extract text and tables from complex enterprise documents (PDF, HTML) using Unstructured.io.
- Generate dense vector embeddings locally using FastEmbed or sentence-transformers.
- Implement hybrid retrieval combining `pgvector` (dense) and BM25 (sparse) search.
- Use simulated read replicas and Redis caching while explaining lag, freshness, and invalidation.
- Compare GraphQL, NoSQL, partitioning, and managed data services at decision level.
- Audit an AI-generated repository or migration change for correctness and architectural risk.

## Tech Setup

- Opinionated REST/gRPC starter repo extended from Project 1.
- Preconfigured `protoc` build scripts, protobuf definitions, and one gRPC extension point.
- Database connection pooling, migration tooling, repository layer, and test harness.
- Docker Compose with PostgreSQL (including `pgvector`), read-replica simulation helper, and Redis.
- API contract tests and integration tests for idempotency, N+1 behavior, cache freshness, and migration safety.
- Optional AWS checkpoint: RDS/read-replica comparison or instructor-led demo if credits are available.
- Seeded flawed AI migration or repository artifact, expected-issue list, and review rubric.

## Learning Objectives

- Design APIs that remain stable as AI integration requirements change.
- Parse and chunk messy enterprise documents for semantic retrieval.
- Implement a hybrid search data layer that supports production-style vector reads, writes, and migrations.
- Explain replication lag, cache invalidation, and read freshness trade-offs from a local simulation.
- Justify when NoSQL, GraphQL, partitioning, sharding, or managed databases are appropriate without building all of them.
- Review AI-assisted implementation for hidden data and decomposition defects.

## Theory Topics

- REST design, API versioning, and API evolution.
- AI-Native Development, Data Preparation, Chunking Strategies.
- Relational production patterns, migrations, repositories, `pgvector`, and transaction boundaries.
- Local Embedding Models (FastEmbed, sentence-transformers).
- Hybrid Retrieval (Dense Vector + BM25 Sparse Search).
- Data replication, read replicas, Redis caching, cache invalidation, and freshness.
- gRPC, protobufs, service boundaries, and DDD (Positioning).
- NoSQL families, partitioning, sharding, use cases (Positioning).

## Delivery Limits

- Raw PostgreSQL WAL or physical streaming replication is not required.
- Students implement unstructured parsing and hybrid search; additional complex service splits are optional.
- NoSQL, GraphQL, partitioning, and sharding are decision-level only unless a separate lab is supplied.
- AWS RDS is optional and must have a local fallback.
- The starter repo must provide database plumbing, migration tooling, replica simulation, tests, flawed AI artifact, expected issues, and rubric before launch.

## Workload

| Field | Hours |
| :--- | ---: |
| Theory time | 22.5 |
| Project work time | 64 |
| Workload calc | 86.5 |
