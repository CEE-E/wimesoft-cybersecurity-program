# NIST CSF 2.0 → CIS v8 (IG2) Mapping — (WimeSoft)

This document maps NIST CSF 2.0 subcategories to CIS Controls v8 (IG2) and provides recommended technical implementations tailored to a small on-premises environment. The mapping explicitly supports the Protect function by ensuring we have documented, measurable controls that enforce secure configuration, access management, data protection, and vulnerability reduction throughout the environment.

---

## Identify (ID)

| NIST CSF Subcategory | CIS v8 (IG2) | Technical Implementation (On-Prem IG2) | Mapped Assets | Notes / Rationale |
|---|---|---|---|---|
| **ID.AM-1 — Physical & software inventory** | CIS 1.1 / 1.2 | Centralized asset registry with unique AssetID, owner, OS/version, serial, location and lifecycle state. Automated discovery plus quarterly manual reconciliation. | A-001 to A-017 | IG2 expects richer metadata and documented reconciliation processes. |
| **ID.AM-2 — Software inventory** | CIS 2.1 | Maintain an approved software registry and an application allowlist; run periodic scans to detect unauthorized software. | A-001, A-002, A-003, A-004, A-006, A-007, A-013 | Reduces attack surface and supports prioritized patching. |
| **ID.AM-4 — External information systems (vendors)** | CIS 1.3 / 15.1 | Vendor inventory including warranty, firmware version, patch SLA and vendor access policy; track on-site access events. | A-004, A-006, A-007, A-008 | IG2 expects formal vendor management even for on-prem hardware. |
| **ID.AM-5 — Resource prioritization / classification** | CIS 4.1 | Asset classification policy (Public / Internal / Confidential / Restricted) mapped to business impact and RTO/RPO. | A-001 to A-017 | Enables prioritized backups, patching and control application. |
| **ID.RA-2 — Threat identification** | CIS 7.1 / 7.2 | Regular authenticated vulnerability scans, periodic threat modeling, and a local risk register. | A-001 to A-017 | IG2 requires recurring vulnerability management and documented triage. |
| **ID.RA-6 — Risk reduction decisions** | CIS 17.1 | Risk treatment plans with compensating controls, acceptance criteria, and remediation SLAs tied to asset criticality. | A-001 to A-017 | Formal, documented risk decisions with approval are expected at IG2. |

---

## Protect (PR)

| NIST CSF Subcategory | CIS v8 (IG2) | Technical Implementation (On-Prem IG2) | Mapped Assets | Notes / Rationale |
|---|---|---|---|---|
| **PR.AC-1 — Account management** | CIS 5.2 / 5.3 | Centralized Active Directory accounts, role-based groups, documented joiner/mover/leaver workflows, and service account lifecycle controls. | A-004; endpoints and servers (A-001 to A-007, A-013) | IG2 requires centralized identity with full lifecycle tracking. |
| **PR.AC-3 — Multi-factor authentication (MFA)** | CIS 6.3 | Enforce MFA for privileged accounts and remote administration (hardware token or TOTP); require MFA for sensitive actions. | Admin accounts on A-001, A-002, A-004, A-007 | IG2 extends MFA beyond a minimal admin set. |
| **PR.AC-5 — Privileged access management** | CIS 6.5 / 6.6 | Use a tiered admin model, eliminate persistent local admin rights, require jump hosts for sensitive tasks and enable session logging. | Servers and endpoints (A-001 to A-007, A-013) | Privilege separation and audited sessions are required at IG2. |
| **PR.DS-1 — Data-at-rest protection** | CIS 3.3 | BitLocker (Windows) and LUKS (Linux) for disk encryption; NAS/encrypted volumes; documented key management and rotation. | A-001 to A-004, A-007, A-008 | Formal encryption and key handling are expected at IG2. |
| **PR.PT-3 / PR.IP-1 — Secure configuration & baselines** | CIS 4.6 / 4.7 | Maintain hardened OS/server images and GPO baselines for endpoints; implement configuration-drift detection and automated audits. | A-001 to A-008, A-010 to A-012 | Baselines should be versioned, tested and enforced at IG2. |
| **PR.MA-1 — Patch management** | CIS 7.3 / 7.4 | WSUS/patch pipeline for Windows; scheduled Linux package updates; patch testing in staging before production rollout. | A-001 to A-008, A-013 | IG2 requires scheduled patch windows and validation logs. |
| **PR.PT-5 — Local access restrictions** | CIS 4.4 | Block removable media via policy, implement application allowlisting (AppLocker or equivalent), and local host firewall rules. | Endpoints (A-001, A-002, A-003) | Reduces opportunities for malware execution and data exfiltration. |
| **PR.IP-3 — Change control** | CIS 4.7 | Formal change request process, CAB approvals, rollback plans and a maintained change log. | All production infrastructure | IG2 expects documented change control for production assets. |
| **PR.PT-4 — Physical security** | CIS 14.1 | Server room badge access, CCTV, visitor logging and rack labeling/tagging. | Server room: A-004, A-005, A-006, A-007, A-008, A-014, A-015 | Physical protections must be auditable at IG2. |

