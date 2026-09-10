# Leadership API - Test Cases

## Test Cases - Leadership

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-LEAD-001 | Dashboard | Lấy dashboard thành công | API hoạt động | 1. GET `/reports/dashboard`<br>2. Kiểm tra response | Không có input | HTTP 200; trả dashboard | High |
| TC-LEAD-002 | Dashboard | Kiểm tra total_trips | Có dữ liệu chuyến | 1. GET dashboard<br>2. Kiểm tra field | `total_trips=5000` | Field tồn tại và là integer | High |
| TC-LEAD-003 | Dashboard | Kiểm tra completed_trips | Có dữ liệu chuyến hoàn thành | 1. GET dashboard | `completed_trips=4600` | Field tồn tại và là integer | High |
| TC-LEAD-004 | Dashboard | Kiểm tra total_revenue_vnd | Có dữ liệu doanh thu | 1. GET dashboard | `total_revenue_vnd=650000000` | Field tồn tại và là number | High |
| TC-LEAD-005 | Dashboard | Kiểm tra active_drivers_count | Có driver hoạt động | 1. GET dashboard | `active_drivers_count=120` | Field tồn tại và là integer | High |
| TC-LEAD-006 | Dashboard | Hệ thống không có dữ liệu | Database empty | 1. GET dashboard | Không có record | API vẫn trả response hợp lệ theo implementation | Medium |
| TC-LEAD-007 | Dashboard | Tất cả giá trị bằng 0 | Database có dữ liệu nhưng metric = 0 | 1. GET dashboard | `0,0,0,0` | Các field trả đúng kiểu dữ liệu và giá trị | Medium |
| TC-LEAD-008 | Dashboard | Giá trị doanh thu lớn | Có dữ liệu lớn | 1. GET dashboard | `total_revenue_vnd=999999999999` | API không overflow; trả number hợp lệ | Medium |
| TC-LEAD-009 | Dashboard | Database timeout | DB unavailable/timeout | 1. GET dashboard | N/A | API trả lỗi phù hợp; không treo vô hạn | High |
| TC-LEAD-010 | Dashboard | Backend exception | Backend phát sinh exception | 1. GET dashboard | N/A | API trả HTTP 5xx phù hợp; server không crash | High |
| TC-LEAD-011 | Dashboard | Network timeout | Network không ổn định | 1. GET dashboard<br>2. Giả lập timeout | N/A | Client xử lý timeout phù hợp | Medium |
| TC-LEAD-012 | Dashboard | Response sai datatype | Backend trả dữ liệu không đúng schema | 1. GET dashboard<br>2. Validate response | `total_trips="5000"` | Schema validation phát hiện sai datatype nếu validation được áp dụng | High |
