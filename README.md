# Microsoft Sentinel Mini SOC Casebook

Documented Microsoft Sentinel detection and investigation workflows using KQL, safe simulated telemetry, Azure Activity logs, watchlists, and incident triage case notes.

## Analyst Workflow

Each scenario follows a repeatable detection and response workflow:

1. Detect suspicious behavior with KQL.
2. Investigate supporting evidence.
3. Map activity to MITRE ATT&CK.
4. Consider false positives and severity.
5. Recommend containment and response.
6. Document findings clearly for incident handoff.

## Tools

- Microsoft Sentinel in the Microsoft Defender portal
- Log Analytics / Kusto Query Language (KQL)
- Azure Activity data connector
- Microsoft Sentinel watchlists
- GitHub for version control and technical documentation

## Lab Architecture

```text
Safe sample data CSVs
        |
        v
Microsoft Sentinel watchlists  --->  KQL detections and investigations
        |
        v
Scheduled analytics rules  --->  Alerts/incidents  --->  Case notes

Azure Activity connector  --->  AzureActivity table  --->  Cloud activity scenario
```

## Detection Scenarios

| ID | Scenario | Analyst Objective | Primary Data Source | Status |
| --- | --- | --- | --- | --- |
| DET-001 | Password spray against multiple accounts | Identify repeated authentication failures from one source IP across multiple accounts | `lab_identity_signins` watchlist or custom table | Planned |
| DET-002 | Suspicious PowerShell execution | Detect encoded/download-style PowerShell behavior and investigate process context | `lab_endpoint_processes` watchlist or custom table | Planned |
| DET-003 | Phishing URL triage | Match email URLs against a suspicious-domain watchlist and document impact | `lab_email_url_events` + `lab_suspicious_domains` watchlists | Planned |
| [DET-004](docs/det-004-azure-suspicious-resource-change.md) | Suspicious Azure resource change | Investigate risky Azure Activity operations such as NSG rule writes or role assignment changes | `AzureActivity` | Detection and investigation evidence captured |

## Repository Structure

```text
detections/       Scheduled-rule KQL, one file per detection
investigations/   Follow-up KQL used after an alert fires
sample-data/      Safe simulated logs used for lab scenarios
watchlists/       CSVs intended for Sentinel watchlist upload
screenshots/      Portal screenshots used in the README and case notes
docs/             Build plan, screenshot guide, cost notes, and case writeups
playbooks/        Manual response playbooks and containment checklists
```

## Evidence To Capture

Each scenario should include:

- Detection query screenshot
- Investigation query screenshot
- Analytics rule configuration screenshot
- Incident or alert screenshot, if generated
- Short case note in `docs/`
- MITRE ATT&CK mapping
- False-positive considerations
- Response recommendation

## Cost And Safety

This lab uses safe simulated telemetry and benign Azure configuration changes. No real malware, credential attacks, phishing delivery, or unauthorized scanning are used.

Cost controls:

- Prefer Microsoft Sentinel free trial usage where available.
- Keep sample data tiny.
- Use Azure Activity because it is listed by Microsoft as a free Microsoft Sentinel data source.
- Avoid high-volume raw Entra, Defender, firewall, and endpoint ingestion unless deliberately enabled and monitored.
- Delete temporary Azure resources after screenshots are captured.

References:

- [Onboard Microsoft Sentinel](https://learn.microsoft.com/azure/sentinel/quickstart-onboard)
- [Create scheduled analytics rules](https://learn.microsoft.com/azure/sentinel/create-analytics-rules)
- [Microsoft Sentinel billing](https://learn.microsoft.com/azure/sentinel/billing)
- [Microsoft Sentinel watchlist queries](https://learn.microsoft.com/azure/sentinel/watchlists-queries)
- [Microsoft Sentinel in the Defender portal](https://learn.microsoft.com/azure/sentinel/microsoft-sentinel-defender-portal)
