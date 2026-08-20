Bước 1: Đọc và phân tích yêu câu sơ khởi của khách hàng ở giai đoạn 1
1. Mục tiêu của giai đoạn 1

Từ yêu cầu của ABC, có thể xác định mục tiêu ban đầu của dự án là:

Xây dựng nền tảng CAB System cho phép khách hàng đặt xe, hệ thống tự động tìm/phân công tài xế, tài xế thực hiện chuyến, hệ thống tính cước và thanh toán, gửi thông báo, đánh giá sau chuyến và cung cấp công cụ quản trị/vận hành.

Đồng thời, hệ thống phải có khả năng:

phục vụ số lượng lớn khách hàng/tài xế;
mở rộng độc lập các thành phần;
bổ sung dịch vụ, phương thức thanh toán, kênh thông báo;
hạn chế việc một thành phần lỗi làm ảnh hưởng toàn bộ hệ thống;
đảm bảo bảo mật và audit;
cho phép triển khai tính năng từng phần.
2. Phạm vi sơ bộ
In scope — thuộc phạm vi dự án
Nhóm	Chức năng sơ bộ
Khách hàng	Đăng ký, đăng nhập, quản lý hồ sơ
Đặt xe	Nhập điểm đón, điểm đến, chọn loại xe, tạo yêu cầu
Theo dõi chuyến	Theo dõi tìm tài xế, tài xế nhận chuyến, ETA, trạng thái
Tài xế	Hồ sơ, phương tiện, trạng thái online/offline/available
Điều phối	Tìm và phân công tài xế
Thực hiện chuyến	Cập nhật trạng thái chuyến
Định vị	Lưu/cập nhật vị trí tài xế
Tính cước	Xác định số tiền phải trả
Thanh toán	Tiền mặt và thanh toán điện tử
Thông báo	Gửi thông báo cho khách hàng/tài xế
Đánh giá	Khách hàng đánh giá tài xế
Lịch sử	Lịch sử chuyến và giao dịch
Vận hành	Quản lý khách hàng, tài xế, xe, chuyến đi
Xử lý sự cố	Hỗ trợ chuyến lỗi, thanh toán lỗi...
Báo cáo	Chuyến, doanh thu, hoàn thành, hủy, hiệu quả tài xế
Phân quyền	Quyền nhân viên vận hành/admin
Audit	Lưu vết thao tác quan trọng
Out of scope / chưa xác định

Chưa thấy yêu cầu rõ về:

chương trình khuyến mãi/voucher;
loyalty/điểm thưởng;
đăng ký doanh nghiệp/corporate account;
thuê xe theo giờ;
giao hàng;
tích hợp bản đồ cụ thể;
nhiều quốc gia/nhiều tiền tệ;
hóa đơn điện tử;
xử lý khiếu nại/CSKH đầy đủ;
surge pricing;
subscription/membership.

Lưu ý: chưa nên kết luận những nội dung trên chắc chắn là out-of-scope. BA cần đưa vào danh sách Open Questions để xác nhận với khách hàng.

3. Xác định các tác nhân

Có thể xác định các actor chính như sau:

3.1. Customer — Khách hàng

Mục đích:

quản lý tài khoản;
tạo yêu cầu đặt xe;
theo dõi chuyến;
thanh toán;
xem lịch sử;
đánh giá tài xế.
3.2. Driver — Tài xế

Mục đích:

quản lý hồ sơ/phương tiện;
chuyển trạng thái sẵn sàng;
nhận thông báo chuyến;
nhận/từ chối chuyến;
cập nhật trạng thái chuyến;
cung cấp vị trí.
3.3. Operation Staff — Nhân viên vận hành

Mục đích:

quản lý customer/driver/vehicle;
giám sát chuyến;
hỗ trợ xử lý sự cố;
tra cứu giao dịch;
theo dõi trạng thái tài xế.
3.4. Administrator

Có thể xem là actor riêng hoặc một role thuộc nhóm Operation.

Quyền dự kiến:

quản lý user/role/permission;
thực hiện thao tác nhạy cảm;
cấu hình hệ thống;
xem audit log.

Điểm cần xác nhận: ABC có thực sự phân biệt Operation Staff và Administrator hay chỉ có một nhóm nhân viên với các permission khác nhau?

3.5. Payment Provider

Hệ thống bên ngoài:

tiếp nhận yêu cầu thanh toán;
xử lý payment;
trả về success/failure;
có thể cung cấp transaction/reference ID.
3.6. Notification Provider

