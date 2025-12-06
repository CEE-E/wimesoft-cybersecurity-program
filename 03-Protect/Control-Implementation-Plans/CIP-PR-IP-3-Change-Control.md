# CIP: PR.IP-3 — Change Control & Configuration Management

**Control ID:** PR.IP-3  
**Framework mapping:** NIST CSF 2.0 (PR.IP-3) - CIS v8 (4.7, IG2)  
**Primary assets:** All production infrastructure (All A-IDs)  
**Owner:** IT Admin / Security engineer/ Engineering Lead
**Status:** Planned

## Objective
Establish a formal change control process with approvals, rollback plans, and documentation for production configuration changes.

## Scope
 Infrastructure, network devices, application platform, Splunk rules, playbook changes.

## Technical Implementation
1. Define change request template (description, impact, test plan, rollback plan, owner).  
2. Create CAB (Change Advisory Board) cadence: emergency (ad-hoc) and regular review (weekly).  
3. Tag change tickets to Git commits for config changes (traceability).  
4. Require playbook updates and test evidence before closing change for major infra changes.

## Validation & Tests
 Audit: Quarterly review of change tickets against deployed configuration and last tested date.  
 Ensure every Splunk rule change has test events and false-positive tuning noted.

## Monitoring & Maintenance
 Monthly change summary with number of emergency changes vs planned changes.

## Rollback
 Execute documented rollback steps in ticket; maintain snapshots for critical systems.

## Artifacts & Evidence
 Change request templates, CAB minutes, ticket IDs linked to commits.
