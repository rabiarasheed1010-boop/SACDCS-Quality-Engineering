# SACDCS Operations

## 1. List of Operations

| Operation ID | Operation Name | Purpose |
|---|---|---|
| OP-01 | RegisterRobot | Register a robot in the system |
| OP-02 | AssignDelivery | Assign a delivery to an available robot |
| OP-03 | ReadTemperature | Read and verify chamber temperature |
| OP-04 | ReadHumidity | Read and verify chamber humidity |
| OP-05 | ReadVibration | Monitor vibration during transport |
| OP-06 | CheckDoorStatus | Check whether the chamber door is secure |
| OP-07 | CheckBattery | Measure remaining battery capacity |
| OP-08 | CorrectChamberConditions | Correct temperature or humidity when outside limits |
| OP-09 | VerifyConservation | Confirm chamber conditions using sensor readings |
| OP-10 | NavigateToDestination | Move toward the assigned destination |
| OP-11 | DetectAndAvoidObstacle | Detect an obstacle and avoid it safely |
| OP-12 | VerifyDelivery | Confirm that delivery conditions are satisfied |
| OP-13 | ReturnToBase | Return the robot to the warehouse |
| OP-14 | EnterSafeMode | Stop normal operations during a critical fault |
| OP-15 | DetectLinkLoss | Detect loss of required communication |
| OP-16 | RestoreConnection | Restore and verify communication |
| OP-17 | AuthenticateCommand | Verify the command sender's identity |
| OP-18 | AuthorizeCommand | Check the sender's role permissions |
| OP-19 | RecordEvent | Record events and safety decisions |
| OP-20 | CheckRailwayClearance | Confirm railway crossing safety before entry |

## 2. Operation Schemas

### OP-02: AssignDelivery

- **Description:** Assign a delivery request to an available registered robot.
- **Inputs:** Delivery ID, destination, robot ID, operator credentials.
- **Outputs:** Assignment result and task ID.
- **Reads:** Robot availability, pending tasks, operator role.
- **Changes:** Robot task status and assigned destination.
- **Sends/Alerts:** Assignment confirmation or rejection.
- **Assumes/Precondition:** Robot is registered and the command is authorized.
- **Result/Postcondition:** One valid task is assigned, and the assignment is logged.

### OP-03: ReadTemperature

- **Description:** Read chamber temperature and compare it with the approved range for the batch.
- **Inputs:** Robot ID, chamber ID, batch profile.
- **Outputs:** Temperature reading, timestamp, status.
- **Reads:** Temperature sensor and approved batch limits.
- **Changes:** Latest chamber telemetry record.
- **Sends/Alerts:** Temperature warning if outside the permitted range.
- **Assumes/Precondition:** The sensor is available and its reading passes validity checks.
- **Result/Postcondition:** A timestamped reading is recorded. The temperature is considered acceptable only if the valid measured value is within the approved range.

### OP-04: ReadHumidity

- **Description:** Measure chamber humidity and compare it with the batch's approved range.
- **Inputs:** Robot ID, chamber ID, batch profile.
- **Outputs:** Humidity reading, timestamp, status.
- **Reads:** Humidity sensor and approved humidity limits.
- **Changes:** Latest humidity telemetry record.
- **Sends/Alerts:** Warning
