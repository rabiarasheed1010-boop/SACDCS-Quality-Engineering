# SACDCS State Model

## 1. States

| State ID | State Name | Meaning | Entry Condition | Exit Condition |
|---|---|---|---|---|
| ST-01 | IDLE | Robot is available and not delivering | Startup checks pass or delivery finishes | Valid delivery is assigned |
| ST-02 | NAVIGATING | Robot moves toward its destination | Delivery is assigned and safety checks pass | Obstacle, arrival, fault, or link loss |
| ST-03 | AVOIDING_OBSTACLE | Robot avoids an obstacle | Obstacle is detected | Path is confirmed clear or a safety fault occurs |
| ST-04 | DELIVERING | Robot completes the delivery | Robot reaches destination and verifies safe delivery conditions | Delivery completes or a fault occurs |
| ST-05 | RETURNING | Robot returns to its warehouse | Delivery completes or a non-emergency return is required | Robot reaches warehouse |
| ST-06 | SAFE_MODE | Normal movement and affected operations are stopped | Critical temperature, emergency battery, or critical safety fault | Fault is cleared and an authorized reset is accepted |
| ST-07 | LINK_LOST | Safety communication is unavailable | Required communication is lost | Connection is restored and safety checks pass |

## 2. Events

- EV-01: Valid delivery assigned
- EV-02: Destination reached
- EV-03: Obstacle detected
- EV-04: Obstacle path confirmed clear
- EV-05: Delivery verified complete
- EV-06: Return destination reached
- EV-07: Critical chamber temperature detected
- EV-08: Emergency battery threshold reached
- EV-09: Required communication lost
- EV-10: Communication restored
- EV-11: Fault cleared and authorized reset accepted
- EV-12: Non-emergency low battery detected
- EV-13: Sensor fault detected

**State vs Event:** A state describes what the robot is currently doing. An event is something that happens and may cause the robot to change state.

## 3. Transition Table

| Current State | Event / Condition | Next State | Requirement ID | Valid? | Evidence |
|---|---|---|---|---|---|
| IDLE | Valid delivery assigned | NAVIGATING | FR-02 | Yes | TC-04 |
| IDLE | Direct delivery command without assignment | DELIVERING | FR-02 | No | TC-06 |
| NAVIGATING | Obstacle detected | AVOIDING_OBSTACLE | FR-04 | Yes | TC-05 |
| AVOIDING_OBSTACLE | Path confirmed clear | NAVIGATING | FR-04 | Yes | TC-05 |
| AVOIDING_OBSTACLE | Direct delivery-complete event | DELIVERING | FR-04 | No | TC-05 |
| NAVIGATING | Destination reached and checks pass | DELIVERING | FR-03 | Yes | TC-06 |
| DELIVERING | Delivery verified complete | RETURNING | FR-10 | Yes | TC-07 |
| RETURNING | Warehouse reached and checks pass | IDLE | FR-10 | Yes | TC-07 |
| NAVIGATING | Non-emergency low battery | RETURNING | FR-10 | Yes | TC-09 |
| AVOIDING_OBSTACLE | Emergency battery threshold reached | SAFE_MODE | FR-08 | Yes | TC-09 |
| DELIVERING | Emergency battery threshold reached | SAFE_MODE | FR-08 | Yes | TC-09 |
| Any active state | Critical chamber temperature detected | SAFE_MODE | FR-08 | Yes | TC-08 |
| Any active state | Emergency battery threshold reached | SAFE_MODE | FR-08 | Yes | TC-09 |
| Any active state | Required communication lost | LINK_LOST | FR-09 | Yes | TC-13 |
| LINK_LOST | Connection restored and safety checks pass | Previous safe state or SAFE_MODE | FR-09 | Conditional | TC-13 |
| SAFE_MODE | Fault cleared and authorized reset accepted | IDLE or RETURNING after assessment | SAF-01 | Conditional | TC-15 |
| SAFE_MODE | Fault still present | NAVIGATING | SAF-01 | No | TC-15 |
| Any active state | Critical sensor fault detected | SAFE_MODE | SAF-04 | Yes | TC-12 |

## 4. Invalid and Missing Transitions

1. **IDLE → DELIVERING:** Invalid because a delivery must be assigned and navigation completed first.
2. **AVOIDING_OBSTACLE → DELIVERING:** Invalid because the robot must confirm the path is clear and resume navigation.
3. **SAFE_MODE → NAVIGATING:** Invalid while a critical fault remains unresolved.
4. **Missing obstacle-resume transition:** If the path becomes clear, the robot must return to NAVIGATING; otherwise it may remain stuck.
5. **Critical battery during obstacle avoidance or delivery:** Emergency battery conditions must take priority and trigger SAFE_MODE within three seconds.
6. **Communication loss during movement:** The robot must stop normal movement and use its defined safe response. It must not continue without required safety confirmation.

## 5. Safety Rules

- Critical temperature or emergency battery conditions trigger SAFE_MODE within three seconds.
- The robot must not enter a railway crossing unless the barrier is confirmed open and no train is approaching.
- A communication or sensor failure must never be treated as proof that conditions are safe.
- SAFE_MODE can only be exited after the fault is cleared, safety checks pass, and an authorized reset is accepted.
- Every critical transition must be timestamped and logged
