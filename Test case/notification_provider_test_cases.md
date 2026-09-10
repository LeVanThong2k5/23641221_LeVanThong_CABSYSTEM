# Notification Provider API - Test Cases

## Test Cases

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-NOTI-001 | Send Notification | Gửi PUSH cho CUSTOMER | Customer tồn tại; provider hoạt động | 1. POST `/notifications/send`<br>2. Kiểm tra response | `recipient_id=101`<br>`recipient_type=CUSTOMER`<br>`channel=PUSH` | HTTP 200; gửi thông báo thành công | High |
| TC-NOTI-002 | Send Notification | Gửi SMS cho CUSTOMER | Customer tồn tại | 1. POST notification | CUSTOMER + SMS | HTTP 200; gửi thành công | High |
| TC-NOTI-003 | Send Notification | Gửi EMAIL cho CUSTOMER | Customer tồn tại | 1. POST notification | CUSTOMER + EMAIL | HTTP 200; gửi thành công | High |
| TC-NOTI-004 | Send Notification | Gửi PUSH cho DRIVER | Driver tồn tại | 1. POST notification | DRIVER + PUSH | HTTP 200; gửi thành công | High |
| TC-NOTI-005 | Send Notification | Gửi SMS cho DRIVER | Driver tồn tại | 1. POST notification | DRIVER + SMS | HTTP 200; gửi thành công | High |
| TC-NOTI-006 | Send Notification | Gửi EMAIL cho DRIVER | Driver tồn tại | 1. POST notification | DRIVER + EMAIL | HTTP 200; gửi thành công | High |
| TC-NOTI-007 | Send Notification | recipient_type sai enum | Provider hoạt động | 1. POST notification | `recipient_type=ADMIN` | Request bị reject | High |
| TC-NOTI-008 | Send Notification | channel sai enum | Provider hoạt động | 1. POST notification | `channel=ZALO` | Request bị reject | High |
| TC-NOTI-009 | Send Notification | recipient_id bị thiếu | Provider hoạt động | 1. POST notification | Bỏ `recipient_id` | Validation error | High |
| TC-NOTI-010 | Send Notification | recipient_type bị thiếu | Provider hoạt động | 1. POST notification | Bỏ `recipient_type` | Validation error | High |
| TC-NOTI-011 | Send Notification | channel bị thiếu | Provider hoạt động | 1. POST notification | Bỏ `channel` | Validation error | High |
| TC-NOTI-012 | Send Notification | title bị thiếu | Provider hoạt động | 1. POST notification | Bỏ `title` | Validation error | High |
| TC-NOTI-013 | Send Notification | content bị thiếu | Provider hoạt động | 1. POST notification | Bỏ `content` | Validation error | High |
| TC-NOTI-014 | Send Notification | Body rỗng | Provider hoạt động | 1. POST notification | `{}` | Validation error | High |
| TC-NOTI-015 | Send Notification | recipient_id sai datatype | Provider hoạt động | 1. POST notification | `recipient_id="101"` | Request bị reject | High |
| TC-NOTI-016 | Send Notification | recipient_id bằng 0 | Provider hoạt động | 1. POST notification | `recipient_id=0` | Xử lý theo implementation; YAML không định nghĩa minimum | Medium |
| TC-NOTI-017 | Send Notification | recipient_id âm | Provider hoạt động | 1. POST notification | `recipient_id=-1` | Xử lý theo implementation; YAML chỉ quy định integer | Medium |
| TC-NOTI-018 | Send Notification | title rỗng | Provider hoạt động | 1. POST notification | `title=""` | Xử lý theo implementation; YAML không khai báo minLength | Medium |
| TC-NOTI-019 | Send Notification | content rỗng | Provider hoạt động | 1. POST notification | `content=""` | Xử lý theo implementation; YAML không khai báo minLength | Medium |
| TC-NOTI-020 | Send Notification | Gửi notification khi provider timeout | Provider không phản hồi | 1. POST notification<br>2. Giả lập timeout | Valid payload | Timeout được xử lý; không làm crash service | High |
| TC-NOTI-021 | Send Notification | Third-party notification service unavailable | Provider bên thứ ba unavailable | 1. POST notification | Valid payload | API trả lỗi phù hợp; không báo thành công giả | Critical |
| TC-NOTI-022 | Send Notification | Network failure | Network bị ngắt | 1. POST notification | Valid payload | Client/service xử lý network error | High |
