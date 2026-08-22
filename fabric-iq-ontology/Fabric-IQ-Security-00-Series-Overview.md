---
title: "Security for Fabric IQ and Ontology — Series Overview"
description: "A prescriptive, 6-part how-to series for the ontology item, its bindings, its graph, and the agents that act on it."
series: "Security for Fabric IQ and Ontology"
layer: "Index"
order: 0
---

# Security for Fabric IQ and Ontology — Series Overview

> A prescriptive, 6-part how-to series for the ontology item, its bindings, its graph, and the agents that act on it.

*Fabric Technical Insiders · 6-part how-to series · Level 300 · Start here*

An ontology is a **shared business vocabulary bound to real data**. It changes who can ask questions of your estate — not who is allowed to see the answers. Every source behind it keeps enforcing its own security, and that split is where most Fabric IQ security thinking goes wrong.

This series covers the Fabric IQ layer in **6 prescriptive entries** across four layers: the tenant foundation, the ontology and its bindings, the graph and query surface, and the agents that act on it. Every entry is a self-contained runbook — **prerequisites → numbered steps → validation → limitations → rollback** — with its own architecture diagram.

This overview is the entry point. Use it to find the layer you need, then work through that layer's entries in order.

![Figure — The four security layers of the series.](images/fabric-iq-security-00.png)

*Figure — The four security layers of the series.*

## How to use this series

- **Secure the bound sources first.** The ontology adds a vocabulary; it does not add a permission boundary.
- **Each entry stands alone.** Land on any single entry and act on it without reading the others.
- **Every step is grounded in Microsoft Learn** and scoped to the Fabric IQ workload.
- **Validate as you go.** Each entry ends with a validation step and a rollback.

> **Preview capability** — The ontology item and the Fabric IQ workload are in **public preview**. Behaviour, limitations and tenant settings change between releases. Verify every step in your own tenant before you rely on it, and re-verify after each Fabric release.

## What's in scope

The **IQ workload** groups several Fabric items, some shared with other workloads. This series covers the ones whose security surface is specific to Fabric IQ:

- **Ontology (preview)** — the entity types, properties, relationships and data bindings.
- **Graph** — the queryable instance graph built from those bindings; also part of Real-Time Intelligence.
- **Operations agent** — monitors live data and takes governed action; also part of Real-Time Intelligence.

**Power BI semantic models** and **data agents** are also part of the IQ workload but have their own dedicated series in this programme — see those for RLS, OLS, Direct Lake identity, and agent sharing.

## Layer 1 — Foundation

- **01 · Enable Fabric IQ Deliberately** — the tenant settings, and what each one opens.
- **02 · Secure an Ontology and Its Data Bindings** — two permissions, not one.

## Layer 2 — Graph & query surface

- **03 · Control What the Graph and Query Layer Expose** — relationships as access paths.

## Layer 3 — Agents on the ontology

- **04 · Govern the Operations Agent Identity** — Entra Agent ID, and the delegated-permission trap.
- **05 · Constrain Operations Agent Actions with OAP** — what outbound access protection blocks.

## Layer 4 — Governance

- **06 · Assemble a Fabric IQ Security Posture** — rollout order and review cadence (capstone).

## Where to start

If you are running an operations agent and have read only one entry, make it **entry 04**. The agent acts with its **creator's** delegated permissions — so when a recipient approves a recommendation, the action runs as the creator, not as the approver. The creator's access defines the blast radius of every approved action.

- **Standing up Fabric IQ?** Entries 01 and 02.
- **Security review of an ontology?** Entries 02 and 03.
- **Running operations agents?** Entries 04 and 05.
- **Building the target posture?** Entry 06.
