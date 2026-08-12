# Project 5 AWS Deployment: Bounded Capstone Runbook

## Purpose and Boundary

Project 5 is the only project that deploys to AWS. Students first pass the local Docker Compose acceptance path and CI checks. They then deploy a temporary, protected reviewer endpoint in a course-managed AWS account. Projects 1-4 remain local-only; Project 1 must not expose a public endpoint.

The program allocation is **$200 per student in total**:

| Allocation | Cap | Use |
| :--- | ---: | :--- |
| Approved LLM API calls | $20 | Bounded P5 provider-adapter usage, manual evaluation, and defense traffic. |
| AWS infrastructure | $180 | CPU endpoint, storage, observability allowance, public IPv4, and scheduled GPU sessions. |
| Total | $200 | No project may use this as an additional or reusable allowance. |

API calls are metered in the application and use a program-issued key with a $20 provider-side cap where the provider supports one. CI uses cached fixtures and does not consume the API allowance.

## Planning Estimate

This is a six-week planning estimate for `us-east-1`, excluding taxes. It uses Linux on-demand reference rates and must be recalculated in AWS Pricing Calculator before each cohort. A continuous `g4dn.xlarge` is explicitly out of scope: at an approximate $0.526/hour, six weeks would exceed $500 for compute alone.

| AWS item | Assumption | Planning amount |
| :--- | :--- | ---: |
| CPU application host | `t3.large`, 1,008 hours at approximately $0.0832/hour | $84 |
| Public IPv4 | 1 address, 1,008 hours at $0.005/hour | $5 |
| Persistent disk | 40 GiB gp3 for six weeks at approximately $0.08/GiB-month | $5 |
| Logs and small operational variance | Capped log retention and no load balancer, NAT gateway, or managed database | $6 |
| Scheduled GPU sessions | `g4dn.xlarge`, maximum 120 hours at approximately $0.526/hour | $63 |
| AWS contingency | Pricing, data-transfer, and operational variance | $17 |
| **AWS total** |  | **$180** |

The endpoint is intentionally CPU and API-backed. GPU sessions are only for the required bounded vLLM serving or Unsloth fine-tuning exercises; training outputs, metrics, and the deployment report are submitted as artifacts. Students must not run a NAT gateway, load balancer, managed database, or a second always-on instance within this budget.

AWS bills usage, so a budget alert is not a hard spending cap. The course platform must configure both alerts and an enforced GPU-session shutdown. AWS documents that Budget Actions can stop targeted EC2 instances or restrict further provisioning; the course account owner, not the student, owns that guardrail. See [AWS Budgets actions](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-controls.html) and [AWS Budgets cost management](https://docs.aws.amazon.com/cost-management/latest/userguide/budgets-managing-costs.html).

## Account and Access Model

- The program provides a course-managed AWS account or isolated student sandbox in the cohort's fixed region. Students do not use personal AWS accounts or payment methods.
- The supplied IAM role permits only the provided CPU and GPU launch templates, security-group attachment, approved parameter access, CloudWatch log viewing, and start/stop actions. It cannot create NAT gateways, load balancers, managed databases, additional public IPs, or arbitrary instance types.
- The program resolves EC2 GPU quota and capacity before P5 begins. If capacity is unavailable, the instructor schedules an equivalent managed GPU session; students are assessed on the same artifacts, not on obtaining capacity themselves.
- An AWS Budget notifies the student and instructor at $144 (80%) and $162 (90%) of the AWS allowance. The scheduled GPU shutdown and provisioning restriction activate before the $180 maximum. The remaining cost margin is reserved for delayed metering and teardown.

## Student Deployment Workflow

1. **Prove the local release.** Run `docker compose up`, execute the required tests, and merge the Project 5 PR. The cloud deployment does not waive local acceptance.
2. **Prepare the release.** Use the supplied production Compose profile, pinned image tag, `.env.example`, and architecture diagram. Put API keys and application secrets in the supplied managed parameter path or host-only configuration. Do not commit secrets, real customer data, or unreviewed tools.
3. **Launch the CPU endpoint.** Start one `t3.large` from the course launch template. Attach only the supplied security group: inbound HTTPS (443) is allowed; SSH (22) is not public. Use the course-approved connection method for administration.
4. **Expose a protected service.** Start the supplied TLS reverse-proxy profile and application Compose stack. Require application authentication for every reviewer. Configure request size and rate limits, a bounded tool allow-list, token and step limits, and structured logs without prompt or secret payloads. The reviewer receives the URL and access instructions through the submission workflow, not from a public unauthenticated link.
5. **Use GPU only in booked sessions.** Start the provided `g4dn.xlarge` template for a booked vLLM or Unsloth session, record the start time and objective, save the adapter/evaluation output, then stop it immediately. The scheduler enforces a 120-hour total allocation; a stopped instance still retains any attached storage costs, so terminate temporary GPU-only storage when the session is complete.
6. **Monitor and defend.** Review application telemetry, CloudWatch log volume, API spend, instance hours, and the AWS Budget alert state before the defense. Demonstrate the protected endpoint, explain the safety and cost trade-offs, and provide reviewer access for the assessment window.
7. **Tear down and submit evidence.** At the end of the review window, stop and terminate the CPU and GPU instances, delete the public IPv4 resource and temporary volumes, revoke reviewer access and parameters, then submit a timestamped cost report and teardown checklist. The instructor confirms that no billable instances, IPs, volumes, or credentials remain.

## Required Security and Operations Evidence

- A security-group screenshot or exported rule set showing HTTPS-only public ingress and no public SSH.
- Evidence of TLS, application authentication, request rate limiting, secrets outside Git, a bounded tool allow-list, and no real personal or regulated data.
- A budget screenshot or export showing the $144 and $162 alerts, plus the GPU-session limit.
- A cost report showing API spend at or below $20 and AWS spend at or below $180.
- A teardown checklist with instance, volume, public IPv4, credential, and endpoint removal timestamps.

## Pricing Sources

- [Amazon EC2 On-Demand Pricing](https://aws.amazon.com/ec2/pricing/on-demand/) explains per-second Linux instance billing and links to AWS Pricing Calculator.
- [Amazon EBS Pricing](https://aws.amazon.com/ebs/pricing/) documents gp3 storage pricing and per-second billing.
- [AWS public IPv4 pricing explanation](https://aws.amazon.com/blogs/networking-and-content-delivery/identify-and-optimize-public-ipv4-address-usage-on-aws/) documents the $0.005 per IP-hour rate used in the estimate.
- [Amazon EC2 data transfer pricing](https://aws.amazon.com/ec2/pricing/on-demand-backup/) documents the shared 100 GB/month internet egress allowance and subsequent usage charges.
