# Watchlists

CSV files in this folder are intended to be uploaded to Microsoft Sentinel as watchlists.

Recommended aliases:

| File | Watchlist Alias | Search Key |
| --- | --- | --- |
| `identity-signins.csv` | `lab_identity_signins` | `IPAddress` |
| `endpoint-processes.csv` | `lab_endpoint_processes` | `DeviceName` |
| `email-url-events.csv` | `lab_email_url_events` | `UrlDomain` |
| `suspicious-domains.csv` | `lab_suspicious_domains` | `Domain` |

Microsoft reference: https://learn.microsoft.com/azure/sentinel/watchlists-queries
