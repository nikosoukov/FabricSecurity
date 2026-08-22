# Security Across Microsoft Fabric — Master Index

A prescriptive, publication-quality how-to programme covering **security for every Microsoft Fabric experience**. Nine series, **105 entries**, each written as a self-contained runbook.

Every entry follows the same shape: **prerequisites → numbered steps → validation → limitations → rollback**, with its own architecture diagram. No conceptual padding — the *what* is kept short so the *how* stays front and centre. Every step is grounded in Microsoft Learn.

---

## At a glance

| # | Series | Entries | Folder | Focus |
|---|---|---|---|---|
| 1 | **OneLake** ⭐ | 9 | `onelake/` | Permission model · Granular data access · Engines & shortcuts · Architecture & governance |
| 2 | **Data Warehouse** | 25 | `data-warehouse/` | Network security · Identity & access · Granular data access · Data protection · Governance & monitoring |
| 3 | **Data Engineering** | 16 | `data-engineering/` | Network security · Identity & access · Data access · Data protection · Governance & monitoring |
| 4 | **Data Pipelines** | 10 | `data-pipelines/` | Network security · Identity & credentials · Access control · Governance & monitoring |
| 5 | **Real-Time Intelligence** | 11 | `real-time-intelligence/` | Network & ingestion · Identity & access · Granular data access · Governance & monitoring |
| 6 | **Semantic Models** | 11 | `semantic-models/` | Access & permissions · Row & object security · Connection identity · Governance & sharing |
| 7 | **Power BI Reports** | 10 | `power-bi-reports/` | Sharing & distribution · Public exposure & export · Classification · Governance |
| 8 | **Data Agents** | 7 | `data-agents/` | Access & sharing · Data boundary · External exposure · Governance |
| 9 | **Fabric IQ & Ontology** | 6 | `fabric-iq-ontology/` | Foundation · Graph & query surface · Agents on the ontology · Governance |
| | **Total** | **105** | | |

⭐ **Start here.** OneLake security is the data plane beneath every other series — several findings elsewhere only make sense once you know that model.

---

## Reading paths by role

| If you are… | Read in this order | Why |
|---|---|---|
| Platform / data-lake owner | OneLake → Data Engineering → Data Warehouse | Start at the data plane, then the engines that write to it. |
| Warehouse or SQL practitioner | OneLake → Data Warehouse → Semantic Models | OneLake first — entry 19 of the Warehouse series assumes that model. |
| BI / reporting lead | Semantic Models → Power BI Reports → OneLake | Model-level rules before distribution; OneLake explains Direct Lake behaviour. |
| Data integration engineer | Data Pipelines → Data Engineering → OneLake | The two network models are opposites — read both before standardizing. |
| Real-time / streaming owner | Real-Time Intelligence → OneLake → Fabric IQ & Ontology | Eventhouse carries its own permission system on top of workspace roles. |
| AI / agent builder | Data Agents → Fabric IQ & Ontology → Semantic Models | Agents inherit source security — fix the source first. |
| Security architect / auditor | OneLake → Data Warehouse → Power BI Reports → Data Agents | The capstone entry of each series is the posture checklist. |

---

## The series

### 1. OneLake ⭐ *foundation*

**9 entries** · `onelake/`

The data plane every other series sits on. Workspace roles versus OneLake security roles, table and folder scoping, RLS and CLS, which engines enforce and which are blocked, shortcut identity, and the recommended primary-workspace architecture.

> **Lead finding.** Workspace Admin, Member and Contributor automatically grant Write to OneLake, which **overrides every OneLake security Read permission you write**. Your consumers must be Viewers for any of it to apply.

- **00 · [Series overview](onelake/Fabric-OL-Security-00-Series-Overview.md)** — start here

**Permission model**

- **01** · [Map the OneLake Permission Model](onelake/Fabric-OL-Security-01-Model-Permission-Model.md)
- **02** · [Handle Default Roles Before They Undo Your Work](onelake/Fabric-OL-Security-02-Model-Default-Roles.md)

**Granular data access**

- **03** · [Secure Tables and Folders](onelake/Fabric-OL-Security-03-Granular-Tables-Folders.md)
- **04** · [Apply Column-Level Security](onelake/Fabric-OL-Security-04-Granular-Column-Level-Security.md)
- **05** · [Apply Row-Level Security](onelake/Fabric-OL-Security-05-Granular-Row-Level-Security.md)
- **06** · [Combine RLS, CLS and Multiple Roles](onelake/Fabric-OL-Security-06-Granular-Combining-Roles.md)

