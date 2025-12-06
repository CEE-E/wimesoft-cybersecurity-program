# CIP: PR.AC-3 — Multi-Factor Authentication for Privileged & Remote Access

**Control ID:** PR.AC-3  
**Framework mapping:** NIST CSF 2.0 (PR.AC-3) to CIS v8 (6.3, IG2)  
**Primary assets:** A-005 (Domain-Controller), A-017 (VPN-Appliance), A-001 (Management-Laptops)  
**Owner:** Security Engineer or IT Admin  
**Status:** Planned

## Objective
Enforce MFA for all privileged accounts and remote access paths to reduce the risk of credential compromise and lateral movement.

## Scope
 Privileged OUs (Domain Admins).  
 Remote entry points (VPN A-017, admin portals).  
 Administrative console and RDP/SSH access to servers.

## Technical Implementation
1. Select MFA mechanism (TOTP via authenticator app and hardware tokens for highest privilege).  
2. Deploy RADIUS/TOTP gateway or integrate with available SSO. Configure AD to require MFA for privileged OUs.  
3. Configure VPN (A-017) to use RADIUS authentication and require MFA for `admins` and `remote` groups.  
4. Enforce conditional access rules where possible (deny or require MFA for non-`admin_known_ips`).  
5. Document and enforce break-glass account process (short-term token, strict logging, rotation).

## Configuration Steps (example)
 Deploy RADIUS/TOTP .  
 Configure AD conditional access or GPO for privileged accounts.  
 Update VPN auth to RADIUS and test with pilot group.  
 Revoke persistent local admin rights; require use of jump host for administrative tasks.

## Validation & Tests
 Test cases:
   Valid credentials + valid MFA = PASS.
   Valid credentials + missing/invalid MFA = FAIL.
   Privileged login from IP not in `asset_inventory.csv` = MFA enforced.
Acceptance criteria: All accounts in privileged OU require MFA; no bypasses present.

## Monitoring & Detection
 Splunk rule: `PR_AC_Privileged_Login_Anomalous_Geo` (alert on privileged login from unknown admin IP).
 Dashboard: Privileged auth events and MFA failure rate.
 Evidence to collect: sample login events with MFA claims, change ticket IDs.

## Rollback / Contingency
 Revert VPN auth to prior config if rollout causes widespread outages.

## Artifacts & Evidence
 Screenshots of VPN/RADIUS config, Splunk saved search, test logs, change request ID.
