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
| `redacted/day-03-08-det004-enabled-rule.png` | Confirms DET-004 is live in Sentinel Analytics as an enabled high-severity scheduled rule. |
| `redacted/day-03-09-det004-unattached-subnets.png` | Confirms the lab NSG is not associated with any subnet before the live rule test. |
| `redacted/day-03-10-det004-unattached-network-interfaces.png` | Confirms the lab NSG is not associated with any network interface before the live rule test. |
| `redacted/day-03-11-det004-fresh-rule-write.png` | Shows the authorized description-only NSG rule update used to generate fresh validation telemetry. |
| `redacted/day-03-12-det004-fresh-event-query.png` | Shows the fresh NSG rule write in Sentinel with matching `Start` and `Accept` events. |
| `redacted/day-03-14-det004-incident-attack-story.png` | Shows the high-severity incident and its linked account and network entities in the Defender incident graph. |
| `redacted/day-03-15-det004-alert-details.png` | Shows the scheduled detection alert, related event, severity, activity time, and workspace details. |
| `redacted/day-03-16-det004-incident-details.png` | Shows the incident in progress with the rule name, source prefix, destination port, and impacted asset context. |
| `redacted/day-03-17-det004-correlation-locator.png` | Shows the analyst locating the shared correlation ID across the `Start`, `Accept`, and `Success` records. |
| `redacted/day-03-18-det004-correlated-timeline.png` | Shows the investigation query reconstructing the completed NSG rule-write timeline while sensitive identity and IP fields remain redacted. |

Do not commit screenshots that expose:

- Subscription IDs
- Tenant IDs
- Personal email addresses
- Public IP addresses
- Billing details
- Secrets or tokens
