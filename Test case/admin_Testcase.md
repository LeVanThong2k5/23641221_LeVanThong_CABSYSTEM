# Admin API - Test Cases

## Test Cases - admin

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-ADMIN-001 | Audit Log | Retrieve all audit logs | Admin API is operational | 1. Send GET `/audit-logs`<br>2. Verify the response | No query parameters | HTTP 200; audit log list is returned | High |
| TC-ADMIN-002 | Audit Log | Retrieve audit logs by user_id | API is operational; user_id exists | 1. Send GET `/audit-logs?user_id=901`<br>2. Verify the response | `user_id=901` | HTTP 200; results are filtered by user_id | High |
| TC-ADMIN-003 | Audit Log | Retrieve audit logs by action | API is operational | 1. Send GET `/audit-logs?action=CANCEL_TRIP`<br>2. Verify the response | `action=CANCEL_TRIP` | HTTP 200; results are filtered by action | High |
| TC-ADMIN-004 | Audit Log | Filter audit logs by user_id and action simultaneously | API is operational | 1. Send GET request<br>2. Verify the response | `user_id=901`<br>`action=CANCEL_TRIP` | HTTP 200; results match both filter conditions | High |
| TC-ADMIN-005 | Audit Log | user_id is 0 | API is operational | 1. Send GET request<br>2. Verify the response | `user_id=0` | API processes the request according to implementation; YAML does not define a minimum value | Medium |
| TC-ADMIN-006 | Audit Log | Negative user_id | API is operational | 1. Send GET request<br>2. Verify the response | `user_id=-1` | API processes the request according to implementation; YAML only defines integer type | Medium |
| TC-ADMIN-007 | Audit Log | user_id has an invalid data type | API is operational | 1. Send GET request | `user_id=ABC` | Request is rejected if API schema validation is applied | High |
| TC-ADMIN-008 | Audit Log | user_id is a decimal number | API is operational | 1. Send GET request | `user_id=901.5` | Request is rejected if integer validation is applied | Medium |
| TC-ADMIN-009 | Audit Log | action is empty | API is operational | 1. Send GET request | `action=` | API processes the request according to implementation; YAML does not define a non-empty rule | Low |
| TC-ADMIN-010 | Audit Log | action contains special characters | API is operational | 1. Send GET request | `action=@@@###` | API does not crash; filter is processed according to implementation | Medium |
| TC-ADMIN-011 | Audit Log | user_id does not exist | API is operational | 1. Send GET request | `user_id=999999` | HTTP 200 with an empty list or behavior according to implementation | Medium |
| TC-ADMIN-012 | Audit Log | API timeout | Backend/database does not respond | 1. Send GET request<br>2. Wait for timeout | Valid request | API returns an appropriate timeout error; request does not hang indefinitely | High |
| TC-ADMIN-013 | Audit Log | Database unavailable | Database service is down | 1. Send GET request | Valid request | API returns an appropriate HTTP 5xx error; system does not crash | High |
| TC-ADMIN-014 | Audit Log | Network connection lost during request | API is operational | 1. Send GET request<br>2. Disconnect network | Valid request | Client receives a network error/timeout; no incorrect data is created | Medium |
