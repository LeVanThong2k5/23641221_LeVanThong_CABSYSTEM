# Operator API - Test Cases

## Test Cases - Operator

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-OP-TRIP-001 | Active Trips | Lấy toàn bộ chuyến đang diễn ra | Operator/API hoạt động | 1. GET `/trips`<br>2. Kiểm tra response | Không truyền status | HTTP 200; trả danh sách chuyến | High |
| TC-OP-TRIP-002 | Active Trips | Filter chuyến theo SEARCHING | Có trip SEARCHING | 1. GET `/trips?status=SEARCHING` | `status=SEARCHING` | HTTP 200; trả kết quả phù hợp filter | High |
| TC-OP-TRIP-003 | Active Trips | Filter bằng status khác | API hoạt động | 1. GET `/trips?status=BUSY` | `status=BUSY` | API xử lý theo implementation; YAML không enum status | Medium |
| TC-OP-TRIP-004 | Active Trips | status rỗng | API hoạt động | 1. GET `/trips?status=` | `status=` | API xử lý theo implementation | Low |
| TC-OP-TRIP-005 | Active Trips | status chứa ký tự đặc biệt | API hoạt động | 1. GET `/trips` | `status=@@@` | API không crash; xử lý filter phù hợp | Medium |
| TC-OP-TRIP-006 | Active Trips | Không có trip đang hoạt động | Database không có active trip | 1. GET `/trips` | N/A | HTTP 200; trả danh sách rỗng hoặc response theo implementation | Medium |
| TC-OP-TRIP-007 | Active Trips | Database timeout | Database unavailable | 1. GET `/trips` | N/A | API trả lỗi phù hợp; không treo | High |
| TC-OP-TRIP-008 | Active Trips | Network timeout | Network không ổn định | 1. GET `/trips` | N/A | Client xử lý timeout | Medium |
| TC-OP-CANCEL-001 | Force Cancel | Operator hủy trip hợp lệ | Trip tồn tại; operator tồn tại | 1. POST `/trips/5001/cancel`<br>2. Kiểm tra response | `operator_id=901`<br>`reason=Tài xế hư xe giữa đường` | HTTP 200; hủy chuyến thành công | Critical |
| TC-OP-CANCEL-002 | Force Cancel | Thiếu operator_id | Trip tồn tại | 1. POST cancel | Chỉ có `reason` | Validation error | Critical |
| TC-OP-CANCEL-003 | Force Cancel | Thiếu reason | Trip tồn tại | 1. POST cancel | Chỉ có `operator_id` | Validation error | Critical |
| TC-OP-CANCEL-004 | Force Cancel | Body rỗng | Trip tồn tại | 1. POST cancel | `{}` | Validation error | Critical |
| TC-OP-CANCEL-005 | Force Cancel | operator_id sai datatype | Trip tồn tại | 1. POST cancel | `operator_id="901"` | Request bị reject | High |
| TC-OP-CANCEL-006 | Force Cancel | operator_id bằng 0 | Trip tồn tại | 1. POST cancel | `operator_id=0` | Xử lý theo implementation; YAML không minimum | Medium |
| TC-OP-CANCEL-007 | Force Cancel | operator_id âm | Trip tồn tại | 1. POST cancel | `operator_id=-1` | Xử lý theo implementation | Medium |
| TC-OP-CANCEL-008 | Force Cancel | trip_id sai datatype | API hoạt động | 1. POST `/trips/ABC/cancel` | `trip_id=ABC` | Request bị reject | High |
| TC-OP-CANCEL-009 | Force Cancel | trip_id bằng 0 | API hoạt động | 1. POST `/trips/0/cancel` | `trip_id=0` | Xử lý theo implementation; YAML không minimum | Medium |
| TC-OP-CANCEL-010 | Force Cancel | trip_id không tồn tại | API hoạt động | 1. POST cancel | `trip_id=999999` | Không hủy trip không tồn tại; trả lỗi phù hợp | Critical |
| TC-OP-CANCEL-011 | Force Cancel | reason rỗng | Trip tồn tại | 1. POST cancel | `reason=""` | Xử lý theo implementation; YAML không khai báo minLength | Medium |
| TC-OP-CANCEL-012 | Force Cancel | reason rất dài | Trip tồn tại | 1. POST cancel | Reason > giới hạn hệ thống nếu có | Xử lý theo implementation; YAML không khai báo maxLength | Medium |
| TC-OP-CANCEL-013 | Force Cancel | Hủy trip đã hoàn thành | Trip COMPLETED | 1. POST cancel | Valid operator + reason | Không được chuyển trạng thái trái business rule | Critical |
| TC-OP-CANCEL-014 | Force Cancel | Hủy trip đã bị hủy | Trip CANCELLED | 1. POST cancel | Valid operator + reason | Không tạo trạng thái sai; xử lý idempotency/business rule | High |
| TC-OP-CANCEL-015 | Force Cancel | Gửi request cancel hai lần | Trip tồn tại | 1. POST cancel lần 1<br>2. POST cancel lần 2 | Same trip/operator/reason | Không gây dữ liệu trạng thái không nhất quán | Critical |
| TC-OP-CANCEL-016 | Force Cancel | Backend timeout | API không phản hồi | 1. POST cancel<br>2. Giả lập timeout | Valid request | Timeout được xử lý; cần kiểm tra trip không bị cập nhật một phần | High |