**Engines & shortcuts**

- **07** · [Make Every Engine Enforce Your Policy](onelake/Fabric-OL-Security-07-Engines-Enforcement.md)
- **08** · [Secure Shortcuts](onelake/Fabric-OL-Security-08-Engines-Shortcut-Security.md)

**Architecture & governance**

- **09** · [Adopt the Recommended OneLake Architecture](onelake/Fabric-OL-Security-09-Architecture-Posture.md)

---

### 2. Data Warehouse

**25 entries** · `data-warehouse/`

The largest series. Inbound and outbound network control, Entra identity and T-SQL permissions, the four granular controls layered together, encryption and classification, then audit and Purview governance.

> **Lead finding.** Outbound access protection now supports **data connection rules for the Warehouse**, confirmed by the product group, though the public docs still say otherwise. Entry 04 is written as supported with the discrepancy flagged.

- **00 · [Series overview](data-warehouse/Fabric-DW-Security-00-Series-Overview.md)** — start here

**Network security**

- **01** · [Lock the Warehouse SQL Endpoint Behind Workspace-Level Private Links](data-warehouse/Fabric-DW-Security-01-Inbound-Private-Links.md)
- **02** · [Restrict the Warehouse to Approved IPs with Workspace Firewall Rules](data-warehouse/Fabric-DW-Security-02-Inbound-IP-Firewall.md)
- **03** · [Gate Warehouse Sign-ins with Microsoft Entra Conditional Access](data-warehouse/Fabric-DW-Security-03-Inbound-Conditional-Access.md)
- **04** · [Stop Warehouse Data Exfiltration with Outbound Access Protection](data-warehouse/Fabric-DW-Security-04-Outbound-Access-Protection.md)
- **05** · [Load Data into a Protected Warehouse with the OneLake Ingestion Pattern](data-warehouse/Fabric-DW-Security-05-Outbound-Ingestion-Patterns.md)

**Identity & access**

- **06** · [Connect to the Warehouse with Microsoft Entra ID](data-warehouse/Fabric-DW-Security-06-Identity-Entra-Authentication.md)
- **07** · [Control Warehouse Access with Fabric Workspace Roles](data-warehouse/Fabric-DW-Security-07-Identity-Workspace-Roles.md)
- **08** · [Grant Granular Warehouse Permissions with T-SQL](data-warehouse/Fabric-DW-Security-08-Identity-TSQL-Permissions.md)
- **09** · [Share the Warehouse and SQL Analytics Endpoint with Least Privilege](data-warehouse/Fabric-DW-Security-09-Identity-Share-Warehouse.md)
- **10** · [Automate Warehouse Access with Service Principals](data-warehouse/Fabric-DW-Security-10-Identity-Service-Principals.md)

**Granular data access**

- **11** · [Restrict Tables, Views, and Procedures with Object-Level Security](data-warehouse/Fabric-DW-Security-11-Granular-Object-Level-Security.md)
- **12** · [Filter Rows per User with Row-Level Security](data-warehouse/Fabric-DW-Security-12-Granular-Row-Level-Security.md)
- **13** · [Hide Sensitive Columns with Column-Level Security](data-warehouse/Fabric-DW-Security-13-Granular-Column-Level-Security.md)
- **14** · [Obfuscate Sensitive Values with Dynamic Data Masking](data-warehouse/Fabric-DW-Security-14-Granular-Dynamic-Data-Masking.md)
- **15** · [Layer OLS, RLS, CLS, and Masking for Defense in Depth](data-warehouse/Fabric-DW-Security-15-Granular-Defense-In-Depth.md)

**Data protection**

- **16** · [Encrypt the Warehouse with Customer-Managed Keys](data-warehouse/Fabric-DW-Security-16-Protection-Customer-Managed-Keys.md)
- **17** · [Classify and Protect Warehouse Data with Sensitivity Labels](data-warehouse/Fabric-DW-Security-17-Protection-Sensitivity-Labels.md)
- **18** · [Detect Sensitive Data in the Warehouse with DLP Policies](data-warehouse/Fabric-DW-Security-18-Protection-Data-Loss-Prevention.md)
- **19** · [Choose the SQL Endpoint Access Mode: OneLake Security or SQL Permissions](data-warehouse/Fabric-DW-Security-19-Protection-SQL-Endpoint-Access-Modes.md)
- **20** · [Assemble a Data-Protection Posture for the Warehouse](data-warehouse/Fabric-DW-Security-20-Protection-Posture.md)