---

## Detect (DE)

| NIST CSF Subcategory | CIS v8 (IG2) | Technical Implementation (On-Prem IG2) | Mapped Assets | Notes / Rationale |
|---|---|---|---|---|
| **DE.CM-1 — Continuous monitoring** | CIS 8.2 / 8.3 | Centralized log collection using SIEM (A-014) ingesting endpoint, firewall, DC, server and NAS logs; log normalization and retention policies. | A-001 to A-015 | IG2 requires cross-system log correlation (SOC-lite). |
| **DE.CM-3 — Monitoring coverage** | CIS 8.4 | Ensure EDR on endpoints, Sysmon or auditd on servers, firewall and DC telemetry; validate collector coverage. | A-001 to A-015 | Broader telemetry coverage than IG1. |
| **DE.CM-7 — Unauthorized / anomalous behavior detection** | CIS 8.5 / 8.6 | Implement detection rules for unusual logons, failed-logon surges, suspicious processes and lateral movement; tier and prioritize alerts. | A-001 to A-015 | Behavior detection and tuning is required at IG2. |
| **DE.AE-2 — Analysis of anomalies** | CIS 8.6 | Correlation rules mapped to MITRE ATT&CK, analyst triage checklists, and defined enrichment sources. | SIEM and Log Collector (A-014, A-015) | Alerts should be triageable with contextual enrichment at IG2. |
| **DE.DP-4 — Logging retention & protection** | CIS 8.1 | Retain logs 30–90 days by asset criticality; protect logs via WORM or write-once archival and offsite copies. | Log storage (A-015), Backup Server (A-008) | Protected logs and retention SLAs are expected at IG2. |
| **DE.DP-2 — Alerts & notifications** | CIS 8.7 | Route alerts to on-call engineer (email/SMS) with linked runbooks and a documented escalation matrix and SLA. | Monitored assets | Alert delivery, SLA and escalation processes are required at IG2. |

---

## Respond (RS)

| NIST CSF Subcategory | CIS v8 (IG2) | Technical Implementation (On-Prem IG2) | Mapped Assets | Notes / Rationale |
|---|---|---|---|---|
| **RS.CO-1 — Response planning** | CIS 11.1 | Maintain a formal IR plan in the repository and file server; assign IR roles (incident owner, communications, IT lead), contact list and escalation paths. | All critical assets | IG2 requires documented and assigned IR roles. |
| **RS.MI-1 — Incident analysis & triage** | CIS 11.2 | Provide runbooks for credential compromise, ransomware-like behavior and insider misuse; include forensic collection procedures (memory, network, disk). | Endpoints and servers (A-001 to A-007, A-013) | Runbooks must include forensic steps and evidence preservation guidance. |
| **RS.MI-3 — Containment & mitigation** | CIS 11.3 | Procedures to suspend AD accounts, isolate hosts via EDR (A-014), apply network ACL quarantine and, if necessary, shut down switch ports. | A-001 to A-007, network devices (A-010 to A-012) | IG2 supports host and network containment capabilities. |
| **RS.RP-1 — Reporting & communication** | CIS 11.5 | Incident report templates, executive summaries, internal/external notification templates and a post-incident review timeline. | All assets | Formalized reporting and lessons-learned processes are expected at IG2. |
| **RS.IM-2 — Evidence preservation** | CIS 11.4 | Chain-of-custody controls, write-block imaging procedures, and a centralized read-only forensic repository. | Affected endpoints and servers | Ensures evidence integrity for remediation and legal needs. |
| **RS.CO-2 — Stakeholder coordination** | CIS 11.6 | Communication matrix including legal, HR, executives and vendors; schedule regular tabletop exercises. | Organization-level | IG2 expects periodic exercises and communication readiness. |

---

## Recover (RC)

| NIST CSF Subcategory | CIS v8 (IG2) | Technical Implementation (On-Prem IG2) | Mapped Assets | Notes / Rationale |
|---|---|---|---|---|
| **RC.RP-1 — Recovery planning** | CIS 12.1 | Document backup and restore policy with RTO/RPO per asset class, defined backup owners, schedules and offsite rotation procedures. | File Server, Database, Backup Server, Source-Control (A-004, A-007, A-008, A-013) | IG2 requires defined RTO/RPO and documented recovery steps. |
| **RC.IM-1 — Recovery execution & testing** | CIS 12.3 | Scheduled restore tests: weekly file-level, monthly full system restores in staging; use validation checklists and measure restore times. | A-004, A-007, A-008 | Regular, documented restore validation is expected at IG2. |
| **RC.CO-1 — Recovery communications & continuous improvement** | CIS 12.4 | Produce post-incident recovery reports; feed lessons learned into playbooks and baselines; maintain version-controlled recovery documentation. | All assets | Recovery outcomes must inform Identify/Protect improvements. |
| **RC.IM-2 — Alternate operations** | CIS 12.5 | Define degraded operation procedures (read-only modes, minimal services) and manual workarounds to maintain critical functions. | Business-critical services | IG2 expects planning for partial outages and operational continuity. |

---
