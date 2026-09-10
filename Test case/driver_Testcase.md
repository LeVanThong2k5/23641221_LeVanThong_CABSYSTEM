# Driver API - Test Cases


## Test Cases - Driver

| Test Case ID | Test Scenario | Test Case | Preconditions | Test Steps | Test Data | Expected Result | Priority |
|---|---|---|---|---|---|---|---|
| TC-DRV-STATUS-001 | Driver Status | Cập nhật trạng thái AVAILABLE | Driver tồn tại | 1. Gửi PUT `/status`<br>2. Kiểm tra response | `driver_id=201`<br>`status=AVAILABLE` | HTTP 200; cập nhật thành công | High |
| TC-DRV-STATUS-002 | Driver Status | Cập nhật trạng thái BUSY | Driver tồn tại | 1. Gửi PUT `/status`<br>2. Kiểm tra response | `driver_id=201`<br>`status=BUSY` | HTTP 200; cập nhật thành công | High |
| TC-DRV-STATUS-003 | Driver Status | Cập nhật trạng thái OFFLINE | Driver tồn tại | 1. Gửi PUT `/status`<br>2. Kiểm tra response | `driver_id=201`<br>`status=OFFLINE` | HTTP 200; cập nhật thành công | High |
| TC-DRV-STATUS-004 | Driver Status | status không thuộc enum | API hoạt động | 1. Gửi PUT `/status` | `status=ONLINE` | Request bị reject | High |
| TC-DRV-STATUS-005 | Driver Status | status rỗng | API hoạt động | 1. Gửi PUT `/status` | `status=` | Request bị reject/validation theo implementation | High |
| TC-DRV-STATUS-006 | Driver Status | Thiếu driver_id | API hoạt động | 1. Gửi PUT `/status` | `status=AVAILABLE` | Validation error | High |
| TC-DRV-STATUS-007 | Driver Status | Thiếu status | API hoạt động | 1. Gửi PUT `/status` | `driver_id=201` | Validation error | High |
| TC-DRV-STATUS-008 | Driver Status | Body rỗng | API hoạt động | 1. Gửi PUT `/status` | `{}` | Validation error | High |
| TC-DRV-STATUS-009 | Driver Status | driver_id sai datatype | API hoạt động | 1. Gửi PUT `/status` | `driver_id="201"` | Request bị reject | High |
| TC-DRV-STATUS-010 | Driver Status | driver_id bằng 0 | API hoạt động | 1. Gửi PUT `/status` | `driver_id=0` | Xử lý theo implementation; YAML không định nghĩa minimum | Medium |
| TC-DRV-STATUS-011 | Driver Status | Driver không tồn tại | API hoạt động | 1. Gửi PUT `/status` | `driver_id=999999`<br>`status=AVAILABLE` | Không cập nhật driver không tồn tại; trả lỗi phù hợp | High |
| TC-DRV-GPS-001 | GPS Location | Gửi vị trí GPS hợp lệ | Driver tồn tại | 1. Gửi POST `/location`<br>2. Kiểm tra response | `driver_id=201`<br>`latitude=10.7769`<br>`longitude=106.7009` | HTTP 200; ghi nhận vị trí GPS | High |
| TC-DRV-GPS-002 | GPS Location | Latitude bằng 0 | Driver tồn tại | 1. POST `/location` | `latitude=0`<br>`longitude=106.7009` | API xử lý thành công theo schema number | Medium |
| TC-DRV-GPS-003 | GPS Location | Longitude bằng 0 | Driver tồn tại | 1. POST `/location` | `latitude=10.7769`<br>`longitude=0` | API xử lý thành công theo schema number | Medium |
| TC-DRV-GPS-004 | GPS Location | Latitude âm | Driver tồn tại | 1. POST `/location` | `latitude=-10.7769` | API xử lý theo implementation; YAML không giới hạn min/max | Medium |
| TC-DRV-GPS-005 | GPS Location | Longitude âm | Driver tồn tại | 1. POST `/location` | `longitude=-106.7009` | API xử lý theo implementation; YAML không giới hạn min/max | Medium |
| TC-DRV-GPS-006 | GPS Location | Latitude/longitude dạng số thập phân | Driver tồn tại | 1. POST `/location` | `latitude=10.77691234`<br>`longitude=106.70091234` | HTTP 200 nếu dữ liệu hợp lệ | Medium |
| TC-DRV-GPS-007 | GPS Location | Thiếu driver_id | API hoạt động | 1. POST `/location` | `latitude=10.7769`<br>`longitude=106.7009` | Validation error | High |
| TC-DRV-GPS-008 | GPS Location | Thiếu latitude | API hoạt động | 1. POST `/location` | `driver_id=201`<br>`longitude=106.7009` | Validation error | High |
| TC-DRV-GPS-009 | GPS Location | Thiếu longitude | API hoạt động | 1. POST `/location` | `driver_id=201`<br>`latitude=10.7769` | Validation error | High |
| TC-DRV-GPS-010 | GPS Location | Body rỗng | API hoạt động | 1. POST `/location` | `{}` | Validation error | High |
| TC-DRV-GPS-011 | GPS Location | latitude sai datatype | API hoạt động | 1. POST `/location` | `latitude="ABC"` | Request bị reject | High |
| TC-DRV-GPS-012 | GPS Location | longitude sai datatype | API hoạt động | 1. POST `/location` | `longitude="ABC"` | Request bị reject | High |
| TC-DRV-GPS-013 | GPS Location | Mất GPS tại thiết bị | Driver App hoạt động nhưng GPS unavailable | 1. Gửi location request khi không có GPS | GPS unavailable | App không gửi dữ liệu GPS sai; xử lý lỗi theo implementation | High |
| TC-DRV-GPS-014 | GPS Location | Network timeout khi gửi GPS | Driver có GPS | 1. Gửi POST `/location`<br>2. Giả lập timeout | Valid GPS | Request timeout được xử lý; không crash app | High |
| TC-DRV-RESP-001 | Trip Response | Driver chấp nhận chuyến | Trip đang chờ phản hồi | 1. POST `/trips/5001/respond` | `driver_id=201`<br>`accepted=true` | HTTP 200; phản hồi accept thành công | Critical |
| TC-DRV-RESP-002 | Trip Response | Driver từ chối chuyến | Trip đang chờ phản hồi | 1. POST `/trips/5001/respond` | `driver_id=201`<br>`accepted=false` | HTTP 200; phản hồi reject thành công | High |
| TC-DRV-RESP-003 | Trip Response | Thiếu driver_id | Trip tồn tại | 1. POST respond | `accepted=true` | Validation error | High |
| TC-DRV-RESP-004 | Trip Response | Thiếu accepted | Trip tồn tại | 1. POST respond | `driver_id=201` | Validation error | High |
| TC-DRV-RESP-005 | Trip Response | accepted sai datatype | Trip tồn tại | 1. POST respond | `accepted="true"` | Request bị reject | High |
| TC-DRV-RESP-006 | Trip Response | accepted=null | Trip tồn tại | 1. POST respond | `accepted=null` | Request bị reject/validation | High |
| TC-DRV-RESP-007 | Trip Response | trip_id sai datatype | API hoạt động | 1. POST `/trips/ABC/respond` | `trip_id=ABC` | Request bị reject | High |
| TC-DRV-RESP-008 | Trip Response | trip_id không tồn tại | API hoạt động | 1. POST respond | `trip_id=999999` | Không xử lý trip không tồn tại; lỗi phù hợp | High |
| TC-DRV-RESP-009 | Trip Response | driver_id không tồn tại | API hoạt động | 1. POST respond | `driver_id=999999`<br>`accepted=true` | Không chấp nhận phản hồi từ driver không tồn tại | High |
| TC-DRV-RESP-010 | Trip Response | Request timeout | Backend hoạt động không ổn định | 1. POST respond<br>2. Giả lập timeout | Valid request | Client xử lý timeout; trạng thái trip không bị cập nhật sai | High |