Hệ thống bên ngoài dùng để gửi:

Push Notification;
SMS;
Email;
hoặc các kênh khác trong tương lai.
3.7. Map/Location Provider

Nhiều khả năng cần một hệ thống bên ngoài để:

xác định tọa độ;
geocoding;
reverse geocoding;
tính khoảng cách;
ETA/route.

Đây là một dependency quan trọng nhưng yêu cầu hiện tại chưa nói rõ provider nào.

4. Quy trình nghiệp vụ end-to-end sơ bộ

Có thể mô hình hóa luồng nghiệp vụ chính:

Customer

→ nhập điểm đón/điểm đến
→ chọn loại xe
→ tạo booking request
→ hệ thống tiếp nhận yêu cầu
→ tìm tài xế phù hợp
→ gửi request cho tài xế
→ Driver accept
→ xác nhận tài xế
→ Customer theo dõi tài xế/ETA
→ Driver đến điểm đón
→ Driver đón khách
→ Driver di chuyển
→ Driver hoàn thành chuyến
→ hệ thống tính cước
→ Customer thanh toán
→ hệ thống xác nhận payment
→ Customer đánh giá Driver
→ lưu lịch sử.

Nhánh thất bại

Nếu:

Driver không phản hồi / từ chối

→ hệ thống chọn Driver khác
→ tiếp tục dispatch.

Nếu:

Không còn Driver phù hợp

→ booking chuyển trạng thái không tìm được tài xế
→ thông báo Customer.

Nếu:

Electronic payment failed

→ thông báo Customer
→ cho phép retry hoặc chuyển sang phương thức khác theo policy.

5. Các trạng thái quan trọng

Một trong những vấn đề BA cần xác định sớm là State Model.

Ví dụ đối với Trip:

REQUESTED

→ SEARCHING_DRIVER

→ DRIVER_ASSIGNED

→ DRIVER_ARRIVING

→ DRIVER_ARRIVED

→ PASSENGER_PICKED_UP

→ IN_PROGRESS

→ COMPLETED

Có thể có các trạng thái kết thúc khác:

CANCELLED_BY_CUSTOMER
CANCELLED_BY_DRIVER
CANCELLED_BY_OPERATION
NO_DRIVER_FOUND
FAILED

Tuy nhiên đây mới là đề xuất sơ bộ, chưa phải business rule cuối cùng.

BA cần làm rõ:

Ai được phép chuyển từng trạng thái?
Có được quay lại trạng thái trước không?
Khi nào booking hết hạn?
Driver đến nhưng customer không có mặt thì trạng thái nào?
Customer hủy sau khi driver đã đến có bị tính phí không?
Driver hủy sau khi đã accept thì xử lý thế nào?
6. Phân tích yêu cầu chức năng sơ bộ
Customer Management

FR-01: Customer có thể đăng ký tài khoản.

FR-02: Customer có thể đăng nhập/đăng xuất.

FR-03: Customer có thể cập nhật thông tin cá nhân.

FR-04: Customer có thể xem lịch sử chuyến.

Booking

FR-05: Customer nhập pickup location.

FR-06: Customer nhập destination.

FR-07: Customer chọn loại dịch vụ/loại xe.

FR-08: Customer tạo booking request.

FR-09: Hệ thống tiếp nhận và tạo Trip/Booking.

FR-10: Hệ thống xác định Driver phù hợp.

FR-11: Hệ thống gửi request tới Driver.

FR-12: Driver có thể accept/reject.

FR-13: Nếu Driver reject/timeout, hệ thống tiếp tục dispatch Driver khác.

FR-14: Nếu không tìm được Driver, hệ thống thông báo Customer.

Trip Tracking

FR-15: Customer xem trạng thái Trip.

FR-16: Customer xem thông tin Driver được phân công.

FR-17: Customer xem ETA.

FR-18: Hệ thống cập nhật vị trí Driver.

FR-19: Driver cập nhật trạng thái thực hiện Trip.

Driver

FR-20: Driver có profile.

FR-21: Driver có thông tin vehicle.

FR-22: Driver có thể chuyển trạng thái hoạt động.

FR-23: Driver nhận notification về booking.

FR-24: Driver accept/reject booking.

FR-25: Driver cập nhật trạng thái Trip.

Fare & Payment

FR-26: Hệ thống tính fare sau khi hoàn thành Trip.

FR-27: Hỗ trợ cash payment.

FR-28: Hỗ trợ electronic payment.

