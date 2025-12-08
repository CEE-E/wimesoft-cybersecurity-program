# WimeSoft — Business Overview

Company name: **WimeSoft**  
Industry: **Internal business applications / SaaS-style tooling**  
Stage and size: **Early-stage startup**  



## Executive Summary
WimeSoft develops internal enterprise tooling for business teams, operating a compact on-premises environment designed for high availability and strong security hygiene. The security program is aligned to **NIST Cybersecurity Framework v2.0**, implemented through **CIS Controls v8 (IG2)** to convert policy into practical controls, detections, and procedures.  

This approach ensures that security is not theoretical but enforceable, measurable, and maintainable by a small operations team.



## Technical Environment

### Infrastructure
- Domain Controller
- File Server
- Application Server
- Database Server
- Source Control and CI Server
- Backup Appliance

### Endpoints
- Management, Engineering, and Finance workstations  
- Hardened OS baselines with EDR protection  

### Network
- pfSense perimeter firewall  
- Managed switches with VLAN segmentation  
- Isolated management, production, and guest networks  

### Remote Access
- VPN access enforced with Multi-Factor Authentication  
- Restricted administrative access  

### Observability and Telemetry
- Splunk SIEM ingesting:
  - AD logs
  - Sysmon logs
  - Firewall/VPN logs
  - Application server logs  

### Backup and Retention
- Daily incremental / weekly full backups  
- Encrypted offline rotation  
- Periodic restore validation  



## Security Program Approach

- Alignment with **NIST CSF v2.0** for program structure  
- Control implementation driven by **CIS Controls v8 IG2**  
- Detection engineering mapped to **MITRE ATT&CK techniques**  
- Incident readiness built through documented and tested playbooks  
- Recovery strategy with defined RTO/RPO and restore procedures  

The program focuses on control effectiveness, operational resilience, and evidence-based compliance.


## Core Objectives
1. Maintain an authoritative asset inventory with ownership and classification.  
2. Implement CIS security baselines including MFA, EDR, logging, hardening, and access control.  
3. Build ATT&CK-mapped SIEM detections with triage documentation.  
4. Maintain incident response and recovery capability with measurable outcomes.  
5. Store all artifacts in Git for integrity, auditability, and lifecycle management.


## Key Deliverables
- Asset inventory and dependency classification  
- NIST CSF ↔ CIS v8 alignment matrix and implementation notes  
- MITRE ATT&CK mapping  
- Splunk detection rule library  
- Incident response playbooks  
- Recovery procedures and restore test logs  
- Change log, approved software list, and policies  

Each deliverable includes ownership, validation steps, and evidence of control effectiveness.


## Prioritized Services and Dependencies
Critical services and dependent systems are documented to support recovery sequencing:

- Identity Services (Active Directory)
- Database Services
- Internal Applications
- File Storage
- Source Control and CI

Dependency mapping ensures that restoration is performed in the correct order following disruption.


## Most Likely Threats and Mitigations

| Threat Scenario | Primary Mitigations |
|----------------|---------------------|
| Credential compromise targeting VPN/AD | MFA, least privilege, login monitoring, SIEM alerts |
| Endpoint compromise or malware execution |  Sysmon logging, application control |
| Misconfiguration or unauthorized change | Change control, config backups, drift detection |


## Governance and Operations
- Change control enforced through ticketing and approved workflows  
- Vulnerability and patch management follow scheduled cadence and SLAs  
- Evidence, artifacts, and documentation stored in Git for traceability  
- Post-incident lessons feed into control updates and detection tuning  


## Summary
WimeSoft operates a structured and framework-aligned security program tailored for a modern startup. With centralized identity, hardened infrastructure, SIEM monitoring, incident response procedures, and tested recovery processes, WimeSoft maintains secure and resilient delivery of internal services while supporting business growth and operational efficiency.

