# DET-004: Suspicious Azure Resource Change

## Scenario Name

Suspicious Azure resource change: broad inbound RDP rule created in a network security group.

## Analyst Objective

Detect and investigate an Azure control-plane change that could expose remote administration access. The goal is to show that an analyst can identify a risky cloud configuration change, parse the important fields from `AzureActivity`, investigate the related event timeline, consider false positives, and recommend containment.

## Data Source

- Microsoft Sentinel table: `AzureActivity`
- Connector: Azure Activity
- Resource involved: `nsg-sentinel-lab-test`
- Rule involved: `Allow-RDP-Lab-Test`

## Safe Lab Action

For this lab, I created an unattached Azure network security group and added an inbound allow rule for RDP:

- Direction: inbound
- Action: allow
- Protocol: TCP
- Source: any source
- Destination port: `3389`
- Priority: `300`

This generated real Azure Activity telemetry without attaching the NSG to a VM, subnet, or network interface. In other words, the lab created a realistic control-plane event without exposing an actual host to the Internet.

## Detection Summary

The detection query looks for high-risk Azure operations such as NSG rule writes, NSG writes, role assignment writes, VM writes, and storage account writes. For NSG security rule events, the query parses the JSON inside `Properties` so it can extract the security rule details:

- `RuleName`
- `RuleAccess`
- `RuleDirection`
- `RuleProtocol`
- `SourceAddressPrefix`
- `DestinationPortRange`

The query raises the severity to `High` when it finds a rule that allows inbound RDP from a broad source such as `*`, `Internet`, or `0.0.0.0/0`.

In plain English: the query is asking, "Did someone create or change an Azure network rule that allows RDP from anywhere?"

## Investigation Summary

The investigation query uses the alert `CorrelationId` to pull the related Azure Activity events for the same operation. In this lab, the timeline showed the security rule write moving through `Start`, `Accept`, and `Success` activity states.

That matters because the detection row alone says "this looks risky," while the investigation query confirms the related event chain and shows whether Azure accepted and completed the change.

The scheduled analytics rule also generated a high-severity Microsoft Sentinel alert and created an incident in the Microsoft Defender portal. The incident was moved to `In progress` while the alert, entities, custom details, and related Azure Activity event were investigated.

## Expected Output Fields

- `TimeGenerated`
- `Severity`
- `AlertReason`
- `OperationNameValue`
- `ActivityStatus`
- `ActivitySubstatusValue`
- `Caller`
- `CallerIpAddress`
- `ResourceGroup`
- `ResourceProviderValue`
- `RuleName`
- `RuleAccess`
- `RuleDirection`
- `RuleProtocol`
- `SourceAddressPrefix`
- `DestinationPortRange`
- `ResourceId`
- `SubscriptionId`
- `CorrelationId`

## MITRE ATT&CK Mapping

