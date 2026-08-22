---
title: "Security for Fabric Semantic Models — Series Overview"
description: "A prescriptive, 11-part how-to series for row-level security, object-level security, and Direct Lake."
series: "Security for Fabric Semantic Models"
layer: "Index"
order: 0
---

# Security for Fabric Semantic Models — Series Overview

> A prescriptive, 11-part how-to series for row-level security, object-level security, and Direct Lake.

*Fabric Semantic Models Technical Insiders · 11-part how-to series · Level 300 · Start here*

A semantic model is where most organisations actually enforce who sees which numbers. It is also where the most security rules are written that **never apply to anyone** — because row-level security only governs the Viewer role, and the people testing it are almost never Viewers.

This series covers that surface in **11 prescriptive entries** across four layers. Every entry is a self-contained runbook — **prerequisites → numbered steps → validation → limitations → rollback** — with its own architecture diagram, scoped to **semantic models** in Power BI and Fabric.

This overview is the entry point. Use it to find the layer you need, then work through that layer's entries in order.

![Figure — The four security layers of the series.](images/fabric-sm-security-00.png)

*Figure — The four security layers of the series.*

## How to use this series

- **Start with permissions.** Who holds Write on the model determines whether any rule you write matters.
- **Each entry stands alone.** Land on any single entry and act on it without reading the others.
- **Every step is grounded in Microsoft Learn** and scoped to semantic models rather than Power BI in general.
- **Validate as you go.** Each entry ends with a validation step and a rollback.

## Layer 1 — Access & permissions

- **01 · Understand the Semantic Model Permission Model** — Read, Build, Reshare, Write, and which one disables your rules.
- **02 · Control Access with Workspace Roles** — why RLS only applies to Viewers.
- **03 · Manage Build Permission** — the four ways users acquire it, and how to take it away.

## Layer 2 — Row & object security

- **04 · Define Row-Level Security Roles** — DAX filters, the authoring workflow, and role membership.
- **05 · Implement Dynamic Row-Level Security** — one role that filters per user via USERPRINCIPALNAME().
- **06 · Secure Tables and Columns with Object-Level Security** — TMDL scripts and metadata hiding.
- **07 · Validate RLS and OLS Before You Publish** — Test as role, and the four things it can't catch.

## Layer 3 — Connection identity

- **08 · Choose SSO or a Fixed Identity for Direct Lake** — whose permissions actually apply.
- **09 · Align Direct Lake Models with OneLake Security** — scope, union-then-intersect, and where to put your rules.

## Layer 4 — Governance & sharing

- **10 · Apply Row-Level Security to External B2B Guests** — where dynamic RLS silently fails.
- **11 · Assemble a Semantic Model Security Posture** — rollout order and review cadence (capstone).

## Where to start

If you already have RLS configured and want to know whether it's working, start at **entry 02**. The most common finding is that the audience it was written for holds Contributor, which means the rules have never applied to them.

- **Building a model from scratch?** Entries 01 and 02 first, then 04.
- **Using Direct Lake?** Entries 08 and 09 — the identity choice changes everything downstream.
- **Sharing with partners?** Entry 10, before you share rather than after.
- **Rules exist but you're not sure they hold?** Entry 07.

> **A note on currency** — Fabric ships quickly. Every step here reflects the product and documentation as of publication — verify current behaviour in your own tenant before standardizing on it, particularly the Direct Lake and OneLake security integration, which is evolving.