FR-29: CAB tích hợp Payment Provider.

FR-30: CAB không lưu trực tiếp dữ liệu nhạy cảm của thẻ/tài khoản.

FR-31: Hệ thống nhận payment result.

FR-32: Hệ thống xử lý payment failure/retry theo policy.

Notification

FR-33: Gửi notification khi booking được tiếp nhận.

FR-34: Gửi notification khi Driver nhận chuyến.

FR-35: Gửi notification khi Driver đến.

FR-36: Gửi notification khi Trip hoàn thành.

FR-37: Gửi notification về payment.

FR-38: Driver nhận notification về booking/chuyến.

Điểm kiến trúc quan trọng ở đây là notification nên được thiết kế theo hướng có thể thay đổi provider/channel, thay vì business logic phụ thuộc trực tiếp vào một nhà cung cấp cụ thể.

Operation

FR-39: Quản lý Customer.

FR-40: Quản lý Driver.

FR-41: Quản lý Vehicle.

FR-42: Xem Trip đang diễn ra.

FR-43: Tra cứu Trip history.

FR-44: Tra cứu transaction.

FR-45: Hỗ trợ xử lý Trip lỗi.

FR-46: Quản lý quyền truy cập.

FR-47: Xem audit log.

Reporting

FR-48: Báo cáo số lượng Trip.

FR-49: Báo cáo doanh thu.

FR-50: Tỷ lệ Trip hoàn thành.

FR-51: Tỷ lệ Trip hủy.

FR-52: Hiệu quả hoạt động của Driver.

7. Yêu cầu phi chức năng

Đây là phần rất quan trọng vì khách hàng nhấn mạnh hệ thống phải phục vụ quy mô lớn và có khả năng mở rộng.

Performance

Cần xác định:

số lượng concurrent users;
số booking/giây;
peak load;
thời gian phản hồi API;
thời gian tìm Driver;
thời gian notification phải được gửi.

Hiện yêu cầu chưa cung cấp con số cụ thể.

Scalability

Hệ thống cần có khả năng:

scale Customer-facing services;
scale Driver/Dispatch;
scale Notification;
scale Payment;
scale Reporting;

một cách độc lập khi tải tăng.

Availability

Cần xác định SLA cụ thể, ví dụ:

99.9%;
99.95%;
hoặc mức khác.

Đây là Open Question, không nên tự mặc định.

Reliability

Payment/Notification lỗi không được làm toàn bộ Booking System ngừng hoạt động.

Ví dụ:

Booking Service

không nên phụ thuộc đồng bộ tuyệt đối vào

Notification Service.

Security
Authentication.
Authorization/RBAC.
Encryption in transit.
Encryption at rest.
Bảo vệ PII.
Bảo vệ location data.
Bảo vệ transaction data.
Audit log.
Không lưu sensitive payment credentials.
Maintainability

Kiến trúc cần hỗ trợ:

thay đổi Payment Provider;
thay đổi Notification Provider;
thêm loại dịch vụ;
thêm payment method;
thay đổi technical component.
Deployability

Có khả năng:

deploy từng component;
rollout từng tính năng;
hạn chế downtime;
giảm ảnh hưởng đến chức năng đang chạy.
8. Business Rules sơ bộ

Từ yêu cầu có thể suy ra một số rule:

BR-01 — Driver phải sẵn sàng

Chỉ Driver đáp ứng điều kiện hoạt động mới được đưa vào danh sách dispatch.

BR-02 — Driver phải phù hợp

Driver phải đáp ứng các tiêu chí về:

vị trí;
trạng thái;
loại xe;
các tiêu chí vận hành khác.
BR-03 — Dispatch fallback

Nếu Driver được đề xuất:

reject;
không phản hồi;
hoặc không còn phù hợp;

thì hệ thống phải tiếp tục tìm Driver khác.

BR-04 — Không tìm được Driver

Booking phải chuyển sang trạng thái phù hợp và Customer phải được thông báo.

BR-05 — Payment

Fare được xác định sau khi Trip hoàn thành theo pricing policy.

BR-06 — Payment Provider

CAB không lưu thông tin nhạy cảm của phương thức thanh toán.

BR-07 — Authorization

Nhân viên chỉ được thực hiện các thao tác nằm trong quyền của role.

BR-08 — Audit

Các thao tác quan trọng phải được ghi nhận.

9. Các ngoại lệ cần phân tích

Đây là phần hiện tại yêu cầu khách hàng còn thiếu khá nhiều.

