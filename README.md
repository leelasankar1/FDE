# IIT_R_FDE — Forward Deployed Engineer Masterclass

A 2-day hands-on masterclass covering the full FDE engineering track — from raw data profiling to live AI-powered automation. Built around the **RetailCo** scenario: a real-world churn prediction and outreach system delivered end-to-end.

---

## Folder Structure

```
IIT_R_FDE/
├── Day 1/
│   ├── N8N/                          # Day 1 n8n workflow (data pipeline)
│   ├── GX_retailco_datasource-retailco_sales.html   # Great Expectations Data Docs report
│   ├── RetailCo_Great_Expectations.ipynb            # GX checkpoint notebook
│   ├── retailco_sales_data.csv                      # Raw RetailCo sales dataset
│   ├── Y_profiling.ipynb                            # ydata-profiling notebook
│   └── Y_profiling_retailco.html                    # Profiling HTML report
│
├── Day 2/
│   ├── Day 2 Automation.json                        # n8n multi-channel outreach workflow
│   ├── retailco_clean_60day.csv                     # Cleaned 60-day dataset for modelling
│   ├── RetailCo_MC2_LangChain_Churn.ipynb           # LangChain churn prediction notebook
│   └── retailco_results_today.csv                   # Today's scored churn results
│
└── Assignments/
    ├── Assignment1_HealthTrack.docx                 # Healthcare: patient readmission risk
    ├── Assignment2_UrbanEats.docx                   # Food delivery: cancellation intelligence
    ├── Assignment3_FinSight.docx                    # Banking: loan default prediction
    ├── healthtrack_patient_records.csv              # Synthetic dataset — Assignment 1
    ├── urbaneats_delivery_orders.csv                # Synthetic dataset — Assignment 2
    └── finsight_loan_applications.csv               # Synthetic dataset — Assignment 3
```

---

## Day 1 — Data Readiness for AI

**Objective:** Profile an unknown client dataset, run verifiable data quality checks, translate findings into business language, and hand off a live Slack automation.

| Tool | Purpose |
|---|---|
| `ydata-profiling` | Automated dataset profiling — missing values, distributions, correlations |
| `Great Expectations` | Data quality checkpoint with business-rule expectations |
| `n8n` | Scheduled workflow: HTTP fetch → JS validation → LLM summary → Slack alert |

**Key files:**
- `Y_profiling.ipynb` — 3-line profiling run on the RetailCo dataset
- `Y_profiling_retailco.html` — Full HTML profiling report (open in browser)
- `RetailCo_Great_Expectations.ipynb` — 4-expectation GX checkpoint
- `GX_retailco_datasource-retailco_sales.html` — GX Data Docs report (open in browser)

**n8n workflow (Day 1):** `Schedule Trigger → HTTP Request → Code (JS) → If → Slack (pass) / OpenAI + Slack (fail)`

---

## Day 2 — AI Pipeline & Multi-Channel Outreach

**Objective:** Train a churn classifier, generate personalised outreach messages using LangChain + Claude, write results to Google Sheets, and trigger automated outreach via Slack, Gmail, and WhatsApp.

| Tool | Purpose |
|---|---|
| `scikit-learn` | Random Forest churn classifier |
| `LangChain + Claude` | Personalised outreach message generation per high-risk customer |
| `n8n` | Daily trigger: Google Sheets read → filter high-risk → Slack + Gmail + WhatsApp |

**Key files:**
- `RetailCo_MC2_LangChain_Churn.ipynb` — Full pipeline: train → score → LangChain outreach → results CSV
- `retailco_clean_60day.csv` — Input: 200-row cleaned dataset with churn labels
- `retailco_results_today.csv` — Output: scored customers with risk level, reason, outreach message
- `Day 2 Automation.json` — Import this into n8n for the live multi-channel workflow

**n8n workflow (Day 2):** `Schedule Trigger → Google Sheets → If (high-risk & today) → Gmail + Slack + WhatsApp / Google Sheets Append`

---

## Assignments

Three independent end-to-end assignments across different domains. Each comes with a synthetic dataset and a full brief document.

| Assignment | Domain | Scenario | Key Skills |
|---|---|---|---|
| **Assignment 1 — HealthTrack** | Healthcare | Predict 30-day patient readmission risk for a hospital network | Profiling, GX, Gradient Boosting, LangChain care alerts, n8n clinical briefing |
| **Assignment 2 — UrbanEats** | Food Delivery Ops | Identify cancellation hotspots across restaurant-zone combinations | Profiling, GX, RF classifier, LangChain ops alerts, n8n Gmail + Slack daily brief |
| **Assignment 3 — FinSight** | Retail Banking | Flag high-risk loan applications before approval; real-time branch alerts | Profiling, GX + compliance framing, RF with class imbalance, LangChain credit analyst notes, n8n webhook escalation |

---

## Setup & Requirements

### Python (Notebooks)
```bash
pip install pandas ydata-profiling great-expectations scikit-learn langchain anthropic jupyter
```

### n8n (Workflows)
1. Install n8n: `npm install -g n8n` or use [n8n Cloud](https://n8n.io)
2. Import any `.json` file via **n8n → Workflows → Import from file**
3. Connect credentials: Google Sheets OAuth, Slack OAuth, Gmail OAuth, Twilio (for WhatsApp)

### API Keys needed
- **Anthropic Claude** — for LangChain outreach and LLM alert generation
- **OpenAI** (Day 1 workflow only) — optional, can be swapped for Claude
- **Slack Bot Token** — for Slack node in n8n
- **Gmail OAuth** — for Gmail node in n8n
- **Twilio** — for WhatsApp node in n8n (Day 2)

---

## Concepts Covered

- **FDE Role** — bridging business problems and AI solutions; discovery before development
- **Data Profiling** — ydata-profiling for automated EDA on unknown client datasets
- **Data Contracts** — Great Expectations checkpoints as a quality gate before modelling
- **Business Translation** — converting technical findings into CFO-ready language
- **Supervised Classification** — Random Forest and Gradient Boosting for churn and risk prediction
- **LLM Chaining** — LangChain PromptTemplates + Claude for contextual message generation
- **RAG Architecture** — retrieval-augmented generation pattern for enterprise AI applications
- **Workflow Automation** — n8n for scheduled, event-driven, and webhook-triggered pipelines
- **Multi-channel Delivery** — Slack, Gmail, and WhatsApp outreach from a single n8n workflow

---

## Scenario Context

All Day 1 and Day 2 work is built around **RetailCo** — a fictional retail company with 18 months of CRM sales data. The engagement simulates a real FDE client project:

> *Day 1:* Received raw data → profiled → found quality issues → built daily automated data check → handed off to client  
> *Day 2:* Clean data received → churn model trained → outreach messages generated → live multi-channel automation deployed

---

*Masterclass delivered as part of the IIT Roorkee FDE Engineering Track.*