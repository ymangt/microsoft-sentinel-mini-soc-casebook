# Azure Inventory

Inventory captured with Azure MCP on 2026-07-03.

## Subscriptions

| Subscription | Status | Notes |
| --- | --- | --- |
| `Azure for Students` | Enabled | Use this subscription for the lab. |
| `Azure subscription 1` | Disabled | Ignore for this project unless it is re-enabled later. |

## Resource Groups

| Subscription | Resource Group | Region | Status |
| --- | --- | --- | --- |
| Azure for Students | `rg-sc200-sentinel-lab` | Canada Central | Existing lab resources live here. |
| Azure for Students | `rg-sc200-sentinel-lab-eastus` | East US | Empty fallback resource group. |
| Azure subscription 1 | `rg-sc200-sentinel-lab-payg` | East US | Belongs to disabled subscription. |

## Existing Sentinel-Related Resources

| Name | Type | Resource Group | Region | Notes |
| --- | --- | --- | --- | --- |
| `law-sc200-sentinel-lab` | Log Analytics workspace | `rg-sc200-sentinel-lab` | Canada Central | Existing workspace; provisioning succeeded. |
| `SecurityInsights(law-sc200-sentinel-lab)` | Operations Management solution | `rg-sc200-sentinel-lab` | Canada Central | Indicates Microsoft Sentinel is enabled on the workspace. |
| `Get-GeoFromIpAndTagIncident` | Logic App workflow | `rg-sc200-sentinel-lab` | Canada Central | Existing Sentinel-style playbook/automation artifact. |
| `SentinelDetectionRulesIdentity` | User-assigned managed identity | `rg-sc200-sentinel-lab` | Canada Central | Existing identity likely created for detection-rule or automation work. |
| `azuresentinel-Get-GeoFromIpAndTagIncident-1` | API connection | `rg-sc200-sentinel-lab` | Canada Central | Connector used by the Logic App. |
| `azuresentinel-Get-GeoFromIpAndTagIncident-2` | API connection | `rg-sc200-sentinel-lab` | Canada Central | Connector used by the Logic App. |

## Workspace Properties

| Property | Value |
| --- | --- |
| Workspace | `law-sc200-sentinel-lab` |
| Resource group | `rg-sc200-sentinel-lab` |
| Region | Canada Central |
| SKU | `pergb2018` |
| Retention | 30 days |
| Provisioning state | Succeeded |
| Public ingestion | Enabled |
| Public query | Enabled |

## Data Check

The workspace currently has no `AzureActivity`, `SecurityAlert`, `SentinelHealth`, or `OfficeActivity` rows returned by the initial 7-day check.

That means Day 2 should focus on confirming data connector setup and generating a harmless Azure Activity event.

## Current Assessment

Use the existing Canada Central workspace instead of creating a new East US workspace. It is already Sentinel-enabled and lives in the enabled student subscription.

Only create new resources if the existing workspace cannot ingest Azure Activity after connector setup.