**Governance & monitoring**

- **21** · [Configure SQL Audit Logs for the Warehouse](data-warehouse/Fabric-DW-Security-21-Governance-SQL-Audit-Logs.md)
- **22** · [Review and Investigate Warehouse Audit Activity](data-warehouse/Fabric-DW-Security-22-Governance-Audit-Review.md)
- **23** · [Control Microsoft Access with Customer Lockbox](data-warehouse/Fabric-DW-Security-23-Governance-Customer-Lockbox.md)
- **24** · [Monitor Warehouse Activity with Query Insights and DMVs](data-warehouse/Fabric-DW-Security-24-Governance-Monitor-Activity.md)
- **25** · [Govern the Warehouse with Microsoft Purview](data-warehouse/Fabric-DW-Security-25-Governance-Purview.md)

---

### 3. Data Engineering

**16 entries** · `data-engineering/`

Notebooks, Spark job definitions and lakehouses. Private links and managed private endpoints, library installation under network lockdown, OneLake security roles from a notebook, cross-workspace reads, and shortcut auditing.

> **Lead finding.** **Contributors bypass OneLake security roles entirely**, and OneLake audit logs don't capture reads. Data connection rules do *not* apply here — managed private endpoints only.

- **00 · [Series overview](data-engineering/Fabric-DE-Security-00-Series-Overview.md)** — start here

**Network security**

- **01** · [Reach Data Engineering Workspaces Only Over Private Links](data-engineering/Fabric-DE-Security-01-Network-Private-Links.md)
- **02** · [Block Outbound Access from Notebooks and Spark Jobs](data-engineering/Fabric-DE-Security-02-Network-Outbound-Access-Protection.md)
- **03** · [Open Approved Destinations with Managed Private Endpoints](data-engineering/Fabric-DE-Security-03-Network-Managed-Private-Endpoints.md)
- **04** · [Install Python Libraries in a Protected Workspace](data-engineering/Fabric-DE-Security-04-Network-Library-Installation.md)

**Identity & access**

- **05** · [Control Data Engineering Access with Workspace Roles](data-engineering/Fabric-DE-Security-05-Identity-Workspace-Roles.md)
- **06** · [Share Notebooks and Spark Job Definitions with Least Privilege](data-engineering/Fabric-DE-Security-06-Identity-Share-Items.md)
- **07** · [Run Automated Spark Jobs Under a Service Principal](data-engineering/Fabric-DE-Security-07-Identity-Service-Principals.md)
- **08** · [Keep Secrets Out of Notebook Code with Azure Key Vault](data-engineering/Fabric-DE-Security-08-Identity-Secrets-Key-Vault.md)

**Data access**

- **09** · [Grant Granular Data Access with OneLake Security Roles](data-engineering/Fabric-DE-Security-09-Data-OneLake-Security-Roles.md)
- **10** · [Filter Rows and Hide Columns in OneLake](data-engineering/Fabric-DE-Security-10-Data-Row-Column-Security.md)
- **11** · [Read Data Across Workspaces from a Notebook](data-engineering/Fabric-DE-Security-11-Data-Cross-Workspace-Access.md)
- **12** · [Audit Shortcut Security Before You Expose Data](data-engineering/Fabric-DE-Security-12-Data-Shortcut-Security.md)

**Data protection**

- **13** · [Encrypt Data Engineering Data with Customer-Managed Keys](data-engineering/Fabric-DE-Security-13-Protection-Customer-Managed-Keys.md)
- **14** · [Restrict OneLake Access from Applications Outside Fabric](data-engineering/Fabric-DE-Security-14-Protection-External-App-Access.md)

**Governance & monitoring**

- **15** · [Audit Data Engineering and OneLake Activity](data-engineering/Fabric-DE-Security-15-Governance-Audit.md)
- **16** · [Assemble a Data Engineering Security Posture](data-engineering/Fabric-DE-Security-16-Governance-Posture.md)

---

### 4. Data Pipelines

**10 entries** · `data-pipelines/`

The opposite network model to Data Engineering: data connection rules only, no managed private endpoints. Trusted workspace access, gateways, workspace identity, Key Vault references, and keeping secrets out of run history.

> **Lead finding.** Allowing a connector **without naming a workspace opens every instance in the tenant**. A pipeline also runs with its *connection's* credentials, not the triggering user's.

- **00 · [Series overview](data-pipelines/Fabric-DP-Security-00-Series-Overview.md)** — start here

**Network security**

