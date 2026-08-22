---
title: "Configure SQL Audit Logs for the Warehouse"
description: "Record database events for security investigations and compliance."
series: "Security for Fabric Data Warehouse"
layer: "Governance & monitoring"
order: 21
---

# Configure SQL Audit Logs for the Warehouse

> Record database events for security investigations and compliance.

*Series: Governance & monitoring · Layer: Governance (1 of 5) · Audience: Fabric DW admins · Level 300*

This post shows you how to enable and scope **SQL audit logs** on a Fabric Warehouse so database events — sign-ins, DML and DDL, and permission changes — are captured for later review and compliance.

It then puts the log to work: a step-by-step **forensic analysis** workflow for reconstructing an incident — who connected, from which IP, what they ran, and how to preserve the evidence.

## What you'll set up

- SQL audit logging enabled on the Warehouse.
- Event categories scoped to what you actually need to retain.
- A repeatable **forensic workflow** — access timeline, principal activity, abuse patterns, and evidence preservation.

![Figure 1 — Warehouse events are captured to the SQL audit log with configurable event categories and retention.](images/fabric-dw-security-21.png)

*Figure 1 — Warehouse events are captured to the SQL audit log with configurable event categories and retention.*

## Prerequisites

- A Fabric workspace on an **active or trial capacity**, with access to the Warehouse item.
- The **Audit** permission on the Warehouse — required to configure and query audit logs.

## Step 1 — Enable SQL audit logs

1. Open the Warehouse item's **Settings** and select the **SQL audit logs** page.
2. Enable **Save events to SQL audit logs**. By default, all actions are captured and retained for **nine years**.
3. Under **Events to record**, select only the event categories or audit action groups you need.

> **Note** — You can configure SQL audit logs in the **Fabric portal** or via the **REST API**. Scope the events you capture to control volume and retention.

## Step 2 — Query the audit logs

- Query the captured audit events to review who performed which actions on the Warehouse.
- Correlate audit events with query activity (see the monitoring post) to reconstruct a full picture.

Read the audit file with `sys.fn_get_audit_file_v2`, bounding the window so you only scan the period you care about:

```sql
SELECT event_time,
       action_id,
       succeeded,
       server_principal_name,
       client_ip,
       application_name,
       statement
FROM sys.fn_get_audit_file_v2(
        '<audit-log-path>', DEFAULT, DEFAULT,
        DATEADD(DAY, -7, SYSUTCDATETIME()), SYSUTCDATETIME())
ORDER BY event_time DESC;
```

## Step 3 — Use the log for forensic analysis

Retention is only half the value. The reason to capture these events is to answer investigative questions later — who touched the data, from where, and what exactly did they run. Work the timeline in this order.

### 1. Establish the access timeline

Start with authentication. Successful and failed logins tell you when a principal arrived and from which address — the anchor for everything that follows.

```sql
SELECT event_time, succeeded, server_principal_name, client_ip, application_name
FROM sys.fn_get_audit_file_v2(
        '<audit-log-path>', DEFAULT, DEFAULT,
        @start_time, @end_time)
WHERE action_id IN ('LGIS','LGIF')   -- login succeeded / failed
ORDER BY event_time;
```

- A burst of `LGIF` events from one address is a credential-guessing signal.
- An `LGIS` from an unexpected `client_ip` or `application_name` is your pivot point — carry that principal and time window into the next query.

### 2. Reconstruct what the principal did

With the principal and window fixed, pull the statements executed in that session to see exactly which objects were read or changed.

```sql
SELECT event_time, action_id, object_name, statement, affected_rows
FROM sys.fn_get_audit_file_v2(
        '<audit-log-path>', DEFAULT, DEFAULT,
        @start_time, @end_time)
WHERE server_principal_name = @principal
ORDER BY event_time;
```

### 3. Look for the specific abuse patterns

- **Privilege escalation** — `GRANT`, `ALTER ROLE`, or role-membership changes, especially self-granted.
- **Bulk extraction** — high `affected_rows` on sensitive tables, or repeated large `SELECT`s outside business hours.
- **Security-control tampering** — changes to RLS policies, masking definitions, or audit settings themselves.
- **Schema changes** — unexpected `DROP` / `ALTER` against production objects.

### 4. Preserve and correlate the evidence

1. Export the filtered result set to an immutable location before the retention window or the investigation moves on.
2. Record the exact query, the time window, and the audit-log path used, so a third party can reproduce your result.
3. Correlate the `client_ip` with **Entra sign-in logs** to tie the database session to a device and Conditional Access outcome (see Post 3).
4. Correlate `event_time` with `queryinsights` history (see Post 24) to recover full query text and duration where the audit statement is truncated.

> **Make this possible before you need it** — Forensics only works on events you were already capturing. If **Events to record** is scoped too narrowly, the evidence simply won't exist after the fact — capture logins, permission changes, and DDL as a baseline even when you exclude high-volume DML.

## Validate

- Perform an audited action (for example, a permission change) and confirm it appears in the audit logs.
- Confirm the enabled event categories match your compliance requirements.
- Run the login-timeline query above and confirm your own test session appears with the expected principal and client IP.

## Limitations & gotchas

- The **Audit** permission is required to both configure and query the logs.
- Capturing **all** actions for nine years can be high-volume — scope **Events to record** deliberately.

## References

- [Configure SQL audit logs in Fabric Data Warehouse — Microsoft Learn](https://learn.microsoft.com/en-us/fabric/data-warehouse/configure-sql-audit-logs)
- [Security for data warehousing in Microsoft Fabric — Microsoft Learn](https://learn.microsoft.com/en-us/fabric/data-warehouse/security)
