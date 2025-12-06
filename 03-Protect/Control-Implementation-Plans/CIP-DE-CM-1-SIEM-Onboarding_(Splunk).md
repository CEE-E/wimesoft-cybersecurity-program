# CIP: DE.CM-1 — SIEM Onboarding & Centralized Log Collection

**Control ID:** DE.CM-1  
**Framework mapping:** NIST CSF 2.0 (DE.CM-1) - CIS v8 (8.2 / 8.3, IG2)  
**Primary assets:** A-005 (DC), A-014 (SIEM), A-015 (Log-Collector), A-001 - A-013  
**Owner:** Security Engineer  
**Status:** In Progress

## Objective
Establish centralized log collection, normalization, and retention to enable detection, triage, and forensic investigation.

## Scope
 Ingest: AD logs, Sysmone telemetry, firewall, VPN, DB audit logs, backup logs.
 Normalize fields for username, src_ip, dest_ip, process, and event type.

## Technical Implementation
1. Deploy Log Collector (A-015) to normalize and forward logs to SIEM (A-014).  
2. Deploy Splunk universal forwarder on endpoints and servers per asset list.  
3. Configure ingestion pipelines: parsing, timestamp normalization, field extraction, and enrichment (whois, geolocation, asset lookup).  
4. Define retention tiers: hot (0–7d), warm (7–30d), archive (30–90d+) per RTO_RPO_Matrix.

## Configuration Steps
 Create agent deployment package and onboarding script for Windows and Linux.  
 Configure forwarder inputs for syslog, Windows Event Forwarding or Splunk UF.  
 Implement lookup `asset_inventory.csv` for enrichment.  
 Create standard saved searches for top detections (credential abuse, lateral movement, exfil).

## Validation & Tests
 Verify each agent ships logs to Log-Collector and SIEM.  
 Test parse + field extractions for AD logs, Sysmon events, and firewall logs.  
 Acceptance: At least 90% of hosts in asset_inventory report expected telemetry fields.

## Monitoring & Maintenance
 Weekly ingestion health report: forwarder status, missing sources, index growth.  
 Monthly review of parsing errors and field extraction coverage.

## Rollback
 Revert ingestion pipeline changes via config version control; stop new index creation if parsing errors occur.

## Artifacts & Evidence
 Onboarding scripts, sample events, saved search IDs, sample dashboard screenshots
