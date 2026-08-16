# Five-Project AI FDE Curriculum Design

## Goal

Create a five-project edition of the focused AI FDE curriculum while preserving the 22-week, 440-hour delivery contract. Combine the current Projects 5 and 6 into one capstone project with phases 5.A and 5.B, require Instructor Presentation / Review recordings after Projects 1–4 and at the Phase 5.A deployment gate, and end Project 5 with a required Final Demo Day after Phase 5.B.

## Version boundary

- Create the new edition under `syllabus-fde-focused-5-projects/`.
- Preserve `syllabus-fde-focused/` unchanged as the six-project source edition.
- Create only the two normative curriculum documents:
  - `fde-focused-5-projects-opensource.md`
  - `fde-focused-5-projects-localstack.md`
- Do not copy the superseded project tree or historical verdict/evaluation artifacts because they evaluate the six-project edition.
- External review files may coexist in the new folder as explicitly non-normative working artifacts; they do not change the two-file normative curriculum set.
- Treat the open-source document as the program of record and LocalStack as an unadopted alternative. Update `AGENTS.md` and `executive-overview.md` to match while preserving the superseded six-project source folder unchanged.

## Project structure

- Projects 1–4 retain their existing schedules, hours, technical scope, and delivery outcomes.
- Project 5 becomes a seven-week, 140-hour capstone across Weeks 16–22.
- Phase 5.A, **Bounded Agent Workflow Under Ambiguity**, retains the current Project 5 content and 80 hours.
- Phase 5.B, **AWS Deployment, Adoption and Handback**, retains the current Project 6 content and 60 hours.
- Rename current task headings `5.1`–`5.5` to `5.A.1`–`5.A.5`.
- Rename current task headings `6.1`–`6.6` to `5.B.1`–`5.B.6`.
- Phase 5.B deploys, accepts, hands back, demonstrates, and tears down the exact release accepted at the Phase 5.A gate in Repository 5.
- The program remains five projects, five physical starter repositories, 31 tasks, 22 weeks, and 440 hours.

## Instructor Presentation / Review

- Projects 1–4 each end with a required **Instructor Presentation / Review** included within their existing final-task hours.
- The presentation uses the project's existing evidence and decision artifacts; it does not introduce a separate build deliverable.
- The instructor applies the project's published Must-Haves and Recommendations, records feedback and the acceptance decision, and identifies any allowed remediation.
- Projects 1–4 add this requirement to Tasks 1.5, 2.5, 3.5, and 4.5 respectively.
- Project 5 receives its Instructor Presentation / Review during Task 5.A.5. This is the technical phase gate that authorizes AWS deployment, not a separate project closeout.
- Five review recordings are required in total: Projects 1–4 and Phase 5.A. Each is one take of at most 10 minutes; an existing defense that serves as the review is not counted twice.
- During Phase 5.B, students may use formative instructor assistance for deployment evidence, acceptance interpretation, and Final Demo Day preparation. This assistance is not another graded presentation.

## Final Demo Day

- Use the exact event name **Final Demo Day** throughout the new edition.
- Final Demo Day is required for program completion and is not optional or ungraded enrichment.
- It occurs at the end of Phase 5.B after acceptance and handback evidence is ready, while the protected endpoint is still available, and before mandatory teardown.
- Each student delivers a 20-minute end-to-end demonstration followed by up to 10 minutes of questions covering the workflow, business value, architecture, safety and authority boundaries, evaluation evidence, AWS operations, cost, limitations, and next recommendation.
- Task 5.B.6 becomes **Final Demo Day, teardown, portfolio and reusable field playbook**. It includes event evidence followed by verified teardown.
- The required event is the culmination of Project 5, not a separate sixth project.
- Final Demo Day occurs after any approved remediation and no later than day 12 of the 14-day endpoint window; verified teardown completes by day 14.

## Delivery constraints

- Projects 1–4 and Phase 5.A remain entirely local and expose no public endpoint.
- Phase 5.B first passes local acceptance, then uses the existing temporary protected AWS profile.
- Preserve the total per-student limits of $20 for approved LLM APIs and $180 for AWS.
- Preserve the no-GPU and no-hands-on-fine-tuning boundaries.
- Preserve deterministic asynchronous grading artifacts. Instructor Presentation / Review and Final Demo Day use the same published evidence floors; they must not reward production polish or unsupported improvisation.
- Keep optional office-hour drills separate from required project closeouts. Phase 5.B instructor assistance remains formative and does not transfer ownership of student decisions or artifacts.

## Acceptance criteria

- Both new editions contain exactly five top-level project sections and 31 task headings.
- Both editions show `60 + 80 + 80 + 80 + 140 = 440` hours across 22 weeks.
- Both editions contain phases 5.A and 5.B under one Project 5 and use Repository 5 throughout both phases.
- Both editions explicitly require five Instructor Presentation / Review recordings: Projects 1–4 and the Phase 5.A gate.
- Both editions explicitly require Final Demo Day at the end of Phase 5.B before teardown.
- Both editions make Task 5.B.5 formative Final Demo Day preparation with optional instructor support and no additional graded defense.
- Both editions name the instructor as the Phase 5.A acceptance authority and bind the Phase 5.B deployment to the accepted tag, commit SHA, and image digest.
- The LocalStack edition scopes `awslocal` and the local-endpoint CI gate to Projects 2–4 and Phase 5.A while permitting the real AWS CLI and supplied adapters in Phase 5.B.
- Neither edition calls Demo Day optional or ungraded.
- Neither edition introduces an alternate name for Final Demo Day.
- No stale top-level Project 6, six-project summary, six-rubric requirement, or Project 6 task numbering remains in the new edition.
- The open-source and LocalStack editions retain aligned project, phase, task, assessment, budget, and workload structure.
- `AGENTS.md` and `executive-overview.md` identify the five-project open-source edition as the sole program of record and describe the same delivery boundary.
- The original `syllabus-fde-focused/` folder remains byte-for-byte unchanged.
