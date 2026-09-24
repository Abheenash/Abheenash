<div align="center">

# Hi, I'm Abheenash 👋

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=3000&pause=800&color=FF9900&center=true&vCenter=true&width=760&lines=Sixteen+repos%2C+every+one+tested+and+measured;Operate+%C2%B7+Ship+%C2%B7+Build+on+AWS;Three+clouds%2C+Kafka+and+Spark+beside+it;Systems+%26+parallel+C%2B%2B+underneath;AWS+Certified+DevOps+Engineer+%E2%80%93+Professional)](https://abheenash.com)

`Cloud` · `DevOps` · `Cloud Security` · `Terraform` · `Serverless` · `Kubernetes` · `GenAI` · `CI/CD` · `Kafka` · `Spark`

<a href="https://abheenash.com"><img src="https://img.shields.io/badge/abheenash.com-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white" alt="Website"/></a>
<a href="https://www.linkedin.com/in/abheenash"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
<a href="https://share.abheenash.com"><img src="https://img.shields.io/badge/Live_Demo-232F3E?style=for-the-badge&logo=amazons3&logoColor=white" alt="Live demo"/></a>
<img src="https://img.shields.io/badge/📍_Houston,_TX-555?style=for-the-badge" alt="Houston, TX"/>
<img src="https://img.shields.io/badge/🟢_Open_to_work-2ea043?style=for-the-badge" alt="Open to work"/>

</div>

Sixteen repos, every one with a test suite and CI, most with a number that was measured rather than claimed. Where a service can be run locally it is — kind, Calico, LocalStack, Redpanda, a real Spark session, the Firestore and Cosmos emulators — so the claims come from something that executed rather than from something that validated. Certifications: **AWS DevOps Engineer – Professional**, **Solutions Architect – Associate** ([verify](#-certifications)). The projects are the point of this page; the write-ups are at [abheenash.com](https://abheenash.com).

---

### ☁️ Operate

**[production-triage-toolkit](https://github.com/Abheenash/production-triage-toolkit)** · Java 17 · PostgreSQL
Fifteen read-only SQL diagnostics for the problems support teams usually hear about from users — double bookings, ghost badges, stalled sync jobs, lock queues — each ranked, each with a runbook. `SHOW transaction_read_only` is checked on the server, not assumed. 1,069 ms for all fifteen over 10 M rows; the war story is an index that made it 4× slower. `--compare` diffs two runs, `--fail-on-regression` pages only on what got worse, `--format prometheus` feeds node_exporter. 176 tests; a CI gate fails the build if the README drifts from the code.

**[cloud-observability-sre](https://github.com/Abheenash/cloud-observability-sre)** · CloudWatch · X-Ray · FIS · Terraform
The observability layer around a service that was already in production. Golden signals, SLOs with an error budget, symptom-vs-cause alarms rolled into one composite, an outside-in canary, RUM on the website. Then the parts that usually stay on a roadmap: multi-window burn-rate alerts, anomaly bands, and a Fault Injection Service experiment that uses the health alarm as its stop condition. `scripts/drill.sh` throttles the Lambda and times the page: 105 s.

**[aws-cloudops-lab](https://github.com/Abheenash/aws-cloudops-lab)** · EC2 ASG · ALB · RDS · SSM · Terraform
Provision → break → detect → recover → document, five times, on a real stack. Detection times 177 / 289 / 166 s for the three alarms that fired; the two that didn't are the best part — one couldn't trip before the ASG self-healed, one had a threshold above the instance's actual connection ceiling — and both are now different alarms. Timed RDS restore: 6 min 36 s against a 60-minute RTO. Brownfield `terraform import` and drift exercise, monthly operating report, moto-tested Boto3 automation.

### 🚀 Ship

**[secure-container-pipeline](https://github.com/Abheenash/secure-container-pipeline)** · ECS Fargate · GitHub Actions · CodeDeploy
Four gates that fail the build — gitleaks, checkov + tfsec, Trivy (CVEs, image secrets, SBOM), pytest against both a mocked DynamoDB and a real `amazon/dynamodb-local` — behind branch protection, plus keyless cosign signing on the way to ECR. [PR #1](https://github.com/Abheenash/secure-container-pipeline/pull/1) carried a planted AWS key and was blocked by two gates independently. Runtime: private subnets over VPC endpoints, WAF on the ALB, read-only rootfs, `/ready` distinct from `/health`, circuit-breaker rollback, and a `deployment_strategy = "blue_green"` switch for CodeDeploy canary shifting with alarm-triggered rollback.

**[aws-eks-platform](https://github.com/Abheenash/aws-eks-platform)** · EKS · Karpenter · Pod Identity · Argo CD · Prometheus
EKS in Terraform — Karpenter on Spot instead of fixed node groups, EKS Pod Identity instead of IRSA, Argo CD app-of-apps so CI never holds cluster-admin, kube-prometheus-stack with multi-window burn-rate alerts. The cluster is torn down, so the Kubernetes layer is proved on **kind** instead, which is free: a rolling deploy served 40/40 requests and a node drain 100/100, while force-killing every replica at once still cost ~2 s — the counter-test is in the write-up too. Running it found four things `terraform validate` and `kubeconform` both pass: a `WebNoTraffic` alert that could never fire (an empty vector is not zero), a metric label colliding with one service discovery attaches, a service-account token mounted for an API server the app never calls, and a NetworkPolicy of mine that allowed every source instead of one.

**[aws-landing-zone](https://github.com/Abheenash/aws-landing-zone)** · Organizations · SCPs · OIDC · Terraform
Guardrails a workload can't undo: an OU tree, five service control policies kept as plain JSON, deploy roles that trust only `main` of named repos and sit under a permissions boundary, an org CloudTrail with a root-usage alarm. Each SCP is run through a small IAM-condition evaluator in pytest — what it denies and what it must leave alone (IAM from any region, the break-glass role). Not applied on purpose; `docs/apply-order.md` stages it and prices it.

### 🔒 Build

**[serverless-file-share](https://github.com/Abheenash/serverless-file-share)** · Lambda · S3 · DynamoDB Streams · KMS · WebCrypto · [live](https://share.abheenash.com)
Files encrypted in the browser with AES-256-GCM, the key living only in the URL fragment, so the backend stores ciphertext it cannot open. Expiry is DynamoDB TTL → Streams → a reaper Lambda, with an S3 lifecycle rule behind it. Password gate (PBKDF2), atomic download caps, SES notifications. The v2 tests found a filename that could inject HTTP headers through the presigned `Content-Disposition`; that's fixed with RFC 5987 encoding and verified against the live endpoint. The suite now also runs end-to-end against LocalStack, which does the thing a mock structurally cannot: sends real HTTP to the presigned URL with no credentials, and checks that S3 itself refuses a tampered signature and an oversized body.

**[job-hunt-command-center](https://github.com/Abheenash/job-hunt-command-center)** · Bedrock · Step Functions · SQS · Cognito
A serverless job tracker I use daily. Bedrock turns a job description into a 2-page LaTeX résumé via structured JSON (so it compiles and can't invent facts), scores it against a rubric, and an EventBridge → SQS → Step Functions pipeline classifies recruiter email and advances the right application. Self-monitoring dashboard and composite alarm, Budgets guard on model spend, twelve Lambdas' test suites in CI, and a bracket-repair pass for replies cut off at `max_tokens`.

**[portfolio-ai-assistant](https://github.com/Abheenash/portfolio-ai-assistant)** · Bedrock · Lambda · EMF
The chat widget on the portfolio: knowledge base in a cached system prompt, no vector store, origin allow-list enforced in code. Each request logs an EMF record — latency, tokens, cache reads, dollars — so the cost is a CloudWatch graph: $0.0015 per answer. A 12-case injection/grounding eval is committed with its results from the live endpoint (12/12).

---

### 🌍 Portable — three clouds, and the data tier

**[azure-container-platform](https://github.com/Abheenash/azure-container-platform)** · Container Apps · Cosmos DB · ACR
**[gcp-container-platform](https://github.com/Abheenash/gcp-container-platform)** · Cloud Run · Firestore · Artifact Registry
The same notes API as `secure-container-pipeline`, built twice more — same routes, same probes, same log shape — so the three can be diffed. **The deliverable is the diff, not the app:** [`aws-vs-azure.md`](https://github.com/Abheenash/azure-container-platform/blob/main/docs/aws-vs-azure.md) and [`three-clouds.md`](https://github.com/Abheenash/gcp-container-platform/blob/main/docs/three-clouds.md) are what a second and third cloud actually show — which decisions were engineering and which were AWS vocabulary. One concrete example, asserted against all three real engines: a missing record makes Cosmos *raise*, DynamoDB return a response with no item, and Firestore return a snapshot whose `.exists` is false. Both suites run against the vendors' own emulators, free and subscription-free.

**[kafka-stream-processor](https://github.com/Abheenash/kafka-stream-processor)** · Kafka · MSK Serverless · Redpanda
The three things that actually go wrong — a rebalance, a redelivery, and one poison record in a partition — rather than the produce/consume every quickstart shows. SQS acknowledges individual messages; Kafka commits an *offset*, and that one difference is what changes your code. Manual commits, idempotency keyed on `(topic, partition, offset)`, a dead-letter topic, topic-scoped IAM. Tested against a fake broker and a real Redpanda. [`kafka-vs-sqs.md`](https://github.com/Abheenash/kafka-stream-processor/blob/main/docs/kafka-vs-sqs.md) argues why `job-hunt-command-center` should *stay* on SQS.

**[spark-lca-pipeline](https://github.com/Abheenash/spark-lca-pipeline)** · PySpark · EMR Serverless
The DOL disclosure pipeline behind `h1b-sponsor-intel`, rewritten for the size the data actually is — millions of rows per fiscal year, one file per quarter, a column set that drifts between them. Explicit schema over `inferSchema`, quarantine-not-drop for bad rows, skew-aware aggregation. Unlike the infrastructure repos this one has **measured output**, because PySpark runs locally and needs no account: 15 tests against a real Spark session, end to end. ANSI mode was the lesson — `cast()` on `"N/A"` raises instead of returning null, which quietly broke the whole quarantine design until `try_cast` replaced it.

---

### ⚙️ Systems & parallel C++

Three single-file demos rebuilt into projects with CMake, tests that pass under ThreadSanitizer and AddressSanitizer in CI, and benchmarks that report the losing rows too.

**[concurrent-kv-store](https://github.com/Abheenash/concurrent-kv-store)** · C++17 · POSIX sockets · kqueue / epoll
A Redis-shaped server: 64-way sharded map under `shared_mutex`, TTLs with lazy + swept expiry, a 22-command line protocol, AOF persistence with atomic compaction and three fsync modes, and three I/O models to compare (thread-per-connection, `poll`, kqueue/epoll). 5.09 M req/s pipelined versus 1.23 M with the original global mutex; kqueue halves the p99 that poll leaves behind. Five macOS socket bugs surfaced by the test suite are documented in the README.

**[parallel-thread-pool](https://github.com/Abheenash/parallel-thread-pool)** · C++17 · header-only
Work-stealing deques, futures with exception propagation, a `parallel_for` whose waiting thread helps (so nesting can't deadlock), backpressure, sleeper-aware wake-ups. 5.37× on 10 cores; spin-before-park lifted a million tiny tasks from 0.60 to 1.98 M/s; fork-join 4.24 M vs 3.38 M tasks/s. The heavy-tailed benchmark is a tie with a global queue, and the README explains why instead of dropping the row.

**[parallel-heat-diffusion](https://github.com/Abheenash/parallel-heat-diffusion)** · C++17 · OpenMP · std::thread
One flat grid, four backends, 320 backend × thread-count runs `memcmp`-identical to serial, mirror symmetry exact to the bit. A STREAM probe sits next to the results: the stencil hits ~100 GB/s at four threads against a measured 98 GB/s ceiling, so 1.9× is the wall; on a cache-resident grid the spin barrier reaches 2.89× where spawn-per-step runs slower than serial.

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
