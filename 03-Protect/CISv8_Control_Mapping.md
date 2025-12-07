# NIST CSF 2.0 to CIS Controls v8 (IG2) Mapping — WimeSoft

**Scope:** Mapping tailored to WimeSoft’s on-premises  asset list (Assets A-001–A-017).  
**Purpose:** Provide a clear, actionable mapping from NIST CSF 2.0 subcategories to CIS Controls v8 (IG2), with recommended technical implementations that are realistic for a small, on-prem startup. This mapping is intended to guide engineering tasks, control implementation plans (CIPs), SIEM detection development, and incident response planning.


## How this mapping supports the *Protect* function

This mapping is intentionally practical: each NIST subcategory mapped to a CIS control includes a concrete technical implementation step that can be actioned, tested, and audited. By translating framework requirements into measurable configurations and processes (GPOs, encryption, MFA, EDR, patch windows, retention SLAs, etc.), the mapping ensures the **Protect** function is not just conceptual — it is a set of repeatable engineering tasks


## Identify (ID)

| NIST CSF Subcategory | CIS v8 (IG2) | Technical Implementation (On-Prem IG2) | Mapped Assets | Notes / Rationale |
| --- | --- | --- | --- | --- |
| **ID.AM-1** — Physical & software inventory | CIS 1.1 / 1.2 | Centralized asset registry with AssetID, owner, OS/version, serial, lifecycle state. Quarterly reconciliation. | A-001 to A-017 | Supports complete asset awareness, lifecycle management and priority-based control application. |
| **ID.AM-2** — Software inventory | CIS 2.1 | Approved software catalog; allowlisting; scanning for unauthorized applications. | A-001, A-002, A-003, A-004, A-006, A-007, A-013 | Reduces attack surface and improves accuracy of vulnerability & patch processes. |
| **ID.AM-4** — External information systems | CIS 1.3 / 15.1 | Vendor inventory, firmware tracking, access rules, onboarding review. | A-004, A-006, A-007, A-008 | Enables informed third-party risk decisions and dependency governance. |
| **ID.AM-5** — Resource prioritization | CIS 4.1 | Classification policy tied to BCP impact & recovery objectives. | A-001 to A-017 | Ensures controls and recovery strategies align with business value of systems. |
| **ID.RA-2** — Threat identification | CIS 7.1 / 7.2 | Vulnerability scanning, threat intel review, local risk register. | A-001 to A-017 | Provides structured view of evolving threats & remediation priorities. |
| **ID.RA-6** — Risk reduction decisions | CIS 17.1 | Risk treatment plans, compensating controls, approval workflow. | A-001 to A-017 | Supports repeatable risk management decisions aligned to tolerance. |



## Protect (PR)

| NIST CSF Subcategory | CIS v8 (IG2) | Technical Implementation | Mapped Assets | Notes / Rationale |
| --- | --- | --- | --- | --- |
| **PR.AC-1** — Account management | CIS 5.2 / 5.3 | AD-backed identity, RBAC, service account lifecycle control. | A-004; A-001–A-007, A-013 | Reduces account sprawl and strengthens access governance. |
| **PR.AC-3** — MFA | CIS 6.3 | MFA for privileged/vpn/remote access. | A-001, A-002, A-004, A-007 | Increases authentication assurance and reduces credential compromise risk. |
| **PR.AC-5** — Privileged access | CIS 6.5 / 6.6 | PAM tiering. | A-001–A-007, A-013 | Limits privilege abuse pathways and improves forensic accountability. |
| **PR.DS-1** — Data at rest | CIS 3.3 | Disk encryption, NAS key rotation. | A-001–A-004, A-007, A-008 | Maintains confidentiality during device theft or breach. |
| **PR.PT-3 / PR.IP-1** — Secure config | CIS 4.6 / 4.7 | Hardened OS templates, GPO baselines, drift monitoring. | A-001–A-008, A-010–A-012 | Reduces risk of misconfigurations exploited in initial access. |
| **PR.MA-1** — Patching | CIS 7.3 / 7.4 | WSUS/Linux patch cadence, testing, maintenance windows. | A-001–A-008, A-013 | Reduces exploit window for known vulnerabilities. |
| **PR.PT-5** — Local access restriction | CIS 4.4 | USB controls, AppLocker, host firewall rules. | Endpoints A-001–A-003 | Minimizes malware execution vectors and exfiltration. |
| **PR.IP-3** — Change control | CIS 4.7 | CAB approval, rollback plans, logged modifications. | All assets | Maintains stability and ensures traceable change history. |
| **PR.PT-4** — Physical security | CIS 14.1 | Badge access, CCTV, visitor logs, rack security. | A-004–A-008, A-014–A-015 | Reduces physical intrusion risk and supports investigations. |