- **01** · [Block Outbound Connections from Pipelines](data-pipelines/Fabric-DP-Security-01-Network-Outbound-Access-Protection.md)
- **02** · [Allow Approved Destinations with Data Connection Rules](data-pipelines/Fabric-DP-Security-02-Network-Data-Connection-Rules.md)
- **03** · [Reach Firewall-Enabled Storage with Trusted Workspace Access](data-pipelines/Fabric-DP-Security-03-Network-Trusted-Workspace-Access.md)
- **04** · [Connect to Private Sources Through Gateways](data-pipelines/Fabric-DP-Security-04-Network-Gateways.md)

**Identity & credentials**

- **05** · [Authenticate Pipelines with Workspace Identity](data-pipelines/Fabric-DP-Security-05-Identity-Workspace-Identity.md)
- **06** · [Store Pipeline Credentials in Azure Key Vault References](data-pipelines/Fabric-DP-Security-06-Identity-Key-Vault-References.md)
- **07** · [Share Connections Without Losing Control](data-pipelines/Fabric-DP-Security-07-Identity-Connection-Sharing.md)

**Access control**

- **08** · [Control Who Can Build and Run Pipelines](data-pipelines/Fabric-DP-Security-08-Access-Roles-And-Runs.md)
- **09** · [Keep Secrets Out of Pipeline Run History](data-pipelines/Fabric-DP-Security-09-Access-Secure-Input-Output.md)

**Governance & monitoring**

- **10** · [Assemble a Data Pipelines Security Posture](data-pipelines/Fabric-DP-Security-10-Governance-Posture.md)

---

### 5. Real-Time Intelligence

**11 entries** · `real-time-intelligence/`

Eventhouse and KQL databases, where two independent permission systems overlap. KQL security roles, RLS that replaces table access for everyone, masking inside the RLS policy, and follower database inheritance.

> **Lead finding.** **RLS replaces table access for everyone, including admins.** There is no separate masking feature — masking is an `extend` inside the RLS policy itself.

- **00 · [Series overview](real-time-intelligence/Fabric-RTI-Security-00-Series-Overview.md)** — start here

**Network & ingestion**

- **01** · [Enable Outbound Access Protection for Real-Time Intelligence](real-time-intelligence/Fabric-RTI-Security-01-Network-Outbound-Access-Protection.md)
- **02** · [Secure Eventstream Ingestion Endpoints](real-time-intelligence/Fabric-RTI-Security-02-Network-Eventstream-Ingestion.md)

**Identity & access**

- **03** · [Understand the Two Permission Systems](real-time-intelligence/Fabric-RTI-Security-03-Identity-Two-Permission-Systems.md)
- **04** · [Assign KQL Database Security Roles](real-time-intelligence/Fabric-RTI-Security-04-Identity-KQL-Security-Roles.md)
- **05** · [Run Automated Workloads Under Service Principals](real-time-intelligence/Fabric-RTI-Security-05-Identity-Service-Principals.md)

**Granular data access**

- **06** · [Grant View Access to a Subset of Tables](real-time-intelligence/Fabric-RTI-Security-06-Data-Table-View-Access.md)
- **07** · [Filter Rows with Row Level Security](real-time-intelligence/Fabric-RTI-Security-07-Data-Row-Level-Security.md)
- **08** · [Mask Sensitive Columns in KQL](real-time-intelligence/Fabric-RTI-Security-08-Data-Masking.md)
- **09** · [Control Access Across Follower and Shortcut Databases](real-time-intelligence/Fabric-RTI-Security-09-Data-Follower-Databases.md)

**Governance & monitoring**

- **10** · [Audit Who Has Access to a KQL Database](real-time-intelligence/Fabric-RTI-Security-10-Governance-Audit-Access.md)
- **11** · [Assemble a Real-Time Intelligence Security Posture](real-time-intelligence/Fabric-RTI-Security-11-Governance-Posture.md)

---

### 6. Semantic Models

**11 entries** · `semantic-models/`

Where RLS and OLS actually apply — and the Write permission that switches them off. Static and dynamic RLS, object-level security via TMDL, Direct Lake identity modes, and external B2B guests.

> **Lead finding.** **RLS and OLS apply only to the Viewer role.** Grant Write and every data-access rule you wrote stops applying. Viewer + Build is the correct self-service pattern.

- **00 · [Series overview](semantic-models/Fabric-SM-Security-00-Series-Overview.md)** — start here

**Access & permissions**

