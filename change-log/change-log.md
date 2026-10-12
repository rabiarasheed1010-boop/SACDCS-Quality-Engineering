# SACDCS Change Log

## Purpose
This file records changes made to the requirements of the Smart Autonomous Cold-Chain Delivery & Control System (SACDCS).

## Change Requests

| Change ID | Description | Reason | Priority | Status |
|---|---|---|---|---|
| CR-01 | The robot shall enter Safe Mode within 3 seconds when a critical temperature or battery condition is detected. | To protect sensitive items and the robot. | High | Accepted |
| CR-02 | The system shall support at least 20 robots operating concurrently. | To support multiple deliveries. | High | Accepted |
| CR-03 | Every control command must be authenticated and role-authorized. | To prevent unauthorized control. | High | Accepted |

## Change History

| Version | Change | Reason |
|---|---|---|
| 1.0 | Added the initial requirements and change requests. | Initial project baseline. |

## Testing Impact

- **CR-01:** Test Safe Mode activation and verify the response occurs within 3 seconds.
- **CR-02:** Test the system with 20 robots operating concurrently.
- **CR-03:** Test valid commands, unauthenticated commands, and commands from unauthorized roles.

