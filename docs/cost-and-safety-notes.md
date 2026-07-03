# Cost And Safety Notes

## Safety Rules

This lab must not include:

- Real phishing delivery
- Credential spraying against live accounts
- Malware execution
- Unauthorized scanning
- Public exploitation
- Terms-of-service gray areas

All risky events should be simulated with small, controlled sample logs or generated through benign Azure configuration changes.

## Cost Controls

- Use a dedicated resource group so lab resources are easy to find and remove.
- Keep sample data small.
- Use watchlists for MVP simulated data.
- Prefer Azure Activity logs for the real Azure scenario.
- Avoid high-volume raw telemetry unless it is needed and you understand pricing.
- Review Microsoft Cost Management during the lab.
- Delete temporary resources after screenshots are captured.

## Microsoft Cost Notes

Microsoft documents a Microsoft Sentinel free trial for new workspaces and lists Azure Activity logs as a free Sentinel data source. Security alerts from several Microsoft Defender products are also listed as free, while raw logs for some products may be paid.

Reference: https://learn.microsoft.com/azure/sentinel/billing
