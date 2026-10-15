Incident Report: Suspected Brute-Force Activity

1. Incident Summary

Incident type: Suspicious authentication activity
Severity: High — provisional pending investigation
Status: Investigation required
Data source: Synthetic Windows security events
Relevant event IDs: 4625 (failed logon), 4624 (successful logon)

Repeated failed login attempts were observed against multiple account names from a common source IP address. The activity was followed by a successful login for the "jsmith" account from that same IP.

This pattern is consistent with possible password guessing or brute-force activity. However, the available evidence does not independently establish malicious intent or confirm that the account was compromised.

2. Evidence Observed

Observation| Evidence| Significance
Repeated failed logins| Eight failures associated with "203.0.113.25" in the sample| May indicate password guessing or another authentication problem
Multiple account names targeted| "jsmith", "admin", and "administrator"| May indicate attempts to discover or access valid accounts
Successful login after failures| Event ID 4624 for "jsmith" from the same IP| Raises the priority of investigating whether access was legitimate
Separate low-volume activity| Two failures from "198.51.100.40"| Insufficient on its own to establish an attack

The addresses are reserved for documentation examples, and the dataset is entirely synthetic.

3. Initial Assessment

Assessment: Suspicious authentication pattern requiring investigation.

The combination of repeated failures, multiple targeted account names, and a subsequent successful login warrants further investigation. Nevertheless, a legitimate user entering an incorrect password repeatedly, an automated service, or another benign explanation could produce some similar signals.

Severity is provisional. The appropriate priority in a real environment would depend on the account's privileges, the asset involved, the source's reputation and location, and the surrounding activity.

4. Recommended Investigation

1. Validate the successful login. Confirm the account owner, login time, source IP, authentication method, device, and whether the activity was expected.
2. Review surrounding events. Examine authentication activity before and after the observed sequence, including relevant logon types and failure details.
3. Check for related activity. Look for other targeted accounts, unusual devices, privilege changes, suspicious processes, and access to sensitive resources.
4. Establish the source context. Determine whether the IP belongs to an approved VPN, corporate network, known service, or an untrusted source.
5. Preserve evidence. Record timestamps, relevant event fields, queries, findings, and investigative decisions.
6. Escalate or contain when justified. If evidence indicates unauthorised access, follow the organisation's incident-response procedure. Any account restriction, credential reset, or session revocation should be coordinated with the appropriate team.

5. Detection and Validation

The project includes draft KQL queries intended to identify failed-login bursts and correlate failures with a subsequent successful login from the same source IP.

The Python prototype was tested against four synthetic scenarios. All four passed:

- Repeated failures followed by a same-IP success.
- A small number of failures.
- Repeated failures without a subsequent success.
- Repeated failures followed by success from a different IP.

These tests validate the expected behaviour of the Python prototype for those scenarios. They do not demonstrate that the KQL queries have been executed successfully in Microsoft Sentinel.

6. Conclusion

The available sample evidence supports treating the event sequence as suspicious and investigating it promptly. It does not prove that an attacker gained access or that the account was compromised.

The next decision should be based on validation of the successful login and any corroborating evidence found in surrounding security telemetry.

7. Analyst Learning Points

- A successful login after repeated failures is a signal to investigate, not proof of compromise.
- Detection thresholds help identify suspicious patterns but can generate false positives.
- Correlation should account for source IP and event timing, while recognising that shared IP addresses do not prove a common actor.
- Findings, assumptions, limitations, and recommended actions should be documented separately.
