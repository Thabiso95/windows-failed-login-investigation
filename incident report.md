SOC Incident Report: Suspected Brute-Force Activity

1. Incident Summary

Case ID: SOC-2026-001
Incident type: Suspicious authentication activity
Initial severity: High — provisional
Status: Open — further investigation required
Environment: Simulated Windows endpoint
Affected computer: WS-001
Potentially affected account: jsmith
Data source: Synthetic Windows Security event records

Executive Summary

An analysis of simulated Windows authentication logs identified repeated failed login attempts from a single source IP address against multiple account names. A successful login to the account "jsmith" was subsequently recorded from the same source.

The pattern is consistent with possible password guessing or brute-force activity followed by a successful authentication. The available evidence does not establish whether the successful login was authorised or whether an account was compromised.

Further investigation is required.

2. Evidence Reviewed

The investigation used a synthetic CSV dataset containing 11 authentication events.

- 10 failed logon events (Event ID 4625).
- 1 successful logon event (Event ID 4624).
- 2 distinct source IP addresses.
- 3 account names targeted.

Primary Source

"203.0.113.25"

This source generated eight failed logon events against the following account names:

- "jsmith"
- "admin"
- "administrator"

A successful logon to "jsmith" was then recorded at 08:03:01 on 15 October 2026.

Secondary Source

"198.51.100.40"

This source generated two failed logon events against "jsmith" at 08:10:00 and 08:10:05.

The addresses belong to documentation-only IP ranges and are not evidence of real-world malicious infrastructure.

3. Timeline

Timestamp| Event| Assessment
08:01:12–08:01:36| Five failed logons to jsmith| Repeated authentication failures
08:02:02–08:02:08| Failed logons to admin and administrator| Multiple account names targeted
08:02:14| Another failed logon to jsmith| Continued activity
08:03:01| Successful logon to jsmith| Requires urgent verification
08:10:00–08:10:05| Two failures from a second source| Separate activity requiring context

All timestamps are from the synthetic dataset and are assumed to use the same time basis.

4. Findings

1. Repeated authentication failures originated from the same recorded source.
2. Multiple account names were targeted in a short period.
3. A successful authentication to "jsmith" followed the repeated failures.
4. A second source generated additional failed attempts.
5. The logs do not contain sufficient context to determine whether the successful authentication was legitimate.

5. MITRE ATT&CK Mapping

Potential technique: T1110 — Brute Force.

The observed pattern is consistent with a possible brute-force or password-guessing attempt. This is a provisional mapping, not confirmation that an attack occurred.

The successful login must be investigated separately before concluding that an account was compromised.

6. Recommended Investigation

1. Verify the successful authentication with the account owner or an authorised administrator.
2. Obtain the original Windows Security events and inspect logon type, authentication package, workstation, and available network details.
3. Review successful and failed authentication events immediately before and after the recorded login.
4. Check for suspicious activity by "jsmith", including unexpected processes, account changes, privilege escalation, and unusual network connections.
5. Determine whether the activity is authorised, malicious, or inconclusive.
6. Preserve relevant evidence and follow the organisation's incident-response and escalation procedures.
7. If compromise is confirmed or strongly suspected, coordinate appropriate account containment, credential resets, session revocation, and endpoint investigation.

7. Conclusion

The available simulated evidence supports classifying this case as suspicious authentication activity requiring prompt investigation.

The initial severity is provisional. Account compromise has not been confirmed.

8. Limitations

- The dataset is fictional and created for training.
- No real Windows endpoint or live SIEM was used.
- No actual attacker attribution is possible from this data.
- No live detection rule has been executed or validated.
- Findings describe the supplied sample only.

9. Analyst Learning Outcomes

This exercise demonstrates basic authentication-log analysis, event correlation, preliminary severity assessment, evidence-based reporting, and proposed incident-response actions.
