# Sample Data

This folder stores safe simulated telemetry used for lab development and documentation.

The initial MVP uses CSV files uploaded as Microsoft Sentinel watchlists. This avoids real attacks and keeps the dataset tiny.

The current sample data lives in `../watchlists` because the MVP upload path is Microsoft Sentinel watchlists:

- `../watchlists/identity-signins.csv`
- `../watchlists/endpoint-processes.csv`
- `../watchlists/email-url-events.csv`
- `../watchlists/suspicious-domains.csv`

Do not include real personal data, real credentials, real tenant IDs, or private IP addresses from a production network.
