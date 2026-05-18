# 🔐 Multi-Cloud Zero Trust Security & Compliance Automation Platform

<p align="left">
  <img src="https://img.shields.io/badge/AWS-FF9900?style=for-the-badge&logo=amazonaws&logoColor=white"/>
  <img src="https://img.shields.io/badge/Azure-0078D4?style=for-the-badge&logo=microsoftazure&logoColor=white"/>
  <img src="https://img.shields.io/badge/GCP-4285F4?style=for-the-badge&logo=googlecloud&logoColor=white"/>
  <img src="https://img.shields.io/badge/Terraform-623CE4?style=for-the-badge&logo=terraform&logoColor=white"/>
  <img src="https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white"/>
  <img src="https://img.shields.io/badge/OPA%2FRego-7D3C98?style=for-the-badge"/>
  <img src="https://img.shields.io/badge/GitHub%20Actions-2088FF?style=for-the-badge&logo=githubactions&logoColor=white"/>
</p>

<p align="left">
  <img src="https://img.shields.io/badge/Zero%20Trust-Enforced-success?style=flat-square"/>
  <img src="https://img.shields.io/badge/CNAPP%2FCSPM-Automated-success?style=flat-square"/>
  <img src="https://img.shields.io/badge/Compliance-FedRAMP%20%7C%20SOC%202%20%7C%20NIST-blue?style=flat-square"/>
  <img src="https://img.shields.io/badge/IaC-Policy--as--Code-blueviolet?style=flat-square"/>
</p>

---

## 📌 Overview

A fully automated **Zero Trust / ZTNA** security enforcement and **GRC compliance automation** platform deployed across **AWS, Azure, and GCP** from a single **Terraform** IaC codebase. This platform eliminates implicit trust, continuously detects misconfigurations and drift, enforces policy-as-code guardrails, and auto-generates audit evidence for **FedRAMP Moderate**, **SOC 2 Type II**, **NIST 800-53**, **CIS Benchmarks**, and **HIPAA** control families.

> **Key Result:** 98% compliance posture maintained across 150+ cloud resources with 70% reduction in manual GRC review overhead.

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                    DEVELOPER / CI/CD LAYER                      │
│  Git Push → GitHub Actions → OPA/Rego Gates → SAST/DAST/SCA   │
│             Gitleaks/TruffleHog → IaC Scan → PR Block/Approve  │
└────────────────────────┬────────────────────────────────────────┘
                         │ Compliant IaC only
┌────────────────────────▼────────────────────────────────────────┐
│                  ZERO TRUST ENFORCEMENT LAYER                   │
│                                                                 │
│  ┌──────────────┐   ┌──────────────┐   ┌──────────────────┐   │
│  │     AWS      │   │    Azure     │   │       GCP        │   │
│  │  Config Rules│   │   Policy     │   │  Security        │   │
│  │  GuardDuty   │   │   Defender   │   │  Command Center  │   │
│  │  IAM/IRSA    │   │   Sentinel   │   │  Chronicle       │   │
│  └──────┬───────┘   └──────┬───────┘   └────────┬─────────┘   │
│         └──────────────────┼───────────────────┘              │
│                  ┌─────────▼────────┐                          │
│                  │  CSPM + CWPP     │                          │
│                  │  Engine (Python) │                          │
│                  │  Misconfiguration│                          │
│                  │  Drift Detection │                          │
│                  └─────────┬────────┘                          │
└────────────────────────────┼────────────────────────────────────┘
                             │
