# Security for Fabric Data Engineering

*A 16-part, prescriptive how-to series for notebooks, Spark job definitions, and environments — built from the network up.*

![The five security layers of the series](images/fabric-de-security-00.png)

Each entry is a self-contained how-to (prerequisites → steps → validation → limitations → rollback) with its own architecture diagram, scoped to Data Engineering items. Start at Layer 1 and work up.

## Contents

### Layer 1 — Network security

- [Reach Data Engineering Workspaces Only Over Private Links](Fabric-DE-Security-01-Network-Private-Links.md) — Route inbound access to notebooks and Spark job definitions through Azure Private Link.
- [Block Outbound Access from Notebooks and Spark Jobs](Fabric-DE-Security-02-Network-Outbound-Access-Protection.md) — Stop Spark clusters reaching the public internet, and know exactly what breaks.
- [Open Approved Destinations with Managed Private Endpoints](Fabric-DE-Security-03-Network-Managed-Private-Endpoints.md) — The only way to create outbound exceptions for notebooks and Spark job definitions.
- [Install Python Libraries in a Protected Workspace](Fabric-DE-Security-04-Network-Library-Installation.md) — Two supported paths when pip can no longer reach public PyPI.

### Layer 2 — Identity & access

- [Control Data Engineering Access with Workspace Roles](Fabric-DE-Security-05-Identity-Workspace-Roles.md) — What Admin, Member, Contributor and Viewer actually grant over notebooks and Spark jobs.
- [Share Notebooks and Spark Job Definitions with Least Privilege](Fabric-DE-Security-06-Identity-Share-Items.md) — Item access and data access are two separate grants — give both, deliberately.
- [Run Automated Spark Jobs Under a Service Principal](Fabric-DE-Security-07-Identity-Service-Principals.md) — Take personal identities out of scheduled pipelines — and understand the token scope limits.
- [Keep Secrets Out of Notebook Code with Azure Key Vault](Fabric-DE-Security-08-Identity-Secrets-Key-Vault.md) — Retrieve credentials at runtime with notebookutils.credentials instead of hardcoding them.

### Layer 3 — Data access

- [Grant Granular Data Access with OneLake Security Roles](Fabric-DE-Security-09-Data-OneLake-Security-Roles.md) — The data-plane control that Spark, SQL and every Fabric engine enforce consistently.
- [Filter Rows and Hide Columns in OneLake](Fabric-DE-Security-10-Data-Row-Column-Security.md) — Author row and column constraints once, enforced across every engine that reads the data.
- [Read Data Across Workspaces from a Notebook](Fabric-DE-Security-11-Data-Cross-Workspace-Access.md) — Get the path form and the network path right — both fail in ways that look like the other.
- [Audit Shortcut Security Before You Expose Data](Fabric-DE-Security-12-Data-Shortcut-Security.md) — Shortcut permissions resolve at the target — not where the shortcut appears.

### Layer 4 — Data protection

- [Encrypt Data Engineering Data with Customer-Managed Keys](Fabric-DE-Security-13-Protection-Customer-Managed-Keys.md) — Add a key you own and control on top of default encryption at rest.
- [Restrict OneLake Access from Applications Outside Fabric](Fabric-DE-Security-14-Protection-External-App-Access.md) — One tenant setting that materially changes how exposed your lake is.

### Layer 5 — Governance & monitoring

- [Audit Data Engineering and OneLake Activity](Fabric-DE-Security-15-Governance-Audit.md) — Know what the log captures — and the significant gap it leaves.
- [Assemble a Data Engineering Security Posture](Fabric-DE-Security-16-Governance-Posture.md) — The order to apply these controls in, and how to verify the whole stack.

---

*See the [series overview](Fabric-DE-Security-00-Series-Overview.md) for the complete entry list and where to start.*
