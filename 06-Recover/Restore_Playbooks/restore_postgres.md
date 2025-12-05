# Playbook: PostgreSQL Restore (A-007)


**Purpose:** Perform point-in-time or full restores of PostgreSQL databases using base backups plus WAL replay to meet RTO/RPO targets.


**Owner:** IT Admin



## Preconditions
 Base backup and WAL archive are available and verified.
 Recovery host prepared with same major PostgreSQL version.
 Application owners notified; plan to take application offline if needed.


## Full Restore (PITR) Steps
1. Notify stakeholders and place application into maintenance mode.
2. Prepare the recovery host with the matching PostgreSQL major release installed.
3. Copy base backup into the PostgreSQL data directory and set proper ownership:
 `chown -R postgres:postgres /var/lib/postgresql/<version>/main`
4. Configure recovery settings (`postgresql.conf`/`recovery.conf` or `standby.signal`) to enable WAL restore, e.g., `restore_command` to fetch WAL files.
5. Start PostgreSQL and monitor WAL replay in logs.
6. Validate data integrity with spot checks and checksum queries against critical tables.
7. Run application smoke tests and monitor performance.
8. Exit maintenance mode and monitor for replication and normal operations.


## Post-Restore Verification
 Critical queries return expected results.
 Application functional tests pass.


## Rollback
 If PITR fails, consider restoring to the previous full backup or failing over to an existing replica if available.
