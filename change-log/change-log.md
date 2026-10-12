# SACDCS Version-Controlled Change Log

## Purpose
This document records the original requirements, approved changes, reasons for changes, and their impact on testing.

## CR-01: Safe Mode Timing

**Status:** Modified

**Old requirement:** The robot shall enter Safe Mode when a critical battery or thermal condition is detected.

**New requirement:** The robot shall enter Safe Mode within 3 seconds when chamber or battery temperature exceeds the critical threshold or battery capacity falls below the emergency level.

**Reason:** The original requirement did not define how quickly Safe Mode must activate or specify the triggering thresholds clearly.

**Why the new wording is more testable:** The detection time and Safe Mode activation time can be recorded and compared. The system passes when activation occurs within 3 seconds after the specified critical condition is detected.

**Verification:** Timed fault-injection tests for critical chamber temperature and low battery.

**Regression tests:** TC-02, TC-03, TC-08, TC-09.

## CR-02: Concurrent Robot Connections

**Status:** Modified

**Old requirement:** The system shall support communication with multiple robots simultaneously.

**New requirement:** The system shall support at least 20 simultaneously connected robots.

**Reason:** The pilot release serves 20 clinics, so the system must handle the planned fleet workload.

**Why the new wording is more testable:** The number of connected robots is measurable. A load test can connect 20 robots and check that the required communication and safety functions remain operational.

**Verification:** Concurrent-load test with at least 20 simulated robot connections.

**Regression tests:** TC-11 and relevant navigation, delivery-status, telemetry, and event-logging tests.

## CR-03: Command Authentication and Authorization

**Status:** Modified

**Old requirement:** Only authenticated operators shall be permitted to issue robot commands.

**New requirement:** The system shall require authenticated and role-authorised operators before accepting any robot command.

**Reason:** Authentication confirms who the operator is, while role authorization checks whether that operator has permission to issue the particular command.

**Why the new wording is more testable:** Tests can use valid operators, invalid credentials, and authenticated operators with insufficient permissions. Only commands that pass both checks should be accepted.

**Verification:** Security tests covering authentication and role-based authorization for each command category.

**Regression tests:** TC-10 and relevant command-execution and command-logging tests.

## Version History

| Version | Change | Reason |
|---|---|---|
| 1.0 | Initial requirements baseline created. | Establish the starting requirements. |
| 1.1 | CR-01 modified Safe Mode timing and triggering conditions. | Make the safety response measurable. |
| 1.2 | CR-02 specified support for at least 20 simultaneous robot connections. | Make scalability measurable. |
| 1.3 | CR-03 added role-based authorization to command acceptance. | Strengthen access control. |

## Change Control Procedure

1. Record the original requirement and proposed replacement.
2. Explain the reason and expected impact.
3. Review the safety, security, and testing implications.
4. Approve the change before treating it as part of the baseline.
5. Commit the updated document to GitHub.
6. Rerun affected tests and record their actual results.

## Test Status
The test identifiers above refer to planned test cases. Their results must be updated after execution; they must not be marked Passed without evidence.
