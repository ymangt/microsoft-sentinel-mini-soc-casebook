# Password Spray Response Checklist

## Initial Triage

1. Confirm the source IP, number of failed attempts, and number of targeted accounts.
2. Check whether any targeted account later had a successful sign-in.
3. Review location, application, and failure reason.
4. Check whether the source IP is known, expected, VPN-related, or suspicious.

## Containment

1. Escalate if a successful sign-in follows the spray activity.
2. Recommend password reset for affected accounts if compromise is suspected.
3. Recommend MFA review or re-registration only when justified.
4. Block source IP only if policy and evidence support it.

## Documentation

Record:

- Alert time
- Source IP
- Affected accounts
- Evidence summary
- False-positive considerations
- Escalation decision
