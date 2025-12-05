# Playbook: Domain Controller Restore (A-005)


**Purpose:** Restore Active Directory domain services to recover authentication, policy, and directory functionality.


**Owner:** IT Admin


## Preconditions
 Verified system-state backup or VM snapshot exists (timestamp + checksum).
 Backup vault access and decryption keys available.
 Communications with stakeholders and planned downtime approvals obtained.


## Short-Term Restore Steps (Authoritative/system-state restore)
1. Notify stakeholders using communication template.
2. If necessary, isolate the DC from the network to prevent replication of an undesired state.
3. Boot to Windows Recovery Environment:
 Select **Repair your computer** and open a command prompt.
4. Restore System State (example using `wbadmin`):
 `wbadmin start systemstaterecovery -version:<VersionIdentifier> -authsysvol`
 If restoring to a new host, ensure OS build and patch level match the original where practical.
5. If required, perform an authoritative restore for directory objects using `ntdsutil`.
6. Bring the DC online and verify replication:
 `dcdiag /v`
 `repadmin /replsummary`
7. Verify DNS, authentication, and Group Policy (`gpupdate /force`).
8. Record restore actions, timestamps, and time-to-restore.


## Post-Restore Verification
 Multiple test users can authenticate.
 Group Policy objects apply correctly to test endpoints.
 AD replication reports no errors.
 
## Rollback/Contingency
If restore fails, revert to pre-restore snapshot or failover to an alternate DC if available. Escalate to vendor  if needed.


## Notes
 Document the restore attempt in the Recovery Test Log and update the playbook where gaps are discovered.
