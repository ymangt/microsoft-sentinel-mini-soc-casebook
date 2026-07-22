# Screenshots

Store final project screenshots here.

## Folder Workflow

- `raw/`: local-only pasted screenshots from the portal. These are ignored by Git because they may contain personal email addresses, public IP addresses, tenant IDs, subscription IDs, or browser tabs.
- `redacted/`: publishable screenshots that have been cropped or redacted and are safe to reference from the public README.

Use the naming convention documented in `../docs/screenshot-guide.md`.

## Current Evidence Set

| File | Purpose |
| --- | --- |
| `redacted/day-02-07-azureactivity-query-results.png` | Confirms Azure Activity logs are reaching the Sentinel workspace. |
| `redacted/day-03-01-nsg-review-create.png` | Shows the lab NSG creation review screen before deployment. |
| `redacted/day-03-02-nsg-deployment-complete.png` | Shows successful deployment of the lab NSG. |
| `redacted/day-03-03-add-rdp-rule-form.png` | Shows the intentionally risky inbound RDP rule before adding it. |
| `redacted/day-03-04-rdp-rule-warning.png` | Shows the Azure portal warning for exposing RDP to the Internet. |
| `redacted/day-03-05-det004-detection-results-01.png` | Shows DET-004 firing on the broad inbound RDP rule with the main result columns visible. |
| `redacted/day-03-05-det004-detection-results-02.png` | Shows the horizontally scrolled DET-004 result columns, including the correlation ID. |
| `redacted/day-03-06-det004-investigation-results-01.png` | Shows the investigation query returning the timeline for the same correlation ID. |
| `redacted/day-03-06-det004-investigation-results-02.png` | Shows the horizontally scrolled investigation result columns for the same event timeline. |
| `redacted/day-03-07-det004-analytics-rule-review.png` | Shows DET-004 configured as an enabled scheduled analytics rule, including its frequency, entity mapping, alert details, and custom evidence fields. |

Do not commit screenshots that expose:

- Subscription IDs
- Tenant IDs
- Personal email addresses
- Public IP addresses
- Billing details
- Secrets or tokens
