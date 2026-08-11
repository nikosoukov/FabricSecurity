---
title: "Stop Warehouse Data Exfiltration with Outbound Access Protection"
description: "Block the Warehouse and SQL analytics endpoint from reaching unapproved external destinations."
series: "Security for Fabric Data Warehouse"
layer: "Network security"
order: 4
---

# Stop Warehouse Data Exfiltration with Outbound Access Protection

> Block the Warehouse and SQL analytics endpoint from reaching unapproved external destinations.

*Series: Network security · Layer: Outbound (1 of 2) · Audience: Fabric DW admins · Level 300*

This post shows you how to turn on **workspace outbound access protection (OAP)** for a workspace that hosts a Fabric Warehouse, so the warehouse and **SQL analytics endpoint** can no longer push or pull data to unapproved external endpoints — closing off ingestion-based exfiltration paths.

## Scenario — when to use this

Inbound is locked down, but a compromised credential or a malicious insider could still use the Warehouse to *push* data out — to an attacker-controlled storage account or an unapproved external endpoint. Your security team wants those data-exfiltration paths closed by default.

Reach for this pattern when you need to guarantee the Warehouse and its **SQL analytics endpoint** cannot reach arbitrary external destinations, and you're ready to standardize ingestion on approved, in-tenant sources. Post 5 shows how to keep loading data once this is on.

For more detail on how this option works, see:

- [Microsoft Fabric security white paper — Microsoft Learn](https://learn.microsoft.com/en-us/fabric/security/white-paper-landing-page)
- [Outbound access protection for Data Warehouse — Microsoft Learn](https://learn.microsoft.com/en-us/fabric/security/workspace-outbound-access-protection-data-warehouse)

## What you'll set up

- OAP enabled on the workspace so **all** outbound public access is blocked by default.
- A clear understanding of what still works for the Warehouse (OneLake-sourced ingestion) and what stops.

![Figure 4 — With OAP on, external destinations and unapproved ingestion are blocked; OneLake-sourced loads still work.](images/fabric-dw-security-04.png)

*Figure 4 — With OAP on, external destinations and unapproved ingestion are blocked; OneLake-sourced loads still work.*

## Prerequisites

- You have the **Admin** role in the workspace.
- The workspace resides on a **Fabric capacity (F SKU)**. No other capacity types are supported.
- A Fabric tenant administrator has enabled the tenant setting **Configure workspace-level outbound network rules**.
- Re-register the **Microsoft.Network** resource provider — Azure portal → **Subscriptions → Resource providers → Microsoft.Network → Re-register**.

## Step 1 — Enable outbound access protection

1. Sign in to Fabric with an account that has the **Admin** role on the target workspace.
2. Open the workspace → **Workspace settings → Network Security**.
3. Under **Outbound access protection**, switch **Block outbound public access** to **On**.
4. If you rely on source control, switch **Allow Git integration** to **On** — Git sync is blocked by default under OAP.

> **Note** — The block-outbound setting can take **up to 15 minutes** to take effect.

## What changes for the Warehouse

Once OAP is on, outbound connections from warehouses and SQL analytics endpoints are restricted to the workspace's administrator-allowed endpoints. Specifically:

- **Warehouses** restrict ingestion to trusted sources. Loads via `COPY INTO`, `OPENROWSET`, and `BULK INSERT` from **unapproved endpoints are blocked**, reducing accidental or unauthorized access.
- **SQL analytics endpoints** limit all queries and data retrieval to resources within the **current workspace**.
- **Exception:** you can still use `COPY INTO` to ingest directly from **OneLake** as a source.

## Validate

- Run a `COPY INTO` from an **external ADLS URL** — the load is blocked.
- Run a `COPY INTO` from a **OneLake** source in the same workspace — the load succeeds.
- Confirm the toggle state under **Workspace settings → Network Security**.

## Limitations & gotchas

- All outbound connections from warehouses and SQL analytics endpoints are blocked; for Data Warehouse, **exceptions can't currently be configured through managed private endpoints**.
- Data-import commands are restricted to sources **within the current workspace**, except `COPY INTO` from OneLake.
- **Git integration** is blocked unless you explicitly allow it.
- Allow **up to 15 minutes** for the setting to apply.

## Rollback

1. Open **Workspace settings → Network Security**.
2. Switch **Block outbound public access** to **Off** to restore outbound connectivity.

## References

- [Enable workspace outbound access protection — Microsoft Learn](https://learn.microsoft.com/en-us/fabric/security/workspace-outbound-access-protection-set-up)
- [Outbound access protection for Data Warehouse — Microsoft Learn](https://learn.microsoft.com/en-us/fabric/security/workspace-outbound-access-protection-data-warehouse)
- [Workspace outbound access protection overview — Microsoft Learn](https://learn.microsoft.com/en-us/fabric/security/workspace-outbound-access-protection-overview)
