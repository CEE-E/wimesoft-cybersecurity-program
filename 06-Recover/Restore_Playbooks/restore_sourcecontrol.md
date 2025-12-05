# Playbook: Source Control Restore (Gitea/GitLab) (A-013)


**Purpose:** Restore repository data and CI configuration to return development services to operation.


**Owner:** Engineering Lead or IT Admin


## Preconditions
 Repository backups and any platform database backups are available.
 CI artifacts backup (if required) is accessible.


## Steps
1. Isolate the source control platform to prevent writes during restore.
2. Restore repository bare archives to the git data directory or use platform-native restore commands.
3. Restore backing database if the platform uses one (follow DB playbook if necessary).
4. Run `git fsck` on restored repositories to verify integrity.
5. Test cloning, pushing, and pulling for a sample repo.
6. Restore or reconfigure CI runners and verify pipeline execution on a sample job.
7. Bring the platform back online and monitor developer activity.


## Post-Restore Verification
 Repositories clone and push/pull successfully.
 CI runner executes a sample job successfully.


## Rollback
 If repository consistency issues occur, restore from an earlier backup and escalate.