## Detect (DE)

| NIST CSF Subcategory | CIS v8 (IG2) | Technical Implementation | Mapped Assets | Notes / Rationale |
| --- | --- | --- | --- | --- |
| **DE.CM-1** — Continuous monitoring | CIS 8.2 / 8.3 | SIEM ingest (FW, DC, endpoints, servers, backup logs). | A-001–A-015 | Enables broad telemetry visibility and event correlation. |
| **DE.CM-3** — Monitoring coverage | CIS 8.4 |  Sysmon logs, firewall telemetry. | A-001–A-015 | Increasing coverage strengthens detection depth. |
| **DE.CM-7** — Anomaly detection | CIS 8.5 / 8.6 | Behavioral rules for login anomalies & suspicious processes. | A-001–A-015 | Detects TTP behavior beyond signature-based alerts. |
| **DE.AE-2** — Analysis & triage | CIS 8.6 | Correlation rules mapped to ATT&CK, enrichment applied. | A-014–A-015 | Improves investigation context & reduces false positives. |
| **DE.DP-4** — Log retention | CIS 8.1 | Tiered retention 30–90 days & archival. | A-015, A-008 | Maintains forensic continuity and audit readiness. |
| **DE.DP-2** — Alerting | CIS 8.7 | Alert routing with SLA and escalation matrix. | All monitored assets | Ensures actionable alerts and reduces response latency. |




## Respond (RS)

| NIST CSF Subcategory | CIS v8 (IG2) | Technical Implementation | Mapped Assets | Notes / Rationale |
| --- | --- | --- | --- | --- |
| **RS.CO-1** — Response plan | CIS 11.1 | IR plan, assigned roles, escalation contacts. | Org-wide | Drives predictable coordinated response under time pressure. |
| **RS.MI-1** — Analysis | CIS 11.2 | Scenario runbooks, evidence workflows. | A-001–A-007, A-013 | Supports structured investigation and evidence preservation. |
| **RS.MI-3** — Containment | CIS 11.3 | Account disable, host isolation, ACL quarantine. | A-001–A-007, A-010–A-012 | Minimizes blast radius of active threat. |
| **RS.RP-1** — Reporting | CIS 11.5 | Notification templates, incident reports, exec summaries. | All assets | Ensures consistent communication and compliance output. |
| **RS.IM-2** — Evidence | CIS 11.4 | Write-blocked imaging, chain-of-custody, repo. | Impacted systems | Maintains forensic integrity for legal or IR use. |
| **RS.CO-2** — Coordination | CIS 11.6 | Comm matrix, tabletop schedule. | Org-level | Improves org-wide readiness and learning maturity. |



## Recover (RC)

| NIST CSF Subcategory | CIS v8 (IG2) | Technical Implementation | Mapped Assets | Notes / Rationale |
| --- | --- | --- | --- | --- |
| **RC.RP-1** — Recovery planning | CIS 12.1 | Backup & restore policy, RTO/RPO defined, offsite copy. | A-004, A-007, A-008, A-013 | Aligns recovery capability with business continuity expectations. |
| **RC.IM-1** — Recovery execution | CIS 12.3 | Restore drills, validation checklists, success metrics. | A-004, A-007, A-008 | Confirms backup integrity and operational readiness. |
| **RC.CO-1** — Comms post-recovery | CIS 12.4 | Incident post-mortem, lessons learned review. | All assets | Drives iterative improvement of control posture. |
| **RC.IM-2** — Alternate operations | CIS 12.5 | Manual fallback & degraded-mode workflows. | Critical services | Ensures business function during partial outage. |

