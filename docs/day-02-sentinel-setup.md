# Day 2 - Sentinel Workspace Setup And Verification

Goal: confirm the existing Microsoft Sentinel workspace is usable, connect Azure Activity logs if needed, run the first KQL query, and capture evidence screenshots.

## What Codex Already Verified

Using Azure MCP, Codex confirmed:

- The enabled subscription is `Azure for Students`.
- The existing workspace is `law-sc200-sentinel-lab`.
- The resource group is `rg-sc200-sentinel-lab`.
- The region is Canada Central.
- The workspace provisioning state is `Succeeded`.
- The `SecurityInsights(law-sc200-sentinel-lab)` solution exists, which indicates Microsoft Sentinel is enabled.
- No Azure Activity rows were returned in the current workspace during the initial check.

## What You Need To Do In The Portal

Use the portal for learning and screenshots. Codex can query and document, but recruiter-facing evidence should show that you worked through the Sentinel interface.

### Step 1 - Open Microsoft Defender Portal

1. Go to https://security.microsoft.com
2. In the left navigation, find **Microsoft Sentinel**.
3. Go to **Microsoft Sentinel** > **Settings** or **Workspaces**.
4. Select workspace `law-sc200-sentinel-lab`.

Screenshot to capture:

```text
screenshots/day-02-01-defender-sentinel-workspace.png
```

What this proves:

- You can access Sentinel from the modern Defender portal.
- You know which workspace the lab uses.

### Step 2 - Confirm Workspace Details

Find the workspace details page and confirm:

- Subscription: `Azure for Students`
- Resource group: `rg-sc200-sentinel-lab`
- Workspace: `law-sc200-sentinel-lab`
- Region: Canada Central

Screenshot to capture:

```text
screenshots/day-02-02-workspace-details.png
```

What this proves:

- Your lab has a real Sentinel-backed Log Analytics workspace.
- You can identify subscription, resource group, workspace, and region.

### Step 3 - Check Content Hub For Azure Activity

1. In Microsoft Sentinel, open **Content management** > **Content hub**.
2. Search for `Azure Activity`.
3. If it is not installed, install it.
4. If it is installed, open it and note the installed status.

Screenshot to capture:

```text
screenshots/day-02-03-content-hub-azure-activity.png
```

What this proves:

- You know Sentinel content is packaged through solutions.
- You can identify the solution that provides Azure Activity connector content.

### Step 4 - Check Azure Activity Data Connector

1. Go to **Microsoft Sentinel** > **Configuration** > **Data connectors**.
2. Search for `Azure Activity`.
3. Open the connector page.
4. Check whether the status says connected.

Screenshot to capture:

```text
screenshots/day-02-04-azure-activity-connector-status.png
```

What this proves:

- You checked the actual ingestion connector rather than assuming the workspace had data.

### Step 5 - Connect Azure Activity If Needed

If the connector is not connected:

1. On the Azure Activity connector page, follow the setup instructions.
2. Launch the Azure Policy Assignment Wizard if prompted.
3. Scope it to the enabled student subscription.
4. Set the primary Log Analytics workspace to `law-sc200-sentinel-lab`.
5. Review and create.

Screenshot to capture:

```text
screenshots/day-02-05-azure-activity-policy-assignment.png
```

What this proves:

- You understand that Sentinel ingestion is connector-based.
- You can connect Azure control-plane activity to the workspace.

### Step 6 - Generate A Harmless Azure Activity Event

Generate a safe control-plane event. Recommended options:

- Add a temporary tag to the resource group.
- Create and delete a harmless empty resource group.
- Open the existing empty East US resource group and make a minor reversible metadata change.

Do not create paid compute, storage, or network resources for this step.

Recommended event:

1. Go to `rg-sc200-sentinel-lab-eastus`.
2. Add a tag:
   - Key: `lab`
   - Value: `sentinel-day-02`
3. Save.

Screenshot to capture:

```text
screenshots/day-02-06-harmless-activity-generated.png
```

What this proves:

- You generated a legitimate Azure control-plane event without risky activity.

### Step 7 - Query AzureActivity

In Sentinel logs or Advanced hunting, run:

```kusto
AzureActivity
| where TimeGenerated >= ago(24h)
| project TimeGenerated, OperationNameValue, ActivityStatusValue, Caller, CallerIpAddress, ResourceGroup, ResourceId, CorrelationId
| order by TimeGenerated desc
| take 20
```

Screenshot to capture:

```text
screenshots/day-02-07-azureactivity-query-results.png
```

What this proves:

- You can run KQL against a Sentinel workspace.
- You can find recent Azure control-plane activity.

### Step 8 - If No Data Appears

Azure Activity ingestion can take time. If the query returns no rows:

1. Wait 10-30 minutes.
2. Rerun the query.
3. Confirm connector status again.
4. Capture a screenshot showing the no-data result and document it as an ingestion troubleshooting note.

Troubleshooting query:

```kusto
search in (AzureActivity) *
| take 10
```

If still empty, use this note in the README:

> Azure Activity ingestion was configured but had not produced rows at the time of initial validation. The lab documents the connector status and reruns validation after ingestion delay.

## Day 2 Completion Criteria

Day 2 is complete when you have:

- Confirmed the Sentinel workspace in the Defender portal.
- Confirmed or installed Azure Activity from Content hub.
- Confirmed or connected the Azure Activity connector.
- Generated one harmless Azure control-plane event.
- Run one `AzureActivity` KQL query.
- Captured at least 4 screenshots.

## What To Tell An Interviewer

> I started by verifying the Sentinel workspace and data connector instead of jumping straight into detections. I wanted the lab to show the basic SOC engineering workflow: confirm the workspace, confirm ingestion, generate a safe test event, validate data with KQL, and only then build detections.
