<div align="center">

# Hi, I'm Abheenash 👋

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=3200&pause=900&color=FF9900&center=true&vCenter=true&width=780&lines=Every+number+here+was+measured%2C+not+estimated;Including+the+ones+that+didn't+flatter+me;Cloud+%C2%B7+DevOps+%C2%B7+Platform+%C2%B7+SRE+on+AWS;AWS+Certified+DevOps+Engineer+%E2%80%93+Professional)](https://abheenash.com)

`Cloud` · `DevOps` · `Cloud Security` · `Terraform` · `Kubernetes` · `Serverless` · `GenAI` · `CI/CD` · `Kafka` · `Spark`

<a href="https://abheenash.com"><img src="https://img.shields.io/badge/abheenash.com-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white" alt="Website"/></a>
<a href="https://www.linkedin.com/in/abheenash"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
<a href="https://share.abheenash.com"><img src="https://img.shields.io/badge/Live_Demo-232F3E?style=for-the-badge&logo=amazons3&logoColor=white" alt="Live demo"/></a>
<img src="https://img.shields.io/badge/📍_Houston,_TX-555?style=for-the-badge" alt="Houston, TX"/>
<img src="https://img.shields.io/badge/🟢_Open_to_work-2ea043?style=for-the-badge" alt="Open to work"/>

</div>

**Sixteen projects, all tested and running in CI. The thing worth knowing about them is that
the numbers were measured on real hardware and real clusters — and the measurements that went
against me are still in the READMEs.**

---

## Four times I was wrong

Skip the rest of this page if you like. This is the part that says what I'm actually like to work with.

