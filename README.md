# 🔐 AI Security Triage

## Overview

**AI Security Triage** is a container-ready, Python-based vulnerability prioritization engine designed for reproducible, team-based security analysis.

Unlike traditional approaches that rely solely on CVSS scores, this system incorporates:

- Business impact  
- Asset exposure  
- Operational context  

to produce a **unified, explainable risk score** and **decision-ready remediation priorities**.

This project simulates a real-world triage workflow used by **SOC** and **vulnerability management teams**.

---

## 👨‍💻 My Contribution

- Tested and validated triage logic across datasets  
- Supported deployment and execution workflows  
- Refined scoring outputs for consistency and explainability  
- Ensured reliability in a team-based execution environment  

---

## 🎯 Core Capabilities

- Merge asset context with vulnerability findings  
- Apply weighted, explainable risk scoring  
- Assign human-readable risk tiers (Critical / High / Medium / Low)  
- Categorize risks (e.g., Network Exposure, Business Impact)  
- Flag escalation scenarios with justification  
- Generate prioritized, decision-ready outputs  

---

## ⚙️ System Workflow

### 1. Data Ingestion

- Load `assets.csv`  
- Load `vulnerabilities.csv`  
- Merge datasets on `asset_id`  

---

### 2. Risk Scoring Model

The risk score is calculated as:


(severity_cvss × exploitability)

(business_criticality × data_sensitivity)
exposure_modifier

**Notes:**
- External exposure increases risk weight  
- Final score is rounded to an integer  
- Model is fully deterministic and explainable  

---

### 3. Risk Tier Mapping

| Score Range | Risk Level |
|------------|-----------|
| ≥ 75       | Critical  |
| ≥ 50       | High      |
| ≥ 25       | Medium    |
| < 25       | Low       |

---

### 4. Risk Categorization

Rule-based tagging enhances explainability:

- Critical Infrastructure  
- Network Exposure  
- Exploitable Vulnerability  
- High Business Impact  
- General Risk  

---

### 5. Escalation Logic

A vulnerability is escalated if any of the following conditions are met:

- Risk level is **Critical**  
- High-risk vulnerability on an **externally exposed asset**  
- Business criticality ≥ 8  
- Exploitability ≥ 8  

**Output Fields:**
- `escalation_flag`  
- `escalation_reason`  

---

## 📊 Output

Results are generated at:


output/results.csv


### Output Includes:

- `run_id`  
- `generated_at`  
- Asset context fields  
- `risk_score`  
- `risk_level`  
- `risk_category`  
- `escalation_flag`  
- `escalation_reason`  

### Additional Features:

- Results sorted by highest risk first  
- Console summary includes:
  - Total rows processed  
  - Distribution by risk level  
  - Top prioritized vulnerabilities  

---

## 🚀 Quick Start

```bash
pip install -r requirements.txt
python src/triage.py
📂 Project Structure
ai-security-triage/
│
├── src/
│   ├── ingest.py
│   ├── scoring.py
│   └── triage.py
│
├── data/
│   ├── assets.csv
│   └── vulnerabilities.csv
│
├── docs/
│   └── walkthrough.md
│
├── output/   # ignored by Git
│
├── requirements.txt
└── README.md

---
## 📦 Reproducibility

This project does not store generated outputs in version control.

To reproduce results:

```bash
python src/triage.py
```

Outputs will be generated in:

```bash
output/results.csv
```