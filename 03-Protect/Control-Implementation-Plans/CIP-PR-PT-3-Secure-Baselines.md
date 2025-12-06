# CIP: PR.PT-3 / PR.IP-1 — Secure Configuration Baselines & Drift Detection

**Control ID:** PR.PT-3 / PR.IP-1  
**Framework mapping:** NIST CSF 2.0 (PR.PT-3, PR.IP-1) - CIS v8 (4.6 / 4.7, IG2)  
**Primary assets:** A-001 - A-008, A-010 - A-012  
**Owner:** IT Admin / Security Engineer  
**Status:** In Progress

## Objective
Create and enforce hardened baselines for servers and endpoints; detect and remediate configuration drift.

## Scope
Windows Server/Client baselines, Ubuntu server baselines, network device configs.

## Technical Implementation
1. Produce hardened images and GPO templates for Windows; Ansible/Immutable images for Linux.  
2. Implement drift detection using config management (Ansible, SCCM, or scripts) and weekly compliance reports.  
3. Maintain versioned baseline artifacts in Git.

## Configuration Steps
 Create baseline config repository.  
 Apply baseline to staging hosts, validate, then roll to production.  
 Configure automated drift checks (cron + playbook) and alert on deviation.

## Validation & Tests
 Weekly compliance check showing drift percentage; sample remediation steps executed.

## Monitoring & Maintenance
 Baseline update for OS or application changes; review after every major patch cycle.

## Rollback
 If baseline causes regressions, revert to previous baseline and open a change ticket.

## Artifacts & Evidence
 Baseline repo, compliance reports, remediation ticket IDs.
