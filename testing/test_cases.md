# SACDCS Test Cases

## Purpose
These test cases verify the requirements, safety behaviour, operations, and security of the Smart Autonomous Cold-Chain Delivery & Control System.

**Note:** The results below are expected results. Tests must be executed before they can be marked as passed.

## Test Case Table

| Test ID | Requirement | Test Procedure | Expected Result | Status |
|---|---|---|---|---|
| TC-01 | FR-01 | Register a robot with valid details. | Robot is registered successfully. | Not Run |
| TC-02 | FR-02, C-07 | Simulate a temperature reading outside the configured permitted range. | The system detects the violation and generates an alert. | Not Run |
| TC-03 | FR-03 | Simulate a battery reading below the critical threshold. | The system detects the critical battery condition and triggers the safety response. | Not Run |
| TC-04 | FR-04 | Assign a valid delivery task to an available robot. | The robot begins navigation to the assigned destination. | Not Run |
| TC-05 | FR-05 | Place a simulated obstacle in the robot's path. | The robot detects and avoids the obstacle safely. | Not Run |
| TC-06 | FR-06 | Attempt delivery with a verified destination and valid delivery conditions. | Delivery proceeds only after required checks pass. | Not Run |
| TC-07 | FR-07 | Complete a simulated delivery. | The system records the delivery status and timestamp. | Not Run |
| TC-08 | CR-01 | Trigger a critical temperature condition and record the detection and Safe Mode activation times. | Safe Mode activates within 3 seconds. | Not Run |
| TC-09 | CR-01 | Trigger a critical battery condition while the robot is avoiding an obstacle or delivering. | Safe Mode activates within 3 seconds, and unsafe normal movement is prevented. | Not Run |
| TC-10 | CR-03 | Submit a valid command, an unauthenticated command, and a command from an unauthorized role. | Only authenticated, role-authorized commands are accepted. | Not Run |
| TC-11 | CR-02 | Simulate 20 robots operating concurrently under a defined workload. | The system supports all 20 robots without violating defined safety requirements. | Not Run |
| TC-12 | C-08 | Simulate a missing or invalid temperature sensor reading. | The system reports a sensor fault and does not treat the reading as safe. | Not Run |
| TC-13 | C-09 | Simulate communication loss during navigation. | The robot follows its defined safe communication-loss procedure. | Not Run |
| TC-14 | C-10 | Attempt to assign a second conflicting active delivery task to one robot. | The conflicting assignment is rejected. | Not Run |
| TC-15 | C-11 | Attempt to exit Safe Mode before the fault is cleared and an authorized reset is received. | The system prevents the unsafe reset. | Not Run |

## Test Execution Rules

1. Execute each test using a controlled simulation or suitable test environment.
2. Record the actual result and evidence, such as logs or screenshots.
3. Mark a test as Passed only when the observed result matches the expected result.
4. Mark a test as Failed when the observed result differs from the expected result.
5. After fixing a defect, rerun the failed test and relevant regression tests.

## Regression Tests

- After CR-01 changes, rerun TC-02, TC-03, TC-08, and TC-09.
- After CR-02 changes, rerun TC-11 and relevant navigation, delivery, and logging tests.
- After CR-03 changes, rerun TC-10 and relevant command-control tests.

## Test Summary

Total test cases: 15

Passed: To be updated after execution.

Failed: To be updated after execution.

Not Run: 15 (initial status).
