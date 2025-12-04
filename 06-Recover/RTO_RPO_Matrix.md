# RTO / RPO Matrix — WimeSoft


This baseline matrix sets Recovery Time Objectives (RTO) and Recovery Point Objectives (RPO) for prioritized assets.

| Asset ID | Logical Name | Business Impact | Suggested RTO | Suggested RPO | Backup Frequency | Retention |
|---:|---|---|---:|---:|---|---|
| A-005 | Domain Controller | Authentication services; organization-wide impact | 2 hours | 1 hour (system-state + AD replication) | System-state hourly; full nightly | 30 days |
| A-007 | Database-Server | Application data | 4 hours | 15 minutes (WAL/PITR) | Daily full + continuous WAL archiving | 90 days |
| A-004 | File-Server | Internal documents & shared drives | 8 hours | 4 hours | Nightly incremental | 90 days |
| A-013 | Source-Control-Server | Repositories & CI | 8 hours | 24 hours | Daily repo backups + weekly full | 90 days |
| A-008 | Backup-Server | Backup catalog & archives | 12 hours | N/A | Snapshot hourly (catalog), archive weekly | 180 days (archives) |
| A-014 | Splunk-Server | Detection & logging | 24 hours | 24 hours | Daily config & index metadata snapshots | 90 days for config; indices archived per policy |
| A-006 | Application-Server | Internal application | 4 hours | 1 hour | Nightly config + DB backups as applicable | 90 days |


> **Note:** RPO targets assume appropriate backup technologies are available.
