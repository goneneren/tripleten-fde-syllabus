# Project 5 AWS Deployment: Bounded Capstone Runbook (LocalStack Pre-Flight Edition)

## Purpose and Boundary

Project 5 is the only project that deploys to AWS. Students first demonstrate **local acceptance** on their open PR: `docker compose up` succeeds, LocalStack `awslocal` pre-flight checks pass, the required tests pass, and CI is green. They then deploy a temporary protected reviewer endpoint in one dedicated course-managed AWS sandbox. Projects 1–4 remain local-only using LocalStack Base and do not expose public endpoints; Project 1 explicitly forbids one.

The re-estimated program allocation for the LocalStack edition is **$414.50 per student in total** (or **$314.50** under the $80 normal AWS planning target):

| Allocation Component | Hard Cap / Estimate | Use |
| :--- | ---: | :--- |
| **LocalStack Base Subscription** | $214.50 | $39/month per student across 22 weeks (~5.5 months / 6 billing cycles). |
| **Approved LLM API calls** | $20.00 | Bounded P5 provider-adapter usage, manual evaluation, and defense traffic. |
| **AWS infrastructure cap** | $180.00 | A short CPU endpoint (`t3.large`), storage, public IPv4, scheduled GPU sessions, and operational variance. ($80 normal target) |
| **Total Combined Allocation** | **$414.50** | Re-estimated total allocation ($314.50 with normal $80 AWS spend). |

If the program adopts **100% LocalStack** without live AWS deployment, the total per-student budget is **$234.50** ($214.50 LocalStack + $20 LLM API).

The normal P5 deployment target is below the AWS cap. The program must refresh this estimate in AWS Pricing Calculator and complete one student-sandbox pilot with Cost Explorer evidence before a cohort launch. Program-owned shared services such as the AWS Organization, domain, DNS automation, and verifier are separately budgeted operating costs; students never use personal accounts or payment methods.

## Planning Estimate

This is a `us-east-1` Linux on-demand planning target for one 14-calendar-day assessment window, excluding taxes. A continuous GPU is explicitly out of scope: a `g4dn.xlarge` at an approximate $0.526/hour would exceed $500 over six weeks for compute alone.

| AWS item | Assumption | Planning amount |
| :--- | :--- | ---: |
| CPU application host | `t3.large`, 336 hours at approximately $0.0832/hour | $28 |
| Public IPv4 | One address, 336 hours at $0.005/hour | $2 |
| CPU persistent disk | 40 GiB gp3 retained for 21 days | $3 |
| Scheduled GPU sessions | `g4dn.xlarge`, maximum 40 hours at approximately $0.526/hour | $21 |
| GPU root disk | 100 GiB gp3, deleted after every booked session | $1 |
| Image registry | Capped student image storage and retention | $1 |
| Logs | Capped retention and synthetic payloads only | $3 |
| Operational contingency | Data transfer, delayed metering, and price variance | $21 |
| **Normal AWS target** |  | **$80** |

The normal target is not a second budget. The per-student AWS hard cap remains $180. Students must not create a NAT gateway, load balancer, managed database, additional public IPv4 address, or second always-on instance. A cost exception requires instructor approval before resources are started.

The endpoint is intentionally CPU and API-backed. GPU sessions are only for the required bounded vLLM serving demonstration or Unsloth fine-tuning. The final endpoint is not expected to host vLLM continuously.

## Account, Cost, and Runtime Controls

- Each student receives one dedicated AWS Organizations member account, tagged by the program with `cohort`, `student-id`, and `project=P5`. Students receive a constrained course role; they do not use personal AWS accounts.
- The bootstrap applies the same required tags to instances, volumes, images, parameters, and logs through launch templates and IAM conditions. The program activates its account and resource cost-allocation tags before P5, then uses them in Cost Explorer, the student cost report, and the account budget filter. AWS supports tag filters for cost budgets after the tags are activated.
- The student role can use only supplied CPU and GPU launch templates, approved parameter paths, CloudWatch views, and Session Manager. It cannot create arbitrary instance types, new launch templates, NAT gateways, load balancers, managed databases, public IPs, IAM principals, or untagged resources.
- The program bootstrap runs inside every student account. It creates an in-account AWS Budget with actual-cost alert at $144 and forecast-cost alert at $162. Its in-account Budget Action denies new EC2 provisioning and stops the tagged CPU/GPU instances at the threshold. AWS Budget Actions cannot target EC2 instances in another account, which is why the stop action is created inside each dedicated sandbox.
- The program-owned GPU booking service maintains the 40-hour ledger. A booking starts the supplied GPU template and creates an in-account EventBridge/Lambda stop action no later than four hours after the start. A nightly in-account sweep stops every running GPU. The student role cannot directly start the GPU template. This runtime control is independent of cost-reporting delay.
- The program confirms G-family quota and capacity for the expected concurrent students before P5 begins. If a session cannot be scheduled, the instructor provides an equivalent managed session as program overhead; it does not consume the student's AWS allocation.

