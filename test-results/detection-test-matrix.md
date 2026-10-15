Detection Test Matrix — Windows Failed Login Investigation

Objective

Validate the failed-login burst detection logic and the correlation of failed logins followed by a successful login using synthetic Windows security event data.

Test configuration

- Failed-login event ID: 4625
- Successful-login event ID: 4624
- Failure threshold: 5 attempts
- Correlation window: 10 minutes
- Correlation requirement: Failed and successful logins must share the same source IP address.
- Environment: Google Colab using Python and synthetic event data
- Validation date: 15 October 2026

Test results

Test ID| Scenario| Failure burst expected| Same-IP correlation expected| Result
T01| Eight failed logins followed by success from the same IP| True| True| PASS
T02| Three failed logins only| False| False| PASS
T03| Eight failed logins with no subsequent success| True| False| PASS
T04| Eight failed logins from one IP followed by success from a different IP| True| False| PASS

Validation summary

- Total scenarios: 4
- Passed: 4
- Failed: 0
- Overall result: PASS

Key findings

1. The detection identifies a burst of failed login attempts above the configured threshold.
2. A small number of failed attempts does not trigger the burst alert.
3. A failure burst without a subsequent successful login does not trigger the correlation alert.
4. A successful login from a different IP does not satisfy the same-IP correlation requirement.

Limitations

- Tests use synthetic data and do not establish that a real account was compromised.
- The Python logic was validated in Google Colab.
- The KQL queries are draft detection rules and have not been validated against a live Microsoft Sentinel workspace.
- A shared source IP does not prove that events came from the same person or device.

Conclusion

All four test scenarios passed. The results support the intended behavior of the prototype against the tested scenarios. Additional testing with real-world log variations and validation in Microsoft Sentinel would be required before production use.
