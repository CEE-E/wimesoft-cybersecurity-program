# CIP: RC.RP-1 — Backup Implementation & Restore Validation

**Control ID:** RC.RP-1  
**Framework mapping:** NIST CSF 2.0 (RC.RP-1) - CIS v8 (12.1, IG2)  
**Primary assets:** A-004 (File-Server), A-007 (DB), A-008 (Backup-Server), A-005 (DC)  
**Owner:** IT Admin / Backup Owner  
**Status:** Implemented (design complete)

## Objective
Implement backup schedules, encryption, retention, and restore validation to meet RTO/RPO objectives.

## Scope
 System-state backups for AD, DB base backups + WAL, file share snapshots, backup server catalog.

## Technical Implementation
1. Configure nightly full + daily incremental backups for file server; PostgreSQL base + WAL archiving for DB.  
2. Encrypt backups at rest and in transit; maintain key management procedures.  
3. Rotate weekly fulls offsite (physically or logically isolated).  
4. Automate checksum verification for backup integrity.

## Validation & Tests
 Weekly: file-level restore sample.  
 Monthly: DB PITR test in staging.  
 Quarterly: full system restore drill per RTO matrix.

## Monitoring & Maintenance
 Daily backup success/failure report to splunk.

## Rollback
 If backup job or restore attempt corrupts data, escalate to backup vendor or use earlier snapshot.

## Artifacts & Evidence
 Backup job configs, sample restore logs, RTO/RPO test results.
