# SACDCS Requirements Traceability Matrix (RTM)

| Requirement ID | State / Transition | Operation | Constraint | Test Case | Risk |
|---|---|---|---|---|---|
| FR-01 | Command validation | OP-14 AuthenticateCommand; OP-15 AuthorizeCommand | C-03 | TC-10 | Critical |
| FR-02 | IDLE → NAVIGATING | OP-02 AssignDelivery | C-10 | TC-04 | High |
| FR-03 | NAVIGATING → crossing clearance | OP-05 NavigateToDestination | C-01, C-02 | TC-13 | Critical |
| FR-04 | NAVIGATING → AVOIDING_OBSTACLE → NAVIGATING | OP-06 DetectObstacle; OP-07 AvoidObstacle | C-05 | TC-05 | Critical |
| FR-05 | Chamber monitoring | OP-03 ReadTemperature; OP-04 ReadBattery | C-07, C-08 | TC-02, TC-03 | High |
| FR-06 | Chamber correction and recovery | OP-03 ReadTemperature | C-07, C-08 | TC-12 | Critical |
| FR-07 | Chamber protection response | OP-11 EnterSafeMode | C-06, C-08 | TC-12 | High |
| FR-08 | Any active state → SAFE_MODE | OP-11 EnterSafeMode | C-01, C-06 | TC-08, TC-09 | Critical |
| FR-09 | Active state → LINK_LOST | OP-12 DetectLinkLoss | C-09 | TC-13 | Critical |
| FR-10 | DELIVERING → RETURNING → IDLE | OP-09 CompleteDelivery; OP-10 ReturnToBase | C-12 | TC-07 | High |
| SAF-02 | Robot waits outside crossing until clearance | OP-05 NavigateToDestination | C-02, C-03 | TC-14 | Critical |
| SAF-03 | Active state → LINK_LOST | OP-12 DetectLinkLoss | C-09 | TC-13 | Critical |
| SAF-04 | Conservation suspended until verification | OP-03 ReadTemperature; OP-16 RecordEvent | C-08, C-12 | TC-12 | Critical |
| CR-02 / NFR-02 | Concurrent robot operations | OP-02 AssignDelivery | C-02 | TC-11 | High |
| CR-03 / NFR-03 | Command authentication and authorization | OP-14 AuthenticateCommand; OP-15 AuthorizeCommand | C-03 | TC-10 | Critical |

## Change Request Regression Testing

- CR-01: Rerun TC-02, TC-03, TC-08, and TC-09.
- CR-02: Rerun TC-11 and relevant telemetry, navigation, delivery, and logging tests.
- CR-03: Rerun TC-10 and relevant command-execution tests.

## Traceability Review
Each requirement must connect to a model element, operation, constraint, test, and risk level. Any missing link must be reviewed before acceptance. Test results must be supported by evidence.
