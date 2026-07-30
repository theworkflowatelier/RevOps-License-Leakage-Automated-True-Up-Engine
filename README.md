# ⚡ TrueUp — Enterprise License Leakage Engine

[![License: Commercial](https://img.shields.io/badge/License-Commercial%20Enterprise-blue.svg)](https://theworkflowatelier.gumroad.com/l/trueup-enterprise)
[![Platform: n8n](https://img.shields.io/badge/Platform-n8n%20v1.0+-ff6600.svg)](https://n8n.io)
[![API Engine: Stripe](https://img.shields.io/badge/API%20Engine-Stripe%20REST%20v1-008CDD.svg)](https://stripe.com/docs/api)
[![Security: SOC 2 Aligned](https://img.shields.io/badge/Security-Zero%20Data%20Retention-00cc44.svg)](#data-security--privacy-standards)

## 📌 Executive Overview
**TrueUp** is an enterprise-grade automation architecture designed to programmatically eliminate SaaS license leakage for mid-market B2B companies ($5M–$50M ARR). 

Unbilled seat usage is a primary driver of silent Net Revenue Retention (NRR) loss. Instead of relying on manual quarterly CSV VLOOKUPs that miss thousands in uncollected revenue, TrueUp automates the end-to-end reconciliation process in under **3 seconds** using self-hosted [n8n](https://n8n.io) and native Stripe REST API integrations.

---

## ⚡ Key Architectural Highlights
* **Deterministic Cross-Referencing:** Bypasses standard customer endpoints to directly parse the Stripe `/v1/subscriptions` array, mathematically calculating actual product usage against live contracted seat quotas.
* **Idempotent Financial Staging:** Eliminates accidental over-billing. The engine strictly utilizes `auto_advance: false` to generate Draft Invoices, ensuring zero customer credit cards are automatically charged without Human-in-the-Loop (HITL) approval.
* **Asynchronous GUI Escalation:** Automatically routes unbilled revenue opportunities into an interactive Notion Kanban Command Center, triggering zero-latency executive email escalations for high-value overages (>$1,000).

---

### 📐 System Topology
The engine operates across 5 isolated asynchronous processing zones:

| Processing Zone | Architectural Function | Output / Routing Action |
| :--- | :--- | :--- |
| **🔵 Zone 1: Usage Ingestion** | Reads raw active user data from Google Sheets/SQL. | Aggregates product usage into active execution memory. |
| **🟣 Zone 2: Contract Baseline** | Queries Stripe API (`GET /v1/subscriptions`). | Normalizes live baseline contracts and seat quantities. |
| **🟡 Zone 3: Logic Engine** | Cross-references active seats vs. contracted seats. | Calculates strict mathematical seat deltas and ARR leakage. |
| **🟢 Zone 4: Execution Gate** | Evaluates if `OVERAGE_DELTA > 0`. | **True:** Routes to Financial Staging.<br>**False:** Terminates iteration safely. |
| **🔴 Zone 5: Staging & Audit** | Generates Draft Invoices & updates Kanban UI. | Appends immutable records to the `RECON_LEDGER` audit dashboard. |

*(View the complete, color-coded interactive Mermaid diagram in our `/Docs/` directory).*

---

## 🔒 Data Security & Privacy Standards
TrueUp is built for zero-data-retention compliance. All processing occurs entirely within your self-hosted or cloud-isolated n8n workspace. 
* Review our formal **[Data Security Addendum (DSA)](.Doc/Enterprise_Security_Addendum.pdf)** for complete technical specifications regarding TLS 1.3 transit security and scoped OAuth 2.0 access governance.
* **Immutable Evidence Versioning & Audit Ledger:** Go beyond ad-hoc billing updates. The Enterprise Engine automatically maps an immutable audit trail to every single execution, logging the exact `COMPANY_ID`, `OVERAGE_DELTA`, `LEAKAGE_USD`, and execution timestamp into the `RECON_LEDGER`. When external auditors require revenue accounting proof for SOC 2 Type II sampling, your evidence trail is automatically structured and exportable.
* **Least-Privilege API Scoping:** The Stripe API token requires only restricted access (`read: subscriptions`, `write: invoices`), ensuring core payment processing layers remain completely isolated from the workflow.

---

## 🛠️ Open-Source Community Skeleton
For developers, automation enthusiasts, and n8n builders wanting to explore the core deterministic logic, we have provided a **Free Open-Source Skeleton** within this repository. 

This base `.json` workflow contains the foundational cross-referencing math and API routing architecture. It allows you to freely pull the asset into your sandbox, reverse-engineer the logic, and build your own custom rate-limit handling, pagination, and UI routing on top.

👉 **[Access the Free OSS Skeleton in this Repository](./WORKFLOW_SKELETON.json)** *(Link to the skeleton file)*

---

## 🚀 Get the Production Automation Engine
The complete, pre-configured **TrueUp production software bundle** is distributed via Commercial Enterprise License.

### What is Included in the Production Release:
1. **`TrueUp_Production_Engine.json`**: The complete production-grade n8n workflow asset ready for 1-click import.
2. **Notion Command Center Template**: 1-click duplicable Kanban GUI tailored for RevOps workflow management.
3. **Turnkey Deployment Manual**: Step-by-step Standard Operating Procedures (SOPs) and architectural constraints mapping for RevOps teams.
4. **Lifetime Updates & Enterprise Standards**: No recurring SaaS seat fees, no vendor lock-in, and zero per-user billing.

👉 **[Download the Complete TrueUp Enterprise Engine](https://theworkflowatelier.gumroad.com/l/asllps)**
OR Visit 
👉 **[The Workflow Atelier for browsing other assets](https://theworkflowatelier.com)**

---
*For enterprise custom deployments, custom database integrations (SQL/Snowflake), or security reviews, contact our technical team via Gumroad.*