Booking
Customer mất mạng ngay sau khi bấm đặt xe.
Customer bấm đặt xe nhiều lần.
Không có Driver.
Driver reject.
Driver không phản hồi.
Driver mất kết nối sau khi accept.
Hai Driver cùng accept một booking.
Customer hủy trong lúc tìm Driver.
Customer hủy sau khi Driver đã đến.
Trip
Driver mất GPS.
GPS trả về vị trí không hợp lệ.
Driver mất kết nối.
Customer không xuất hiện tại pickup.
Driver cập nhật sai trạng thái.
Trip bị treo ở một trạng thái quá lâu.
Payment
Payment timeout.
Payment failed.
Payment Provider unavailable.
Customer retry nhiều lần.
Payment callback bị gửi duplicate.
Payment thành công nhưng CAB không nhận được callback.
CAB nhận callback nhiều lần.
Notification
Notification Provider down.
Push notification thất bại.
User offline.
Notification được gửi duplicate.
Notification gửi trễ.
10. Các vấn đề chưa rõ cần BA xác nhận

Đây có lẽ là phần quan trọng nhất của Bước 1.

A. Pricing

Cần hỏi:

Công thức tính cước là gì?
Tính theo km, thời gian hay kết hợp?
Có phí mở cửa không?
Có phí chờ không?
Có surge/dynamic pricing không?
Có phụ phí theo thời điểm/khu vực không?
Fare được chốt trước hay sau chuyến?
Có minimum fare không?
B. Driver Dispatch
Khoảng cách được tính theo đường chim bay hay road distance?
Tiêu chí ưu tiên Driver là gì?
Chỉ ưu tiên khoảng cách hay còn rating, acceptance rate, loại xe?
Driver có bao nhiêu giây để phản hồi?
Timeout bao lâu?
Có gửi đồng thời cho nhiều Driver không?
Hay gửi tuần tự từng Driver?
Nếu nhiều Driver accept gần như đồng thời thì ai thắng?
Driver reject có bị ảnh hưởng ranking không?
C. Cancellation

Cần xác định:

Customer có thể hủy ở trạng thái nào?
Driver có thể hủy ở trạng thái nào?
Có cancellation fee không?
Ai chịu phí?
Có giới hạn số lần hủy không?
Operation có quyền force cancel không?
D. Payment
Payment method nào cần hỗ trợ trong MVP?
Nhà cung cấp payment nào?
Có authorization/capture hay charge trực tiếp?
Retry bao nhiêu lần?
Nếu payment failed thì Trip vẫn COMPLETED hay chuyển PAYMENT_PENDING?
Có refund không?
Ai có quyền refund?
Có reconciliation với payment provider không?
E. Location
Tần suất cập nhật GPS?
Lưu location trong bao lâu?
Có lưu toàn bộ route không?
Có cần realtime tracking không?
Accuracy tối thiểu bao nhiêu?
Map provider nào?
F. Notification
Kênh MVP là Push, SMS hay Email?
Notification nào bắt buộc?
Có retry không?
Nếu notification thất bại thì booking có bị ảnh hưởng không?
Có lưu notification history không?
G. Data Retention

Chưa xác định:

Trip history lưu bao lâu?
Payment transaction lưu bao lâu?
GPS data lưu bao lâu?
Audit log lưu bao lâu?
User data khi account bị deactivate xử lý thế nào?
11. Ưu tiên MVP trong 7 tuần

Vì thời gian triển khai chỉ 7 tuần, BA cần tránh đưa toàn bộ yêu cầu vào MVP mà không ưu tiên.

Có thể đề xuất phân loại sơ bộ:

Must Have
Authentication.
Customer profile.
Driver profile/vehicle.
Booking.
Dispatch Driver.
Accept/reject.
Trip lifecycle.
Driver location.
Fare calculation cơ bản.
Cash payment.
Một electronic payment provider.
Notification cơ bản.
Trip history.
Operation dashboard.
RBAC cơ bản.
Audit log cơ bản.
Should Have
Retry payment.
Báo cáo cơ bản.
ETA.
Advanced operation tools.
Notification retry.
Driver performance report.
Could Have
nhiều payment provider;
nhiều notification provider;
advanced pricing;
promotion;
advanced analytics;
nhiều loại dịch vụ mở rộng.

Tuy nhiên, đây chỉ là đề xuất ưu tiên ban đầu. Product Owner/Business phải xác nhận trước khi chốt scope 7 tuần.

12. Ước lượng các module chính

