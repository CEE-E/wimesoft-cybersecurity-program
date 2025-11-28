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

