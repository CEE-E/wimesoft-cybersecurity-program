# MITRE ATT&CK Mapping

**Scope:** Mapping tailored to Wimesoft's assets 001 through A-017.  

**Purpose:** This document provides a structured mapping between NIST Cybersecurity Framework (CSF) 2.0 subcategories and CIS Controls v8 (Implementation Group 2), and links those control areas to relevant MITRE ATT&CK techniques for WimeSoft’s on-premises environment (Assets A-001 through A-017). It is intended as a prescriptive reference for detection engineering, SIEM rule development, control implementation and validation, and incident response planning. The mapping is also used to ensure the Protect function is complete and verifiable, enabling the team to define, implement, and continuously validate technical safeguards (configuration baselines, access controls, encryption, patching) and to trace detection logic back to specific controls and assets.
## Identify (ID)

### ID.AM-1 — Physical & software inventory
**Techniques**
 T1078 — Valid Accounts  
 T1543 — Create or Modify System Process

**Rationale**  
A comprehensive asset and software inventory enables detection of unauthorized accounts and unapproved service or process changes.

**Telemetry / Sources**  
Active Directory logs, Sysmon service creation events, asset inventory feeds.

**Mapped Assets**  
A-001 through A-017

**Recommended Detections**
 New computer object created in AD where the hostname is not present in the asset inventory.  
 Service or process creation events on servers that lack an approved change record.



### ID.AM-2 — Software inventory
**Techniques**
 T1059 — Command and Scripting Interpreter (including PowerShell T1086)  
 T1204 — User Execution

**Rationale**  
Unauthorized tooling and scripting frequently indicate misuse or initial compromise through user execution.

**Telemetry / Sources**  
Sysmon process creation, package manager logs (apt/dpkg, Windows Installer), configuration management scans.

**Mapped Assets**  
A-001, A-002, A-003, A-013

**Recommended Detections**
 Interpreter (PowerShell, cmd, bash) executions spawned by non-standard parent processes.  
 Installation of packages or binaries not present in the approved packages registry.



### ID.AM-4 — External information systems (vendors)
**Techniques**
 T1499 / T1490 — Impact (network/service disruption)

**Rationale**  
Vendor firmware updates or remote management operations can change device behavior; tracking these events reduces misattribution and shortens response time.

**Telemetry / Sources**  
Firmware update logs, device management console logs, vendor access session logs.

**Mapped Assets**  
A-009, A-010, A-015

**Recommended Detections**
 Unscheduled firmware upgrades or configuration commits on network devices.  
 Management console access from unknown accounts or unexpected source IPs.



### ID.AM-5 — Resource prioritization / classification
**Techniques**
 T1486 — Data Encrypted for Impact (Ransomware)

**Rationale**  
High-value assets (databases, file servers, code repositories) are primary targets for encryption and extortion; classification informs protection and recovery priorities.

**Telemetry / Sources**  
File modification events, file rename patterns,  behavioral indicators, file integrity monitoring.

**Mapped Assets**  
A-004, A-007, A-013

**Recommended Detections**
 Rapid, repeated file modifications or renames on critical shares/datastores.  
 Processes performing recursive file operations that deviate from baseline behavior.



### ID.RA-2 / ID.RA-6 — Threat identification / risk reduction
**Techniques**
 T1110 — Brute Force  
 T1078 — Valid Accounts

**Rationale**  
Credential compromise via brute force or credential stuffing is a common initial access vector in small organizations.

**Telemetry / Sources**  
AD failed logon events, VPN authentication logs, perimeter firewall logs.

**Mapped Assets**  
A-005, A-017, A-009

**Recommended Detections**
 Bursts of authentication failures for a single account or from a single source IP.  
 Privileged account logins from anomalous geolocations or at unusual hours.



## Protect (PR)

### PR.AC-1 / PR.AC-3 / PR.AC-5 — Account management, MFA, privileged access
**Techniques**
 T1078 — Valid Accounts  
 T1110 — Brute Force

**Rationale**  
Centralized identity, MFA, and least privilege reduce the success of credential attacks and limit lateral movement.

**Telemetry / Sources**  
AD authentication and privilege events, VPN logs.

**Mapped Assets**  
A-001 through A-003, A-005, A-017

**Recommended Detections**
 Privileged logon activity without documented approval or contextual justification.  
 Repeated or suspicious MFA failures and potential MFA bypass attempts.



### PR.DS-1 / PR.DS-2 — Data protection (at-rest and in-transit)
**Techniques**
 T1005 — Data from Local System  
 T1041 — Exfiltration Over C2 Channel

**Rationale**  
Encryption and monitoring reduce exposure and enable detection of abnormal data movements.

**Telemetry / Sources**  
Database query logs, SMB/CIFS transfer logs, network flow records.

**Mapped Assets**  
A-004, A-007, A-008, A-006

**Recommended Detections**
 Large outbound transfers from application or database servers outside scheduled backups.  
 Unusual patterns of data access or exports from restricted shares.



### PR.PT-3 / PR.IP-1 — Secure configuration & baselines
**Techniques**
 T1547 — Boot or Logon Autostart Execution

