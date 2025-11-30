## 1) Valid Accounts — T1078

**Goal:**  
Detect logins that use valid accounts from unusual sources, unexpected hosts, or hosts that do not belong to the account owner (possible misuse or persistence).

**Primary Assets:**  
 AD logs (dc-01 / A-005)  
 VPN logs (vpn-01 / A-017)  
 Splunk (A-014)

**Required Indexes:**  
 `wineventlog`   
 `index=vpn`  
  
### Sample rule on splunk to detect Login from Unexpected Host / Suspicious VPN Multi-Host
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/1.png)

## 2) Brute Force / Credential Stuffing — T1110

**Goal:**  
Detect repeated failed authentication attempts against DC (A-005), VPN (A-017), or other authentication endpoints indicating brute-force or credential-stuffing activity.

**Required telemetry:**  
 AD failed logon events (`EventCode=4625`)  
 VPN logs


### Failed Logon Threshold
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/2.2.png)

### VPN-specific variant
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/3.png)

## 3) Credential Dumping — T1003

**Goal:**  
Detect access to LSASS memory or actions consistent with credential dumping (e.g., ProcessAccess events, suspicious tools reading `lsass.exe`).

**Primary  Assets:**  
 EDR / LSASS  (via EDR ingest to SIEM)  
 Sysmon ProcessAccess (`EventID=10`)  
 Hosts: dc-01 (A-005) and endpoints (A-001–A-007)

**Required Index:**  
 `index=sysmon` (Sysmon events)



### LSASS Access Detection
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/4.1.png)

## 4) Remote Services — T1021 (RDP/SMB/SSH Lateral Movement)

**Goal:**  
Detect suspicious RDP, SMB, or SSH usage patterns and potential lateral movement attempts across endpoints (A-001–A-007) or servers (A-004, A-007).

**Primary Assets:**  
 AD logs  
 Sysmon Process Creation (`EventID=1`)  
 Firewall logs (fw-01)  
 Linux authentication logs (SSH)


###  Suspicious RDP Connection & Process
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/5.png)

### ssh-lateral-from-unexpected-host
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/6.png)

## 5) Command & Scripting Interpreter — T1059

**Goal:**  
Detect suspicious usage of scripting interpreters (PowerShell, cmd, bash, Python), especially those involving encoded commands or remote download/execution patterns.

**Primary Telemetry:**  
 Sysmon Process Creation (`EventID=1`)  
 EDR process telemetry

**Assets:**  
 Endpoints (A-001–A-003)  
 Developer hosts (A-002)



### PowerShell Encoded IOC
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/7.png)

### Scripting-on-critical-host
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/8.png)

## 6) Data Encrypted for Impact (Ransomware) — T1486

**Goal:**  
Detect mass file modifications, rapid file renames or extension changes, bulk deletions, or EDR ransomware indicators on file servers (file-srv-01 / A-004) and database servers (db-01 / A-007).

**Telemetry Sources:**  
 EDR file event telemetry  
 File change monitoring (FsChange)  
 SIEM file modification logs



### Mass File Modification
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/9.png)

### Extension-change-detection
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/10.png)

## 7) Exfiltration / Command & Control — T1041 / T1071

**Goal:**  
Detect unexpected large outbound data transfers or persistent C2-like beaconing to unusual external destinations.

**Primary Telemetry:**  
 Firewall logs (fw-01 / A-009)  
 NetFlow  
 Proxy logs  
 SIEM correlation (A-014)

**Required Indexes:**  
 `index=network` (flows)  
 `index=fw`



### Large Egress Volume from Critical Hosts
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/11.png)

### Slow-exfil-beaconing
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/12.png)


## 8) Create / Modify System Process — T1543  
*(Service / Scheduled Task Creation)*

**Goal:**  
Detect the creation or modification of Windows services or scheduled tasks on servers (A-004, A-006, A-013), which is a common persistence mechanism.

**Telemetry Sources:**  
 Windows System Event Log (`EventCode=7045` — Service Installed)  
 Sysmon Process Creation (`EventID=1` for `sc.exe`, `schtasks.exe`, and scheduled task creation)



### Service Creation — Windows
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/13.png)

### Scheduled-task-create-detect
![SPL Example Screenshot](https://raw.githubusercontent.com/CEE-E/splunk-ss/main/14.png)


