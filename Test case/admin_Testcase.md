# Admin API - Test Cases

## Test Cases - Admin

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-ADMIN-001 | Audit Log | Lấy toàn bộ audit log | API Admin đang hoạt động | 1. Gửi GET `/audit-logs`<br>2. Kiểm tra response | Không truyền query parameter | HTTP 200; trả danh sách audit log | High |
| TC-ADMIN-002 | Audit Log | Tra cứu audit log theo user_id | API hoạt động; user_id tồn tại | 1. Gửi GET `/audit-logs?user_id=901`<br>2. Kiểm tra response | `user_id=901` | HTTP 200; kết quả được filter theo user_id | High |
| TC-ADMIN-003 | Audit Log | Tra cứu audit log theo action | API hoạt động | 1. Gửi GET `/audit-logs?action=CANCEL_TRIP`<br>2. Kiểm tra response | `action=CANCEL_TRIP` | HTTP 200; kết quả được filter theo action | High |
| TC-ADMIN-004 | Audit Log | Filter đồng thời user_id và action | API hoạt động | 1. Gửi GET request<br>2. Kiểm tra kết quả | `user_id=901`<br>`action=CANCEL_TRIP` | HTTP 200; trả các log phù hợp cả hai điều kiện | High |
| TC-ADMIN-005 | Audit Log | user_id bằng 0 | API hoạt động | 1. Gửi GET request<br>2. Kiểm tra response | `user_id=0` | API xử lý theo implementation; YAML không định nghĩa minimum | Medium |
| TC-ADMIN-006 | Audit Log | user_id âm | API hoạt động | 1. Gửi GET request<br>2. Kiểm tra response | `user_id=-1` | API xử lý theo implementation; YAML chỉ quy định integer | Medium |
| TC-ADMIN-007 | Audit Log | user_id sai datatype | API hoạt động | 1. Gửi GET request | `user_id=ABC` | Request bị validation/reject nếu API áp dụng schema validation | High |
| TC-ADMIN-008 | Audit Log | user_id dạng số thập phân | API hoạt động | 1. Gửi GET request | `user_id=901.5` | Request bị reject nếu integer validation được áp dụng | Medium |
| TC-ADMIN-009 | Audit Log | action để trống | API hoạt động | 1. Gửi GET request | `action=` | API xử lý theo implementation; không có rule non-empty trong YAML | Low |
| TC-ADMIN-010 | Audit Log | action chứa ký tự đặc biệt | API hoạt động | 1. Gửi GET request | `action=@@@###` | API không crash; xử lý filter theo implementation | Medium |
| TC-ADMIN-011 | Audit Log | user_id không tồn tại | API hoạt động | 1. Gửi GET request | `user_id=999999` | HTTP 200 với danh sách rỗng hoặc behavior theo implementation | Medium |
| TC-ADMIN-012 | Audit Log | API timeout | Backend/database không phản hồi | 1. Gửi GET request<br>2. Chờ timeout | Valid request | API trả lỗi timeout phù hợp; không treo request vô hạn | High |
| TC-ADMIN-013 | Audit Log | Database unavailable | Database ngừng hoạt động | 1. Gửi GET request | Valid request | API trả HTTP 5xx phù hợp; không làm crash toàn hệ thống | High |
| TC-ADMIN-014 | Audit Log | Mất kết nối mạng khi request | API đang hoạt động | 1. Gửi GET request<br>2. Ngắt network | Valid request | Client nhận network error/timeout; hệ thống không tạo dữ liệu sai | Medium |
