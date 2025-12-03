# Incident Response Playbooks — Written for identified High-Priority ATT&CK Techniques

This section provides standardized incident response playbooks for Wimesoft, focused on the high-priority MITRE ATT&CK techniques identified in the Protect and Detect phases. These playbooks define the required actions for containment, eradication, recovery, and post-incident review, ensuring a consistent and repeatable response process across Wimesoft’s environment.


## Playbook 1 — Credential Compromise (T1078)

### Containment

 **Disable affected AD account**  
  Execute: `Disable-ADAccount -Identity "USERNAME"`.

 **Revoke active sessions**  
  Terminate VPN/SSO sessions and block the `src_ip` at the perimeter firewall (Asset: A-009).

 **Isolate endpoints**  
  Quarantine affected hosts.  
  Suspend any suspicious service accounts.

 **Preserve evidence**  
   AD logs  
   Splunk search exports (CSV)  
   Endpoint volatile memory snapshot (when indicated)



### Eradication

 Reset compromised credentials and enforce MFA.  
 Rotate associated administrative or service credentials and secrets.  
 Remove persistence mechanisms (unauthorized services, scheduled tasks, scripts).  
 Patch any exploited vulnerabilities.  
 Reimage hosts if indicators suggest deep compromise.



### Communication

 **Internal**  
  Provide a short incident summary including impacted users/assets, containment actions performed, required next steps, and asset/application owners involved.

 **External**  
  Only issue legal-reviewed notifications when customer/regulatory thresholds are met.



### Post-Incident Analysis

 Collect AD and VPN logs for **±7 days** around the event.  
 Gather memory images and suspicious binaries where applicable.  
 Perform root-cause analysis (phishing, credential reuse, leaked secrets, misconfiguration).  
 Add or tune Splunk detections for MFA-bypass patterns and related anomalous authentication indicators.

## Playbook 2 — Remote Services / Lateral Movement (T1021)

### Containment

 **Isolate source and target hosts**  
  Quarantine affected endpoints.
 **Block lateral movement channels**  
  Block or restrict lateral ports/protocols on internal firewalls. (Asset: A-009)

 **Disable implicated accounts**  
  Disable user/service accounts observed performing suspicious lateral activity (Asset: A-005).

 **Restrict admin sessions**  
  Terminate or restrict remote administrative sessions. Force re-authentication for active admin sessions.

 **Preserve evidence**  
  Collect process lists, network connections, and memory snapshots from isolated hosts before remediation.



### Eradication

 **Remove persistence & lateral tooling**  
  Identify and remove malicious scripts, scheduled tasks, backdoors, and any tools used for lateral movement.

 **Reimage or remediate hosts**  
  Reimage hosts showing signs of deep compromise. If reimaging is not immediately possible, perform full forensic cleanup and validation.

 **Patch network-facing & remote services**  
  Apply patches to RDP gateways, management servers, and vulnerable services; remove legacy/unsupported remote services.

 **Rotate privileged credentials**  
  Rotate credentials for local admin, service accounts, and any exposed privileged keys or certificates.



### Communication

 **Notify Network Engineers & Application Owners**  
  Inform NetOps, application owners, and identity team about affected systems and coordinate containment/remediation.

 **Coordinate maintenance windows**  
  Schedule reimages, configuration rollbacks, or patch windows with stakeholders to minimize service disruption.

 **Escalation**  
  Escalate to business owners if lateral movement reaches critical systems or sensitive data.



### Post-Incident Analysis

 **Hunt for secondary compromise**  
  Conduct enterprise-wide hunts for additional lateral traces.

 **Audit privileged session logs**  
  Review Windows Event logs for unusual admin activity and timeline reconstruction.

 **Harden remote services**  
   Require MFA and conditional access for remote admin sessions.   
   Disable legacy remote management protocols where possible.

 **Tune detections**  
  Add or refine Splunk rules for suspicious remote execution (e.g., unusual use of PsExec/WinRM, lateral file copies, abnormal RDP session patterns).

 **Lessons learned & remediation**  
  Document root cause, update playbooks and runbooks, and apply configuration/architecture changes to reduce future lateral risk.



