# Notification Provider API - Test Cases

## Test Cases - Notification Provider

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-NOTI-001 | Send Notification | Send PUSH notification to CUSTOMER | Customer exists; provider is operational | 1. POST `/notifications/send`<br>2. Verify the response | `recipient_id=101`<br>`recipient_type=CUSTOMER`<br>`channel=PUSH` | HTTP 200; notification is sent successfully | High |
| TC-NOTI-002 | Send Notification | Send SMS notification to CUSTOMER | Customer exists | 1. POST notification | CUSTOMER + SMS | HTTP 200; notification is sent successfully | High |
| TC-NOTI-003 | Send Notification | Send EMAIL notification to CUSTOMER | Customer exists | 1. POST notification | CUSTOMER + EMAIL | HTTP 200; notification is sent successfully | High |
| TC-NOTI-004 | Send Notification | Send PUSH notification to DRIVER | Driver exists | 1. POST notification | DRIVER + PUSH | HTTP 200; notification is sent successfully | High |
| TC-NOTI-005 | Send Notification | Send SMS notification to DRIVER | Driver exists | 1. POST notification | DRIVER + SMS | HTTP 200; notification is sent successfully | High |
| TC-NOTI-006 | Send Notification | Send EMAIL notification to DRIVER | Driver exists | 1. POST notification | DRIVER + EMAIL | HTTP 200; notification is sent successfully | High |
| TC-NOTI-007 | Send Notification | recipient_type has an invalid enum value | Provider is operational | 1. POST notification | `recipient_type=ADMIN` | Request is rejected | High |
| TC-NOTI-008 | Send Notification | channel has an invalid enum value | Provider is operational | 1. POST notification | `channel=ZALO` | Request is rejected | High |
| TC-NOTI-009 | Send Notification | Missing recipient_id | Provider is operational | 1. POST notification | Remove `recipient_id` | Validation error is returned | High |
| TC-NOTI-010 | Send Notification | Missing recipient_type | Provider is operational | 1. POST notification | Remove `recipient_type` | Validation error is returned | High |
| TC-NOTI-011 | Send Notification | Missing channel | Provider is operational | 1. POST notification | Remove `channel` | Validation error is returned | High |
| TC-NOTI-012 | Send Notification | Missing title | Provider is operational | 1. POST notification | Remove `title` | Validation error is returned | High |
| TC-NOTI-013 | Send Notification | Missing content | Provider is operational | 1. POST notification | Remove `content` | Validation error is returned | High |
| TC-NOTI-014 | Send Notification | Empty request body | Provider is operational | 1. POST notification | `{}` | Validation error is returned | High |
| TC-NOTI-015 | Send Notification | recipient_id has an invalid data type | Provider is operational | 1. POST notification | `recipient_id="101"` | Request is rejected | High |
| TC-NOTI-016 | Send Notification | recipient_id is 0 | Provider is operational | 1. POST notification | `recipient_id=0` | Process according to implementation; YAML does not define a minimum value | Medium |
| TC-NOTI-017 | Send Notification | Negative recipient_id | Provider is operational | 1. POST notification | `recipient_id=-1` | Process according to implementation; YAML only defines integer type | Medium |
| TC-NOTI-018 | Send Notification | Empty title | Provider is operational | 1. POST notification | `title=""` | Process according to implementation; YAML does not define minLength | Medium |
| TC-NOTI-019 | Send Notification | Empty content | Provider is operational | 1. POST notification | `content=""` | Process according to implementation; YAML does not define minLength | Medium |
| TC-NOTI-020 | Send Notification | Provider timeout | Provider does not respond | 1. POST notification<br>2. Simulate timeout | Valid payload | Timeout is handled; service does not crash | High |
| TC-NOTI-021 | Send Notification | Third-party notification service unavailable | Third-party provider is unavailable | 1. POST notification | Valid payload | API returns an appropriate error; it does not falsely report success | Critical |
| TC-NOTI-022 | Send Notification | Network failure | Network connection is interrupted | 1. POST notification | Valid payload | Client/service handles the network error | High |
