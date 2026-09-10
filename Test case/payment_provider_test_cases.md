# Payment Provider API - Test Cases

## Test Cases - Payment

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-PAY-001 | Payment Callback | Callback thanh toán SUCCESS | Payment provider hoạt động; trip tồn tại | 1. POST `/webhook/callback`<br>2. Kiểm tra response | `partner_transaction_id=MOMO_20260903_998877`<br>`trip_id=5001`<br>`amount=65000`<br>`status=SUCCESS` | HTTP 200; ghi nhận kết quả thanh toán | Critical |
| TC-PAY-002 | Payment Callback | Callback thanh toán FAILED | Payment provider hoạt động; trip tồn tại | 1. POST callback | `partner_transaction_id=MOMO_20260903_998878`<br>`trip_id=5001`<br>`amount=65000`<br>`status=FAILED` | HTTP 200; ghi nhận thanh toán thất bại | Critical |
| TC-PAY-003 | Payment Callback | Thiếu partner_transaction_id | API hoạt động | 1. POST callback | Bỏ `partner_transaction_id` | Validation error | Critical |
| TC-PAY-004 | Payment Callback | Thiếu trip_id | API hoạt động | 1. POST callback | Bỏ `trip_id` | Validation error | Critical |
| TC-PAY-005 | Payment Callback | Thiếu status | API hoạt động | 1. POST callback | Bỏ `status` | Validation error | Critical |
| TC-PAY-006 | Payment Callback | Thiếu amount | API hoạt động | 1. POST callback | Bỏ `amount` | Validation error | Critical |
| TC-PAY-007 | Payment Callback | Body rỗng | API hoạt động | 1. POST callback | `{}` | Validation error | Critical |
| TC-PAY-008 | Payment Callback | status=SUCCESS | API hoạt động | 1. POST callback | `status=SUCCESS` | Request hợp lệ; HTTP 200 nếu các field còn lại hợp lệ | Critical |
| TC-PAY-009 | Payment Callback | status=FAILED | API hoạt động | 1. POST callback | `status=FAILED` | Request hợp lệ; HTTP 200 nếu các field còn lại hợp lệ | Critical |
| TC-PAY-010 | Payment Callback | status sai enum | API hoạt động | 1. POST callback | `status=PENDING` | Request bị reject | Critical |
| TC-PAY-011 | Payment Callback | status rỗng | API hoạt động | 1. POST callback | `status=""` | Request bị reject/validation | High |
| TC-PAY-012 | Payment Callback | partner_transaction_id sai datatype | API hoạt động | 1. POST callback | `partner_transaction_id=12345` | Request bị reject | High |
| TC-PAY-013 | Payment Callback | trip_id sai datatype | API hoạt động | 1. POST callback | `trip_id="5001"` | Request bị reject | High |
| TC-PAY-014 | Payment Callback | amount sai datatype | API hoạt động | 1. POST callback | `amount="65000"` | Request bị reject | High |
| TC-PAY-015 | Payment Callback | amount bằng 0 | API hoạt động | 1. POST callback | `amount=0` | YAML không định nghĩa minimum; xử lý theo Business Rule/implementation | High |
| TC-PAY-016 | Payment Callback | amount âm | API hoạt động | 1. POST callback | `amount=-1000` | YAML không định nghĩa minimum; cần xác nhận Business Rule | High |
| TC-PAY-017 | Payment Callback | amount dạng số thập phân | API hoạt động | 1. POST callback | `amount=65000.50` | Hợp lệ theo schema `number`, nếu business rule cho phép | Medium |
| TC-PAY-018 | Payment Callback | trip_id bằng 0 | API hoạt động | 1. POST callback | `trip_id=0` | YAML không định nghĩa minimum; xử lý theo implementation | Medium |
| TC-PAY-019 | Payment Callback | trip_id âm | API hoạt động | 1. POST callback | `trip_id=-1` | YAML không định nghĩa minimum; xử lý theo implementation | Medium |
| TC-PAY-020 | Payment Callback | transaction ID rỗng | API hoạt động | 1. POST callback | `partner_transaction_id=""` | YAML không khai báo minLength; cần kiểm tra Business Rule | High |
| TC-PAY-021 | Payment Callback | trip_id không tồn tại | API hoạt động | 1. POST callback | `trip_id=999999` | Không ghi nhận thanh toán cho trip không tồn tại; trả lỗi phù hợp | Critical |
| TC-PAY-022 | Payment Callback | Transaction ID trùng | Transaction đã được xử lý | 1. Gửi callback lần 1<br>2. Gửi lại callback cùng transaction ID | Same transaction ID | Không ghi nhận thanh toán hai lần; đảm bảo idempotency | Critical |
| TC-PAY-023 | Payment Callback | Cùng transaction SUCCESS rồi FAILED | Transaction đã SUCCESS | 1. Gửi SUCCESS<br>2. Gửi FAILED cùng transaction | Same transaction ID | Không làm trạng thái thanh toán chuyển ngược trái business rule | Critical |
| TC-PAY-024 | Payment Callback | Payment provider timeout | Backend unavailable | 1. POST callback<br>2. Giả lập timeout | Valid callback | Timeout được xử lý; không tạo duplicate khi retry | High |
| TC-PAY-025 | Payment Callback | Database unavailable | Database unavailable | 1. POST callback | Valid callback | API trả lỗi phù hợp; không ghi nhận dữ liệu không hoàn chỉnh | Critical |
| TC-PAY-026 | Payment Callback | Network interruption | Network bị ngắt | 1. POST callback<br>2. Ngắt network | Valid callback | Request thất bại/timeout; retry không gây duplicate | High |
