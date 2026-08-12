# Security for Fabric Data Warehouse

*A 25-post, prescriptive how-to blog series for Fabric Data Warehouse admins — built from the network up.*

![The five security layers of the series](images/fabric-dw-security-00.png)

Each post is a self-contained how-to (prerequisites → steps → validation → limitations → rollback) with its own architecture diagram, scoped to the Warehouse and SQL analytics endpoint. Start at Layer 1 and work up.

## Contents

### Layer 1 — Network security

- [Lock the Warehouse SQL Endpoint Behind Workspace-Level Private Links](Fabric-DW-Security-01-Inbound-Private-Links.md) — Route inbound Warehouse connections over Azure Private Link and shut off the public internet.
- [Restrict the Warehouse to Approved IPs with Workspace Firewall Rules](Fabric-DW-Security-02-Inbound-IP-Firewall.md) — Permit inbound Warehouse connections only from your corporate egress and branch ranges.
- [Gate Warehouse Sign-ins with Microsoft Entra Conditional Access](Fabric-DW-Security-03-Inbound-Conditional-Access.md) — Require MFA, compliant devices, and trusted locations before any Warehouse connection.
- [Stop Warehouse Data Exfiltration with Outbound Access Protection](Fabric-DW-Security-04-Outbound-Access-Protection.md) — Block the Warehouse and SQL analytics endpoint by default, then allow only approved destinations.
- [Load Data into a Protected Warehouse with the OneLake Ingestion Pattern](Fabric-DW-Security-05-Outbound-Ingestion-Patterns.md) — Keep ingesting after outbound access protection is on — using OneLake as the supported source.

### Layer 2 — Identity & access

- [Connect to the Warehouse with Microsoft Entra ID](Fabric-DW-Security-06-Identity-Entra-Authentication.md) — Every Warehouse connection is an Entra-authenticated identity — there are no SQL logins.
- [Control Warehouse Access with Fabric Workspace Roles](Fabric-DW-Security-07-Identity-Workspace-Roles.md) — Assign the least-privileged workspace role that still lets the user do the job.
- [Grant Granular Warehouse Permissions with T-SQL](Fabric-DW-Security-08-Identity-TSQL-Permissions.md) — Use GRANT, DENY, and REVOKE with database roles for fine-grained, least-privilege access.
- [Share the Warehouse and SQL Analytics Endpoint with Least Privilege](Fabric-DW-Security-09-Identity-Share-Warehouse.md) — Grant the minimum item permission, then refine object access with T-SQL.
- [Automate Warehouse Access with Service Principals](Fabric-DW-Security-10-Identity-Service-Principals.md) — Give apps and pipelines a scoped Entra identity instead of a user account.

### Layer 3 — Granular data access

- [Restrict Tables, Views, and Procedures with Object-Level Security](Fabric-DW-Security-11-Granular-Object-Level-Security.md) — Grant and deny access to specific database objects by role.
- [Filter Rows per User with Row-Level Security](Fabric-DW-Security-12-Granular-Row-Level-Security.md) — Restrict which rows each identity can read with a security policy and predicate function.
- [Hide Sensitive Columns with Column-Level Security](Fabric-DW-Security-13-Granular-Column-Level-Security.md) — Grant SELECT on a column subset so unlisted columns stay out of reach.
- [Obfuscate Sensitive Values with Dynamic Data Masking](Fabric-DW-Security-14-Granular-Dynamic-Data-Masking.md) — Mask columns at query time for non-privileged users, with minimal application change.
- [Layer OLS, RLS, CLS, and Masking for Defense in Depth](Fabric-DW-Security-15-Granular-Defense-In-Depth.md) — Combine the granular controls on one sensitive table and validate they hold together.

### Layer 4 — Data protection

- [Encrypt the Warehouse with Customer-Managed Keys](Fabric-DW-Security-16-Protection-Customer-Managed-Keys.md) — Add your Azure Key Vault key on top of Fabric's default at-rest encryption.
- [Classify and Protect Warehouse Data with Sensitivity Labels](Fabric-DW-Security-17-Protection-Sensitivity-Labels.md) — Apply Purview Information Protection labels that follow the data on export.
- [Detect Sensitive Data in the Warehouse with DLP Policies](Fabric-DW-Security-18-Protection-Data-Loss-Prevention.md) — Use Purview Data Loss Prevention to flag sensitive data in Fabric warehouses.
- [Choose the SQL Endpoint Access Mode: OneLake Security or SQL Permissions](Fabric-DW-Security-19-Protection-SQL-Endpoint-Access-Modes.md) — Enforce data access centrally in OneLake, or granularly with SQL permissions.
- [Assemble a Data-Protection Posture for the Warehouse](Fabric-DW-Security-20-Protection-Posture.md) — Sequence encryption, classification, leakage detection, and access governance.

### Layer 5 — Governance & monitoring

- [Configure SQL Audit Logs for the Warehouse](Fabric-DW-Security-21-Governance-SQL-Audit-Logs.md) — Record database events for security investigations and compliance.
- [Review and Investigate Warehouse Audit Activity](Fabric-DW-Security-22-Governance-Audit-Review.md) — Two complementary paths: in-warehouse T-SQL and the tenant unified audit log.
- [Control Microsoft Access with Customer Lockbox](Fabric-DW-Security-23-Governance-Customer-Lockbox.md) — Require explicit approval before Microsoft engineers can access your data.
- [Monitor Warehouse Activity with Query Insights and DMVs](Fabric-DW-Security-24-Governance-Monitor-Activity.md) — Track performance and user activity from built-in views.
- [Govern the Warehouse with Microsoft Purview](Fabric-DW-Security-25-Governance-Purview.md) — Discover, classify, trace lineage, and endorse across your data estate.

## Suggested publishing cadence

Publish in numbered order (01 → 25) so the audience builds understanding foundation-up. **Weekly** is recommended (~6 months); bi-weekly (~12 months) suits a lighter schedule; a five-day sprint per layer suits a launch moment.

---

*See the [full series index & publishing guide](Fabric-DW-Security-00-Series-Index-and-Publishing-Guide.md) for the complete post list and cadence table.*
