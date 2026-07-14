---
title: "Security for Fabric Data Warehouse — Series Index & Publishing Guide"
description: "All 25 how-to posts across five layers, with a suggested publishing cadence."
series: "Security for Fabric Data Warehouse"
layer: "Index"
order: 0
---

# Security for Fabric Data Warehouse — Series Index & Publishing Guide

> All 25 how-to posts across five layers, with a suggested publishing cadence.

*Fabric Data Warehouse Technical Insiders · 25-post blog series · Level 300 · Companion index*

This is the companion index for the **Security for Fabric Data Warehouse** blog series — 25 prescriptive, how-to posts organized into five layers, built from the network up. Each post is a self-contained deliverable (prerequisites → numbered steps → validation → limitations → rollback) with its own architecture diagram, scoped to the Warehouse and SQL analytics endpoint.

Files are named `Fabric-DW-Security-NN-…​.docx` where `NN` runs 01–25, so they sort in publishing order. This index (00) sits at the front of that set.

![Figure — The five security layers of the series, built from the network up.](images/fabric-dw-security-00.png)

*Figure — The five security layers of the series, built from the network up.*

## How to use the series

- **Read (and publish) in order.** The layers build on one another — network access first, then identity, then what data is visible, then how the data itself is protected, then how you govern and watch it.
- **Each post stands alone.** A reader can land on any single post and act on it without the others, which is what makes the set publishable as a running series.
- **Every step is grounded in Microsoft Learn** (pages current through mid-2026), scoped to the Warehouse and SQL analytics endpoint.

## Layer 1 — Network security

| # | Post | Focus |
| --- | --- | --- |
| 01 | **Lock the Warehouse SQL Endpoint Behind Workspace-Level Private Links** | Route SQL connections over Azure Private Link; deny public access |
| 02 | **Restrict the Warehouse to Approved IPs with Workspace Firewall Rules** | IP allow-lists (single IP, range, CIDR) on the workspace |
| 03 | **Gate Warehouse Sign-ins with Microsoft Entra Conditional Access** | MFA, compliant device, and location on SQL-endpoint sign-ins |
| 04 | **Stop Warehouse Data Exfiltration with Outbound Access Protection** | Enable OAP; block unapproved outbound connections |
| 05 | **Load Data into a Protected Warehouse with the OneLake Ingestion Pattern** | OneLake-sourced COPY INTO under outbound access protection |

## Layer 2 — Identity & access

| # | Post | Focus |
| --- | --- | --- |
| 06 | **Connect to the Warehouse with Microsoft Entra ID** | Entra-only authentication; the Read floor; access via groups |
| 07 | **Control Warehouse Access with Fabric Workspace Roles** | Admin / Member / Contributor / Viewer capabilities |
| 08 | **Grant Granular Warehouse Permissions with T-SQL** | GRANT / DENY / REVOKE and database roles |
| 09 | **Share the Warehouse and SQL Analytics Endpoint with Least Privilege** | Read / ReadData / ReadAll; least-privilege sharing |
| 10 | **Automate Warehouse Access with Service Principals** | SPN via workspace role or Entra group; scoped in T-SQL |

## Layer 3 — Granular data access

| # | Post | Focus |
| --- | --- | --- |
| 11 | **Restrict Tables, Views, and Procedures with Object-Level Security** | GRANT / DENY on specific objects by role |
| 12 | **Filter Rows per User with Row-Level Security** | Security policy + inline predicate on USER_NAME() |
| 13 | **Hide Sensitive Columns with Column-Level Security** | GRANT SELECT on a column subset; SELECT * fails |
| 14 | **Obfuscate Sensitive Values with Dynamic Data Masking** | MASKED WITH functions; UNMASK / CONTROL |
| 15 | **Layer OLS, RLS, CLS, and Masking for Defense in Depth** | Combine and validate the four granular controls |

## Layer 4 — Data protection

| # | Post | Focus |
| --- | --- | --- |
| 16 | **Encrypt the Warehouse with Customer-Managed Keys** | CMK + Azure Key Vault; envelope encryption, rotate/revoke |
| 17 | **Classify and Protect Warehouse Data with Sensitivity Labels** | Purview labels that travel with exports |
| 18 | **Detect Sensitive Data in the Warehouse with DLP Policies** | Purview DLP now covers Fabric warehouses |
| 19 | **Choose the SQL Endpoint Access Mode: OneLake or SQL** | User-identity (OneLake) vs delegated (SQL) modes |
| 20 | **Assemble a Data-Protection Posture for the Warehouse** | Rollout order and control map (capstone) |

## Layer 5 — Governance & monitoring

| # | Post | Focus |
| --- | --- | --- |
| 21 | **Configure SQL Audit Logs for the Warehouse** | Enable, scope event categories, retention |
| 22 | **Review and Investigate Warehouse Audit Activity** | In-warehouse T-SQL + tenant unified audit log |
| 23 | **Control Microsoft Access with Customer Lockbox** | Approve/deny Microsoft-engineer access requests |
| 24 | **Monitor Warehouse Activity with Query Insights and DMVs** | queryinsights views + dynamic management views |
| 25 | **Govern the Warehouse with Microsoft Purview** | Unified Catalog, lineage, endorsement |

## Suggested publishing cadence

Publish in numbered order so the audience builds understanding foundation-up. **Weekly is the recommended cadence** — one post per week keeps the series visible for about six months. A **bi-weekly** cadence (~12 months) suits a lighter schedule; a five-day **sprint per layer** suits a launch or event moment.

| Layer | Posts | Suggested window | Publishing hook |
| --- | --- | --- | --- |
| L1 · Network security | 01–05 | Weeks 1–5 | “Lock down the front door” — start with the foundation |
| L2 · Identity & access | 06–10 | Weeks 6–10 | “Who gets in, and as what” |
| L3 · Granular data access | 11–15 | Weeks 11–15 | “What they can see once inside” |
| L4 · Data protection | 16–20 | Weeks 16–20 | “Protecting the data itself” |
| L5 · Governance & monitoring | 21–25 | Weeks 21–25 | “Prove it, and watch it” |

- Open each layer with a 2–3 sentence framing (why this layer matters) and close each post with a pointer to the next.
- Consider a short **kickoff/overview** post to launch the series (this five-layer map is its backbone) and a **wrap-up recap** at the end.
- The numbering leaves room for interstitials — insert a “layer recap” between batches without renumbering the core 25.
