# Project 02 — Enterprise Data Integration and Hybrid RAG

- Edition status: Alternative under evaluation; not the program of record.
- Canonical edition: The Open-Source edition remains canonical.
- Licensing boundary: Mandatory LocalStack use depends on written confirmation that its licensing is compatible with this paid program.
- Student fallback: A student who cannot obtain a LocalStack token may use the open-source variant without penalty.

## #

- 2

## Project

- Enterprise Data Integration and Hybrid RAG

## Project description 

- Students scope and deliver a retrieval system over messy client documents without turning the engagement into a platform rewrite. They establish data ownership and access constraints, build a reproducible ingestion path, implement hybrid retrieval, measure failure modes, and defend a statement of work.
- The engagement connects business discovery to ingestion quality, retrieval architecture, evaluation evidence, scope negotiation, and a client-facing delivery agreement.

## Skills

- Discover the supported decision, data owners, access constraints, freshness needs, failure consequences, and measurable retrieval acceptance criteria.
- Integrate LocalStack S3 through the supplied ObjectStore adapter and endpoint-safe client factory.
- Normalize metadata, deduplicate sources, handle malformed content, chunk documents, create embeddings, and validate ingestion quality.
- Implement dense and sparse retrieval, reciprocal-rank fusion, local reranking, authorization metadata propagation, and a versioned API extension.
- Design a compact golden set, measure retrieval quality and latency, attribute errors, and recommend one evidence-backed improvement.
- Write and defend a SoW with outcomes, assumptions, exclusions, responsibilities, estimates, acceptance criteria, and controlled change handling.

## Tech setup

- Docker Compose with LocalStack S3, PostgreSQL/pgvector, PostgreSQL full-text search, FastAPI, and Alembic.
- `awslocal`, the supplied client factory and ObjectStore adapter, sentinel credentials and region, deterministic initialization scripts, and ObjectStore FIDELITY.md.
- Supplied PDF/HTML parser, bounded document fixtures, local embedding model, reciprocal-rank-fusion function, and cross-encoder wrapper.
- Pytest, OpenTelemetry, evaluation fixtures, recall/precision metrics, golden-query template, and supplied reporting script.
- Stakeholder role cards, data inventory, access matrix, SoW template, estimation worksheet, assumption log, and timed scope-change inject.

## Learning Objectives

- Define who retrieval supports, which data may be used, and what measurable quality, latency, and access conditions constitute success.
- Build a reproducible ingestion pipeline over LocalStack S3 with inspectable metadata, access labels, chunking, embeddings, and quality evidence.
- Use the supplied ObjectStore adapter and endpoint-safe client factory without constructing local-stage SDK clients elsewhere.
- Deliver a production-shaped hybrid retrieval API using pgvector, PostgreSQL full-text search, fusion, and local reranking.
- Preserve source and authorization metadata and justify candidate depth, fusion parameters, and rerank cut-off using measured effects.
- Explain retrieval successes and failures by component and meet the published held-out quality and latency floor.
- Defend a bounded SoW and reject unsupported scope expansion without moving time or budget.

## Theory topics

- Data and use-case discovery, ownership, access control, freshness, failure consequences, and acceptance-criteria design.
- S3 API integration, endpoint-safe SDK configuration, client factories, sentinel credentials, deterministic initialization, and portable ObjectStore boundaries.
- Enterprise document ingestion, metadata normalization, deduplication, chunking, embeddings, and data-quality validation.
- Dense retrieval, PostgreSQL full-text search, pgvector, reciprocal-rank fusion, reranking, and authorization metadata propagation.
- Golden sets, precision and recall, latency analysis, error attribution, held-out evaluation, and evidence-based iteration.
- SoW structure, estimation, assumptions, exclusions, responsibilities, negotiation, change rejection, and acceptance definition.
- LocalStack fidelity limits: local S3 evidence does not prove real-AWS performance, durability, authorization, encryption, quotas, or network behavior.

## Delivery Limits

- Starts from TripleTen's reference solution to Project 1 in Repository 2; earlier student defects do not propagate.
- Runs and is graded locally; no real AWS account, cloud deployment, or public endpoint is required or allowed.
- LocalStack Hobby requires a student-controlled account and token; a student who cannot obtain a token may use the open-source variant without penalty.
- Projects 2-4 and Phase 5.A use only `awslocal`; Compose injects sentinel credentials and region values, host AWS credential directories are never mounted, and CI rejects local-stage SDK clients outside the supplied client factory.
- Initialization scripts recreate local state; no task assumes LocalStack Hobby persistence.
- The document set is deliberately bounded; OCR library selection and broad document-platform construction are out of scope.
- The assessed retrieval path remains PostgreSQL/pgvector and PostgreSQL full-text search with supplied fusion and reranking wrappers.
- ObjectStore FIDELITY.md must name the supported API subset and evidence limits; LocalStack evidence is not real-S3 proof.
- The graded SoW defense is the project's single Instructor Presentation / Review recording.

## Theory time (25% allocation)

- 20
- Hours: 20

## Project work time (75% allocation)

- 60
- Hours: 60

## Workload calc

- Formula: `=I4+J4`
- Calculated total: 80 hours
- Allocation basis: 25% theory time and 75% project work time from the canonical project estimate.

Source: `syllabus-fde-focused-5-projects/fde-focused-5-projects-localstack.md`
