<div align="center">

# Hi, I'm Abheenash 👋

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=3000&pause=800&color=FF9900&center=true&vCenter=true&width=760&lines=IT+Analyst+%E2%80%93+Application+Support+%40+Phillips+66;AWS+Certified+DevOps+Engineer+%E2%80%93+Professional;Cloud+operations+%C2%B7+Production+support+%C2%B7+Incident+response;Building%2C+operating+%26+diagnosing+AWS+%2B+Linux+systems)](https://abheenash.com)

`Cloud Operations` · `Production Support` · `Incident Response` · `AWS` · `Linux` · `Terraform` · `CI/CD` · `Kubernetes` · `GenAI`

<a href="https://abheenash.com"><img src="https://img.shields.io/badge/abheenash.com-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white" alt="Website"/></a>
<a href="https://www.linkedin.com/in/abheenash"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
<a href="https://share.abheenash.com"><img src="https://img.shields.io/badge/Live_Demo-232F3E?style=for-the-badge&logo=amazons3&logoColor=white" alt="Live demo"/></a>
<img src="https://img.shields.io/badge/📍_Houston,_TX-555?style=for-the-badge" alt="Houston, TX"/>
<img src="https://img.shields.io/badge/🟢_Open_to_work-2ea043?style=for-the-badge" alt="Open to work"/>

</div>

**IT Analyst – Application Support at Phillips 66** and **AWS Certified DevOps Engineer – Professional**. Cloud operations, production support, incident response, root-cause analysis and CI/CD on AWS and Linux — I keep 7 workplace applications running for ~13,000 employees and contractors, fix defects in Java, C++ and Perl, and build the tooling that finds problems before users report them. M.S. in Computer & Systems Engineering (University of Houston).

---

### 💼 Experience

**Phillips 66** — *IT Analyst, Application Support* · Houston, TX · Feb 2026 – present
Support 7 workplace applications (contractor access, work permits, facility requests) for ~13,000 employees and contractors across refineries, terminals and offices, on AWS and on-prem RHEL. ~20 production tickets a month via Splunk and SQL against Oracle / SQL Server; 12 production defects fixed in Java, C++ and Perl — including a C++ memory leak in the site-access service, isolated with Valgrind and GDB. Splunk alerts + Terraform-managed CloudWatch alarms that caught 3 failures before users did. On-call one week in five. Built a nightly Java reconciliation job across Oracle, ISNetworld and SAP that cut gate-access tickets from ~12 to ~4 a month.

**Cloudflare** — *Systems Engineering Intern* · Austin, TX · May – Aug 2025
Built a Go service that audits on-call ownership and alert routing across ~120 internal services, exporting gaps as Prometheus metrics (31 services with missing/stale owners found; runbook + Grafana dashboard delivered). Found ~1,800 orphaned ownership records with read-only SQL against PostgreSQL and ClickHouse and wrote a cleanup with a tested rollback. Shadowed on-call for 6 weeks; coauthored 2 incident reports.

**HCLTech** — *DevOps Engineer, AWS Cloud Operations* · Hyderabad, India · Apr 2022 – Dec 2023
Supported a US client's AWS B2B platform (~300 business customers, ~3M API requests/day) on ECS Fargate, RDS and Linux. On-call one week in four; 10+ RCAs. Golden-signal and composite alarms cut pages per on-call week from ~30 to ~11. Automated release pipeline (~2 h → <20 min) and migrated ~150 hand-built resources into Terraform (env setup ~3 days → 90 min).

---

### ⭐ Flagship — [Job Hunt Command Center](https://github.com/Abheenash/job-hunt-command-center)

An **AI-powered, full-stack serverless job-application tracker** built end-to-end on AWS, private behind Cognito. A JWT-authorized API Gateway HTTP API fronts a Lambda → DynamoDB + versioned S3 backend — all provisioned in Terraform and shipped through a DevSecOps CI/CD pipeline (gitleaks · Checkov/tfsec · Trivy) via GitHub Actions OIDC.

**AI résumé generator** *(headline feature)* — paste a job description and it produces a tailored 2-page résumé as LaTeX plus a server-compiled PDF (bundled tectonic Lambda layer). Model-selectable on **Amazon Bedrock** (Claude Sonnet 4.6 default, Haiku for cheap bulk, Opus for best): the model returns structured JSON that Lambda renders into LaTeX deterministically, so output always compiles and can never fabricate facts outside the candidate's corpus. Includes a weighted match-score rubric, an ATS keyword-match rate, AI-suggested custom fields, auto-fit to 2 pages, and an optional cover letter.

**Event-driven email-intelligence pipeline** — EventBridge → read-only IMAP Scanner Lambda → SQS (+DLQ) → Dispatcher → Step Functions Express (Classify → Enrich). Bedrock classifies recruiter replies, interviews, and rejections, then **auto-advances and enriches** the matching application, with per-message retries and poison-message DLQ isolation. Plus JD field extraction, JD↔résumé match scoring, and a natural-language **"Ask-AI" Q&A** over your applications.

**Self-monitoring** — a CloudWatch golden-signals dashboard, SLO alarms rolled into a composite service-health alarm → SNS, X-Ray tracing on every Lambda and the state machine, per-alarm runbooks, and an AWS Budgets guard on Bedrock spend. A weekly SES digest and conversion analytics (funnel, response rate by source, résumé-match vs. outcome) round it out.

---

### ☁️ More AWS projects — build → ship → operate

**[Production Triage Toolkit](https://github.com/Abheenash/production-triage-toolkit)** — *diagnose before users do* · **Java**
A Java 17 CLI that finds data drift, stuck jobs and database-health problems **before users report them** — 15 read-only SQL diagnostics against PostgreSQL, ranked by severity, each linked to a runbook that says how to confirm, fix, prevent and escalate. Safe to point at production by four independent layers, including asking the server `SHOW transaction_read_only` and closing the connection if the answer isn't `on`. **1,069 ms against 10 million rows** — and 1,228 ms on a single CPU. 163 tests, 5 CI criteria, shipped with validated systemd units, a Kubernetes CronJob and ECS/EventBridge Terraform. [Case study](https://github.com/Abheenash/production-triage-toolkit/blob/main/CASE_STUDY.md) — including the index that made it 4x *slower*.

**[Serverless File Share](https://github.com/Abheenash/serverless-file-share)** — *build securely* · [live demo](https://share.abheenash.com)
Zero-knowledge, self-destructing file & secret sharing. Payloads are **AES-256-GCM encrypted in the browser** (the key never touches the server), with SSE-KMS defense-in-depth and a DynamoDB **TTL → Streams reaper**. Terraform + keyless CI/CD.

**[AWS EKS Platform](https://github.com/Abheenash/aws-eks-platform)** — *run on Kubernetes*
Kubernetes on **Amazon EKS** via Terraform (official VPC + EKS modules), ALB Ingress (AWS Load Balancer Controller, IRSA), and CPU-based HPA autoscaling, delivered by keyless GitHub Actions CI/CD — proven with live drills (pod self-heal, HPA scale-out).

**[Secure Container Pipeline](https://github.com/Abheenash/secure-container-pipeline)** — *ship securely*
A containerized service on **ECS Fargate** behind a DevSecOps GitHub Actions pipeline (gitleaks · checkov/tfsec · trivy) that blocks insecure merges — proven by automatically blocking a PR carrying a planted secret. All Terraform.

**[Cloud Observability & Incident Response](https://github.com/Abheenash/cloud-observability-sre)** — *operate reliably*
X-Ray, RUM and Logs Insights on a live API Gateway/Lambda/DynamoDB service; SLOs, error budgets, a composite service-health alarm and an external Synthetics canary, all Terraform. Validated by setting Lambda concurrency to zero — **detected in ~60 s**, restored via the runbook.

**[AWS Cloud Operations & Recovery Lab](https://github.com/Abheenash/aws-cloudops-lab)** — *day-2 ops*
EC2 Auto Scaling + ALB + RDS PostgreSQL in Terraform with patching, log shipping, golden-signal alarms, runbooks and Boto3/Lambda automation. **5 live drills** (5xx in 177 s, latency in 289 s, DB dependency in 166 s; 2 alarm-tuning findings documented) and an RDS restore in **6 min 36 s** against a 60-minute target.

<sub>Also: **[portfolio-ai-assistant](https://github.com/Abheenash/portfolio-ai-assistant)** — a Bedrock (Claude) chatbot over my portfolio.</sub>

---

### ⚙️ Systems & parallel C++ — the layer underneath

**[Parallel Heat Diffusion](https://github.com/Abheenash/parallel-heat-diffusion)** — *std::thread vs OpenMP, head to head*
A 2D finite-difference stencil on a double-buffered grid, parallelized two ways so the strategies can be benchmarked on identical inputs. Scales 1–8 threads with a **memory-bandwidth-bound analysis** explaining exactly where and why it plateaus.

**[Parallel Thread Pool](https://github.com/Abheenash/parallel-thread-pool)** — *producer–consumer*
Persistent workers sleeping on a condition variable and waking on demand — no busy-waiting, graceful drain-and-join shutdown. **5.2x speedup at 8 threads**, with an identical checksum across every thread count proving no data races.

**[Concurrent KV Store](https://github.com/Abheenash/concurrent-kv-store)** — *client–server over TCP*
A multithreaded key-value server on **POSIX sockets**, thread-per-connection with mutex-protected shared state. `SET`/`GET` over the network from many clients at once.

<sub>Contrast worth noting: the thread pool scales near-linearly because it is compute-bound; the stencil plateaus early on the same machine because it is memory-bound. Same hardware, opposite behaviour — which is the point.</sub>

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

**Operations:** Linux/Unix (RHEL) · incident response & on-call · root-cause analysis · runbooks · log analysis · query plans (EXPLAIN) · ServiceNow · Control-M · GDB · Valgrind · strace
**Monitoring:** CloudWatch (alarms, dashboards, Synthetics, Logs Insights, RUM) · X-Ray · PagerDuty · Splunk · Prometheus · Grafana · SLOs · failure drills · restore testing
**Cloud (AWS):** EC2 · ECS Fargate · EKS · ALB · S3 · VPC · IAM · KMS · Lambda · API Gateway · DynamoDB · Cognito · EventBridge · SQS · Step Functions · Systems Manager · SES · SNS · CloudFront · Route 53 · Secrets Manager · WAF · Bedrock
**Databases:** PostgreSQL · RDS · MySQL · DynamoDB · Oracle · SQL Server · ClickHouse
**GenAI:** Amazon Bedrock (Claude Sonnet 4.6 · Haiku · Opus) · AI résumé generation (structured JSON → LaTeX/PDF) · LLM classification & enrichment · JD↔résumé match scoring · RAG-style Q&A
**Containers & Kubernetes:** Amazon EKS · AWS Load Balancer Controller (IRSA) · HPA autoscaling · ECS Fargate · Docker
**IaC & CI/CD:** Terraform · GitHub Actions · OIDC (keyless) · branch protection · Docker · Kubernetes · CronJobs · systemd timers
**DevSecOps & Security:** IAM least privilege · KMS/SSE encryption · Secrets Manager · WAF · Checkov · tfsec · Trivy · gitleaks
**Systems & Software:** TCP/IP · DNS · load balancing · auto scaling · caching · replication · Multi-AZ failover · OOP design · data structures & algorithms · multithreading · POSIX sockets · OpenMP
**Languages:** Python (Boto3) · SQL · Java · Bash · C · C++ · JavaScript · Go · Ruby · Perl

---

### 📜 Certifications

- **AWS Certified DevOps Engineer – Professional** (DOP-C02) · Sep 2026 — [verify](https://www.credly.com/badges/247b90b9-b578-46b1-b987-e778322017c3/public_url)
- **AWS Certified Solutions Architect – Associate** (SAA-C03) · Jul 2026 — [verify](https://www.credly.com/badges/e499fee9-1b8b-4fce-a65c-bc4ddcb2f8b9/public_url)
- **AWS Certified Cloud Practitioner** (CLF-C02) · Jun 2026 — [verify](https://www.credly.com/badges/a9a04423-7b7b-4e75-99c9-8edb3488d9cb/public_url)

---

<div align="center">

<img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Abheenash&layout=compact&theme=tokyonight&hide_border=true&langs_count=8" alt="Top Languages" height="150"/>

</div>

---

<sub>Full write-ups, with the war stories and the benchmarks behind every number above, at <a href="https://abheenash.com">abheenash.com</a>.</sub>