**Rationale**  
Configuration drift enables persistence and unauthorized autoruns; maintained baselines make deviations detectable.

**Telemetry / Sources**  
Sysmon ImageLoad and service events, registry change events, baseline configuration reports.

**Mapped Assets**  
A-001 through A-007

**Recommended Detections**
 Registry autorun entries or new startup services not present in the baseline.  
 Configuration drift alerts for hardened endpoints or servers.



### PR.MA-1 — Patch management
**Techniques**
 T1190 — Exploit Public-Facing Application  
 T1203 — Exploitation for Client Execution

**Rationale**  
Timely patching reduces exposure to known exploits in application and infrastructure components.

**Telemetry / Sources**  
Vulnerability scanner results, web server logs, IDS/WAF alerts.

**Mapped Assets**  
A-006, A-013

**Recommended Detections**
 Inbound traffic patterns consistent with known CVE exploit attempts.  
 Correlation between vulnerability scanner findings and anomalous inbound connections or behavior.



### PR.PT-5 — Local access restrictions (allowlisting, USB block)
**Techniques**
 T1055 — Process Injection

**Rationale**  
Application allowlisting and media controls reduce opportunities for arbitrary code execution and process injection.

**Telemetry / Sources**  
Endpoint process creation events, USB mount logs, Windows audit logs.

**Mapped Assets**  
A-001 through A-003

**Recommended Detections**
 Execution of binaries from removable media or non-standard filesystem paths.  
 Indicators of process injection or suspicious parent/child process relationships.



### PR.PT-4 — Physical security
**Techniques**
 T1202 — Indirect Command Execution (physical compromise enabling code execution)

**Rationale**  
Physical access can enable multiple ATT&CK techniques; physical controls and correlation are required.

**Telemetry / Sources**  
Badge access logs, CCTV event logs, physical access records.

**Mapped Assets**  
Server room: A-004, A-005, A-007, A-014, A-015

**Recommended Detections**
 Unscheduled physical access to the server room outside approved maintenance windows.  
 Administrative console access coincident with recorded physical access events.



## Detect (DE)

### DE.CM-1 / DE.CM-3 — Centralized logging & coverage
**Techniques**
 T1078, T1110, T1059, T1003, T1021

**Rationale**  
Comprehensive telemetry across identity, endpoints, network, and servers enables detection of credential abuse, scripting misuse, credential dumping, and lateral movement.

**Telemetry / Sources**  
AD security events (A-005), Sysmon process and network telemetry (A-001 through A-007), firewall and VPN logs (A-009, A-017), normalized logs via Log Collector (A-015) into SIEM (A-014).

**Recommended Detections**
 Suspicious interactive administrative logons from external IP addresses.  
 Indicators of credential dumping.  
 Rapid multi-host authentication activity via remote services (RDP/SMB/SSH).



### DE.CM-7 / DE.AE-2 — Behavior detection & analysis
**Techniques**
 T1003, T1059/T1086, T1055, T1486, T1490/T1499

**Rationale**  
Behavioral detection with correlation reduces false positives and raises fidelity for high-value TTPs.

**Telemetry / Sources**  
End point processes and command-line telemetry, file integrity monitoring (A-004, A-007), SIEM correlation and firewall logs.

**Recommended Detections**
 Correlated alerts for credential dumping or process injection with unusual outbound traffic.  
 File integrity alerts for mass modifications on critical shares.



### DE.DP-4 / DE.DP-2 — Retention and alerting
**Rationale**  
Historical visibility is required to investigate exfiltration, credential abuse, and lateral movement.

**Telemetry / Sources**  
SIEM log retention (A-014), archival storage (A-008), log integrity controls (A-015).

**Recommended Practices**
 Maintain 30–90 day retention based on asset criticality.  
 Ensure alerts route to on-call personnel and link to appropriate runbooks and escalation paths.



## High-Priority ATT&CK Techniques — Quick Reference

| ATT&CK ID | Technique | Relevance | Primary Telemetry / Primary Assets |
|---:|---|---|---|
| T1078 | Valid Accounts | Common vector for privilege misuse and persistence | AD logs (A-005), VPN (A-017), SIEM (A-014) |
| T1110 | Brute Force | Credential stuffing / brute force against DC or VPN | AD failed logon events, VPN logs (A-017) |
| T1003 | Credential Dumping | Privilege escalation via LSASS/memory | LSASS telemetry (A-014), Sysmon (A-005) |
| T1021 | Remote Services | Lateral movement via RDP/SMB/SSH | AD logs, firewall logs (A-009) |
| T1059 | Command & Scripting Interpreter | Post-exploitation activity (scripting) | Sysmon process creation,  (A-001 through A-007) |
| T1486 | Data Encrypted for Impact | Ransomware targeting DB/file servers | File modification spikes (A-004, A-007) |
| T1041 / T1071 | Exfiltration / C2 | Data exfiltration over network or C2 channels | Firewall logs (A-009), SIEM correlation (A-014) |
| T1543 | Create/Modify System Process | Persistence via service or scheduled task creation | Sysmon/service events (A-004, A-006, A-013) |



