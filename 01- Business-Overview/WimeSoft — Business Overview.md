# WimeSoft — Business Overview

**Company Name:** WimeSoft (Fictional)  
**Industry:** SaaS / Internal Business Applications  
**Company Size:** Early-stage startup  
**Mission:** Deliver secure, reliable, and efficient internal business software while maintaining strong alignment with modern security frameworks and operational best practices.



## Business Summary
WimeSoft develops internal enterprise tools and operational business applications for small and mid-sized teams. The organization operates a compact but structured on-premises environment, featuring centralized identity, protected data stores, and tightly controlled development systems. Security, service availability, and operational efficiency form the foundation of WimeSoft’s delivery model.



## Technical Environment

### Infrastructure
 **On-Prem Systems:** Domain Controller, File Server, Application Server, Database Server, Source-Control Server, Backup Appliance  
 **Endpoints:** Management, Engineering, and Finance workstations  
 **Network:** pfSense firewall, managed switches, segmented VLANs, secure WLAN  
 **Remote Access:** VPN with MFA  
 **Monitoring:** Splunk SIEM aggregating AD, Sysmon, EDR, firewall, and network telemetry  
 **Backup Strategy:** Daily incremental, weekly full backups, offline rotation

### Development Environment
 On-prem Git and CI services  
 Hardened engineering workstations using approved software baselines  
 Controlled administrative privileges and auditable development pipelines



## Security Program Overview

WimeSoft operates a small, high-impact on-premises environment requiring strong asset visibility, resilient operations, and effective detection and response. This security program applies **NIST CSF 2.0** and **CIS Controls v8 IG2** to **define, develop, implement, and manage standards, policies, procedures, and solutions** that mitigate risk and maximize security, service availability, efficiency, and operational effectiveness.

## Core Objectives

 Establish authoritative asset inventory and classification.
 Apply CIS Controls v8 IG2 protections and security baselines.
 Build MITRE ATT&CK–aligned detection and SIEM monitoring.
 Create tested incident response and recovery capabilities.
 Maintain version-controlled standards, policies, and procedures.




## Key Deliverables

 Asset inventory with classification and dependencies.
 NIST CSF to CISv8 Controls alignment matrix.
 MITRE ATT&CK mapping.
 Splunk/ELK detection rule library.
 Incident response and recovery playbooks.
 Backup and restore procedures + recovery test logs.
 Change log, approved packages list, and version-controlled standards/policies.





## Prioritized Services & Dependencies

Critical business services include:

1. **Identity Services (Active Directory)**  
2. **Database Services**  
3. **Internal Application Platform**  
4. **File Storage**  
5. **Source Control & CI Pipeline**

All dependencies are documented to support recovery sequencing, accurate RTO/RPO planning, and resilient operational continuity.



## Likely Threats & Preparedness

Given WimeSoft’s architecture, the most probable operational threats include:

 **Credential compromise** (e.g., VPN, AD, MFA targeting)  
 **Endpoint compromise or malware execution**  
 **Service outages caused by misconfigurations or unauthorized changes**

WimeSoft’s SIEM detections, access controls, system hardening, and playbook-driven response procedures directly mitigate these risks.



## Operational Excellence & Governance
 Formal change management and approved software controls  
 Defined IAM workflows for onboarding/offboarding  
 Structured patch lifecycle and CVE triage rhythm  
 Lessons-learned loop feeding back into Identify/Protect/Detect improvements  
 All documentation version-controlled in Git for integrity and auditability



## Summary Statement
WimeSoft maintains a disciplined, framework-aligned operations and security program tailored for a modern startup. Through centralized identity, hardened infrastructure, SIEM-driven monitoring, documented IR and recovery processes, and dependable backup protections, WimeSoft ensures secure, resilient, and highly efficient delivery of internal business services.



