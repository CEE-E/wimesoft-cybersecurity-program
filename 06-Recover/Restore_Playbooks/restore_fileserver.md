# Playbook: File Server Restore (A-004)


**Purpose:** Restore critical file shares, including ACLs and permissions, and validate data integrity.


**Owner:** IT Admin


## Preconditions
 Nightly or selected backup snapshot is available.
 Backup owner and restoration medium are accessible.


## Steps
1. Place file server shares into maintenance/unavailable state to prevent writes during restore.
2. Identify the restore point consistent with RPO requirements.
3. Restore files from backup appliance or archive to temporary restore location.
4. Restore ACLs/NTFS permissions from backup metadata where available; otherwise, reapply known templates.
5. Validate restored files via sampling and checksum comparison.
6. Remount shares to a test host and run application-level access tests.
7. Bring shares online and monitor for missing files or user access issues.


## Post-Restore Verification
 Representative users can access expected files.
 ACLs and group-based permissions behave as intended.


## Rollback
 If users encounter major issues, revert shares to pre-restore snapshot and escalate.
