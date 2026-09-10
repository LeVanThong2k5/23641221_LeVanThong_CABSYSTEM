# Operator API - Test Cases

## Test Cases - Operator

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-OP-TRIP-001 | Active Trips | Retrieve all active trips | Operator/API is operational | 1. GET `/trips`<br>2. Verify the response | No status parameter | HTTP 200; trip list is returned | High |
| TC-OP-TRIP-002 | Active Trips | Filter trips by SEARCHING status | SEARCHING trips exist | 1. GET `/trips?status=SEARCHING` | `status=SEARCHING` | HTTP 200; matching results are returned | High |
| TC-OP-TRIP-003 | Active Trips | Filter by another status | API is operational | 1. GET `/trips?status=BUSY` | `status=BUSY` | API processes according to implementation; YAML does not define a status enum | Medium |
| TC-OP-TRIP-004 | Active Trips | status is empty | API is operational | 1. GET `/trips?status=` | `status=` | API processes according to implementation | Low |
| TC-OP-TRIP-005 | Active Trips | status contains special characters | API is operational | 1. GET `/trips` | `status=@@@` | API does not crash; filter is processed appropriately | Medium |
| TC-OP-TRIP-006 | Active Trips | No active trips exist | Database has no active trips | 1. GET `/trips` | N/A | HTTP 200; empty list or response according to implementation | Medium |
| TC-OP-TRIP-007 | Active Trips | Database timeout | Database is unavailable | 1. GET `/trips` | N/A | API returns an appropriate error; request does not hang | High |
| TC-OP-TRIP-008 | Active Trips | Network timeout | Network is unstable | 1. GET `/trips` | N/A | Client handles timeout | Medium |
| TC-OP-CANCEL-001 | Force Cancel | Operator cancels a valid trip | Trip exists; operator exists | 1. POST `/trips/5001/cancel`<br>2. Verify the response | `operator_id=901`<br>`reason=Driver vehicle broke down during trip` | HTTP 200; trip cancellation is successful | Critical |
| TC-OP-CANCEL-002 | Force Cancel | Missing operator_id | Trip exists | 1. POST cancel | Only `reason` is provided | Validation error is returned | Critical |
| TC-OP-CANCEL-003 | Force Cancel | Missing reason | Trip exists | 1. POST cancel | Only `operator_id` is provided | Validation error is returned | Critical |
| TC-OP-CANCEL-004 | Force Cancel | Empty request body | Trip exists | 1. POST cancel | `{}` | Validation error is returned | Critical |
| TC-OP-CANCEL-005 | Force Cancel | operator_id has an invalid data type | Trip exists | 1. POST cancel | `operator_id="901"` | Request is rejected | High |
| TC-OP-CANCEL-006 | Force Cancel | operator_id is 0 | Trip exists | 1. POST cancel | `operator_id=0` | Process according to implementation; YAML does not define a minimum value | Medium |
| TC-OP-CANCEL-007 | Force Cancel | Negative operator_id | Trip exists | 1. POST cancel | `operator_id=-1` | Process according to implementation | Medium |
| TC-OP-CANCEL-008 | Force Cancel | trip_id has an invalid data type | API is operational | 1. POST `/trips/ABC/cancel` | `trip_id=ABC` | Request is rejected | High |
| TC-OP-CANCEL-009 | Force Cancel | trip_id is 0 | API is operational | 1. POST `/trips/0/cancel` | `trip_id=0` | Process according to implementation; YAML does not define a minimum value | Medium |
| TC-OP-CANCEL-010 | Force Cancel | trip_id does not exist | API is operational | 1. POST cancel | `trip_id=999999` | Non-existing trip is not cancelled; appropriate error is returned | Critical |
| TC-OP-CANCEL-011 | Force Cancel | reason is empty | Trip exists | 1. POST cancel | `reason=""` | Process according to implementation; YAML does not define minLength | Medium |
| TC-OP-CANCEL-012 | Force Cancel | reason is very long | Trip exists | 1. POST cancel | Reason exceeds system limit if one exists | Process according to implementation; YAML does not define maxLength | Medium |
| TC-OP-CANCEL-013 | Force Cancel | Cancel a completed trip | Trip status is COMPLETED | 1. POST cancel | Valid operator + reason | Trip must not be changed against business rules | Critical |
| TC-OP-CANCEL-014 | Force Cancel | Cancel an already cancelled trip | Trip status is CANCELLED | 1. POST cancel | Valid operator + reason | No invalid state is created; idempotency/business rule is handled | High |
| TC-OP-CANCEL-015 | Force Cancel | Send cancellation request twice | Trip exists | 1. POST cancel once<br>2. POST cancel again | Same trip/operator/reason | No inconsistent trip state or duplicate effect occurs | Critical |
| TC-OP-CANCEL-016 | Force Cancel | Backend timeout | API does not respond | 1. POST cancel<br>2. Simulate timeout | Valid request | Timeout is handled; trip is not partially or incorrectly updated | High |
