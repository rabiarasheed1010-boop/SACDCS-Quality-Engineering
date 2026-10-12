# SACDCS Robot State Model

## 1. Robot States

| State ID | State | Description |
|---|---|---|
| ST-01 | IDLE | The robot is waiting for a task. |
| ST-02 | NAVIGATING | The robot is moving toward its destination. |
| ST-03 | AVOIDING_OBSTACLE | The robot is avoiding an obstacle. |
| ST-04 | DELIVERING | The robot is delivering the item. |
| ST-05 | RETURNING | The robot is returning to its base. |
| ST-06 | SAFE_MODE | The robot stops normal operations due to a critical condition. |
| ST-07 | LINK_LOST | Communication with the control system has been lost. |

## 2. State Transitions

| Current State | Event | Next State | Expected Behaviour |
|---|---|---|---|
| IDLE | Task assigned | NAVIGATING | Start the assigned journey. |
| NAVIGATING | Obstacle detected | AVOIDING_OBSTACLE | Avoid the obstacle safely. |
| AVOIDING_OBSTACLE | Path clear | NAVIGATING | Resume navigation. |
| NAVIGATING | Destination reached | DELIVERING | Begin delivery. |
| DELIVERING | Delivery completed | RETURNING | Return to base. |
| RETURNING | Base reached | IDLE | Wait for another task. |
| Any active state | Critical temperature or battery | SAFE_MODE | Enter Safe Mode within 3 seconds. |
| Any active state | Communication lost | LINK_LOST | Stop unsafe movement and follow the safe communication-loss procedure. |
| LINK_LOST | Communication restored and verified | Previous safe state | Resume only when safe. |
| SAFE_MODE | Fault cleared and authorized reset | IDLE | Resume normal operation only after safety checks. |

## 3. Invalid Transitions

- IDLE → DELIVERING: Invalid because the robot must receive a task and navigate to the destination first.
- AVOIDING_OBSTACLE → DELIVERING: Invalid unless the destination has been reached and the delivery conditions are verified.
- SAFE_MODE → NAVIGATING: Invalid without fault clearance, safety checks, and an authorized reset.

## 4. Safety Checks

- The robot must check temperature and battery conditions during all active states.
- A critical condition must trigger Safe Mode within 3 seconds.
- The robot must not resume movement while an unresolved critical fault exists.
- Communication loss must not cause unsafe movement.
- Every state transition should be recorded with a timestamp.

## 5. Verification Evidence

State transitions should be verified through test cases, event logs, and simulated fault conditions. Tests must include obstacle detection, critical battery during delivery, communication loss, and safe recovery.