## DNS, Access, and Security Baseline

- The program owns the capstone DNS zone and automation assigns each student one hostname. The supplied Caddy reverse-proxy profile obtains and renews a publicly trusted certificate using TLS-ALPN-01 over port 443. Students receive no DNS-zone permission.
- The security group permits public TCP 443 only. This allows certificate validation and reviewer reachability; the application requires a unique reviewer token, valid only for the 14-day assessment window. The service limits each token to 30 requests per minute and 128 KiB request bodies. Public SSH is prohibited.
- Administration uses AWS Systems Manager Session Manager. The launch template requires IMDSv2. It uses a metadata hop limit of 1 because application containers do not need instance metadata; the pre-launch verifier confirms that containers cannot reach link-local metadata. The instance profile is least privilege.
- Application containers may call only the approved LLM provider endpoints and required AWS service endpoints. They must block link-local metadata access and deny arbitrary tool-network egress. Tool execution remains limited to the approved allow-list, step limit, and token budget.
- Secrets are stored in AWS SSM Parameter Store or Secrets Manager outside Git (validated locally via LocalStack SSM during development). Application logs exclude prompts and secrets. Phoenix traces and Ragas artifacts contain synthetic data only, retain for at most seven days, and are deleted during teardown.

## Student Deployment Workflow (With LocalStack Pre-Flight)

1. **Prove local acceptance & LocalStack pre-flight.** On an open Project 5 PR, run `docker compose up`, execute `awslocal` pre-flight verification scripts against LocalStack (confirming SSM parameter lookups and S3 bucket creation), run required unit/integration tests, and obtain a green CI run. Submit local evidence; do not merge before cloud review.
2. **Prepare the release.** Use the supplied production Compose profile, pinned image tag, `.env.example`, architecture diagram, scenario results, and managed SSM parameter path. Do not commit secrets, real customer data, or unreviewed tools.
3. **Launch the CPU endpoint.** Start the supplied `t3.large` template. The course automation assigns the program hostname and starts the supplied TLS reverse proxy and application stack.
4. **Verify before reviewer access.** Run the course verifier. It checks tags, TLS, security group, authentication, rate/request limits, metadata controls, egress controls, API allowance, and the scheduled teardown. Resolve failures before inviting a reviewer.
5. **Use booked GPU sessions only.** Join the scheduled vLLM or Unsloth session, record the objective and outcome, upload the model-serving or fine-tuning evidence, then let the in-account stop action end the session. Temporary GPU disks are deleted after each session.
6. **Defend and revise.** Reviewer access opens for 14 calendar days from the first verified endpoint. Revisions use the same endpoint and window; an extension needs instructor approval within the $180 cap. The 15-minute defense covers the protected endpoint, scenario results, model-serving evidence, security controls, telemetry, and cost report.
7. **Tear down.** At the end of the assessment window, course automation terminates instances and removes volumes, public IPv4, reviewer tokens, parameters, traces, images, and DNS records. The verifier records timestamps and produces the final report.

## Required Evidence and Assessment

- A course-verifier report, not screenshots alone, for the cloud security, tag, budget, GPU-control, and teardown checks.
- A cost report showing API spend at or below $20 and AWS spend at or below $180.
- Held-out scenario results, scheduled vLLM evidence, LocalStack `awslocal` pre-flight verification logs, protected-endpoint reviewer instructions, and the 15-minute defense.
- The detailed pass/fail requirements are in [`projects/project-5-rubric.md`](../projects/project-5-rubric.md).

## Pricing and Control Sources

- [Amazon EC2 On-Demand Pricing](https://aws.amazon.com/ec2/pricing/on-demand/) explains per-second Linux instance billing and links to AWS Pricing Calculator.
- [Amazon EBS Pricing](https://aws.amazon.com/ebs/pricing/) documents gp3 storage pricing and per-second billing.
- [AWS public IPv4 pricing explanation](https://aws.amazon.com/blogs/networking-and-content-delivery/identify-and-optimize-public-ipv4-address-usage-on-aws/) documents the $0.005 per IP-hour rate used in the estimate.
- [AWS Budgets actions](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-controls.html) documents in-account EC2 actions and forecast-cost actions.
- [Budget filters](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-create-filters.html) documents activated tag filters for cost budgets.
- [EC2 scheduled stop/start](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Stop_Start.html) documents EventBridge/Lambda scheduling patterns.
- [EC2 metadata options](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/configuring-instance-metadata-options.html) documents IMDSv2 enforcement and hop limits.
- [Systems Manager Session Manager](https://docs.aws.amazon.com/systems-manager/latest/userguide/session-manager.html) documents managed access without open inbound administrative ports.
- [LocalStack Documentation](https://docs.localstack.cloud/overview/) documents LocalStack emulated services (S3, SQS, SNS, SSM, Secrets Manager, DynamoDB, CloudWatch).
