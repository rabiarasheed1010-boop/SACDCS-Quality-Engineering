# SACDCS Operations and Operation Schemas

## 1. List of System Operations

| Operation ID | Operation | Description |
|---|---|---|
| OP-01 | RegisterRobot | Registers a delivery robot. |
| OP-02 | AssignDelivery | Assigns a delivery task to a robot. |
| OP-03 | ReadTemperature | Reads the chamber temperature. |
| OP-04 | ReadBattery | Reads the robot's battery level. |
| OP-05 | NavigateToDestination | Moves the robot toward its destination. |
| OP-06 | DetectObstacle | Detects obstacles in the robot's path. |
| OP-07 | AvoidObstacle | Moves safely around an obstacle. |
| OP-08 | VerifyDelivery | Checks whether delivery conditions are satisfied. |
| OP-09 | CompleteDelivery | Records a completed delivery. |
| OP-10 | ReturnToBase | Sends the robot back to its base. |
| OP-11 | EnterSafeMode | Activates Safe Mode during a critical condition. |
| OP-12 | DetectLinkLoss | Detects loss of communication. |
| OP-13 | RestoreConnection | Restores and verifies communication. |
| OP-14 | AuthenticateCommand | Checks the identity of the command sender. |
| OP-15 | AuthorizeCommand | Checks whether the sender's role permits the command. |
| OP-16 | RecordEvent | Records an important system event. |

## 2. Operation Schemas

### OP-02: AssignDelivery

**Description:** Assigns a delivery task to an available robot.

- **Inputs:** Robot ID, delivery ID, destination
- **Outputs:** Assignment result
- **Reads:** Robot status, destination details
- **Changes:** Robot's assigned task
- **Sends/Alerts:** Task assignment notification
- **Preconditions:** Robot is registered and available.
- **Postconditions:** The task is assigned, or a rejection is recorded.

### OP-03: ReadTemperature

**Description:** Reads the temperature of the conservation chamber.

- **Inputs:** Chamber ID, sensor reading
- **Outputs:** Temperature value, reading status
- **Reads:** Temperature sensor
- **Changes:** Latest temperature record
- **Sends/Alerts:** Temperature alert if the reading is outside the permitted range
- **Preconditions:** Chamber and sensor are registered.
- **Postconditions:** A valid reading is recorded, or a sensor fault is reported.

### OP-04: ReadBattery

**Description:** Checks the robot's battery level.

- **Inputs:** Robot ID, battery sensor reading
- **Outputs:** Battery percentage, battery status
- **Reads:** Battery sensor
- **Changes:** Latest battery record
- **Sends/Alerts:** Low-battery or critical-battery alert
- **Preconditions:** Robot is registered and the battery sensor is available.
- **Postconditions:** Battery status is recorded, or a sensor fault is reported.

### OP-08: VerifyDelivery

**Description:** Checks whether a delivery can safely proceed.

- **Inputs:** Delivery ID, destination, temperature reading, robot status
- **Outputs:** Approved or rejected result
- **Reads:** Delivery details, temperature, robot status
- **Changes:** Delivery verification status
- **Sends/Alerts:** Rejection alert if a safety condition fails
- **Preconditions:** A delivery task exists.
- **Postconditions:** Delivery is approved only when all required conditions are satisfied.

### OP-11: EnterSafeMode

**Description:** Places the robot in Safe Mode when a critical condition occurs.

- **Inputs:** Robot ID, critical temperature or battery event
- **Outputs:** Safe Mode status
- **Reads:** Current robot state, sensor readings
- **Changes:** Robot state becomes SAFE_MODE
- **Sends/Alerts:** Critical safety alert
- **Preconditions:** A critical condition has been detected.
- **Postconditions:** Safe Mode is activated within 3 seconds, and the event is logged.

### OP-14: AuthenticateCommand

**Description:** Verifies the identity of a person or system sending a command.

- **Inputs:** Command, credentials, sender identity
- **Outputs:** Authenticated or rejected result
- **Reads:** User or system account records
- **Changes:** Authentication audit log
- **Sends/Alerts:** Rejection alert for invalid credentials
- **Preconditions:** A command has been received.
- **Postconditions:** The sender's identity is verified or the command is rejected.

## 3. Sensor Verification

The following operations require sensor verification:

1. **OP-03 ReadTemperature:** Check sensor validity and reject missing or faulty readings.
2. **OP-04 ReadBattery:** Check that the battery reading is valid and within the expected range.

Invalid sensor readings must not be treated as safe readings. The system should report the fault and follow its safety procedure.
