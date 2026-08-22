---
title: "Security for Power BI Reports — Series Overview"
description: "A prescriptive, 10-part how-to series for sharing, public exposure, export, and classification."
series: "Security for Power BI Reports"
layer: "Index"
order: 0
---

# Security for Power BI Reports — Series Overview

> A prescriptive, 10-part how-to series for sharing, public exposure, export, and classification.

*Power BI Technical Insiders · 10-part how-to series · Level 300 · Start here*

A report is a **view over a semantic model**, not a security boundary. Sharing one shares access to the model beneath it — and a consumer's access is not limited to what the report displays. Most report-level security incidents start with that misunderstanding.

This series covers the report layer in **10 prescriptive entries** across four layers: how content is shared, how it becomes publicly exposed, how data leaves through export, and how it's classified. Every entry is a self-contained runbook — **prerequisites → numbered steps → validation → limitations → rollback** — with its own architecture diagram.

This overview is the entry point. Use it to find the layer you need, then work through that layer's entries in order.

![Figure — The four security layers of the series.](images/fabric-rpt-security-00.png)

*Figure — The four security layers of the series.*

## How to use this series

- **Secure the model first.** This series assumes RLS and OLS are already in place — the companion Semantic Models series covers that.
- **Each entry stands alone.** Land on any single entry and act on it without reading the others.
- **Every step is grounded in Microsoft Learn** and scoped to reports, apps, and distribution rather than the model.
- **Validate as you go.** Each entry ends with a validation step and a rollback.

## Layer 1 — Sharing & distribution

- **01 · What Sharing a Report Actually Shares** — the model beneath, and why hiding isn't security.
- **02 · Share Reports with the Right Link Type** — three link types, and the two permission toggles.
- **03 · Distribute Reports with Apps and Audiences** — packaged read-only experiences at scale.
- **04 · Share Reports Outside Your Organization** — Entra B2B, and the group type that breaks it.

## Layer 2 — Public exposure & export

- **05 · Control Publish to Web** — the highest-risk control in Power BI.
- **06 · Govern Export Paths from Reports** — every route data takes out of the service.
- **07 · Embed Reports Securely Instead of Publicly** — the option that looks similar and behaves nothing alike.

## Layer 3 — Classification

- **08 · Apply Sensitivity Labels to Reports** — manual, default, mandatory, and inherited labeling.
- **09 · Make Label Protection Hold on Export** — supported paths, and the gaps to design around.

## Layer 4 — Governance

- **10 · Assemble a Report Security Posture** — rollout order and review cadence (capstone).

## Where to start

If you administer a tenant and have read only one entry, make it **entry 05**. Publish to web makes a report — and the full underlying model data — publicly readable with no authentication, and it is a single menu click for anyone with edit rights.

- **Auditing an existing estate?** Entry 05 for embed codes, then entry 10.
- **Setting up distribution?** Entries 02 and 03.
- **Sharing with partners?** Entry 04.
- **Compliance asking about classification?** Entries 08 and 09.

> **A note on currency** — Fabric and Power BI ship quickly. Every step here reflects the product and documentation as of publication — verify current behaviour in your own tenant before standardizing on it.