## Playbook 3 — Command & Scripting Interpreter Abuse (T1059)

### Containment

 **Isolate affected host**  
  Quarantine the endpoint to stop further execution and network interaction.

 **Terminate malicious processes**  
  Kill offending processes. Example: `Stop-Process -Id <PID> -Force` (for forensic capture, capture a copy of memory/process image first if possible).

 **Revoke session credentials**  
  Revoke or disable accounts / sessions used in the malicious interpreter session (Asset: A-005). Revoke any active SSH/VPN tokens tied to the session (Asset: A-009).

 **Collect volatile evidence immediately**  
   Capture command-line history, running process list, loaded modules.  
   Export script files, scheduled tasks, and relevant registry autorun keys.  
   Snapshot endpoint volatile memory if code injection or living-off-the-land binaries are suspected.



### Eradication

 **Remove malicious script artifacts**  
  Delete identified script files, lateral/exfiltration scripts, and scheduled executions (tasks, cron, systemd timers).

 **Remove persistence mechanisms**  
  Clean registry autoruns, service installations, WMI persistence, and startup folders used to launch interpreters.

 **Reimage when necessary**  
  Reimage hosts when process injection, kernel-level persistence, or evasive rootkits are detected; otherwise perform thorough forensic cleanup and validation.

 **Patch & reduce attack surface**  
  Patch scripting engines and interpreter runtimes and remove unused interpreters from endpoints where possible.

 **Rotate credentials**  
  Rotate any credentials or keys that were accessed or used by the scripting activity.



### Communication

 **Notify application & system owners**  
  Inform application owners, system administrators, and identity teams of affected hosts and remediation actions.

 **Coordinate scanning & remediation**  
  Request targeted scans of related endpoints and deployments to locate reused scripts or copied tooling.

 **Escalation**  
  Escalate to Incident Commander if abuse affects critical systems, privileged accounts, or indicates broader foothold.



### Post-Incident Analysis

 **Capture and codify Indicators**  
  Add detections for captured command lines, script filenames, file hashes, loaded modules, and syscall patterns.

 **Harden scripting policy**  
  Enforce Constrained PowerShell / transcription & logging, implement AppLocker and restrict execution of unauthorized interpreters.

 **Improve visibility**  
  Confirm that command-line auditing is enabled and collect parent/child process relationships and script block logs for future correlation.

 **Tune detections & playbooks**  
  Adjust Splunk rules to alert on uncommon interpreter launches, encoded command strings, and script downloads from external hosts. Update runbooks with observed TTPs and remediation steps.

 **Lessons learned**  
  Document root cause, attacker tooling, and recommended controls (least privilege, endpoint hardening, network segmentation); incorporate into training and tabletop exercises.



## Playbook 4 — Persistence (T1547 / T1053)

### Containment

 **Quarantine affected host(s)**  
  Isolate the endpoint to prevent further persistence activity and lateral use.

 **Disable related accounts**  
  Disable any user, service, or scheduled-service accounts implicated in persistence mechanisms.

 **Block C2 & malicious destinations**  
  Block known or suspected command-and-control IPs or domains at firewalls. Use DNS sinkholing where neccessary.

 **Preserve volatile evidence**  
  Collect registry hives, scheduled task exports, service configurations, WMI repository dumps, file system snapshots and memory images prior to remediation.



### Eradication

 **Remove persistence artifacts**  
   Delete scheduled tasks and cron jobs.  
   Remove malicious/unknown services and service binaries.  
   Clean registry autorun entries and startup folder items.  
   Remove WMI event consumers/providers and COM objects used for persistence.

 **Address multiple vectors**  
  If multiple persistence vectors are present (services + scheduled tasks + WMI + registry autoruns), perform full remediation across all vectors before returning host to production.

 **Reimage when necessary**  
  Reimage hosts when evidence of tampering, multiple or kernel-level persistence, or unreliable cleanup is found.

 **Patch & remediate software**  
  Patch vulnerable or misconfigured software/mechanisms that enabled persistence (update OS, agent software, management tools).

 **Rotate credentials & secrets**  
  Rotate any credentials, service account passwords, API keys, or certificates that may have been exposed or abused.



