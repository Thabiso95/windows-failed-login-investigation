Windows Failed Login Investigation

Project Overview

This project demonstrates a basic Security Operations Centre (SOC) investigation into suspicious Windows authentication activity using synthetic security event data.

The investigation focuses on repeated failed logins and whether a successful login follows a burst of failures from the same source IP address.

The project simulates parts of a Tier 1 SOC analyst workflow: identifying suspicious activity, validating detection logic, documenting findings, and recommending investigative actions.

Investigation Scenario

The sample dataset contains Windows authentication events:

- Event ID 4625: Failed logon
- Event ID 4624: Successful logon

The main scenario contains repeated failed login attempts against several account names, followed by a successful login for "jsmith" from the same source IP.

This pattern may indicate password guessing or brute-force activity, but it does not independently prove malicious intent or account compromise.

All event data is synthetic. The sample IP addresses are reserved for documentation and examples.

Detection Logic

The project includes draft Kusto Query Language (KQL) queries intended for Microsoft Sentinel:

- ""detections/brute-force.kql"" (detections/brute-force.kql) — identifies source IPs associated with repeated failed logins.
- ""detections/failures-followed-by-success.kql"" (detections/failures-followed-by-success.kql) — correlates failed and successful logins from the same source IP within a defined time window.

Python was used in Google Colab to validate the prototype's expected behaviour against synthetic test scenarios.

Test Results

Python prototype: 4 of 4 test scenarios passed.

Test| Scenario| Expected result| Outcome
T01| Repeated failures followed by same-IP success| Both alerts trigger| PASS
T02| Three failed logins only| Neither alert triggers| PASS
T03| Repeated failures without subsequent success| Failure-burst alert only| PASS
T04| Failures followed by success from a different IP| Failure-burst alert only| PASS

Test Execution Evidence

The screenshot below shows the Python prototype's test results.

(screenshots/python-test-results.jpg)

See the "detection test matrix" (test-results/detection-test-matrix.md) and "test execution evidence" (evidence/test-execution.md) for more detail.

Investigation Documentation

- "Incident report" (incident-report.md)
- "Synthetic authentication logs" (sample-logs.csv)
- "Correlation and false-positive test report" (test-results/correlation-and-false-positive-tests.md)
- "Detection test matrix" (test-results/detection-test-matrix.md)
- "Test execution evidence" (evidence/test-execution.md)

Analyst Workflow Demonstrated

1. Detect: Identify repeated Windows authentication failures.
2. Correlate: Check for a successful login following repeated failures from the same IP.
3. Validate: Test expected detection behaviour against synthetic scenarios.
4. Document: Record evidence, findings, limitations, and recommended actions.
5. Improve: Identify weaknesses and refine detection logic.

Skills and Tools

- Windows Security Event IDs 4624 and 4625
- Python and pandas
- Kusto Query Language (KQL)
- Microsoft Sentinel detection concepts
- Authentication-event analysis
- Basic detection engineering and test design
- False-positive awareness
- Incident documentation and triage

Project Status

- [x] Synthetic Windows authentication dataset created
- [x] Incident report documented
- [x] Draft KQL detection queries written
- [x] Python prototype tested against four scenarios
- [x] Test results documented
- [x] Screenshot of test results added to the README
- [ ] KQL validated in a Microsoft Sentinel workspace
- [ ] Additional testing against varied event patterns

Limitations

The Python prototype passed the four documented synthetic test scenarios. These results do not establish that the KQL queries execute correctly in Microsoft Sentinel.

The KQL queries remain drafts pending schema verification, execution, and further testing. Correlation by source IP and time does not prove that events originated from the same person or device.

Disclaimer

This is a personal learning project using synthetic data. It does not represent a live security incident, a production-ready detection, or proof of a real account compromise.
