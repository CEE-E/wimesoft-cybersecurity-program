# WimeSoft — README

This repository is a practical, hands-on security program based on a *fictional organization* that demonstrates how NIST Cybersecurity Framework version 2.0 and CIS Controls version 8 (Implementation Group 2) can be applied in a small, on-premises environment. It is intentionally focused on strategic planning, evidence of applied learning, and a place to show initiative. It is not a running production environment and is by no means a perfect rendition.

It is a demonstrable, version-controlled design that maps business risk to controls, detection, and recovery. It is useful to assess technical depth (detection engineering, control implementation), systems thinking (traceability, dependencies), and operational practicality (playbooks, validation).


## Key skills and outcomes demonstrated

- Framework mapping: NIST CSF v2.0, CIS Controls v8 (IG2)  
- Threat alignment: MITRE ATT&CK mapping for detections and playbooks  
- Detection engineering: Splunk searches, lookups, and tuning guidance  
- Practical controls: MFA, patching, secure baselines, backup & restore testing  
- Incident handling: playbooks that preserve evidence and restore operations  
- Risk management: prioritized risk register and traceability to controls  
- Documentation & maintainability: versioned artifacts, validation steps, and owner assignment


## A short, honest note on limitations

This repository is a design and planning project, created with the tools and constraints. Because it is not, by itself, a live production system, there are governance and operational gaps:

- There is no full SOC or dedicated 24x7 monitoring team included here. That is an operational next step.  
- Some automation and integration are described but not deployed (for example orchestration playbooks, automated patch deployment, or vendor-managed appliances).  
- Vendor contracts, SLAs and full procurement records are not included beyond example templates.  
- Some detection and tuning guidance uses representative examples rather than data-driven thresholds from a production environment.

The artifacts show how to convert policy into implementable controls and testable outcomes.

Applying these designs in a real environment will add operational telemetry and enable further refinement.


## Navigating this repo

- [01- Business-Overview](01-%20Business-Overview/) — context, goals, and program scope.  
- [02- Identify](02-Identify/) — asset_inventory.csv, data classification, risk register, threat modelling/mapping.  
- [03- Protect](03-Protect/) — Control Implementation Plans (CIPs) for MFA, patching, secure baselines, backups.  
- [04- Detect](04-Detect/) — Splunk detection rules, lookups, detection engineering notes.  
- [05- Respond](05-Respond/) — incident response playbooks, triage runbooks, evidence-handling steps.  
- [06- Recover](06-Recover/) — backup policy, RTO/RPO matrix, restore playbooks and validation logs.



