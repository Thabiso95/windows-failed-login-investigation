Correlation and False-Positive Test Results

Test 1: Failed Logins Followed by Success

Objective: Identify successful authentication events preceded by repeated failed logins from the same source IP.

Detection condition: At least five failed logins within the ten minutes before a successful login.

Expected result: The synthetic source "203.0.113.25" should trigger a correlated alert for the successful login to "jsmith".

Interpretation: The event sequence is suspicious and requires investigation. It does not independently prove account compromise.

Test 2: Threshold Validation

Scenario| Failed Attempts| Expected Result
Normal password mistakes| 3| No alert
Repeated failures| 8| Alert

Interpretation: The threshold distinguishes these two deliberately selected scenarios. Additional test cases are required before making claims about real-world false-positive rates.

Limitations

- All records are synthetic.
- Source addresses are documentation-only IP addresses.
- The tests validate Python logic, not a live Sentinel analytics rule.
- The threshold is illustrative and requires tuning against representative data.

Next Steps

- Align KQL with the tested correlation logic.
- Test successful logins from a different source IP.
- Test failures spread across multiple time windows.
- Test legitimate authentication bursts.
- Document expected outcomes for each test case.
