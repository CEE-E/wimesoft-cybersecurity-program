# Risk Register — WimeSoft

This folder contains the  risk register for the WimeSoft security program.

## Files
 `risk_register.csv` — Master risk register .  


## How to use the risk register
Columns in `risk_register.csv`:
 **RiskID:** Unique identifier for the risk.  
 **Title / Description:** Concise title and longer description of the risk.  
 **AssetIDs:** Asset IDs impacted (refer to `02-Identify/Assets/asset_inventory.csv`).  
 **Likelihood / Impact / RiskScore:** Qualitative assessment (Low/Medium/High) or numeric scoring as preferred.  
 **ExistingControls:** Controls currently in place.  
 **RelevantCIP:** Filename of the Control Implementation Plan that addresses the risk.  
 **MitigationActions:** Planned remediation or treatment actions.  
 **Owner:** Person accountable for mitigation.  
 **TargetDate:** Target completion / mitigation date.  
 **ResidualRisk / Status / LastReviewed / Notes:** Governance fields for tracking.

## Governance
 **Review cadence:** The register should be reviewed monthly by the Security Lead and IT Admin, and formally every quarter with executive sponsor.  
 **Risk treatment:** For each high or critical risk, create or update a corresponding CIP and schedule mitigation tasks with owners.  


## Editing
Edit `risk_register.csv` directly in GitHub or via local clone. Keep entries concise and include links to CIP files where relevant.
