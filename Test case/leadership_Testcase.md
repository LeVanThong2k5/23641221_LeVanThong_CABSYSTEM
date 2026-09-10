# Leadership API - Test Cases

## Test Cases - Leadership

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-LEAD-001 | Dashboard | Retrieve dashboard successfully | API is operational | 1. GET `/reports/dashboard`<br>2. Verify the response | No input | HTTP 200; dashboard data is returned | High |
| TC-LEAD-002 | Dashboard | Verify total_trips | Trips data exists | 1. GET dashboard<br>2. Verify the field | `total_trips=5000` | Field exists and is an integer | High |
| TC-LEAD-003 | Dashboard | Verify completed_trips | Completed trip data exists | 1. GET dashboard | `completed_trips=4600` | Field exists and is an integer | High |
| TC-LEAD-004 | Dashboard | Verify total_revenue_vnd | Revenue data exists | 1. GET dashboard | `total_revenue_vnd=650000000` | Field exists and is a number | High |
| TC-LEAD-005 | Dashboard | Verify active_drivers_count | Active driver data exists | 1. GET dashboard | `active_drivers_count=120` | Field exists and is an integer | High |
| TC-LEAD-006 | Dashboard | System has no data | Database is empty | 1. GET dashboard | No records | API still returns a valid response according to implementation | Medium |
| TC-LEAD-007 | Dashboard | All values are 0 | Metrics contain zero values | 1. GET dashboard | `0,0,0,0` | All fields return correct data types and values | Medium |
| TC-LEAD-008 | Dashboard | Very large revenue value | Large data set exists | 1. GET dashboard | `total_revenue_vnd=999999999999` | API does not overflow; valid number is returned | Medium |
| TC-LEAD-009 | Dashboard | Database timeout | Database is unavailable/timeout | 1. GET dashboard | N/A | API returns an appropriate error; request does not hang indefinitely | High |
| TC-LEAD-010 | Dashboard | Backend exception | Backend throws an exception | 1. GET dashboard | N/A | API returns an appropriate HTTP 5xx error; server does not crash | High |
| TC-LEAD-011 | Dashboard | Network timeout | Network is unstable | 1. GET dashboard<br>2. Simulate timeout | N/A | Client handles timeout appropriately | Medium |
| TC-LEAD-012 | Dashboard | Response contains incorrect data type | Backend returns invalid schema data | 1. GET dashboard<br>2. Validate response | `total_trips="5000"` | Schema validation detects incorrect data type if validation is applied | High |