- **01** · [Understand the Semantic Model Permission Model](semantic-models/Fabric-SM-Security-01-Access-Permission-Model.md)
- **02** · [Control Access with Workspace Roles](semantic-models/Fabric-SM-Security-02-Access-Workspace-Roles.md)
- **03** · [Manage Build Permission](semantic-models/Fabric-SM-Security-03-Access-Build-Permission.md)

**Row & object security**

- **04** · [Define Row-Level Security Roles](semantic-models/Fabric-SM-Security-04-Security-Row-Level-Security.md)
- **05** · [Implement Dynamic Row-Level Security](semantic-models/Fabric-SM-Security-05-Security-Dynamic-RLS.md)
- **06** · [Secure Tables and Columns with Object-Level Security](semantic-models/Fabric-SM-Security-06-Security-Object-Level-Security.md)
- **07** · [Validate RLS and OLS Before You Publish](semantic-models/Fabric-SM-Security-07-Security-Validate.md)

**Connection identity**

- **08** · [Choose SSO or a Fixed Identity for Direct Lake](semantic-models/Fabric-SM-Security-08-Identity-Direct-Lake-SSO.md)
- **09** · [Align Direct Lake Models with OneLake Security](semantic-models/Fabric-SM-Security-09-Identity-OneLake-Security.md)

**Governance & sharing**

- **10** · [Apply Row-Level Security to External B2B Guests](semantic-models/Fabric-SM-Security-10-Governance-External-Guests.md)
- **11** · [Assemble a Semantic Model Security Posture](semantic-models/Fabric-SM-Security-11-Governance-Posture.md)

---

### 7. Power BI Reports

**10 entries** · `power-bi-reports/`

The consumption layer. What a share really grants, the three link types, apps and audiences, Publish to web, every export path, secure embedding, and sensitivity labels.

> **Lead finding.** **Sharing a report shares access to the semantic model beneath it**, and hiding a field is explicitly not a security measure. Publish to web needs no authentication at all.

- **00 · [Series overview](power-bi-reports/Fabric-RPT-Security-00-Series-Overview.md)** — start here

**Sharing & distribution**

- **01** · [What Sharing a Report Actually Shares](power-bi-reports/Fabric-RPT-Security-01-Sharing-What-You-Share.md)
- **02** · [Share Reports with the Right Link Type](power-bi-reports/Fabric-RPT-Security-02-Sharing-Link-Types.md)
- **03** · [Distribute Reports with Apps and Audiences](power-bi-reports/Fabric-RPT-Security-03-Sharing-Apps.md)
- **04** · [Share Reports Outside Your Organization](power-bi-reports/Fabric-RPT-Security-04-Sharing-External-Users.md)

**Public exposure & export**

- **05** · [Control Publish to Web](power-bi-reports/Fabric-RPT-Security-05-Exposure-Publish-To-Web.md)
- **06** · [Govern Export Paths from Reports](power-bi-reports/Fabric-RPT-Security-06-Exposure-Export-Paths.md)
- **07** · [Embed Reports Securely Instead of Publicly](power-bi-reports/Fabric-RPT-Security-07-Exposure-Secure-Embedding.md)

**Classification**

- **08** · [Apply Sensitivity Labels to Reports](power-bi-reports/Fabric-RPT-Security-08-Classification-Sensitivity-Labels.md)
- **09** · [Make Label Protection Hold on Export](power-bi-reports/Fabric-RPT-Security-09-Classification-Label-Protection.md)

**Governance**

- **10** · [Assemble a Report Security Posture](power-bi-reports/Fabric-RPT-Security-10-Governance-Posture.md)

---

### 8. Data Agents

**7 entries** · `data-agents/`

Conversational access to governed data. The three sharing permission models, minimum source permissions per data source, proving RLS and CLS passthrough, cross-geo boundaries, and consumption outside Fabric.

> **Lead finding.** **Sharing a data agent is not sharing its data.** Below the minimum source permission, queries fail *or return empty results* — indistinguishable from "there is no data".

- **00 · [Series overview](data-agents/Fabric-DA-Security-00-Series-Overview.md)** — start here

**Access & sharing**

- **01** · [Share a Data Agent with the Right Permission Model](data-agents/Fabric-DA-Security-01-Access-Permission-Models.md)
- **02** · [Grant the Minimum Source Permissions](data-agents/Fabric-DA-Security-02-Access-Source-Permissions.md)

**Data boundary**