| Tactic | Technique | Reason |
| --- | --- | --- |
| Defense Impairment | [T1578 - Modify Cloud Compute Infrastructure](https://attack.mitre.org/techniques/T1578/) | The event is a cloud control-plane modification that could weaken infrastructure security posture. MITRE describes this technique as adversaries modifying cloud infrastructure components to evade defenses or bypass restrictions. |
| Defense Impairment | [T1578.005 - Modify Cloud Compute Configurations](https://attack.mitre.org/techniques/T1578/005/) | This is a best-fit mapping for a risky cloud configuration change. The lab event changed a network access control setting associated with Azure infrastructure. |

## False Positive Considerations

This alert can be legitimate if:

- The change was made during an approved maintenance window.
- The rule was created temporarily for testing and removed afterward.
- The source was broad only because the resource is not attached to any VM, subnet, or network interface.
- The change came from approved infrastructure-as-code automation.
- A break-glass or emergency support process required temporary RDP access.

The rule should be treated as more suspicious if:

- The NSG is attached to a production subnet, VM NIC, or Internet-facing workload.
- The caller is unusual for this resource group.
- The caller IP is unexpected for the user or organization.
- The change happens near role assignments, VM changes, public IP creation, or failed sign-in activity.

## Severity Logic

- `High`: inbound allow rule for RDP from a broad source, or privileged role assignment write.
- `Medium`: other NSG security rule writes that require review.
- `Low`: other monitored Azure control-plane changes that may still be useful context.

## Triage Steps

1. Open the detection result and record the `CorrelationId`.
2. Run the investigation query with that `CorrelationId`.
3. Confirm the rule details: direction, action, protocol, source, and destination port.
4. Check whether the NSG is attached to a subnet or network interface.
5. Validate whether the caller and caller IP are expected.
6. Review nearby Azure Activity events for role assignment changes, VM changes, public IP creation, or additional networking changes.
7. Decide whether the alert is an approved change, a lab/test event, a misconfiguration, or suspicious activity.
8. Document the decision and recommended response.

## Containment And Response Recommendation

If this happened in a real environment and was not approved:

- Remove the broad inbound RDP rule or change the source to an approved management IP range.
- Prefer just-in-time VM access, VPN/private connectivity, or Azure Bastion instead of Internet-exposed RDP.
- Confirm whether the NSG is attached to any production resources.
- Review the caller account for unusual sign-in activity and recent privilege changes.
- Revoke sessions, reset credentials, and require MFA re-authentication if the account appears compromised.
- Create an incident ticket with the correlation ID, resource ID, rule details, and timeline.

## Screenshots

| Screenshot | Purpose |
| --- | --- |
| `../screenshots/redacted/day-03-01-nsg-review-create.png` | Shows the NSG creation review screen before deployment. |
| `../screenshots/redacted/day-03-02-nsg-deployment-complete.png` | Shows the NSG deployment succeeded. |
| `../screenshots/redacted/day-03-03-add-rdp-rule-form.png` | Shows the inbound RDP rule configuration before adding it. |
| `../screenshots/redacted/day-03-04-rdp-rule-warning.png` | Shows Azure warning that RDP port `3389` is exposed to the Internet. |
| `../screenshots/redacted/day-03-05-det004-detection-results-01.png` | Shows the detection query firing on the broad inbound RDP rule. |
| `../screenshots/redacted/day-03-05-det004-detection-results-02.png` | Shows the horizontally scrolled detection output with the correlation ID. |
| `../screenshots/redacted/day-03-06-det004-investigation-results-01.png` | Shows the investigation query returning the related event timeline. |
| `../screenshots/redacted/day-03-06-det004-investigation-results-02.png` | Shows the horizontally scrolled investigation output for the same timeline. |
| `../screenshots/redacted/day-03-07-det004-analytics-rule-review.png` | Shows the validated scheduled analytics rule configuration before saving. |
| `../screenshots/redacted/day-03-08-det004-enabled-rule.png` | Confirms the scheduled rule is enabled in Sentinel Analytics. |
| `../screenshots/redacted/day-03-09-det004-unattached-subnets.png` | Confirms the NSG has no associated subnet before live validation. |
| `../screenshots/redacted/day-03-10-det004-unattached-network-interfaces.png` | Confirms the NSG has no associated network interface before live validation. |
| `../screenshots/redacted/day-03-11-det004-fresh-rule-write.png` | Shows the authorized description-only rule update that generated fresh telemetry. |
| `../screenshots/redacted/day-03-12-det004-fresh-event-query.png` | Shows the fresh `Start` and `Accept` Azure Activity events returned by KQL. |
| `../screenshots/redacted/day-03-14-det004-incident-attack-story.png` | Shows the generated high-severity incident and its entity graph in Microsoft Defender. |
| `../screenshots/redacted/day-03-15-det004-alert-details.png` | Shows the alert details, related event, activity time, detection source, and workspace. |
| `../screenshots/redacted/day-03-16-det004-incident-details.png` | Shows the incident in progress with custom evidence fields and impacted asset context. |

## Lessons Learned

- Azure Activity events may use status values such as `Accept`, not only `Success`, so detection logic should account for both.
- Useful NSG rule details are nested inside the `Properties` JSON field, so parsing is required to extract the rule name, direction, access, source, protocol, and port.
- A single portal action can create multiple related Azure Activity rows. The `CorrelationId` is important for connecting them.
- Portal result tables often require horizontal scrolling, so paired screenshots can be clearer than one overly cropped screenshot.
- A scheduled rule can successfully generate an alert and incident even when the preview-only Rule Runs panel has no records. Rule execution health telemetry is a separate monitoring feature.

## Limitations

- This lab used an unattached NSG, so no real VM exposure occurred.
- The Rule Runs preview did not display execution records because analytics-rule health monitoring was not available for the workspace during this test. The generated alert and incident independently confirm that the rule executed.
- Caller identity and public IP values are redacted in public screenshots.
- The query is intentionally beginner-to-intermediate and should be tuned before use in a production SOC.