Từ yêu cầu sơ khởi, có thể chia hệ thống thành các domain/module:

CAB System
│
├── Customer Management
├── Driver Management
├── Vehicle Management
├── Booking / Trip
├── Driver Dispatch
├── Location / Tracking
├── Pricing / Fare
├── Payment
├── Notification
├── Rating
├── Operation / Admin
├── Reporting
├── Authentication / Authorization
└── Audit / Logging

Điểm đáng chú ý là Booking/Trip, Dispatch, Payment, Notification và Location là những khu vực có độ phức tạp nghiệp vụ và kỹ thuật cao nhất.

13. Các rủi ro được phát hiện ngay ở giai đoạn 1
Rủi ro	Mức độ	Ảnh hưởng
Pricing chưa chốt	Cao	Ảnh hưởng Fare/Payment
Dispatch criteria chưa chốt	Cao	Ảnh hưởng core business
Cancellation policy chưa chốt	Cao	Ảnh hưởng Trip/Fare
Payment provider chưa xác định	Cao	Ảnh hưởng integration
Notification channel chưa xác định	Trung bình/Cao	Ảnh hưởng architecture
Data retention chưa chốt	Trung bình	Ảnh hưởng database/compliance
Peak load chưa có số liệu	Cao	Khó xác định scalability
SLA chưa xác định	Cao	Khó thiết kế NFR
GPS/Map provider chưa xác định	Cao	Ảnh hưởng tracking/ETA
Scope 7 tuần lớn	Cao	Rủi ro trễ MVP
Offline/network behavior chưa rõ	Cao	Ảnh hưởng mobile app
Role/permission chưa chi tiết	Trung bình	Ảnh hưởng Admin


Bước 2: Tìm ra và xác nhận các stakeholder trong đây chia làm 2 cột cột thứ 1: tên của stakeholder, cột thứ 2: vai trò của nó, sau đó vẽ 1 ma trận tên stakeholder matrix cho biết sự ảnh hưởng tầm quan trọng vai trò của stakeholder trong hệ thống( dùng cộng cụ mermaid)
1. Danh sách Stakeholder
Tên Stakeholder	Vai trò
Ban giám đốc / Business Sponsor	Định hướng mục tiêu kinh doanh, phê duyệt ngân sách, phạm vi và các quyết định quan trọng của dự án.
Product Owner / Business Owner	Đại diện nghiệp vụ, xác định product vision, ưu tiên tính năng và xác nhận sản phẩm đáp ứng nhu cầu doanh nghiệp.
Business Analyst (BA)	Thu thập, phân tích, làm rõ và quản lý yêu cầu; kết nối Business với đội phát triển.
Khách hàng (Customer)	Người sử dụng CAB để đăng ký, đặt xe, theo dõi chuyến, thanh toán và đánh giá tài xế.
Tài xế (Driver)	Nhận và thực hiện chuyến, cập nhật trạng thái, vị trí và thông tin phương tiện.
Nhân viên vận hành (Operation Staff)	Theo dõi chuyến, quản lý tài xế/khách hàng/xe và hỗ trợ xử lý các tình huống bất thường.
Quản trị hệ thống (System Administrator)	Quản lý cấu hình, tài khoản, role/permission và các vấn đề vận hành kỹ thuật của hệ thống.
Bộ phận tài chính / kế toán	Theo dõi doanh thu, giao dịch, đối soát và các vấn đề liên quan đến thanh toán.
Bộ phận CSKH	Hỗ trợ khách hàng, xử lý khiếu nại và các vấn đề phát sinh trong quá trình đặt/thực hiện chuyến.
Đội phát triển phần mềm (Development Team)	Phân tích kỹ thuật, xây dựng và tích hợp các chức năng của CAB.
QA / Tester	Kiểm thử hệ thống, xác nhận chức năng và chất lượng sản phẩm theo yêu cầu.
DevOps / IT Operations	Triển khai, giám sát, vận hành hạ tầng và đảm bảo khả năng mở rộng/ổn định của hệ thống.
Payment Provider	Cung cấp dịch vụ thanh toán điện tử và trả kết quả giao dịch cho CAB.
Map / Location Provider	Cung cấp bản đồ, tọa độ, khoảng cách, route và/hoặc ETA phục vụ đặt xe và tracking.
Notification Provider	Cung cấp các kênh gửi Push Notification, SMS, Email hoặc các kênh khác.
Cơ quan quản lý / pháp lý	Có thể liên quan đến các yêu cầu về bảo vệ dữ liệu cá nhân, giao dịch điện tử, lưu trữ và vận hành dịch vụ.

