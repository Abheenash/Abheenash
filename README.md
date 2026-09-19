<div align="center">

# Hi, I'm Abheenash 👋

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=3000&pause=800&color=FF9900&center=true&vCenter=true&width=760&lines=AWS+Certified+DevOps+Engineer+%E2%80%93+Professional;Cloud+%C2%B7+DevOps+%C2%B7+Cloud+Security;Serverless+%C2%B7+Kubernetes+%C2%B7+GenAI+on+AWS;Building%2C+operating+%26+diagnosing+AWS+infrastructure)](https://abheenash.com)

`Cloud` · `DevOps` · `Cloud Security` · `Terraform` · `Serverless` · `Kubernetes` · `GenAI` · `CI/CD`

<a href="https://abheenash.com"><img src="https://img.shields.io/badge/abheenash.com-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white" alt="Website"/></a>
<a href="https://www.linkedin.com/in/abheenash"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
<a href="https://share.abheenash.com"><img src="https://img.shields.io/badge/Live_Demo-232F3E?style=for-the-badge&logo=amazons3&logoColor=white" alt="Live demo"/></a>
<img src="https://img.shields.io/badge/📍_Houston,_TX-555?style=for-the-badge" alt="Houston, TX"/>
<img src="https://img.shields.io/badge/🟢_Open_to_work-2ea043?style=for-the-badge" alt="Open to work"/>

</div>

**AWS Certified DevOps Engineer – Professional**, Solutions Architect – Associate & Cloud Practitioner — building, operating and diagnosing secure, reliable infrastructure on AWS.

---

### ⭐ Flagship — [Job Hunt Command Center](https://github.com/Abheenash/job-hunt-command-center)

An **AI-powered, full-stack serverless job-application tracker** built end-to-end on AWS, private behind Cognito. A JWT-authorized API Gateway HTTP API fronts a Lambda → DynamoDB + versioned S3 backend — all provisioned in Terraform and shipped through a DevSecOps CI/CD pipeline (gitleaks · Checkov/tfsec · Trivy) via GitHub Actions OIDC.

**AI résumé generator** *(headline feature)* — paste a job description and it produces a tailored 2-page résumé as LaTeX plus a server-compiled PDF (bundled tectonic Lambda layer). Model-selectable on **Amazon Bedrock** (Claude Sonnet 4.6 default, Haiku for cheap bulk, Opus for best): the model returns structured JSON that Lambda renders into LaTeX deterministically, so output always compiles and can never fabricate facts outside the candidate's corpus. Includes a weighted match-score rubric, an ATS keyword-match rate, AI-suggested custom fields, auto-fit to 2 pages, and an optional cover letter.

**Event-driven email-intelligence pipeline** — EventBridge → read-only IMAP Scanner Lambda → SQS (+DLQ) → Dispatcher → Step Functions Express (Classify → Enrich). Bedrock classifies recruiter replies, interviews, and rejections, then **auto-advances and enriches** the matching application, with per-message retries and poison-message DLQ isolation. Plus JD field extraction, JD↔résumé match scoring, and a natural-language **"Ask-AI" Q&A** over your applications.

**Self-monitoring** — a CloudWatch golden-signals dashboard, SLO alarms rolled into a composite service-health alarm → SNS, X-Ray tracing on every Lambda and the state machine, per-alarm runbooks, and an AWS Budgets guard on Bedrock spend. A weekly SES digest and conversion analytics (funnel, response rate by source, résumé-match vs. outcome) round it out.

---

### ☁️ More AWS projects — build → ship → operate → recover

Every repo below has a test suite and CI (Linux + macOS where it applies, ThreadSanitizer/AddressSanitizer on the C++, checkov against a reviewed baseline on the Terraform). The numbers are measured, and the write-ups say what went wrong before it went right.

**[Production Triage Toolkit](https://github.com/Abheenash/production-triage-toolkit)** — *diagnose before users do* · **Java**
A Java 17 CLI that finds data drift, stuck jobs and database-health problems **before users report them** — 15 read-only SQL diagnostics against PostgreSQL, ranked by severity, each linked to a runbook. Safe to point at production by four independent layers, including asking the server `SHOW transaction_read_only` and closing the connection if the answer isn't `on`. **1,069 ms against 10 million rows.** New: `--compare` / `--history-dir` / `--fail-on-regression` — every check classified NEW / RESOLVED / WORSENED / IMPROVED / BROKE against the previous run, so a scheduled run pages only for what got worse. **172 tests**, 5 CI criteria including one that fails the build when the README stops being true. [Case study](https://github.com/Abheenash/production-triage-toolkit/blob/main/CASE_STUDY.md) — including the index that made it 4x *slower*.

**[Cloud Observability & Incident Response](https://github.com/Abheenash/cloud-observability-sre)** — *operate reliably*
Golden signals, X-Ray, RUM, SLOs with error budgets and a composite health alarm on a live serverless service — plus **multi-window multi-burn-rate SLO alerts**, anomaly-detection alarms, and the failure drill as an **AWS Fault Injection Service experiment** whose stop condition *is* the health alarm (detection aborts the fault, so production can't be left broken). An automated drill measures instead of eyeballing: **induce → ALARM in 105 s**, restore → OK in 297 s. All Terraform, all applied.

**[AWS Cloud Operations & Recovery Lab](https://github.com/Abheenash/aws-cloudops-lab)** — *day-2 ops*
EC2 Auto Scaling + ALB + RDS PostgreSQL in Terraform with patching, log shipping, golden-signal alarms, runbooks and Boto3/Lambda automation. **5 live drills** (5xx in 177 s, latency in 289 s, DB dependency in 166 s) and an RDS restore in **6 min 36 s** against a 60-minute target. The two drills that *didn't* fire became design changes: a degraded-capacity alarm (`HealthyHostCount < desired`) and an RDS connection threshold derived from the instance class's real ceiling. The non-prod scheduler is now infrastructure with scoped IAM and its own alarm; 12 moto-mocked tests.

**[Secure Container Pipeline](https://github.com/Abheenash/secure-container-pipeline)** — *ship securely*
ECS Fargate in private subnets via VPC endpoints, ALB + WAF, least-privilege task roles, all Terraform — behind **four hard gates** (gitleaks · checkov/tfsec · trivy · the app's own pytest suite) enforced by branch protection, proven by a PR carrying a planted AWS credential landing in **merge state: BLOCKED**. Trivy also emits a **CycloneDX SBOM** and secret-scans the image; a gated CD job pushes to ECR and **signs the image by digest with keyless cosign**. Readiness (`/ready` = DynamoDB reachable) is separate from liveness, the ECS service has a deployment circuit breaker with automatic rollback and CPU autoscaling, and one variable turns on TLS 1.3 with an HTTP→HTTPS redirect.

**[Serverless File Share](https://github.com/Abheenash/serverless-file-share)** — *build securely* · [live demo](https://share.abheenash.com)
Zero-knowledge, self-destructing file & secret sharing. Payloads are **AES-256-GCM encrypted in the browser** (the key never touches the server), with SSE-KMS defense-in-depth and a DynamoDB **TTL → Streams reaper**. Hardened in v2: a filename could once write HTTP headers through the presigned `Content-Disposition` — now sanitised and RFC 5987-encoded, verified live; structured JSON logs; partial-batch failure reporting so one failed delete retries alone; 16 moto-backed tests covering the presigned PUT bound to the declared size, the atomic download cap and the password gate.

**[AWS EKS Platform](https://github.com/Abheenash/aws-eks-platform)** — *run on Kubernetes*
Kubernetes on **Amazon EKS** via Terraform, ALB Ingress under IRSA, CPU-based HPA, keyless GitHub Actions CI/CD — drilled live (pod self-heal in 7 s, HPA 2 → 6). The two honest findings are fixed and pinned by a CI policy check: the 502s during pod replacement (preStop drain + readiness 503 on SIGTERM + a 15 s deregistration delay) and the restart under load (CPU work moved to a child process; liveness, readiness and startup probes separated). PodDisruptionBudget, kubeconform strict validation, and a runtime image that ships no package manager at all.

**[Portfolio AI Assistant](https://github.com/Abheenash/portfolio-ai-assistant)** — *build with GenAI* · the "Ask AI" widget on [abheenash.com](https://abheenash.com)
API Gateway → Lambda → **Amazon Bedrock (Claude Haiku 4.5)**, the knowledge base in a cached system prompt instead of a vector DB. Every request emits CloudWatch EMF metrics — latency, tokens, cache reads, cost — so the numbers are read, not estimated: **4,000 cache-read tokens and $0.0015 per answer**. Origin allow-list enforced in the Lambda, alarms on errors / p95 / hourly spend, 24 tests with a fake Bedrock, and a committed **12-case prompt-injection eval** run against the live endpoint: 12/12.

---

### ⚙️ Systems & parallel C++ — the layer underneath

Rebuilt from single-file demos into real projects — each with CMake, a test suite that runs clean under **ThreadSanitizer and AddressSanitizer** in CI, and benchmarks that say where a design decision pays off *and where it doesn't*.

**[Concurrent KV Store](https://github.com/Abheenash/concurrent-kv-store)** — *a Redis-style server on raw POSIX sockets*
64-way sharded store under `std::shared_mutex` with TTLs, a newline-framed 22-command protocol, **append-only-file persistence** with replay, atomic-rename compaction and `always`/`everysec`/`no` fsync, two I/O models (thread-per-connection and N `poll()` reactors that each accept for themselves), `sigwait` shutdown, and a load generator with p50/p99. **5.09 M req/s** pipelined with shards vs 1.23 M with the old global mutex; 502/502 clients accepted at 500 concurrent. Its own tests found five real macOS/BSD socket bugs before the benchmark could run — all written up.

**[Parallel Thread Pool](https://github.com/Abheenash/parallel-thread-pool)** — *work-stealing scheduler, header-only*
`submit()` → `std::future` with exception propagation, `parallel_for` whose calling thread *helps* so nested loops can't deadlock, backpressure, graceful shutdown. Per-worker deques with random-victim stealing; submitters only take the wake-up mutex when a sleeper count says someone is parked. **5.37× on 10 cores** compute-bound; spin-before-park took tiny tasks 0.60 → 1.98 M/s; the fork-join tree shows stealing's edge (4.24 vs 3.38 M tasks/s) — and the heavy-tailed benchmark shows where a global FIFO queue ties it, reported honestly.

**[Parallel Heat Diffusion](https://github.com/Abheenash/parallel-heat-diffusion)** — *four backends, one measured roofline*
Serial, spawn-per-step threads, persistent threads with a spinning barrier, and OpenMP on one flat grid — **320 backend/thread-count combinations bitwise-identical** to serial, plus physical invariants including exact mirror symmetry. A STREAM-style probe quantifies the wall: the 2000² grid reaches ~100 GB/s at 4 threads against a measured 98 GB/s ceiling, so the ~1.9× observed is the maximum possible; a cache-resident grid shows spawn-per-step *slower than serial* and the spin barrier lifting 2.14× → 2.89×.

---

### 🛠️ Tech

<p>
<img src="https://img.shields.io/badge/AWS-232F3E?style=for-the-badge&logo=amazon-aws&logoColor=FF9900" alt="AWS"/>
<img src="https://img.shields.io/badge/Amazon_Bedrock-232F3E?style=for-the-badge&logo=amazonaws&logoColor=FF9900" alt="Amazon Bedrock"/>
<img src="https://img.shields.io/badge/Kubernetes_(EKS)-326CE5?style=for-the-badge&logo=kubernetes&logoColor=white" alt="Kubernetes / EKS"/>
<img src="https://img.shields.io/badge/Terraform-7B42BC?style=for-the-badge&logo=terraform&logoColor=white" alt="Terraform"/>
<img src="https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logo=docker&logoColor=white" alt="Docker"/>
<img src="https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white" alt="GitHub Actions"/>
<img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white" alt="Python"/>
<img src="https://img.shields.io/badge/Java-ED8B00?style=for-the-badge&logo=openjdk&logoColor=white" alt="Java"/>
<img src="https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL"/>
<img src="https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=cplusplus&logoColor=white" alt="C++"/>
<img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux"/>
<img src="https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white" alt="Bash"/>
</p>

**Cloud (AWS):** Lambda · API Gateway · S3 · DynamoDB · Cognito · Bedrock · EventBridge · SQS · Step Functions · SES · SNS · EKS · ECS Fargate · ECR · VPC · ALB · CloudFront · Route 53 · KMS · Secrets Manager · IAM · WAF · CloudWatch · X-Ray · CloudTrail
**GenAI:** Amazon Bedrock (Claude Sonnet 4.6 · Haiku · Opus) · AI résumé generation (structured JSON → LaTeX/PDF) · LLM classification & enrichment · JD↔résumé match scoring · RAG-style Q&A
**Containers & Kubernetes:** Amazon EKS · AWS Load Balancer Controller (IRSA) · HPA autoscaling · ECS Fargate · Docker
**IaC & CI/CD:** Terraform · GitHub Actions · OIDC (keyless) · branch protection
**DevSecOps & Security:** IAM least privilege · KMS/SSE encryption · Secrets Manager · WAF · Checkov · tfsec · Trivy · gitleaks · SBOM (CycloneDX) · cosign keyless signing · Dependabot
**Observability / SRE:** CloudWatch dashboards & alarms · X-Ray · Synthetics · RUM · SLOs, error budgets & burn-rate alerts · anomaly detection · AWS Fault Injection Service · incident response · production triage & runbooks · PostgreSQL diagnostics
**Languages:** Python · Java · Bash · SQL · C++ · C · JavaScript · Go · Ruby · Perl

---

### 📜 Certifications

- **AWS Certified DevOps Engineer – Professional** (DOP-C02) — [verify](https://www.credly.com/badges/247b90b9-b578-46b1-b987-e778322017c3/public_url)
- **AWS Certified Solutions Architect – Associate** (SAA-C03) — [verify](https://www.credly.com/badges/e499fee9-1b8b-4fce-a65c-bc4ddcb2f8b9/public_url)
- **AWS Certified Cloud Practitioner** (CLF-C02) — [verify](https://www.credly.com/badges/a9a04423-7b7b-4e75-99c9-8edb3488d9cb/public_url)

---

<div align="center">

<img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Abheenash&layout=compact&theme=tokyonight&hide_border=true&langs_count=8" alt="Top Languages" height="150"/>

</div>

---

<sub>Full write-ups, with the war stories and the benchmarks behind every number above, at <a href="https://abheenash.com">abheenash.com</a>.</sub>
