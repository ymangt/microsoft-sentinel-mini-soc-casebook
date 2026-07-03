# Detections

This folder contains KQL intended for Microsoft Sentinel scheduled analytics rules.

Each detection should:

- Return `TimeGenerated`.
- Return fields useful for entity mapping.
- Include a short comment explaining the detection idea.
- Avoid destructive or unsafe activity.
- Have a matching investigation query in `../investigations`.
