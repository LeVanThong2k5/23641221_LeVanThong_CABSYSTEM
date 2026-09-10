# Driver API - Test Cases


## Test Cases - Driver
| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-DRV-STATUS-001 | Driver Status | Update driver status to AVAILABLE | Driver exists | 1. Send PUT `/status`<br>2. Verify the response | `driver_id=201`<br>`status=AVAILABLE` | HTTP 200; status is updated successfully | High |
| TC-DRV-STATUS-002 | Driver Status | Update driver status to BUSY | Driver exists | 1. Send PUT `/status`<br>2. Verify the response | `driver_id=201`<br>`status=BUSY` | HTTP 200; status is updated successfully | High |
| TC-DRV-STATUS-003 | Driver Status | Update driver status to OFFLINE | Driver exists | 1. Send PUT `/status`<br>2. Verify the response | `driver_id=201`<br>`status=OFFLINE` | HTTP 200; status is updated successfully | High |
| TC-DRV-STATUS-004 | Driver Status | Status is not included in the enum | API is operational | 1. Send PUT `/status` | `status=ONLINE` | Request is rejected | High |
| TC-DRV-STATUS-005 | Driver Status | Status is empty | API is operational | 1. Send PUT `/status` | `status=` | Request is rejected/validated according to implementation | High |
| TC-DRV-STATUS-006 | Driver Status | Missing driver_id | API is operational | 1. Send PUT `/status` | `status=AVAILABLE` | Validation error is returned | High |
| TC-DRV-STATUS-007 | Driver Status | Missing status | API is operational | 1. Send PUT `/status` | `driver_id=201` | Validation error is returned | High |
| TC-DRV-STATUS-008 | Driver Status | Empty request body | API is operational | 1. Send PUT `/status` | `{}` | Validation error is returned | High |
| TC-DRV-STATUS-009 | Driver Status | driver_id has an invalid data type | API is operational | 1. Send PUT `/status` | `driver_id="201"` | Request is rejected | High |
| TC-DRV-STATUS-010 | Driver Status | driver_id is 0 | API is operational | 1. Send PUT `/status` | `driver_id=0` | Process according to implementation; YAML does not define a minimum value | Medium |
| TC-DRV-STATUS-011 | Driver Status | Driver does not exist | API is operational | 1. Send PUT `/status` | `driver_id=999999`<br>`status=AVAILABLE` | Non-existing driver is not updated; an appropriate error is returned | High |
| TC-DRV-GPS-001 | GPS Location | Send valid GPS location | Driver exists | 1. Send POST `/location`<br>2. Verify the response | `driver_id=201`<br>`latitude=10.7769`<br>`longitude=106.7009` | HTTP 200; GPS location is recorded | High |
| TC-DRV-GPS-002 | GPS Location | Latitude is 0 | Driver exists | 1. Send POST `/location` | `latitude=0`<br>`longitude=106.7009` | API processes successfully according to number schema | Medium |
| TC-DRV-GPS-003 | GPS Location | Longitude is 0 | Driver exists | 1. Send POST `/location` | `latitude=10.7769`<br>`longitude=0` | API processes successfully according to number schema | Medium |
| TC-DRV-GPS-004 | GPS Location | Negative latitude | Driver exists | 1. Send POST `/location` | `latitude=-10.7769` | API processes according to implementation; YAML does not define min/max | Medium |
| TC-DRV-GPS-005 | GPS Location | Negative longitude | Driver exists | 1. Send POST `/location` | `longitude=-106.7009` | API processes according to implementation; YAML does not define min/max | Medium |
| TC-DRV-GPS-006 | GPS Location | Latitude and longitude contain decimal values | Driver exists | 1. Send POST `/location` | `latitude=10.77691234`<br>`longitude=106.70091234` | HTTP 200 if data is valid | Medium |
| TC-DRV-GPS-007 | GPS Location | Missing driver_id | API is operational | 1. Send POST `/location` | `latitude=10.7769`<br>`longitude=106.7009` | Validation error is returned | High |
| TC-DRV-GPS-008 | GPS Location | Missing latitude | API is operational | 1. Send POST `/location` | `driver_id=201`<br>`longitude=106.7009` | Validation error is returned | High |
| TC-DRV-GPS-009 | GPS Location | Missing longitude | API is operational | 1. Send POST `/location` | `driver_id=201`<br>`latitude=10.7769` | Validation error is returned | High |
| TC-DRV-GPS-010 | GPS Location | Empty request body | API is operational | 1. Send POST `/location` | `{}` | Validation error is returned | High |
| TC-DRV-GPS-011 | GPS Location | latitude has an invalid data type | API is operational | 1. Send POST `/location` | `latitude="ABC"` | Request is rejected | High |
| TC-DRV-GPS-012 | GPS Location | longitude has an invalid data type | API is operational | 1. Send POST `/location` | `longitude="ABC"` | Request is rejected | High |
| TC-DRV-GPS-013 | GPS Location | GPS is unavailable on the device | Driver App is running but GPS is unavailable | 1. Send location request when GPS is unavailable | GPS unavailable | App does not send invalid GPS data; error is handled according to implementation | High |
| TC-DRV-GPS-014 | GPS Location | Network timeout while sending GPS data | Driver has GPS signal | 1. Send POST `/location`<br>2. Simulate timeout | Valid GPS data | Timeout is handled; application does not crash | High |
| TC-DRV-RESP-001 | Trip Response | Driver accepts a trip | Trip is waiting for driver response | 1. POST `/trips/5001/respond` | `driver_id=201`<br>`accepted=true` | HTTP 200; trip acceptance is successful | Critical |
| TC-DRV-RESP-002 | Trip Response | Driver rejects a trip | Trip is waiting for driver response | 1. POST `/trips/5001/respond` | `driver_id=201`<br>`accepted=false` | HTTP 200; trip rejection is successful | High |
| TC-DRV-RESP-003 | Trip Response | Missing driver_id | Trip exists | 1. POST respond | `accepted=true` | Validation error is returned | High |
| TC-DRV-RESP-004 | Trip Response | Missing accepted | Trip exists | 1. POST respond | `driver_id=201` | Validation error is returned | High |
| TC-DRV-RESP-005 | Trip Response | accepted has an invalid data type | Trip exists | 1. POST respond | `accepted="true"` | Request is rejected | High |
| TC-DRV-RESP-006 | Trip Response | accepted is null | Trip exists | 1. POST respond | `accepted=null` | Request is rejected/validated | High |
| TC-DRV-RESP-007 | Trip Response | trip_id has an invalid data type | API is operational | 1. POST `/trips/ABC/respond` | `trip_id=ABC` | Request is rejected | High |
| TC-DRV-RESP-008 | Trip Response | trip_id does not exist | API is operational | 1. POST respond | `trip_id=999999` | Non-existing trip is not processed; appropriate error is returned | High |
| TC-DRV-RESP-009 | Trip Response | driver_id does not exist | API is operational | 1. POST respond | `driver_id=999999`<br>`accepted=true` | Response from non-existing driver is not accepted | High |
| TC-DRV-RESP-010 | Trip Response | Request timeout | Backend is unstable | 1. POST respond<br>2. Simulate timeout | Valid request | Client handles timeout; trip status is not incorrectly updated | High |

