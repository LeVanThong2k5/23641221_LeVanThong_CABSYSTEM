# Payment Provider API - Test Cases
## Test Cases - Payment

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-PAY-001 | Payment Callback | Successful payment callback | Payment provider is operational; trip exists | 1. POST `/webhook/callback`<br>2. Verify the response | `partner_transaction_id=MOMO_20260903_998877`<br>`trip_id=5001`<br>`amount=65000`<br>`status=SUCCESS` | HTTP 200; payment result is recorded successfully | Critical |
| TC-PAY-002 | Payment Callback | Failed payment callback | Payment provider is operational; trip exists | 1. POST callback | `partner_transaction_id=MOMO_20260903_998878`<br>`trip_id=5001`<br>`amount=65000`<br>`status=FAILED` | HTTP 200; failed payment is recorded | Critical |
| TC-PAY-003 | Payment Callback | Missing partner_transaction_id | API is operational | 1. POST callback | Remove `partner_transaction_id` | Validation error is returned | Critical |
| TC-PAY-004 | Payment Callback | Missing trip_id | API is operational | 1. POST callback | Remove `trip_id` | Validation error is returned | Critical |
| TC-PAY-005 | Payment Callback | Missing status | API is operational | 1. POST callback | Remove `status` | Validation error is returned | Critical |
| TC-PAY-006 | Payment Callback | Missing amount | API is operational | 1. POST callback | Remove `amount` | Validation error is returned | Critical |
| TC-PAY-007 | Payment Callback | Empty request body | API is operational | 1. POST callback | `{}` | Validation error is returned | Critical |
| TC-PAY-008 | Payment Callback | status=SUCCESS | API is operational | 1. POST callback | `status=SUCCESS` | Request is valid; HTTP 200 if all other fields are valid | Critical |
| TC-PAY-009 | Payment Callback | status=FAILED | API is operational | 1. POST callback | `status=FAILED` | Request is valid; HTTP 200 if all other fields are valid | Critical |
| TC-PAY-010 | Payment Callback | Invalid status enum | API is operational | 1. POST callback | `status=PENDING` | Request is rejected | Critical |
| TC-PAY-011 | Payment Callback | Empty status | API is operational | 1. POST callback | `status=""` | Request is rejected/validated | High |
| TC-PAY-012 | Payment Callback | partner_transaction_id has an invalid data type | API is operational | 1. POST callback | `partner_transaction_id=12345` | Request is rejected | High |
| TC-PAY-013 | Payment Callback | trip_id has an invalid data type | API is operational | 1. POST callback | `trip_id="5001"` | Request is rejected | High |
| TC-PAY-014 | Payment Callback | amount has an invalid data type | API is operational | 1. POST callback | `amount="65000"` | Request is rejected | High |
| TC-PAY-015 | Payment Callback | amount is 0 | API is operational | 1. POST callback | `amount=0` | YAML does not define a minimum; process according to Business Rule/implementation | High |
| TC-PAY-016 | Payment Callback | Negative amount | API is operational | 1. POST callback | `amount=-1000` | YAML does not define a minimum; Business Rule must be confirmed | High |
| TC-PAY-017 | Payment Callback | Decimal amount | API is operational | 1. POST callback | `amount=65000.50` | Valid according to `number` schema if permitted by business rules | Medium |
| TC-PAY-018 | Payment Callback | trip_id is 0 | API is operational | 1. POST callback | `trip_id=0` | YAML does not define a minimum; process according to implementation | Medium |
| TC-PAY-019 | Payment Callback | Negative trip_id | API is operational | 1. POST callback | `trip_id=-1` | YAML does not define a minimum; process according to implementation | Medium |
| TC-PAY-020 | Payment Callback | Empty transaction ID | API is operational | 1. POST callback | `partner_transaction_id=""` | YAML does not define minLength; Business Rule must be checked | High |
| TC-PAY-021 | Payment Callback | trip_id does not exist | API is operational | 1. POST callback | `trip_id=999999` | Payment is not recorded for a non-existing trip; appropriate error is returned | Critical |
| TC-PAY-022 | Payment Callback | Duplicate transaction ID | Transaction has already been processed | 1. Send callback once<br>2. Send the same transaction callback again | Same transaction ID | Payment is not recorded twice; idempotency is maintained | Critical |
| TC-PAY-023 | Payment Callback | Same transaction changes from SUCCESS to FAILED | Transaction has already been marked SUCCESS | 1. Send SUCCESS<br>2. Send FAILED using the same transaction ID | Same transaction ID | Payment status does not incorrectly move backward against business rules | Critical |
| TC-PAY-024 | Payment Callback | Payment provider timeout | Backend is unavailable | 1. POST callback<br>2. Simulate timeout | Valid callback | Timeout is handled; retry does not create duplicate payment | High |
| TC-PAY-025 | Payment Callback | Database unavailable | Database is unavailable | 1. POST callback | Valid callback | API returns an appropriate error; incomplete data is not recorded | Critical |
| TC-PAY-026 | Payment Callback | Network interruption | Network is disconnected | 1. POST callback<br>2. Disconnect network | Valid callback | Request fails/times out; retry does not create duplicate payment | High |
