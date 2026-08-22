# Security for Fabric Data Agents

*A 7-part, prescriptive how-to series for sharing, source permissions, data boundary, and external consumption.*

![The four security layers of the series](images/fabric-da-security-00.png)

Each entry is a self-contained how-to (prerequisites → steps → validation → limitations → rollback) with its own architecture diagram, scoped to semantic models. Start at Layer 1 and work up.

## Contents

### Layer 1 — Access & sharing

- [Share a Data Agent with the Right Permission Model](Fabric-DA-Security-01-Access-Permission-Models.md) — Three models — and publishing state changes what every one of them means.
- [Grant the Minimum Source Permissions](Fabric-DA-Security-02-Access-Source-Permissions.md) — Sharing the agent is not sharing the data — and Read is enough for semantic models.

### Layer 2 — Data boundary

- [Prove RLS and CLS Reach the Agent](Fabric-DA-Security-03-Boundary-RLS-CLS.md) — The agent honors every user permission — validate it with a real restricted account, not your own.
- [Scope What a Data Agent Can Reach](Fabric-DA-Security-04-Boundary-Scope-Sources.md) — Five sources, chosen tables, and a precedence model that instructions cannot override.

### Layer 3 — External exposure

- [Configure the Tenant Settings and Cross-Geo Boundary](Fabric-DA-Security-05-Exposure-Tenant-Settings.md) — Five switches — two of which move data outside your compliance boundary.
- [Control Consumption Outside Fabric](Fabric-DA-Security-06-Exposure-External-Consumption.md) — Foundry, Copilot Studio, M365 Copilot and MCP — and the authentication choice that decides whose data everyone sees.

### Layer 4 — Governance

- [Govern Data Agents with Purview and Lifecycle Controls](Fabric-DA-Security-07-Governance-Posture.md) — The order to apply these controls in — starting one layer below the agent.

---

*See the [series overview](Fabric-DA-Security-00-Series-Overview.md) for the complete entry list and where to start.*