Lưu ý BA: Một số stakeholder như CSKH, Finance, System Administrator, Map Provider... không được nêu trực tiếp trong đề bài nhưng được suy ra hợp lý từ nghiệp vụ. Cần xác nhận lại với ABC trước khi chốt stakeholder register.

2. Stakeholder Matrix

Để đánh giá stakeholder, sử dụng ma trận Power/Influence – Interest:

Power/Influence: Mức độ stakeholder có khả năng tác động đến quyết định và kết quả dự án.
Interest: Mức độ stakeholder quan tâm và bị ảnh hưởng bởi hệ thống.
Phân loại
Nhóm	Stakeholder tiêu biểu	Cách quản lý
High Power – High Interest	Ban giám đốc, Product Owner/Business Owner, Operation Manager	Manage Closely – tham gia quyết định và trao đổi thường xuyên
High Power – Low/Medium Interest	Finance, System Administrator, Legal/Compliance	Keep Satisfied – cung cấp thông tin cần thiết, tham vấn khi có thay đổi
Low/Medium Power – High Interest	Customer, Driver, Operation Staff, CSKH, BA	Keep Informed / Involve Closely – thường xuyên lấy feedback
Low Power – Low Interest	Một số external provider hoặc stakeholder hỗ trợ	Monitor – theo dõi và quản lý theo nhu cầu
Mermaid – Stakeholder Matrix

Có thể sử dụng đoạn Mermaid dưới đây để vẽ Power/Interest Matrix:

quadrantChart
    title CAB System - Stakeholder Matrix
    x-axis "Low Interest" --> "High Interest"
    y-axis "Low Influence" --> "High Influence"


    quadrant-1 "Manage Closely"
    quadrant-2 "Keep Satisfied"
    quadrant-3 "Monitor"
    quadrant-4 "Keep Informed"


    "Ban giám đốc / Sponsor": [0.85, 0.95]
    "Product Owner / Business Owner": [0.95, 0.90]
    "Operation Manager": [0.90, 0.82]


    "Finance / Kế toán": [0.55, 0.70]
    "System Administrator": [0.55, 0.72]
    "Legal / Compliance": [0.35, 0.68]


    "Customer": [0.92, 0.48]
    "Driver": [0.90, 0.52]
    "Operation Staff": [0.88, 0.62]
    "CSKH": [0.78, 0.45]
    "Business Analyst": [0.95, 0.65]


    "Development Team": [0.78, 0.40]
    "QA / Tester": [0.70, 0.30]
    "DevOps / IT Operations": [0.62, 0.55]


    "Payment Provider": [0.30, 0.45]
    "Map / Location Provider": [0.25, 0.30]
    "Notification Provider": [0.20, 0.25]
Cách đọc ma trận

1. Manage Closely – ảnh hưởng cao, quan tâm cao

Các stakeholder quan trọng nhất:

Ban giám đốc / Sponsor
Product Owner / Business Owner
Operation Manager

Đây là nhóm BA cần trao đổi thường xuyên vì họ có quyền quyết định phạm vi, ưu tiên và chính sách nghiệp vụ.

2. Keep Satisfied – ảnh hưởng cao

Ví dụ:

Finance/Kế toán
System Administrator
Legal/Compliance

Họ không nhất thiết tham gia mọi cuộc họp nhưng các yêu cầu của họ có thể ảnh hưởng trực tiếp đến Payment, Security, Data Retention và vận hành.

3. Keep Informed – quan tâm cao

Ví dụ:

Customer
Driver
Operation Staff
CSKH
BA

Đây là nhóm cần được lấy feedback thường xuyên vì họ trực tiếp sử dụng hoặc phân tích hệ thống.

4. Monitor

Các external provider như:

Payment Provider
Map/Location Provider
Notification Provider

cần được quản lý thông qua integration requirements, SLA và contract/API specification.

3. Kết luận Bước 2

Stakeholder quan trọng nhất đối với dự án CAB có thể tập trung thành 4 nhóm:

                    CAB SYSTEM
                        │
        ┌───────────────┼────────────────┐
        │               │                │
     BUSINESS          USER           INTERNAL
        │               │                │
  Sponsor/PO       Customer/Driver    Operation
  Management                         Finance/CSKH
        │
        └───────────────┬────────────────┘
                        │
                    EXTERNAL
                        │
          Payment / Map / Notification
