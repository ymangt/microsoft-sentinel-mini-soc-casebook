# Day 1 - Project Scope

## Final Project Name

Microsoft Sentinel Mini SOC Casebook

## Recruiter-Facing Positioning

This project is meant to show fresh, practical security operations ability for entry-level SOC analyst, security analyst, and junior IT security analyst roles.

The project should read like a small analyst portfolio:

- I can write and test KQL.
- I understand how alerts become investigations.
- I can explain suspicious activity without overstating it.
- I can map detections to MITRE ATT&CK.
- I can document triage, false positives, and response recommendations.

## Scope Rules

Do:

- Use safe simulated data.
- Use Azure Activity for at least one real Microsoft Sentinel data source.
- Keep each scenario small enough to explain in an interview.
- Capture screenshots as evidence.
- Prefer clean documentation over a giant detection library.

Avoid:

- Real attacks or terms-of-service gray areas.
- Expensive raw log ingestion.
- More than 4 scenarios before the first public version.
- Overclaiming incident response experience.

## Scenario Priority

1. Password spray against multiple accounts
2. Suspicious PowerShell execution
3. Phishing URL triage
4. Suspicious Azure Activity change

## Day 1 Deliverables

- Repository structure
- README skeleton
- Scenario plan
- Screenshot guide
- Starter detection and investigation files
- Cost and safety notes
- Open questions for portal setup and GitHub rename
