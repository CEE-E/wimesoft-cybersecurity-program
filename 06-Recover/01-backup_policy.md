# Backup Policy — WimeSoft


**Purpose:** Ensure reliable backup, integrity, and recoverability for critical systems to meet business continuity and recovery objectives.


**Scope:** All on-prem servers and data stores defined as Critical or High in the asset inventory: Domain Controller, Database Server, File Server, Source-Control Server, Backup Server, Log Collector (Splunk).


## Key Policy Statements
 **Ownership:** Each backupable asset has an assigned backup owner (see asset inventory). Backup owners are responsible for backup configuration, retention, and successful test restores.
 **Frequency & Retention:** Refer to the RTO/RPO Matrix (`Recover/RTO_RPO_Matrix.md`) for per-asset frequency and retention. Minimum retention is 30 days for logs; key business data retained 90 days or as required by regulation.
 **Encryption:** All backups must be encrypted at rest and in transit. Backup encryption keys must be managed under the documented Key Management Procedure.
 **Offsite Copies:** Weekly full backups are rotated offline to an offsite or logically isolated storage location.
 **Integrity & Verification:** Backups include checksum/hash verification and weekly test restores of representative datasets.
 **Change Control:** Any backup configuration changes require a documented change request and approval per the change control process.
 **Access Control:** Backup systems and backup data access are limited to backup owners and designated IT staff. Production restores require multi-party approval when applicable.
 **Audit & Logging:** Backup job execution, success/failure, and verification steps are logged and forwarded to the splunk.


## Exceptions
 Exceptions to frequency, retention, or encryption require documented business justification and security sign-off.


## Review Cadence
 Policy review: Annually
 Operational report review: Monthly (IT Admin & Security Engineer)