┌────────────────────────────▼────────────────────────────────────┐
│                  COMPLIANCE & REMEDIATION LAYER                 │
│                                                                 │
│  Auto-Remediation → Jira Tickets → Audit Evidence Collection   │
│  SOC 2 CC6/CC7 · FedRAMP AC/CM · NIST 800-53 · HIPAA · CIS   │
│                                                                 │
│  GitOps (Flux/ArgoCD) → OPA Gate → Drift-Free Sync            │
└─────────────────────────────────────────────────────────────────┘
```

---

## ✨ Key Features

### 🔒 Zero Trust / ZTNA Enforcement
- Identity-aware proxy controls with continuous device posture validation
- Least-privilege IAM boundaries enforced via **RBAC + ABAC + IGA** across all three clouds
- Workload Identity Federation replacing static credentials
- Micro-segmentation eliminating implicit east-west trust

### 🛡️ CSPM + CWPP Engine
- Python/Boto3 engine auditing **150+ cloud resource configurations** in real-time
- Detects misconfigurations, drift, and policy violations across AWS, Azure, and GCP simultaneously
- Auto-generates remediation tickets with severity scoring and compliance mapping
- Integrated with **AWS Config Rules**, **Azure Policy**, and **GCP Security Command Center**

### ⚙️ Shift-Left DevSecOps Pipeline
- **OPA/Rego policy-as-code** gates block non-compliant IaC at PR stage
- **SAST** — static analysis on every commit
- **SCA/Dependency Scanning** — open-source vulnerability detection
- **Secrets Detection** — Gitleaks + TruffleHog prevent credential leakage
- **DAST** — runtime scanning integrated into staging pipelines

### 📋 GRC Compliance Automation
- Automated audit evidence collection mapped to control families:
  - SOC 2 Type II — CC6, CC7
  - FedRAMP Moderate — AC, CM, SI control families
  - NIST 800-53 — AC-2, AC-6, CM-2, CM-6, SI-2
  - HIPAA — Administrative, Physical, Technical Safeguards
  - CIS Benchmarks — Level 1 & 2

### 🔄 GitOps Continuous Compliance
- **Flux + ArgoCD + Helm** enforce drift-free cluster and infrastructure state
- Every infrastructure change passes OPA gates before sync
- Fully auditable change history with compliance evidence auto-linked

---

## 📊 Results & Impact

| Metric | Result |
|--------|--------|
| Compliance posture | **98%** across all frameworks |
| Non-compliant IaC blocked | **100%** at PR stage |
| GRC review overhead | **70% reduction** |
| Cloud resources monitored | **150+** across 3 clouds |
| Manual audit hours eliminated | **15+ hrs/week** |
| Compliance frameworks covered | **5** (SOC 2, FedRAMP, NIST, HIPAA, CIS) |

---

## 🗂️ Repository Structure

```
multicloud-zero-trust-platform/
├── terraform/
│   ├── aws/                    # AWS Zero Trust IaC modules
│   ├── azure/                  # Azure Policy + Defender config
│   ├── gcp/                    # GCP SCC + IAM config
│   └── modules/                # Shared reusable modules
├── opa-policies/
│   ├── aws/                    # AWS resource policies (Rego)
│   ├── azure/                  # Azure resource policies (Rego)
│   ├── gcp/                    # GCP resource policies (Rego)
│   └── tests/                  # OPA unit tests
├── cspm-engine/
│   ├── scanner.py              # Main CSPM scanning engine
│   ├── remediation.py          # Auto-remediation playbooks
│   ├── evidence_collector.py   # GRC audit evidence collection
│   └── compliance_mapper.py    # Control family mapping
├── pipelines/
│   ├── .github/workflows/      # GitHub Actions CI/CD
│   ├── sast-scan.yml           # SAST pipeline
│   ├── sca-scan.yml            # Dependency scanning
│   ├── iac-scan.yml            # IaC policy-as-code gate
│   └── secrets-scan.yml        # Gitleaks + TruffleHog
├── gitops/
│   ├── flux/                   # Flux GitOps config
│   └── argocd/                 # ArgoCD app definitions
├── compliance/
│   ├── soc2/                   # SOC 2 evidence templates
│   ├── fedramp/                # FedRAMP control mappings
│   ├── nist/                   # NIST 800-53 mappings
│   └── hipaa/                  # HIPAA control mappings
├── docs/
│   ├── architecture.md
│   ├── setup-guide.md
│   └── compliance-guide.md
└── README.md
```

---

## 🚀 Getting Started

### Prerequisites
```bash
# Required tools
terraform >= 1.5.0
python >= 3.11
opa >= 0.58.0
aws-cli >= 2.x
az-cli >= 2.x
gcloud >= 450.x
flux >= 2.x
```

### 1. Clone the repository
```bash
git clone https://github.com/deekshithreddyk/multicloud-zero-trust-platform.git
cd multicloud-zero-trust-platform
```

### 2. Configure cloud credentials
```bash
# AWS
export AWS_PROFILE=your-profile

# Azure
az login

# GCP
gcloud auth application-default login
```

### 3. Deploy Zero Trust IaC
```bash
cd terraform/aws
terraform init
terraform plan -var-file="vars/production.tfvars"
terraform apply
```

### 4. Run CSPM Scanner
```bash
cd cspm-engine
pip install -r requirements.txt
python scanner.py --clouds aws,azure,gcp --output reports/
```

### 5. Validate OPA Policies
```bash
cd opa-policies
opa test ./tests/ -v
opa eval --data aws/ --input sample-resource.json "data.aws.deny"
```

---

## 🛠️ Tech Stack

| Category | Tools |
|----------|-------|
| Cloud | AWS, Azure, GCP |
| IaC | Terraform, CloudFormation |
| Policy-as-Code | OPA/Rego, AWS Config Rules, Azure Policy |
| CI/CD | GitHub Actions, GitLab CI |
| GitOps | Flux, ArgoCD, Helm |
| CSPM | Python/Boto3, AWS Security Hub, GCP SCC |
| Security Scanning | SAST, DAST, SCA, Gitleaks, TruffleHog, Trivy |
| Compliance | SOC 2, FedRAMP, NIST 800-53, HIPAA, CIS, ISO 27001 |
| Language | Python, Bash, Go, Rego |

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

---

<p align="center">Built by <a href="https://github.com/deekshithreddyk">Deekshith Reddy Kothakapu</a> · Cloud Security Engineer</p>
