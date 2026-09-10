# Customer API - Test Cases

## Test Cases - Customer

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-CUST-REG-001 | Customer Registration | Register with valid data | API is operational | 1. POST `/register`<br>2. Verify the response | `full_name=Nguyen Van A`<br>`phone_number=0901234567` | HTTP 201; registration is successful | High |
| TC-CUST-REG-002 | Customer Registration | Register with a valid email | API is operational | 1. POST `/register` | `full_name=Nguyen Van A`<br>`phone_number=0901234567`<br>`email=nguyenvana@gmail.com` | HTTP 201; registration is successful | High |
| TC-CUST-REG-003 | Customer Registration | Missing full_name | API is operational | 1. POST `/register` | Only phone_number is provided | Validation error is returned | High |
| TC-CUST-REG-004 | Customer Registration | Missing phone_number | API is operational | 1. POST `/register` | Only full_name is provided | Validation error is returned | High |
| TC-CUST-REG-005 | Customer Registration | Empty request body | API is operational | 1. POST `/register` | `{}` | Validation error is returned | High |
| TC-CUST-REG-006 | Customer Registration | full_name has an invalid data type | API is operational | 1. POST `/register` | `full_name=12345` | Request is rejected | Medium |
| TC-CUST-REG-007 | Customer Registration | phone_number has an invalid data type | API is operational | 1. POST `/register` | `phone_number=901234567` | Request is rejected if schema validation is applied | High |
| TC-CUST-REG-008 | Customer Registration | email has an invalid data type | API is operational | 1. POST `/register` | `email=12345` | Request is rejected | Medium |
| TC-CUST-REG-009 | Customer Registration | full_name is null | API is operational | 1. POST `/register` | `full_name=null` | Validation error is returned | High |
| TC-CUST-REG-010 | Customer Registration | phone_number is null | API is operational | 1. POST `/register` | `phone_number=null` | Validation error is returned | High |
| TC-CUST-PRO-001 | Customer Profile | Retrieve valid customer profile | Customer exists | 1. GET `/profile/101` | `customer_id=101` | HTTP 200; customer information is returned | High |
| TC-CUST-PRO-002 | Customer Profile | customer_id does not exist | API is operational | 1. GET `/profile/999999` | `customer_id=999999` | Non-existing profile is not returned; appropriate error is returned | High |
| TC-CUST-PRO-003 | Customer Profile | customer_id has an invalid data type | API is operational | 1. GET `/profile/ABC` | `customer_id=ABC` | Request is rejected | High |
| TC-CUST-PRO-004 | Customer Profile | customer_id is 0 | API is operational | 1. GET `/profile/0` | `customer_id=0` | YAML does not define a minimum; process according to implementation | Medium |
| TC-CUST-PRO-005 | Customer Profile | Negative customer_id | API is operational | 1. GET `/profile/-1` | `customer_id=-1` | YAML does not define a minimum; process according to implementation | Medium |
| TC-CUST-TRIP-001 | Create Trip | Create a trip with valid data | Customer exists | 1. POST `/trips` | `customer_id=101`<br>`pickup_address=123 Le Loi`<br>`destination_address=456 Nguyen Hue`<br>`vehicle_type=4-seater` | HTTP 201; trip is created successfully | Critical |
| TC-CUST-TRIP-002 | Create Trip | Create trip using CASH payment | Customer exists | 1. POST `/trips` | `payment_method=CASH` | HTTP 201 | High |
| TC-CUST-TRIP-003 | Create Trip | Create trip using WALLET payment | Customer exists | 1. POST `/trips` | `payment_method=WALLET` | HTTP 201 | High |
| TC-CUST-TRIP-004 | Create Trip | Create trip using CARD payment | Customer exists | 1. POST `/trips` | `payment_method=CARD` | HTTP 201 | High |
| TC-CUST-TRIP-005 | Create Trip | Do not provide payment_method | Customer exists | 1. POST `/trips` | No payment_method | Request is valid according to schema | Medium |
| TC-CUST-TRIP-006 | Create Trip | Missing customer_id | API is operational | 1. POST `/trips` | Remove customer_id | Validation error is returned | Critical |
| TC-CUST-TRIP-007 | Create Trip | Missing pickup_address | API is operational | 1. POST `/trips` | Remove pickup_address | Validation error is returned | Critical |
| TC-CUST-TRIP-008 | Create Trip | Missing destination_address | API is operational | 1. POST `/trips` | Remove destination_address | Validation error is returned | Critical |
| TC-CUST-TRIP-009 | Create Trip | Missing vehicle_type | API is operational | 1. POST `/trips` | Remove vehicle_type | Validation error is returned | Critical |
| TC-CUST-TRIP-010 | Create Trip | Invalid payment_method enum | API is operational | 1. POST `/trips` | `payment_method=BITCOIN` | Request is rejected | High |
| TC-CUST-TRIP-011 | Create Trip | customer_id has an invalid data type | API is operational | 1. POST `/trips` | `customer_id="101"` | Request is rejected | High |
| TC-CUST-TRIP-012 | Create Trip | Empty request body | API is operational | 1. POST `/trips` | `{}` | Validation error is returned | Critical |
| TC-CUST-TRIP-013 | Create Trip | customer_id does not exist | API is operational | 1. POST `/trips` | `customer_id=999999` | Trip is not created for a non-existing customer | Critical |
| TC-CUST-TRIP-014 | Create Trip | pickup_address is empty | API is operational | 1. POST `/trips` | `pickup_address=""` | YAML does not define minLength; Business Rule must be checked | High |
| TC-CUST-TRIP-015 | Create Trip | destination_address is empty | API is operational | 1. POST `/trips` | `destination_address=""` | YAML does not define minLength; Business Rule must be checked | High |
| TC-CUST-STATUS-001 | Trip Status | Retrieve valid trip status | Trip exists | 1. GET `/trips/5001` | `trip_id=5001` | HTTP 200; trip information is returned | High |
| TC-CUST-STATUS-002 | Trip Status | trip_id does not exist | API is operational | 1. GET `/trips/999999` | `trip_id=999999` | Non-existing trip is not returned; appropriate error is returned | High |
| TC-CUST-STATUS-003 | Trip Status | trip_id has an invalid data type | API is operational | 1. GET `/trips/ABC` | `trip_id=ABC` | Request is rejected | High |
| TC-CUST-STATUS-004 | Trip Status | trip_id is 0 | API is operational | 1. GET `/trips/0` | `trip_id=0` | YAML does not define a minimum; process according to implementation | Medium |
| TC-CUST-RATE-001 | Rating | Submit a 1-star rating | Valid trip exists | 1. POST `/ratings` | `trip_id=5001`<br>`customer_id=101`<br>`score=1` | HTTP 201; rating is submitted successfully | High |
| TC-CUST-RATE-002 | Rating | Submit a 5-star rating | Valid trip exists | 1. POST `/ratings` | `score=5` | HTTP 201; rating is submitted successfully | High |
| TC-CUST-RATE-003 | Rating | Submit a 3-star rating | Valid trip exists | 1. POST `/ratings` | `score=3` | HTTP 201 | Medium |
| TC-CUST-RATE-004 | Rating | score = 0 | API is operational | 1. POST `/ratings` | `score=0` | Request is rejected because it is below minimum=1 | High |
| TC-CUST-RATE-005 | Rating | score = 6 | API is operational | 1. POST `/ratings` | `score=6` | Request is rejected because it exceeds maximum=5 | High |
| TC-CUST-RATE-006 | Rating | Negative score | API is operational | 1. POST `/ratings` | `score=-1` | Request is rejected | High |
| TC-CUST-RATE-007 | Rating | Missing score | API is operational | 1. POST `/ratings` | Remove score | Validation error is returned | Critical |
| TC-CUST-RATE-008 | Rating | score has an invalid data type | API is operational | 1. POST `/ratings` | `score="5"` | Request is rejected | High |
| TC-CUST-RATE-009 | Rating | Missing trip_id | API is operational | 1. POST `/ratings` | Remove trip_id | Validation error is returned | High |
| TC-CUST-RATE-010 | Rating | Missing customer_id | API is operational | 1. POST `/ratings` | Remove customer_id | Validation error is returned | High |
| TC-CUST-RATE-011 | Rating | Rating includes a comment | Valid trip exists | 1. POST `/ratings` | `score=5`<br>`comment=Friendly driver and clean car` | HTTP 201; rating is submitted successfully | Medium |
| TC-CUST-RATE-012 | Rating | Empty comment | Valid trip exists | 1. POST `/ratings` | `score=5`<br>`comment=""` | Process according to implementation; comment is not required | Low |
| TC-CUST-RATE-013 | Rating | Empty request body | API is operational | 1. POST `/ratings` | `{}` | Validation error is returned | High |
