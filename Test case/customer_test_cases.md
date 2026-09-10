# Customer API - Test Cases

## Test Cases - Customer

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-CUST-REG-001 | Customer Registration | Đăng ký với dữ liệu hợp lệ | API hoạt động | 1. POST `/register`<br>2. Kiểm tra response | `full_name=Nguyễn Văn A`<br>`phone_number=0901234567` | HTTP 201; đăng ký thành công | High |
| TC-CUST-REG-002 | Customer Registration | Đăng ký với email hợp lệ | API hoạt động | 1. POST `/register` | `full_name=Nguyễn Văn A`<br>`phone_number=0901234567`<br>`email=nguyenvana@gmail.com` | HTTP 201; đăng ký thành công | High |
| TC-CUST-REG-003 | Customer Registration | Thiếu full_name | API hoạt động | 1. POST `/register` | Chỉ có phone_number | Validation error | High |
| TC-CUST-REG-004 | Customer Registration | Thiếu phone_number | API hoạt động | 1. POST `/register` | Chỉ có full_name | Validation error | High |
| TC-CUST-REG-005 | Customer Registration | Body rỗng | API hoạt động | 1. POST `/register` | `{}` | Validation error | High |
| TC-CUST-REG-006 | Customer Registration | full_name sai datatype | API hoạt động | 1. POST `/register` | `full_name=12345` | Request bị reject | Medium |
| TC-CUST-REG-007 | Customer Registration | phone_number sai datatype | API hoạt động | 1. POST `/register` | `phone_number=901234567` | Request bị reject nếu schema validation | High |
| TC-CUST-REG-008 | Customer Registration | email sai datatype | API hoạt động | 1. POST `/register` | `email=12345` | Request bị reject | Medium |
| TC-CUST-REG-009 | Customer Registration | full_name null | API hoạt động | 1. POST `/register` | `full_name=null` | Validation error | High |
| TC-CUST-REG-010 | Customer Registration | phone_number null | API hoạt động | 1. POST `/register` | `phone_number=null` | Validation error | High |
| TC-CUST-PRO-001 | Customer Profile | Lấy profile customer hợp lệ | Customer tồn tại | 1. GET `/profile/101` | `customer_id=101` | HTTP 200; trả thông tin customer | High |
| TC-CUST-PRO-002 | Customer Profile | customer_id không tồn tại | API hoạt động | 1. GET `/profile/999999` | `customer_id=999999` | Không trả profile không tồn tại; lỗi phù hợp | High |
| TC-CUST-PRO-003 | Customer Profile | customer_id sai datatype | API hoạt động | 1. GET `/profile/ABC` | `customer_id=ABC` | Request bị reject | High |
| TC-CUST-PRO-004 | Customer Profile | customer_id bằng 0 | API hoạt động | 1. GET `/profile/0` | `customer_id=0` | YAML không khai báo minimum; xử lý theo implementation | Medium |
| TC-CUST-PRO-005 | Customer Profile | customer_id âm | API hoạt động | 1. GET `/profile/-1` | `customer_id=-1` | YAML không khai báo minimum; xử lý theo implementation | Medium |
| TC-CUST-TRIP-001 | Create Trip | Đặt chuyến hợp lệ | Customer tồn tại | 1. POST `/trips` | `customer_id=101`<br>`pickup_address=123 Lê Lợi`<br>`destination_address=456 Nguyễn Huệ`<br>`vehicle_type=4-seater` | HTTP 201; đặt chuyến thành công | Critical |
| TC-CUST-TRIP-002 | Create Trip | Đặt chuyến bằng CASH | Customer tồn tại | 1. POST `/trips` | `payment_method=CASH` | HTTP 201 | High |
| TC-CUST-TRIP-003 | Create Trip | Đặt chuyến bằng WALLET | Customer tồn tại | 1. POST `/trips` | `payment_method=WALLET` | HTTP 201 | High |
| TC-CUST-TRIP-004 | Create Trip | Đặt chuyến bằng CARD | Customer tồn tại | 1. POST `/trips` | `payment_method=CARD` | HTTP 201 | High |
| TC-CUST-TRIP-005 | Create Trip | Không truyền payment_method | Customer tồn tại | 1. POST `/trips` | Không có payment_method | Request hợp lệ theo schema | Medium |
| TC-CUST-TRIP-006 | Create Trip | Thiếu customer_id | API hoạt động | 1. POST `/trips` | Bỏ customer_id | Validation error | Critical |
| TC-CUST-TRIP-007 | Create Trip | Thiếu pickup_address | API hoạt động | 1. POST `/trips` | Bỏ pickup_address | Validation error | Critical |
| TC-CUST-TRIP-008 | Create Trip | Thiếu destination_address | API hoạt động | 1. POST `/trips` | Bỏ destination_address | Validation error | Critical |
| TC-CUST-TRIP-009 | Create Trip | Thiếu vehicle_type | API hoạt động | 1. POST `/trips` | Bỏ vehicle_type | Validation error | Critical |
| TC-CUST-TRIP-010 | Create Trip | payment_method sai enum | API hoạt động | 1. POST `/trips` | `payment_method=BITCOIN` | Request bị reject | High |
| TC-CUST-TRIP-011 | Create Trip | customer_id sai datatype | API hoạt động | 1. POST `/trips` | `customer_id="101"` | Request bị reject | High |
| TC-CUST-TRIP-012 | Create Trip | Body rỗng | API hoạt động | 1. POST `/trips` | `{}` | Validation error | Critical |
| TC-CUST-TRIP-013 | Create Trip | customer_id không tồn tại | API hoạt động | 1. POST `/trips` | `customer_id=999999` | Không tạo trip cho customer không tồn tại | Critical |
| TC-CUST-TRIP-014 | Create Trip | pickup_address rỗng | API hoạt động | 1. POST `/trips` | `pickup_address=""` | YAML không có minLength; cần kiểm tra Business Rule | High |
| TC-CUST-TRIP-015 | Create Trip | destination_address rỗng | API hoạt động | 1. POST `/trips` | `destination_address=""` | YAML không có minLength; cần kiểm tra Business Rule | High |
| TC-CUST-STATUS-001 | Trip Status | Lấy trạng thái trip hợp lệ | Trip tồn tại | 1. GET `/trips/5001` | `trip_id=5001` | HTTP 200; trả thông tin trip | High |
| TC-CUST-STATUS-002 | Trip Status | trip_id không tồn tại | API hoạt động | 1. GET `/trips/999999` | `trip_id=999999` | Không trả trip không tồn tại; lỗi phù hợp | High |
| TC-CUST-STATUS-003 | Trip Status | trip_id sai datatype | API hoạt động | 1. GET `/trips/ABC` | `trip_id=ABC` | Request bị reject | High |
| TC-CUST-STATUS-004 | Trip Status | trip_id bằng 0 | API hoạt động | 1. GET `/trips/0` | `trip_id=0` | YAML không minimum; xử lý theo implementation | Medium |
| TC-CUST-RATE-001 | Rating | Đánh giá 1 sao | Trip hợp lệ | 1. POST `/ratings` | `trip_id=5001`<br>`customer_id=101`<br>`score=1` | HTTP 201; đánh giá thành công | High |
| TC-CUST-RATE-002 | Rating | Đánh giá 5 sao | Trip hợp lệ | 1. POST `/ratings` | `score=5` | HTTP 201; đánh giá thành công | High |
| TC-CUST-RATE-003 | Rating | Đánh giá 3 sao | Trip hợp lệ | 1. POST `/ratings` | `score=3` | HTTP 201 | Medium |
| TC-CUST-RATE-004 | Rating | score = 0 | API hoạt động | 1. POST `/ratings` | `score=0` | Reject vì nhỏ hơn minimum=1 | High |
| TC-CUST-RATE-005 | Rating | score = 6 | API hoạt động | 1. POST `/ratings` | `score=6` | Reject vì lớn hơn maximum=5 | High |
| TC-CUST-RATE-006 | Rating | score âm | API hoạt động | 1. POST `/ratings` | `score=-1` | Reject | High |
| TC-CUST-RATE-007 | Rating | Thiếu score | API hoạt động | 1. POST `/ratings` | Bỏ score | Validation error | Critical |
| TC-CUST-RATE-008 | Rating | score sai datatype | API hoạt động | 1. POST `/ratings` | `score="5"` | Request bị reject | High |
| TC-CUST-RATE-009 | Rating | Thiếu trip_id | API hoạt động | 1. POST `/ratings` | Bỏ trip_id | Validation error | High |
| TC-CUST-RATE-010 | Rating | Thiếu customer_id | API hoạt động | 1. POST `/ratings` | Bỏ customer_id | Validation error | High |
| TC-CUST-RATE-011 | Rating | Rating có comment | Trip hợp lệ | 1. POST `/ratings` | `score=5`<br>`comment=Tài xế thân thiện, xe sạch` | HTTP 201; đánh giá thành công | Medium |
| TC-CUST-RATE-012 | Rating | comment rỗng | Trip hợp lệ | 1. POST `/ratings` | `score=5`<br>`comment=""` | Xử lý theo implementation; comment không required | Low |
| TC-CUST-RATE-013 | Rating | Body rỗng | API hoạt động | 1. POST `/ratings` | `{}` | Validation error | High |
