# Assets Directory Overview

The `assets/` directory contains the authoritative system-of-record for all operational, technical, and security-related inventories used within the WimeSoft Cybersecurity Program. These inventories support NIST CSF 2.0 **Identify (ID)** activities and CIS Controls v8 **IG2 Asset Management** requirements, enabling full visibility, ownership accountability, configuration governance, and change tracking across the environment.

This directory includes two primary inventories:

---

## 1. assets (Identify)/asset_inventory.csv

**Purpose:**  
Provides a centralized and structured register of all critical assets across the WimeSoft environment, including endpoints, servers, network devices, infrastructure components, and security systems.

**Why it matters:**  
A complete asset inventory is foundational to all security functions—patch management, vulnerability management, logging, monitoring, access control, and incident response. This inventory establishes:

- Ownership and accountability  
- Criticality ratings  
- Data sensitivity classifications  
- OS and firmware visibility  
- Network addressing and segmentation context  
- Status and lifecycle tracking  
- Security controls applied (EDR, logging, encryption, etc.)

**Structure:**  
| Field | Description |
|-------|-------------|
| AssetID | Unique identifier for internal tracking |
| Hostname | System hostname or logical name |
| AssetName | Human-readable name |
| AssetType | Endpoint, Server, Network Device, Power Device |
| Owner | Responsible person or role |
| Location | Office, Server Room, Cloud, etc. |
| Criticality | High, Medium, Low |
| DataSensitivity | Internal, Confidential, Restricted |
| OS_Version | Operating system or firmware |
| IP_Address | Assigned network address |
| MAC_Address | Interface identifier |
| Status | Active, Retired, Maintenance |
| Notes | Security controls, configuration, dependencies |

**Usage in the program:**  
- SIEM onboarding prioritization  
- Patch/vulnerability SLA enforcement  
- ATT&CK mapping (credential abuse, lateral movement, exfiltration)  
- Incident response scoping and containment  
- Backup and recovery requirements  
- Annual asset certification reviews  

---

## 2. assets (Identify)/approved_packages.csv

**Purpose:**  
Documents all **corporate-approved software** permitted within the WimeSoft environment. This forms the authoritative list used by:

- Endpoint hardening baselines  
- Application allowlisting  
- Developer workstation standards  
- Patch level verification  
- Third-party risk management  
- Compliance with CIS v8 Control 2 (Software Inventory)

**Why it matters:**  
Unmanaged software introduces risk through:

- Shadow IT  
- Unpatched applications  
- Unauthorized runtimes (Java, Python)  
- Malicious or untrusted binaries  
- Inconsistent developer environments  

This inventory ensures all installed software aligns with defined security baselines and operational requirements.

**Structure:**  
| Field | Description |
|--------|-------------|
| pkg | Application or runtime name |
| version | Approved version(s) |
| platform | Windows, Linux, or multi-platform |
| approved | true/false flag |
| notes | Business justification or restrictions |

**Usage in the program:**  
- Compliance checks during workstation/server hardening  
- Automated drift detection  
- SOC alerts for unapproved executables  
- Developer environment consistency  
- Dependency tracking for security patching  

---

## Governance and Maintenance

Both inventories follow a controlled lifecycle to maintain reliability and alignment with operational changes:

### Update Frequency
- **Monthly:** Reconciliations against EDR, AD, configuration management tools, and network scans  
- **Quarterly:** Formal review by Security Engineer + IT Admin  
- **Annually:** Audit for completeness, accuracy, and system lifecycle status  

### Change Control
All edits must follow the **WimeSoft Change Management Policy** and require:

1. Pull request
2. Reviewer approval (Security + IT)
3. Commit traceability preserved for audit

### Mapping to Framework Requirements
- **NIST CSF 2.0:** ID.AM-01, ID.AM-02, ID.RA-01  
- **CIS Controls v8 IG2:** Control 1 (Enterprise Asset Inventory), Control 2 (Software Inventory)  
- **MITRE ATT&CK:** Supports visibility for ATT&CK techniques T1087, T1018, T1057  

---

## Summary

The `assets/` directory represents the foundation of WimeSoft’s cybersecurity program.  
It enables accurate detection, effective response, informed risk decisions, and mature operational governance.  
As the environment grows, additional inventories (network diagrams, dependency mapping, backup schedules) may be added here or under related directories.





