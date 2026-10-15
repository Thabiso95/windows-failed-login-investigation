Test Execution Evidence

Environment

- Platform: Google Colab
- Language: Python
- Dataset: Synthetic Windows authentication events
- Validation date: 15 October 2026

Purpose

Validate the prototype's failed-login burst detection and same-source-IP failure-to-success correlation logic.

Test execution summary

Test| Description| Expected result| Observed result
T01| Eight failed logins followed by a same-IP success| Both alerts trigger| PASS
T02| Three failed logins only| Neither alert triggers| PASS
T03| Eight failed logins without a success| Failure-burst alert only| PASS
T04| Eight failed logins followed by success from a different IP| Failure-burst alert only| PASS

Overall result: 4/4 scenarios passed.

Interpretation

The tests confirm that the Python prototype behaved as expected for these four scenarios. In particular, T04 verifies that the correlation logic does not incorrectly associate a successful login from a different source IP with the preceding failures.

Scope and limitations

- The test data is synthetic.
- The tests cover only the scenarios listed above.
- Shared IP addresses do not establish a common actor.
- These results validate the Python prototype, not the KQL queries in Microsoft Sentinel.
- Further testing is required before the detection logic could be considered production-ready.
