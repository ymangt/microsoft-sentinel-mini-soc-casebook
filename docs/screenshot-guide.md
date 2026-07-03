# Screenshot Guide

Use screenshots as evidence, not decoration. Every screenshot should prove one part of the analyst workflow.

## Naming Convention

Use this pattern:

```text
screenshots/<scenario-id>-<step>-<short-description>.png
```

Examples:

```text
screenshots/det-001-01-watchlist-loaded.png
screenshots/det-001-02-detection-results.png
screenshots/det-001-03-investigation-query.png
screenshots/det-001-04-analytics-rule.png
screenshots/det-001-05-incident-summary.png
```

## What To Capture For Each Scenario

Required:

- Data source or watchlist loaded
- Detection KQL result
- Investigation KQL result
- Analytics rule configuration
- Final case note evidence

Strong:

- Entity mapping
- Custom details
- Alert or incident page
- MITRE mapping
- Tuning or false-positive note

## Redaction Checklist

Before committing screenshots:

- Hide subscription IDs if visible.
- Hide tenant IDs if visible.
- Hide personal email addresses if visible.
- Hide billing pages and payment information.
- Hide access tokens, secrets, connection strings, and API keys.

## Screenshot Captions

Each screenshot referenced in the README should answer:

- What is this showing?
- Why does it matter?
- What decision did it support?