### Communication

 **Notify forensic & system owners**  
  Share a list of affected hosts, identified persistence artifacts, and initial containment/eradication actions with the forensic team and system/application owners.

 **Coordinate remediation windows**  
  Work with Network engineers IT admins to schedule reimages, agent reinstalls, or configuration changes to minimize impact.

 **Regulatory/legal escalation**  
  Escalate to legal/compliance if persistence indicates data exposure, regulatory threshold, or contractual obligations.



### Post-Incident Analysis

 **Hunt for related persistence**  
  Hunt for identical or similar persistence indicators (service names, task names, registry keys, WMI artifacts, file hashes).

 **Harden baselines & reduce privileges**  
  Remove unnecessary local admin rights where possible, enforce least privilege for service accounts, and lock down startup locations.

 **Detection & logging**  
  Add detections for persistence-creation events: process creation that writes to common autorun locations, new service creation, scheduled task registration, WMI consumer/provider creation. Ensure logging covers these telemetry sources.

 **Improve controls**  
  Implement/expand application allowlisting  endpoint tamper protection, and configuration baselining to prevent unauthorized persistence.

 **Lessons learned & runbook updates**  
  Document root cause, persistence techniques observed, remediation steps, and update playbooks/runbooks and detection rules accordingly. Run a validation sweep after controls are applied.



## Playbook 5 — Data Exfiltration (T1074 / T1020 / T1030)

### Containment

 **Block outbound channels**  
   Block known C2 / exfil destinations at perimeter firewalls. (Asset: A-009)  
   Apply temporary egress restrictions (block large file transfers) where feasible.

 **Isolate staging hosts**  
  Quarantine hosts used for data staging.


 **Suspend involved accounts & services**  
  Temporarily disable user/service accounts involved in staging or transfer until validated.

 **Preserve evidence**  
   Collect file manifests, timestamps, hashes, and storage access logs (object-store audit logs).  
   Preserve firewall and splunk telemetry showing transfer activity.  
   Snapshot staging hosts and collect memory if live exfil tools are suspected.



### Eradication

 **Remove staged files**  
  Locate and securely delete staged data from temporary locations (endpoints, shares, object buckets). Record hashes and deletion actions for chain-of-custody.

 **Rotate compromised credentials & secrets**  
  Rotate service-account keys that may have been exposed or abused.

 **Secure storage permissions**    
   Remove overly permissive public access and shared links; replace with least-privilege access patterns.

 **Reimage or remediate staging hosts**  
  Reimage hosts where exfil tooling, upload agents, or unknown binaries are found.

 **Patch & remove tooling**  
  Remove attacker tooling, scheduled upload jobs, and any automation used for exfil. Patch vulnerable services used as staging vectors.



### Communication

 **Engage Legal & PR**  
  Notify legal/compliance and public relations early to assess regulatory notification requirements and prepare external messaging.

 **Notify Data/Business Owners**  
  Inform business, data owners, and impacted application teams with a clear summary of data types, scope, and containment actions.

 **Customer / Regulatory Notification**  
  If thresholds are met, coordinate legal-reviewed notifications to customers and regulators with required timelines and content.




### Post-Incident Analysis

 **Review access & transfer patterns**  
  Analyze who accessed the data, when, and how it was aggregated and transferred.


 **Enhance detection for anomalous uploads**  
  Add Splunk alerts for large or unusual uploads,  creation of archive files, and use of uncommon transfer protocols or ports.

 **Hunt for secondary exfil**  
  Conduct enterprise-wide hunts for matching file hashes, similar upload patterns, recreated staging locations, or reuse of compromised credentials.

 **Data validation & recovery**  
  Verify integrity of remaining data, restore from known-good backups where necessary, and ensure deleted sensitive files are unrecoverable per policy.

 **Lessons learned & controls**  
  Document root cause, attack chain, and control gaps. Update playbooks, runbooks, IAM policies, backup/config baselines, and run tabletop exercises to validate improvements.

 **Evidence retention**  
  Store collected artifacts, logs, and forensic images in secure evidence storage for potential legal/regulatory needs.
