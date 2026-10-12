# SACDCS Constraints and Formal Rules

## 1. System Constraints

| Constraint ID | Constraint | Purpose |
|---|---|---|
| C-01 | Safe Mode must activate within 3 seconds of a critical condition. | Protects the robot and items. |
| C-02 | The system must support at least 20 concurrent robots. | Supports multiple deliveries. |
| C-03 | Every command must be authenticated and role-authorized. | Prevents unauthorized control. |
| C-04 | The robot must not deliver to an unverified destination. | Ensures correct delivery. |
| C-05 | The robot must avoid detected obstacles. | Prevents collisions. |
| C-06 | The robot must not continue normal movement during an unresolved critical fault. | Maintains safety. |
| C-07 | Temperature must remain within the permitted range for the stored item. | Protects item quality. |
| C-08 | Invalid or missing sensor readings must be reported as faults. | Prevents unsafe decisions. |
| C-09 | Communication loss must trigger a safe response. | Prevents uncontrolled operation. |
| C-10 | A robot must not be assigned two conflicting active delivery tasks. | Prevents task conflicts. |
| C-11 | Safe Mode must not be exited without fault clearance and an authorized reset. | Prevents unsafe recovery. |
| C-12 | Important state changes and safety events must be logged with timestamps. | Supports auditing and testing. |

## 2. Logical Formalization

Let:
- `critical` = a critical condition is detected.
- `safeMode` = the robot is in Safe Mode.
- `authenticated` = the command sender is authenticated.
- `authorized` = the sender's role permits the command.
- `destinationVerified` = the destination has been verified.
- `sensorValid` = the sensor reading is valid.
- `linkLost` = communication has been lost.
- `faultCleared` = the critical fault has been cleared.
- `resetAuthorized` = an authorized reset has been received.

| Constraint | Formal Rule |
|---|---|
| C-01 | `critical → safeMode within 3 seconds` |
| C-03 | `commandAccepted → (authenticated AND authorized)` |
| C-04 | `deliveryStarted → destinationVerified` |
| C-05 | `obstacleDetected → obstacleAvoidanceRequired` |
| C-06 | `critical AND NOT faultCleared → NOT normalMovement` |
| C-08 | `NOT sensorValid → sensorFaultReported` |
| C-09 | `linkLost → safeCommunicationResponse` |
| C-10 | `activeTaskCount(robot) ≤ 1` |
| C-11 | `exitSafeMode → (faultCleared AND resetAuthorized)` |
| C-12 | `stateChange → eventLoggedWithTimestamp` |

## 3. Example Constraint Violations

| Violation | Example | Detection | Required Response |
|---|---|---|---|
| V-01 | Safe Mode activates after 5 seconds instead of 3 seconds. | Compare event and activation timestamps. | Record failure and investigate the delay. |
| V-02 | A system accepts a command from an unauthorized user. | Check authentication and role logs. | Reject the command and record a security event. |
| V-03 | Temperature is 12°C when the permitted range is 2°C–8°C. | Compare the reading with the item's configured limits. | Raise a critical alert and follow the approved safety procedure. |
| V-04 | A sensor returns no reading, but the system treats it as safe. | Check sensor validity and missing-reading logs. | Report a sensor fault and prevent unsafe decisions. |
| V-05 | The robot continues normal movement after communication is lost. | Check communication status and movement logs. | Apply the defined safe communication-loss procedure. |
| V-06 | Two active delivery tasks are assigned to one robot. | Check the robot's active task records. | Reject the conflicting assignment. |

## 4. Verification

Each constraint must be checked through suitable test cases, event logs, and simulated fault conditions. Failed tests must be recorded and repeated after the relevant correction.
