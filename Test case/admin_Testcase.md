Test Case ID	Test Scenario	Test Case	Preconditions	Test Steps	Test Data	Expected Result	Priority
TC-CUST-REG-001	Register Customer	Đăng ký với dữ liệu hợp lệ	API hoạt động	1. Gửi POST /register	full_name=Nguyễn Văn A; phone_number=0901234567	HTTP 201; đăng ký thành công	High
TC-CUST-REG-002	Register Customer	Đăng ký có email hợp lệ	API hoạt động	1. Gửi POST /register	full_name=Nguyễn Văn A; phone=0901234567; email=nguyenvana@gmail.com	HTTP 201	High
TC-CUST-REG-003	Register Customer	Thiếu full_name	API hoạt động	1. Gửi request	phone_number=0901234567	Request bị reject do thiếu required field	High
TC-CUST-REG-004	Register Customer	Thiếu phone_number	API hoạt động	1. Gửi request	full_name=Nguyễn Văn A	Request bị reject	High
TC-CUST-REG-005	Register Customer	Body rỗng	API hoạt động	1. Gửi request {}	{}	Request bị reject validation	High
TC-CUST-REG-006	Register Customer	full_name sai datatype	API hoạt động	1. Gửi request	full_name=12345	Request bị reject	Medium
TC-CUST-REG-007	Register Customer	phone_number sai datatype	API hoạt động	1. Gửi request	phone_number=901234567	Request bị reject	High
TC-CUST-REG-008	Register Customer	email sai datatype	API hoạt động	1. Gửi request	email=12345	Request bị reject	Medium
TC-CUST-REG-009	Register Customer	full_name null	API hoạt động	1. Gửi request	full_name=null	Request bị reject	High
TC-CUST-REG-010	Register Customer	phone_number null	API hoạt động	1. Gửi request	phone_number=null	Request bị reject	High
TC-CUST-PRO-001	Customer Profile	Lấy profile với customer_id hợp lệ	Customer tồn tại	1. GET /profile/101	customer_id=101	HTTP 200; trả thông tin customer	High
TC-CUST-PRO-002	Customer Profile	customer_id không tồn tại	API hoạt động	1. GET profile	customer_id=999999	Không trả profile của customer không tồn tại	High
TC-CUST-PRO-003	Customer Profile	customer_id sai datatype	API hoạt động	1. GET profile	customer_id=ABC	Request bị reject	High
TC-CUST-PRO-004	Customer Profile	customer_id=0	API hoạt động	1. GET profile	0	Kiểm tra behavior thực tế; YAML không khai báo minimum	Medium
TC-CUST-PRO-005	Customer Profile	customer_id âm	API hoạt động	1. GET profile	-1	Kiểm tra behavior thực tế; YAML không khai báo minimum	Medium
TC-CUST-TRIP-001	Create Trip	Tạo chuyến hợp lệ	Customer tồn tại	1. POST /trips	customer_id=101; pickup; destination; vehicle_type=4-seater	HTTP 201; đặt chuyến thành công	Critical
TC-CUST-TRIP-002	Create Trip	Thanh toán CASH	Customer tồn tại	1. POST /trips	payment_method=CASH	HTTP 201	High
TC-CUST-TRIP-003	Create Trip	Thanh toán WALLET	Customer tồn tại	1. POST /trips	payment_method=WALLET	HTTP 201	High
TC-CUST-TRIP-004	Create Trip	Thanh toán CARD	Customer tồn tại	1. POST /trips	payment_method=CARD	HTTP 201	High
TC-CUST-TRIP-005	Create Trip	Không truyền payment_method	Customer tồn tại	1. POST /trips	Không có payment_method	Request hợp lệ theo schema	High
TC-CUST-TRIP-006	Create Trip	Thiếu customer_id	API hoạt động	1. POST /trips	Bỏ customer_id	Validation error	Critical
TC-CUST-TRIP-007	Create Trip	Thiếu pickup_address	API hoạt động	1. POST /trips	Bỏ pickup_address	Validation error	Critical
TC-CUST-TRIP-008	Create Trip	Thiếu destination_address	API hoạt động	1. POST /trips	Bỏ destination_address	Validation error	Critical
TC-CUST-TRIP-009	Create Trip	Thiếu vehicle_type	API hoạt động	1. POST /trips	Bỏ vehicle_type	Validation error	Critical
TC-CUST-TRIP-010	Create Trip	payment_method sai enum	API hoạt động	1. POST /trips	payment_method=BITCOIN	Request bị reject	High
TC-CUST-TRIP-011	Create Trip	customer_id sai datatype	API hoạt động	1. POST /trips	customer_id="101"	Request bị reject	High
TC-CUST-TRIP-012	Create Trip	Body rỗng	API hoạt động	1. POST /trips	{}	Validation error	Critical
TC-CUST-STATUS-001	Trip Status	Lấy trạng thái trip hợp lệ	Trip tồn tại	1. GET /trips/5001	trip_id=5001	HTTP 200	High
TC-CUST-STATUS-002	Trip Status	trip_id không tồn tại	API hoạt động	1. GET trip	trip_id=999999	Không trả trip không tồn tại	High
TC-CUST-STATUS-003	Trip Status	trip_id sai datatype	API hoạt động	1. GET trip	trip_id=ABC	Request bị reject	High
TC-CUST-STATUS-004	Trip Status	trip_id=0	API hoạt động	1. GET trip	0	Kiểm tra implementation; YAML không minimum	Medium
TC-CUST-RATE-001	Rating	Đánh giá 1 sao	Trip hợp lệ	1. POST /ratings	score=1	HTTP 201	High
TC-CUST-RATE-002	Rating	Đánh giá 5 sao	Trip hợp lệ	1. POST /ratings	score=5	HTTP 201	High
TC-CUST-RATE-003	Rating	Đánh giá 3 sao	Trip hợp lệ	1. POST /ratings	score=3	HTTP 201	Medium
TC-CUST-RATE-004	Rating	score=0	API hoạt động	1. POST /ratings	score=0	Reject vì nhỏ hơn minimum=1	High
TC-CUST-RATE-005	Rating	score=6	API hoạt động	1. POST /ratings	score=6	Reject vì lớn hơn maximum=5	High
TC-CUST-RATE-006	Rating	score=-1	API hoạt động	1. POST /ratings	score=-1	Reject	High
TC-CUST-RATE-007	Rating	Thiếu score	API hoạt động	1. POST /ratings	Không có score	Validation error	Critical
TC-CUST-RATE-008	Rating	score sai datatype	API hoạt động	1. POST /ratings	score="5"	Reject	High
TC-CUST-RATE-009	Rating	Thiếu trip_id	API hoạt động	1. POST /ratings	Không có trip_id	Validation error	High
TC-CUST-RATE-010	Rating	Thiếu customer_id	API hoạt động	1. POST /ratings	Không có customer_id	Validation error	High
TC-CUST-RATE-011	Rating	Rating có comment	Trip hợp lệ	1. POST /ratings	score=5; comment="Tài xế thân thiện"	HTTP 201	Medium
TC-CUST-RATE-012	Rating	Body rỗng	API hoạt động	1. POST /ratings	{}	Validation error	High
