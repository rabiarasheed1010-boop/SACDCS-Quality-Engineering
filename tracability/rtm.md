# SACDCS Requirements Traceability Matrix (RTM)

## Purpose
The RTM connects system requirements with robot states, operations, constraints, test cases, and risks. It helps ensure that requirements are implemented and tested.

| Requirement ID | State / Transition | Operation | Constraint | Test Case | Risk |
|---|---|---|---|---|---|
| FR-01 | IDLE | OP-01 RegisterRobot | C-12 | TC-01 | Unregistered robot |
| FR-02 | NAVIGATING | OP-03 ReadTemperature | C-07, C-08 | TC-02 | Item temperature becomes unsafe |
| FR-03 | NAVIGATING | OP-04 ReadBattery | C-01 | TC-03 | Robot battery failure |
| FR-04 | IDLE → NAVIGATING | OP-05 NavigateToDestination | C-04 | TC-04 | Robot goes to the wrong destination |
| FR-05 | NAVIGATING → AVOIDING_OBSTACLE | OP-06 DetectObstacle | C-05 | TC-05 | Collision |
| FR-06 | NAVIGATING → DELIVERING | OP-08 VerifyDelivery | C-04 | TC-06 | Incorrect or unsafe delivery |
| FR-07 | DELIVERING → RETURNING | OP-09 CompleteDelivery | C-12 | TC-07 | Missing delivery record |
| FR-08 | Any active state → SAFE_MODE | OP-11 EnterSafeMode | C-01 | TC-08 | Critical condition not handled |
| FR-09 | Any active state → SAFE_MODE | OP-11 EnterSafeMode | C-06, C-11 | TC-09 | Unsafe robot movement |
| FR-10 | Command processing | OP-14 AuthenticateCommand; OP-15 AuthorizeCommand | C-03 | TC-10 | Unauthorized control |

## Change Request Traceability

| Change Request | Related Requirement | Test Case | Required Verification |
|---|---|---|---|
| CR-01 | FR-09 | TC-08, TC-09 | Safe Mode activates within 3 seconds of a critical condition. |
| CR-02 | NFR-02 | TC-11 | At least 20 robots operate concurrently. |
| CR-03 | FR-10, NFR-03 | TC-10 | Unauthenticated and unauthorized commands are rejected. |

## Regression Testing

After a change is implemented, repeat the affected tests:

- **CR-01:** Repeat TC-02, TC-03, TC-08, and TC-09 because temperature, battery, and Safe Mode behaviour are related.
- **CR-02:** Repeat TC-11 and check navigation, delivery status, and event logging under concurrent operation.
- **CR-03:** Repeat TC-10 and relevant delivery-control tests to confirm unauthorized commands cannot trigger operations.

## Traceability Review

Every requirement should have a corresponding verification test. Any requirement without a test must be reviewed before the system is accepted.
