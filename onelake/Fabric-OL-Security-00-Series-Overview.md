---
title: "Security for OneLake — Series Overview"
description: "A prescriptive, 9-part how-to series for the data-plane security model that every Fabric engine inherits."
series: "Security for OneLake"
layer: "Index"
order: 0
---

# Security for OneLake — Series Overview

> A prescriptive, 9-part how-to series for the data-plane security model that every Fabric engine inherits.

*Fabric Technical Insiders · 9-part how-to series · Level 300 · Start here*

OneLake security is the **data plane** for Fabric. Every other series in this programme — Warehouse, Data Engineering, Semantic Models, Reports, Agents — sits on top of it. A policy authored once in OneLake is enforced consistently across every engine that reads the data.

This series covers that layer in **9 prescriptive entries** across four layers: the permission model, granular data access, engine and shortcut behaviour, and the reference architecture. Every entry is a self-contained runbook — **prerequisites → numbered steps → validation → limitations → rollback** — with its own architecture diagram.

This overview is the entry point. Use it to find the layer you need, then work through that layer's entries in order.

![Figure — The four security layers of the series.](images/fabric-ol-security-00.png)

*Figure — The four security layers of the series.*

## How to use this series

- **Start here if you are new to OneLake security** — entries 01 and 02 are the model everything else assumes.
- **Each entry stands alone.** Land on any single entry and act on it without reading the others.
- **Every step is grounded in Microsoft Learn** and scoped to OneLake rather than a single workload.
- **Validate as you go.** Each entry ends with a validation step and a rollback.

## Layer 1 — Permission model

- **01 · Map the OneLake Permission Model** — control plane versus data plane, and the roles that override your rules.
- **02 · Handle Default Roles Before They Undo Your Work** — DefaultReader, and virtualized membership.

## Layer 2 — Granular data access

- **03 · Secure Tables and Folders** — object-level security, and what actually counts as a table.
- **04 · Apply Column-Level Security** — hiding columns, and three engines that react differently.
- **05 · Apply Row-Level Security** — the SQL subset, the operators, and the silent failure mode.
- **06 · Combine RLS, CLS and Multiple Roles** — union everywhere, except the one place it intersects.

## Layer 3 — Engines & shortcuts

- **07 · Make Every Engine Enforce Your Policy** — filtered versus blocked, and the two modes you must switch.
- **08 · Secure Shortcuts** — passthrough versus delegated, and the identity exception that breaks both.

## Layer 4 — Architecture & governance

- **09 · Adopt the Recommended OneLake Architecture** — the primary-workspace pattern (capstone).

## Where to start

If you have already created a OneLake security role and have read only one entry, make it **entry 02**. Every new item ships with a **DefaultReader** role whose membership is virtualized — adding a user to your carefully-scoped role does nothing while they remain in DefaultReader, because they keep full access to the item.

- **Designing the model?** Entries 01 and 02.
- **Implementing fine-grained access?** Entries 03 through 06.
- **Users seeing the wrong data in one engine?** Entry 07.
- **Sharing data across workspaces or clouds?** Entry 08.
- **Rolling out at scale?** Entry 09.

> **A note on currency** — OneLake security is generally available, but several parts of the surface — Eventhouse enforcement, authorized third-party engines — remain in preview. Every step reflects the product and documentation as of publication; verify current behaviour in your own tenant before standardizing on it.
