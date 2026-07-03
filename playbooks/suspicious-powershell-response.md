# Suspicious PowerShell Response Checklist

## Initial Triage

1. Review the command line and suspicious reason.
2. Identify the user, host, parent process, and timestamp.
3. Check nearby process events for script execution, downloads, or persistence.
4. Determine whether the command matches admin tooling or expected software.

## Containment

1. Escalate if command includes download and execution behavior.
2. Recommend isolating the host only if malicious activity is likely or confirmed.
3. Recommend collecting script, command line, file hash, and user context.
4. Recommend endpoint scan or EDR review where available.

## Documentation

Record:

- Host
- User
- Parent process
- Full command line
- Reason for suspicion
- Triage conclusion
