# CIP: PR.MA-1 — Patch Management & Vulnerability Remediation

**Control ID:** PR.MA-1  
**Framework mapping:** NIST CSF 2.0 (PR.MA-1) - CIS v8 (7.3 / 7.4, IG2)  
**Primary assets:** A-001 - A-008, A-013  
**Owner:** IT Admin / Security Engineer  
**Status:** Planned

## Objective
Implement a predictable, auditable patching process that reduces exposure to known CVEs and meets remediation SLAs.

## Scope
 All Windows and Linux servers, workstations, network appliances capable of receiving updates.

## Technical Implementation
1. Establish WSUS  for Windows patch distribution.  
2. Define Linux patch pipeline: staging - test host - production during maintenance windows.  
3. Maintain vulnerability scanning cadence (authenticated scans) and link CVE findings to patch tickets.

## Configuration Steps
 Configure WSUS and configure clients via GPO.  
 Create patch runbook and smoke tests for critical services.  
 Define patch urgency mapping to SLAs (Critical: 7 days, High: 30 days, Medium: 90 days).

## Validation & Tests
 Monthly patch compliance report.  
 Test reboots and service validation on staging before production push.

## Monitoring & Maintenance
 Weekly report: patch success rate, failed updates, systems missing patches.

## Rollback
 Maintain system snapshots before large patch bundles; rollback via VM snapshot if needed.

## Artifacts & Evidence
 Patch schedules, scan output, remediation ticket IDs, test results.
