<div align="center">

# Hi, I'm Abheenash 👋

[![Typing SVG](https://readme-typing-svg.demolab.com?font=Fira+Code&weight=600&size=22&duration=3000&pause=800&color=FF9900&center=true&vCenter=true&width=760&lines=AWS+Certified+Solutions+Architect+%E2%80%93+Associate;Cloud+%C2%B7+DevOps+%C2%B7+Cloud+Security;Serverless+%C2%B7+Kubernetes+%C2%B7+GenAI+on+AWS;Building+%26+operating+secure+infrastructure+on+AWS)](https://abheenash.com)

`Cloud` · `DevOps` · `Cloud Security` · `Terraform` · `Serverless` · `Kubernetes` · `GenAI` · `CI/CD`

<a href="https://abheenash.com"><img src="https://img.shields.io/badge/abheenash.com-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white" alt="Website"/></a>
<a href="https://www.linkedin.com/in/abheenash"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn"/></a>
<a href="https://share.abheenash.com"><img src="https://img.shields.io/badge/Live_Demo-232F3E?style=for-the-badge&logo=amazons3&logoColor=white" alt="Live demo"/></a>
<img src="https://img.shields.io/badge/📍_Houston,_TX-555?style=for-the-badge" alt="Houston, TX"/>
<img src="https://img.shields.io/badge/🟢_Open_to_work-2ea043?style=for-the-badge" alt="Open to work"/>

</div>

**AWS Certified Solutions Architect – Associate & Cloud Practitioner**, building and operating secure, reliable infrastructure on AWS.

---

### ⭐ Flagship — [Job Hunt Command Center](https://github.com/Abheenash/job-hunt-command-center)

An **AI-powered, full-stack serverless job-application tracker** built end-to-end on AWS, private behind Cognito. A JWT-authorized API Gateway HTTP API fronts a Lambda → DynamoDB + versioned S3 backend — all provisioned in Terraform and shipped through a DevSecOps CI/CD pipeline (gitleaks · Checkov/tfsec · Trivy) via GitHub Actions OIDC.

**AI résumé generator** *(headline feature)* — paste a job description and it produces a tailored 2-page résumé as LaTeX plus a server-compiled PDF (bundled tectonic Lambda layer). Model-selectable on **Amazon Bedrock** (Claude Sonnet 4.6 default, Haiku for cheap bulk, Opus for best): the model returns structured JSON that Lambda renders into LaTeX deterministically, so output always compiles and can never fabricate facts outside the candidate's corpus. Includes a weighted match-score rubric, an ATS keyword-match rate, AI-suggested custom fields, auto-fit to 2 pages, and an optional cover letter.

**Event-driven email-intelligence pipeline** — EventBridge → read-only IMAP Scanner Lambda → SQS (+DLQ) → Dispatcher → Step Functions Express (Classify → Enrich). Bedrock classifies recruiter replies, interviews, and rejections, then **auto-advances and enriches** the matching application, with per-message retries and poison-message DLQ isolation. Plus JD field extraction, JD↔résumé match scoring, and a natural-language **"Ask-AI" Q&A** over your applications.

**Self-monitoring** — a CloudWatch golden-signals dashboard, SLO alarms rolled into a composite service-health alarm → SNS, X-Ray tracing on every Lambda and the state machine, per-alarm runbooks, and an AWS Budgets guard on Bedrock spend. A weekly SES digest and conversion analytics (funnel, response rate by source, résumé-match vs. outcome) round it out.

---

### ☁️ More AWS projects — build → ship → operate

**[Serverless File Share](https://github.com/Abheenash/serverless-file-share)** — *build securely* · [live demo](https://share.abheenash.com)
Zero-knowledge, self-destructing file & secret sharing. Payloads are **AES-256-GCM encrypted in the browser** (the key never touches the server), with SSE-KMS defense-in-depth and a DynamoDB **TTL → Streams reaper**. Terraform + keyless CI/CD.

**[AWS EKS Platform](https://github.com/Abheenash/aws-eks-platform)** — *run on Kubernetes*
Kubernetes on **Amazon EKS** via Terraform (official VPC + EKS modules), ALB Ingress (AWS Load Balancer Controller, IRSA), and CPU-based HPA autoscaling, delivered by keyless GitHub Actions CI/CD — proven with live drills (pod self-heal, HPA scale-out).

**[Secure Container Pipeline](https://github.com/Abheenash/secure-container-pipeline)** — *ship securely*
A containerized service on **ECS Fargate** behind a DevSecOps GitHub Actions pipeline (gitleaks · checkov/tfsec · trivy) that blocks insecure merges — proven by automatically blocking a PR carrying a planted secret. All Terraform.

**[Cloud Observability & SRE](https://github.com/Abheenash/cloud-observability-sre)** — *operate reliably*
CloudWatch golden-signals dashboards, X-Ray tracing, SLOs, a Synthetics canary, and RUM — observing his live serverless stack. Terraform.

**[AWS CloudOps Lab](https://github.com/Abheenash/aws-cloudops-lab)** — *day-2 ops*
A day-2 operations lab (EC2 ASG + ALB + RDS) with incident drills, RCAs, and restore tests. Terraform.

<sub>Also: **[portfolio-ai-assistant](https://github.com/Abheenash/portfolio-ai-assistant)** — a Bedrock (Claude) chatbot over my portfolio. Systems foundation in C++ concurrency: **parallel-thread-pool**, **parallel-heat-diffusion**, **concurrent-kv-store**.</sub>

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
<img src="https://img.shields.io/badge/C++-00599C?style=for-the-badge&logo=cplusplus&logoColor=white" alt="C++"/>
<img src="https://img.shields.io/badge/Linux-FCC624?style=for-the-badge&logo=linux&logoColor=black" alt="Linux"/>
<img src="https://img.shields.io/badge/Bash-4EAA25?style=for-the-badge&logo=gnubash&logoColor=white" alt="Bash"/>
</p>

**Cloud (AWS):** Lambda · API Gateway · S3 · DynamoDB · Cognito · Bedrock · EventBridge · SQS · Step Functions · SES · SNS · EKS · ECS Fargate · ECR · VPC · ALB · CloudFront · Route 53 · KMS · Secrets Manager · IAM · WAF · CloudWatch · X-Ray · CloudTrail
**GenAI:** Amazon Bedrock (Claude Sonnet 4.6 · Haiku · Opus) · AI résumé generation (structured JSON → LaTeX/PDF) · LLM classification & enrichment · JD↔résumé match scoring · RAG-style Q&A
**Containers & Kubernetes:** Amazon EKS · AWS Load Balancer Controller (IRSA) · HPA autoscaling · ECS Fargate · Docker
**IaC & CI/CD:** Terraform · GitHub Actions · OIDC (keyless) · branch protection
**DevSecOps & Security:** IAM least privilege · KMS/SSE encryption · Secrets Manager · WAF · Checkov · tfsec · Trivy · gitleaks
**Observability / SRE:** CloudWatch dashboards & alarms · X-Ray · Synthetics · RUM · SLOs & error budgets · incident response
**Languages:** Python · Bash · SQL · C++ · C · JavaScript

---

### 📜 Certifications

- **AWS Certified Solutions Architect – Associate** (SAA-C03)
- **AWS Certified Cloud Practitioner** (CLF-C02)

---

<div align="center">

<img src="https://github-readme-stats.vercel.app/api/top-langs/?username=Abheenash&layout=compact&theme=tokyonight&hide_border=true&langs_count=8" alt="Top Languages" height="150"/>

</div>

---

<sub>Systems foundation: multithreaded C++, OpenMP, POSIX sockets, and performance benchmarking — the layer underneath the cloud work. Full write-ups (with the war stories) at <a href="https://abheenash.com">abheenash.com</a>.</sub>