- **03** · [Prove RLS and CLS Reach the Agent](data-agents/Fabric-DA-Security-03-Boundary-RLS-CLS.md)
- **04** · [Scope What a Data Agent Can Reach](data-agents/Fabric-DA-Security-04-Boundary-Scope-Sources.md)

**External exposure**

- **05** · [Configure the Tenant Settings and Cross-Geo Boundary](data-agents/Fabric-DA-Security-05-Exposure-Tenant-Settings.md)
- **06** · [Control Consumption Outside Fabric](data-agents/Fabric-DA-Security-06-Exposure-External-Consumption.md)

**Governance**

- **07** · [Govern Data Agents with Purview and Lifecycle Controls](data-agents/Fabric-DA-Security-07-Governance-Posture.md)

---

### 9. Fabric IQ & Ontology

**6 entries** · `fabric-iq-ontology/`

Ontology, graph and operations agents — both in public preview. Tenant settings, data bindings as a second permission surface, relationships as access paths, and the delegated identity model behind agent actions.

> **Lead finding.** An operations agent runs with its **creator's** delegated permissions — so when a recipient approves a recommendation, the action executes as the creator, not the approver.

- **00 · [Series overview](fabric-iq-ontology/Fabric-IQ-Security-00-Series-Overview.md)** — start here

**Foundation**

- **01** · [Enable Fabric IQ Deliberately](fabric-iq-ontology/Fabric-IQ-Security-01-Foundation-Tenant-Settings.md)
- **02** · [Secure an Ontology and Its Data Bindings](fabric-iq-ontology/Fabric-IQ-Security-02-Foundation-Ontology-Bindings.md)

**Graph & query surface**

- **03** · [Control What the Graph and Query Layer Expose](fabric-iq-ontology/Fabric-IQ-Security-03-Graph-Query-Surface.md)

**Agents on the ontology**

- **04** · [Govern the Operations Agent Identity](fabric-iq-ontology/Fabric-IQ-Security-04-Agents-Operations-Agent-Identity.md)
- **05** · [Constrain Operations Agent Actions with OAP](fabric-iq-ontology/Fabric-IQ-Security-05-Agents-Outbound-Access-Protection.md)

**Governance**

- **06** · [Assemble a Fabric IQ Security Posture](fabric-iq-ontology/Fabric-IQ-Security-06-Governance-Posture.md)

---

## Cross-cutting topics

Several controls appear in more than one series, and they do **not** always behave the same way. Use this to find every treatment of a topic before you standardize on one.

**OneLake security roles**  
Defined in **OneLake 01–06**. Bypassed by Contributors — see **Data Engineering 09**. Unioned then intersected with Direct Lake model roles in **Semantic Models 09**.

**Row-level security**  
Four different implementations: **OneLake 05** (SQL predicate), **Warehouse 12** (T-SQL), **RTI 07** (KQL, replaces table access), **Semantic Models 04–05** (DAX, Viewer-only). They do not compose automatically.

**Outbound access protection (OAP)**  
**Warehouse 04**, **Data Engineering 02**, **Data Pipelines 01**, **RTI 01**, **Fabric IQ 05**. Behaviour differs sharply per workload — DE uses managed private endpoints, DP uses data connection rules, and the two are mutually exclusive.

**Sensitivity labels & Purview**  
**Warehouse 17–18, 25**, **Reports 08–09**, **Data Agents 07**. Label protection travels on Excel/PDF/PowerPoint/.pbix but **not** .csv/.txt, and not cross-tenant.

**Service principals**  
**Warehouse 10**, **Data Engineering 07**, **RTI 05**. Note they **cannot** be added to semantic model RLS roles (**Semantic Models 04**).

**Shortcuts**  
**OneLake 08** is the reference. Also **Data Engineering 12** (auditing) and **Semantic Models 09** (Direct Lake identity passthrough exception).

**Customer-managed keys**  
**Warehouse 16** and **Data Engineering 13** — workspace-scoped, set before data lands.

---

## A note on currency

Fabric ships quickly. Every entry reflects the product and the documentation as of publication, and preview capabilities are labelled in-content. Two areas move fastest and are worth re-verifying before you rely on them:

- **Fabric IQ and ontology** are in public preview end to end.
- **Eventhouse OneLake security enforcement**, **authorized third-party engines**, and **operations agent support for OAP** are each in preview.

Where a documented behaviour and the product disagree, the entry says so explicitly rather than quietly picking one. Verify in your own tenant before standardizing.

---

*Prepared by Nicolas Soukoff, Principal Solution Engineer - Fabric Technical Insider, Americas.*
