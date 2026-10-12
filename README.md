# SACDCS — Software Quality Engineering OEL

## Project Overview

The Smart Autonomous Cold-Chain Delivery & Control System (SACDCS) is a proposed system for managing autonomous robots that transport temperature-sensitive items. The system monitors temperature and battery conditions, manages robot navigation, detects obstacles, and responds to critical faults.

## Project Objectives

- Define functional and non-functional requirements.
- Manage change requests using version control.
- Model robot states and transitions.
- Identify system operations and operation schemas.
- Define constraints and formal rules.
- Connect requirements to tests through a Requirements Traceability Matrix (RTM).
- Document test cases and regression testing.

## Repository Structure

| Folder | Contents |
|---|---|
| `requirements/` | Functional and non-functional requirements |
| `change-log/` | Change requests and change history |
| `state-model/` | Robot states and transition rules |
| `operations/` | System operations and operation schemas |
| `constraints/` | Constraints, formal rules, and violations |
| `traceability/` | Requirements Traceability Matrix |
| `testing/` | Test cases and regression testing |

## Key Change Requests

- **CR-01:** Enter Safe Mode within 3 seconds of a critical temperature or battery condition.
- **CR-02:** Support at least 20 robots operating concurrently.
- **CR-03:** Require authentication and role-based authorization for control commands.

## Version Control

GitHub is used to store project documentation and maintain a history of changes through commits.

## Testing Status

Test cases are documented with expected results. Their execution status must be updated only after testing has been performed.

## Conclusion

This project applies software quality engineering techniques to requirements, change management, state modelling, operation design, constraints, traceability, and testing for SACDCS.

