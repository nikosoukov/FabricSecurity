---
title: "Security for Fabric Data Pipelines — Series Overview"
description: "A prescriptive, 10-part how-to series for pipelines, Copy jobs, and Dataflows Gen2."
series: "Security for Fabric Data Pipelines"
layer: "Index"
order: 0
---

# Security for Fabric Data Pipelines — Series Overview

> A prescriptive, 10-part how-to series for pipelines, Copy jobs, and Dataflows Gen2.

*Fabric Data Factory Technical Insiders · 10-part how-to series · Level 300 · Start here*

A data pipeline is a credential holder with a schedule. It reaches into source systems, moves data across boundaries, and does it unattended — which makes it one of the highest-leverage things to secure in Fabric, and one of the easiest to leave wide open.

This series covers that surface in **10 prescriptive entries** across four layers. Every entry is a self-contained runbook — **prerequisites → numbered steps → validation → limitations → rollback** — with its own architecture diagram, scoped to **pipelines**, **Copy jobs**, and **Dataflows Gen2 (CI/CD)**.

This overview is the entry point. Use it to find the layer you need, then work through that layer's entries in order.

![Figure — The four security layers of the series, built from the network up.](images/fabric-dp-security-00.png)

*Figure — The four security layers of the series, built from the network up.*

## How to use this series

- **Work from the bottom up.** Network boundary first, then the credentials pipelines carry, then who can build and run them, then how you watch it all.
- **Each entry stands alone.** Land on any single entry and act on it without reading the others.
- **Every step is grounded in Microsoft Learn** and scoped to Data Factory items rather than Fabric in general.
- **Validate as you go.** Each entry ends with a validation step and a rollback.

## Layer 1 — Network security

- **01 · Block Outbound Connections from Pipelines** — enable OAP and understand what stops working.
- **02 · Allow Approved Destinations with Data Connection Rules** — connector granularity and how to scope precisely.
- **03 · Reach Firewall-Enabled Storage with Trusted Workspace Access** — resource instance rules via ARM or PowerShell.
- **04 · Connect to Private Sources Through Gateways** — on-premises and VNet data gateways under OAP.

## Layer 2 — Identity & credentials

- **05 · Authenticate Pipelines with Workspace Identity** — a managed service principal with no keys to rotate.
- **06 · Store Pipeline Credentials in Azure Key Vault References** — a pointer to the secret, never a copy.
- **07 · Share Connections Without Losing Control** — the three connection roles and how to restrict resharing.

## Layer 3 — Access control

- **08 · Control Who Can Build and Run Pipelines** — workspace roles, item sharing, and the identity a run actually uses.
- **09 · Keep Secrets Out of Pipeline Run History** — secure input and secure output, used as a pair.

## Layer 4 — Governance & monitoring

- **10 · Assemble a Data Pipelines Security Posture** — rollout order, connection inventory, and review cadence (capstone).

## Where to start

If you're securing a Data Factory workspace from scratch, start at **entry 10** to build the inventory, then work up from **Layer 1**. Pipelines are the one workload where inventory genuinely comes first — you cannot safely enable a network control without knowing what your pipelines connect to.

- **Credentials scattered across connections?** Entries 05 and 06 are the highest-value pair in the series.
- **Firewall-enabled storage you can't reach?** Entry 03.
- **Someone shared a connection and now half the org can use it?** Entry 07.
- **A secret showed up in run history?** Entry 09, today.

> **A note on currency** — Fabric ships quickly. Every step here reflects the product and documentation as of publication — verify current behaviour in your own tenant before standardizing on it, particularly for capabilities that recently reached GA.
