# Security for Fabric Real-Time Intelligence

*An 11-part, prescriptive how-to series for Eventhouse, KQL databases, Eventstream, and Activator — built from the network up.*

![The five security layers of the series](images/fabric-rti-security-00.png)

Each entry is a self-contained how-to (prerequisites → steps → validation → limitations → rollback) with its own architecture diagram, scoped to Real-Time Intelligence items. Start at Layer 1 and work up.

## Contents

### Layer 1 — Network & ingestion

- [Enable Outbound Access Protection for Real-Time Intelligence](Fabric-RTI-Security-01-Network-Outbound-Access-Protection.md) — Restrict outbound connections from Eventhouse, Eventstream, and Activator — and know what stops.
- [Secure Eventstream Ingestion Endpoints](Fabric-RTI-Security-02-Network-Eventstream-Ingestion.md) — Replace shared SAS keys with Microsoft Entra ID authentication for producers and consumers.

### Layer 2 — Identity & access

- [Understand the Two Permission Systems](Fabric-RTI-Security-03-Identity-Two-Permission-Systems.md) — Workspace roles govern the item; KQL security roles govern the data. You need both.
- [Assign KQL Database Security Roles](Fabric-RTI-Security-04-Identity-KQL-Security-Roles.md) — Six roles, and the management commands that add, drop, and replace them.
- [Run Automated Workloads Under Service Principals](Fabric-RTI-Security-05-Identity-Service-Principals.md) — Producers that write but cannot read, and dashboards that read but cannot write.

### Layer 3 — Granular data access

- [Grant View Access to a Subset of Tables](Fabric-RTI-Security-06-Data-Table-View-Access.md) — Three approaches, because the viewer role cannot be scoped to individual tables.
- [Filter Rows with Row Level Security](Fabric-RTI-Security-07-Data-Row-Level-Security.md) — A policy that replaces table access entirely — for every user, including admins.
- [Mask Sensitive Columns in KQL](Fabric-RTI-Security-08-Data-Masking.md) — Anonymize values inside the same RLS policy that filters rows.
- [Control Access Across Follower and Shortcut Databases](Fabric-RTI-Security-09-Data-Follower-Databases.md) — One policy, inherited everywhere — and how to vary it without a second policy.

### Layer 4 — Governance & monitoring

- [Audit Who Has Access to a KQL Database](Fabric-RTI-Security-10-Governance-Audit-Access.md) — List every principal and role — and understand the cross-tenant blind spot.
- [Assemble a Real-Time Intelligence Security Posture](Fabric-RTI-Security-11-Governance-Posture.md) — The order to apply these controls in, starting with the one that's hardest to change later.

---

*See the [series overview](Fabric-RTI-Security-00-Series-Overview.md) for the complete entry list and where to start.*
