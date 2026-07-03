# Implementation Plan

## Day 1 - Repo And Scope

Deliverables:

- Confirm project name and scope.
- Create repo structure.
- Add README, scenario plan, screenshot guide, and starter KQL.
- Confirm GitHub remote and rename plan.

## Day 2 - Sentinel Workspace Setup

Deliverables:

- Use the existing enabled `Azure for Students` subscription.
- Use existing resource group `rg-sc200-sentinel-lab`.
- Use existing Log Analytics workspace `law-sc200-sentinel-lab`.
- Confirm Microsoft Sentinel is enabled.
- Open Sentinel from the Microsoft Defender portal.
- Confirm or install the Azure Activity solution from Content hub.
- Confirm or connect the Azure Activity data connector.
- Generate one harmless Azure Activity event.
- Validate ingestion with KQL.

Screenshots:

- Sentinel workspace in Defender portal
- Azure Activity connector status
- First `AzureActivity` query result

## Day 3 - Azure Activity Scenario

Deliverables:

- Generate one safe Azure Activity event, such as creating and deleting a temporary NSG rule or resource group.
- Run the Azure Activity detection query.
- Write a short case note.

Screenshots:

- Query result
- Resource activity evidence
- Analytics rule setup, if created

## Day 4 - Watchlists And Sample Data

Deliverables:

- Upload small CSVs as Microsoft Sentinel watchlists.
- Verify `_GetWatchlist()` queries work.
- Capture watchlist screenshots.

Watchlists:

- `lab_identity_signins`
- `lab_endpoint_processes`
- `lab_email_url_events`
- `lab_suspicious_domains`

## Day 5 - Password Spray Detection

Deliverables:

- Run detection KQL.
- Run investigation KQL.
- Create or draft analytics rule settings.
- Complete case note.

## Day 6 - Suspicious PowerShell Detection

Deliverables:

- Run detection KQL.
- Run investigation KQL.
- Document suspicious command logic.
- Complete case note.

## Day 7 - Phishing URL Triage

Deliverables:

- Run URL watchlist match detection.
- Investigate affected user, sender, domain, and URL.
- Complete case note and response checklist.

## Day 8 - Analytics Rules And Incidents

Deliverables:

- Create scheduled analytics rules for the strongest scenarios.
- Configure severity, MITRE mapping, entity mapping, and custom details.
- Capture alert or incident screenshots.

## Day 9 - Repo Polish

Deliverables:

- Finalize README.
- Add screenshot captions.
- Review all KQL filenames and comments.
- Confirm each case note has analyst objective, evidence, conclusion, limitations, and response.

## Day 10 - Interview Packaging

Deliverables:

- Add resume bullets.
- Add interview talking points.
- Do a final recruiter-readability pass.