| I expected | What happened | What I did about it |
|---|---|---|
| Adding the obvious index would speed up the slowest check | It made the run **slower** — the planner swapped one bulk hash join for 910,750 individual index probes | Rewrote it as a window function over a sorted pass: **2,147 ms → 526 ms**. Then measured index usage and deleted four indexes with zero scans (410 MB). [→](https://github.com/Abheenash/production-triage-toolkit/blob/main/docs/benchmark.md) |
| My Kubernetes manifests were fine — every validator passed them | Running them on a free local cluster found **five bugs**, including an alert meant to catch total silence that **could never fire** (in that language, "no data at all" is not zero) | Fixed all five and wrote up the run, including the counter-test where killing every replica at once still cost ~2 s — because no manifest can prevent that. [→](https://github.com/Abheenash/aws-eks-platform/blob/main/docs/drills/2026-09-24-kind-cluster.md) |
| My five failure drills would trip five alarms | **Two never fired.** One couldn't: the autoscaler replaced the instance faster than the alarm's window. The other's threshold was 80 connections on a database whose real ceiling is ~87 | Both became different alarms — one on *healthy* host count, one at 70% of the instance class's actual limit. [→](https://github.com/Abheenash/aws-cloudops-lab) |
| Work-stealing would beat a simple global queue | On heavy-tailed workloads it's a **tie** | Published the tie. A benchmark table that only shows the rows where you won isn't a benchmark. [→](https://github.com/Abheenash/parallel-thread-pool) |

---

## Start here

**[aws-eks-platform](https://github.com/Abheenash/aws-eks-platform)** — *Kubernetes on AWS, the way a team would run it*
Terraform-provisioned EKS: Karpenter on Spot instead of fixed node groups, Pod Identity instead of IRSA, Argo CD so CI never holds cluster-admin, Prometheus with multi-window burn-rate alerts. The cluster is destroyed to avoid cost, so the Kubernetes layer is proven on a free local one instead — **a rolling deploy served 40/40 requests, a node drain 100/100**, and force-killing every replica cost ~2 s, which is in the write-up too.

**[secure-container-pipeline](https://github.com/Abheenash/secure-container-pipeline)** — *A build pipeline that actually stops things*
Four gates that fail the build, plus keyless signing on the way to ECR. **[PR #1](https://github.com/Abheenash/secure-container-pipeline/pull/1) carried a deliberately planted AWS key and was blocked by two gates independently.** Tests run against both a mocked DynamoDB and a real one. The container ships without a package installer — and the instruction that removes it now fails the build if it ever stops working, because it used to fail *silently*.

**[production-triage-toolkit](https://github.com/Abheenash/production-triage-toolkit)** — *Fifteen read-only database diagnostics, in Java*
The problems support teams hear about from users — double bookings, ghost badges, stalled sync jobs, lock queues — each ranked, each with a runbook. **1,069 ms for all fifteen across 10 million rows.** Read-only is enforced on the server, not assumed. 176 tests, and a CI gate that fails the build if the README stops matching the code.

<details>
<summary><b>The other thirteen</b> — click to expand</summary>

<br>

**Operate**
- **[cloud-observability-sre](https://github.com/Abheenash/cloud-observability-sre)** — golden signals, SLOs with an error budget, burn-rate alerts, and a fault-injection experiment that uses the health alarm as its own stop condition. `scripts/drill.sh` throttles the function and times the page: **105 s**.
- **[aws-cloudops-lab](https://github.com/Abheenash/aws-cloudops-lab)** — provision → break → detect → recover → document, five times on a real stack. Detection at **177 / 289 / 166 s**; a timed database restore in **6 min 36 s** against a 60-minute target.

**Ship**
- **[aws-landing-zone](https://github.com/Abheenash/aws-landing-zone)** — guardrails a workload can't undo: an account tree, five service control policies as plain JSON, deploy roles that trust only `main` of named repos. Each policy is run through a small permissions evaluator in tests — what it denies *and* what it must leave alone.

**Build**
- **[serverless-file-share](https://github.com/Abheenash/serverless-file-share)** · [live](https://share.abheenash.com) — files encrypted in the browser, the key living only in the URL fragment, so the backend stores something it cannot open. Tests now send real HTTP to the signed upload link with no credentials, and check that the storage service itself refuses a tampered signature.
- **[job-hunt-command-center](https://github.com/Abheenash/job-hunt-command-center)** — a serverless job tracker I use daily. Generates a 2-page résumé from a job description via structured output, so it compiles and can't invent facts; classifies recruiter email through a queue-and-workflow pipeline.
- **[portfolio-ai-assistant](https://github.com/Abheenash/portfolio-ai-assistant)** — the chat widget on my site. Every request logs its own cost, so the price is a graph: **$0.0015 per answer**. A 12-case prompt-injection eval is committed with its results.

**Portable — the same service, three clouds**
- **[azure-container-platform](https://github.com/Abheenash/azure-container-platform)** · **[gcp-container-platform](https://github.com/Abheenash/gcp-container-platform)** — the same API built again on Azure and on Google Cloud, so the three can be diffed. **The write-up is the deliverable, not the app.** One concrete difference, checked against all three real engines: a missing record makes one *raise an error*, one return an empty response, and one return a result object that says it doesn't exist.

**Data & streaming**
- **[kafka-stream-processor](https://github.com/Abheenash/kafka-stream-processor)** — the three things that actually go wrong (a rebalance, a redelivery, one poison record), not the produce/consume every tutorial shows. The companion doc argues why my *other* project should **stay** on a simpler queue.
- **[spark-lca-pipeline](https://github.com/Abheenash/spark-lca-pipeline)** — a data pipeline rewritten for the size the data really is: millions of rows per year, one file per quarter, columns that drift between them. Runs locally, so this one has **measured output** rather than a plan.

**Systems & parallel C++** — *three demos rebuilt as projects, tested under thread and memory sanitizers*
- **[concurrent-kv-store](https://github.com/Abheenash/concurrent-kv-store)** — a Redis-shaped server: sharded map, TTLs, a 22-command protocol, append-only persistence, three I/O models to compare. **5.09 M requests/sec pipelined against 1.23 M** with the original single global lock.
- **[parallel-thread-pool](https://github.com/Abheenash/parallel-thread-pool)** — work-stealing, futures with exception propagation, a parallel loop whose waiting thread helps so nesting can't deadlock. **5.37× on 10 cores.**
- **[parallel-heat-diffusion](https://github.com/Abheenash/parallel-heat-diffusion)** — one grid, four backends, 320 combinations bitwise-identical to the serial reference. A memory-bandwidth probe sits beside the results and explains why **1.9× is the ceiling, not a bug**.

</details>

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
**Containers & Kubernetes:** Amazon EKS · Karpenter · EKS Pod Identity · AWS Load Balancer Controller · Argo CD (GitOps) · HPA · PodDisruptionBudgets · NetworkPolicy · Helm · kind · OpenShift port · ECS Fargate · Azure Container Apps · Google Cloud Run · Docker
**IaC & CI/CD:** Terraform (AWS, azurerm, google) · `terraform test` with mocked providers · GitHub Actions · OIDC (keyless) · pre-commit · branch protection
**Multi-cloud:** Azure (Container Apps · Cosmos DB · ACR · managed identity) · GCP (Cloud Run · Firestore · Artifact Registry · workload identity federation)
**Data & streaming:** Apache Kafka (MSK Serverless · Redpanda) · Apache Spark / PySpark (EMR Serverless) · DynamoDB · PostgreSQL
**DevSecOps & Security:** IAM least privilege · KMS/SSE encryption · Secrets Manager · WAF · Checkov · tfsec · Trivy · gitleaks · SBOM (CycloneDX) · cosign keyless signing · Dependabot
**Observability / SRE:** CloudWatch dashboards & alarms · Prometheus & Grafana (kube-prometheus-stack, ServiceMonitor, PrometheusRule) · Datadog · Splunk · X-Ray · Synthetics · RUM · SLOs, error budgets & burn-rate alerts · anomaly detection · AWS Fault Injection Service · incident response · production triage & runbooks · PostgreSQL diagnostics
**Languages:** Python · Java · Bash · SQL · C++ · C · JavaScript · Go · Ruby · Perl
**Testing:** pytest · moto · JUnit · testcontainers-style local services (LocalStack · DynamoDB Local · Firestore & Cosmos emulators · Redpanda · kind + Calico) · ThreadSanitizer & AddressSanitizer

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
