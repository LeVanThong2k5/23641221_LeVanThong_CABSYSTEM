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

Bước 3: Xác định mục tiêu của business goal, BG01 là cái gì, BG02 là cái gì, làm giảm thời gian tìm tài xế, mục đích hệ thống có chức năng tìm tài xế, hỗ trọ cho phép thanh toán bằng tiền mặt hoặc trực tuyến
Business Goals
Mã	Business Goal	Mục tiêu
BG01	Tự động hóa quy trình tìm và phân công tài xế	Hệ thống tự động tìm tài xế phù hợp dựa trên vị trí, trạng thái sẵn sàng và các tiêu chí vận hành, giảm sự phụ thuộc vào việc điều phối thủ công.
BG02	Giảm thời gian tìm tài xế	Rút ngắn thời gian từ lúc khách hàng gửi yêu cầu đặt xe đến khi có tài xế nhận chuyến, đồng thời tự động tìm tài xế khác nếu tài xế được đề xuất từ chối hoặc không phản hồi.
BG03	Hỗ trợ thanh toán linh hoạt	Cho phép khách hàng thanh toán bằng tiền mặt hoặc phương thức thanh toán điện tử, đồng thời tích hợp với Payment Provider mà không lưu trực tiếp thông tin nhạy cảm của thẻ/tài khoản trong CAB.
BG04	Nâng cao trải nghiệm khách hàng	Cho phép khách hàng đặt xe, theo dõi trạng thái chuyến, biết thông tin tài xế/ETA, xem lịch sử và đánh giá tài xế.
BG05	Nâng cao hiệu quả vận hành	Cung cấp công cụ để nhân viên vận hành theo dõi chuyến, quản lý tài xế, xử lý sự cố và tra cứu giao dịch.
BG06	Xây dựng nền tảng có khả năng mở rộng	Cho phép hệ thống phục vụ lượng lớn khách hàng/tài xế và có thể bổ sung dịch vụ, payment method, notification provider hoặc các thành phần kỹ thuật mới trong tương lai.
BG07	Đảm bảo tính ổn định và bảo mật	Hạn chế việc lỗi của Payment/Notification làm ảnh hưởng toàn bộ hệ thống, đồng thời bảo vệ dữ liệu cá nhân, vị trí, giao dịch và kiểm soát quyền truy cập.
Mối quan hệ giữa các mục tiêu
flowchart LR
    BG01["BG01 - Tự động tìm và phân công tài xế"]
    BG02["BG02 - Giảm thời gian tìm tài xế"]
    BG03["BG03 - Hỗ trợ thanh toán tiền mặt / trực tuyến"]


    F1["Chức năng Driver Dispatch"]
    F2["Chức năng tìm Driver gần khách"]
    F3["Cơ chế Reject / Timeout / Retry"]
    F4["Cash Payment"]
    F5["Online Payment"]


    BG01 --> F1
    BG01 --> F2
    BG02 --> F3
    BG02 --> F2
    BG03 --> F4
    BG03 --> F5

Ý nghĩa: BG01 và BG02 liên quan trực tiếp đến Driver Dispatch, còn BG03 là mục tiêu nghiệp vụ dẫn đến nhóm chức năng Payment. Đây sẽ là cơ sở để sang bước tiếp theo xác định Business Requirement (BR) và Functional Requirement (FR).

Bước 4 xác định phạm vi yêu cầu để thực hiện, ví dụ, quản lý khách hàng, quản lý tài xế, xác định các modun cơ bản, xác định các phần mềm mvd, cái gì nên làm và cái gì không nên làm, làm theo dạng markdown
1. Phạm vi tổng thể

Phạm vi MVP của CAB System nên tập trung vào quy trình cốt lõi:

Đăng ký → Đặt xe → Tìm tài xế → Nhận chuyến → Thực hiện chuyến → Tính cước → Thanh toán → Thông báo → Đánh giá

Ngoài ra cần có Admin/Operation để doanh nghiệp quản lý và giám sát hoạt động.

2. Các module cơ bản của hệ thống
Mã	Module	Nội dung chính	MVP
M01	Quản lý khách hàng	Đăng ký, đăng nhập, hồ sơ, lịch sử chuyến	✅ Nên làm
M02	Quản lý tài xế	Hồ sơ, trạng thái hoạt động, thông tin phương tiện	✅ Nên làm
M03	Quản lý phương tiện	Loại xe, biển số, thông tin xe	✅ Nên làm
M04	Đặt xe	Điểm đón, điểm đến, loại xe, tạo yêu cầu	✅ Nên làm
M05	Tìm & phân công tài xế	Tìm Driver phù hợp, accept/reject, timeout, retry	✅ Bắt buộc
M06	Quản lý chuyến đi	Theo dõi và cập nhật trạng thái Trip	✅ Bắt buộc
M07	Định vị & ETA	Vị trí Driver, khoảng cách, thời gian dự kiến	✅ Nên làm
M08	Tính cước	Xác định fare sau khi hoàn thành chuyến	✅ Bắt buộc
M09	Thanh toán	Tiền mặt + thanh toán trực tuyến	✅ Bắt buộc
M10	Thông báo	Thông báo cho Customer/Driver	✅ Bắt buộc
M11	Đánh giá	Customer đánh giá Driver sau chuyến	✅ Nên làm
M12	Quản trị & vận hành	Quản lý Customer, Driver, Vehicle, Trip	✅ Bắt buộc
M13	Phân quyền	Role/Permission cho nhân viên	✅ Bắt buộc
M14	Báo cáo	Trip, doanh thu, hoàn thành, hủy	🟡 Cơ bản
M15	Audit Log	Lưu vết thao tác quan trọng	✅ Nên làm
M16	Khuyến mãi	Voucher, discount, campaign	❌ Không làm MVP
M17	Loyalty	Điểm thưởng, membership	❌ Không làm MVP
M18	Corporate Account	Tài khoản doanh nghiệp	❌ Không làm MVP
M19	Advanced Analytics	BI, dashboard phân tích nâng cao	❌ Không làm MVP
M20	Multi-service	Giao hàng, thuê xe, dịch vụ khác	❌ Không làm MVP
3. Phân chia phạm vi theo chức năng
3.1. Quản lý khách hàng
Nên làm
Đăng ký tài khoản.
Đăng nhập.
Đăng xuất.
Cập nhật thông tin cá nhân.
Xem lịch sử chuyến.
Xem thông tin chuyến.
Xem số tiền phải thanh toán.
Đánh giá tài xế.
Không nên làm trong MVP
Loyalty/điểm thưởng.
Membership.
Social login nếu chưa cần thiết.
Referral.
Chương trình khách hàng thân thiết.
4. Quản lý tài xế
Nên làm
Tạo tài khoản Driver.
Cập nhật hồ sơ.
Quản lý thông tin phương tiện.
Online/Offline.
Available/Unavailable.
Nhận booking.
Accept/Reject booking.
Cập nhật trạng thái chuyến.
Gửi vị trí.
Không nên làm trong MVP
Hệ thống thưởng Driver phức tạp.
Xếp hạng Driver nâng cao.
Gamification.
Tự động tính hoa hồng phức tạp.
5. Đặt xe

Customer có thể:

Nhập điểm đón
      ↓
Nhập điểm đến
      ↓
Chọn loại xe
      ↓
Xác nhận đặt xe
      ↓
Tạo Booking
      ↓
Tìm Driver
Nên làm
Pickup location.
Destination.
Vehicle type.
Create booking.
Cancel booking theo policy.
Cần xác nhận
Có cho phép đặt xe trước không?
Có đặt xe cho người khác không?
Có nhiều điểm đến không?
Có chuyến khứ hồi không?

Nếu chưa có yêu cầu, không đưa vào MVP.

6. Tìm và phân công tài xế

Đây là module quan trọng nhất của CAB.

Nên làm
Booking Created
       ↓
Tìm Driver phù hợp
       ↓
Ưu tiên Driver gần
       ↓
Gửi Request
       ↓
 ┌─────┴─────┐
Accept      Reject/Timeout
  ↓              ↓
Assign       Tìm Driver khác

Hệ thống phải:

tìm Driver đang available;
kiểm tra loại xe;
xác định Driver phù hợp;
ưu tiên Driver gần khách;
gửi yêu cầu;
xử lý timeout;
xử lý reject;
tiếp tục tìm Driver khác;
thông báo nếu không tìm được.
Không nên làm MVP
AI/ML dự đoán Driver.
Dynamic dispatch quá phức tạp.
Thuật toán tối ưu hàng triệu Driver.
Driver bidding.
Multi-driver assignment phức tạp.

Có thể thiết kế architecture để sau này mở rộng, nhưng MVP nên dùng rule-based dispatch.

7. Quản lý chuyến đi
MVP

Trip State Machine:

REQUESTED
    ↓
SEARCHING_DRIVER
    ↓
DRIVER_ASSIGNED
    ↓
DRIVER_ARRIVING
    ↓
DRIVER_ARRIVED
    ↓
PASSENGER_PICKED_UP
    ↓
IN_PROGRESS
    ↓
COMPLETED

Các trạng thái kết thúc:

CANCELLED
NO_DRIVER_FOUND
FAILED

Cần xác định rõ ai có quyền thay đổi từng trạng thái.

8. Tính cước
Nên làm

Hệ thống phải có một pricing engine cơ bản:

Fare
 =
Base Fare
+ Distance Fee
+ Time Fee
+ Surcharge
- Discount

Nhưng công thức thực tế chưa được chốt, vì vậy BA cần xác nhận với Business trước khi development.

Không nên làm MVP
Dynamic pricing phức tạp.
Pricing theo AI.
Hàng chục loại promotion.
Pricing engine quá phức tạp nếu Business chưa có policy.
9. Thanh toán
Nên làm

Hỗ trợ:

                Payment
                   │
          ┌────────┴────────┐
          ↓                 ↓
       Cash              Online
                            ↓
                   Payment Provider

Online payment cần:

tạo payment request;
nhận kết quả;
success/failure;
retry theo policy;
lưu transaction/reference ID.

Không lưu trực tiếp thông tin nhạy cảm của thẻ/tài khoản thanh toán.

Không nên làm MVP
Tích hợp nhiều Payment Provider cùng lúc.
Ví điện tử nội bộ.
Subscription.
Buy Now Pay Later.
Loyalty payment.

Nên thiết kế Payment Adapter/Interface để sau này có thể thêm provider mới.

10. Notification
Nên làm

Các event quan trọng:

Event	Customer	Driver
Booking created	✅	
Driver assigned	✅	
New booking		✅
Driver arrived	✅	
Trip completed	✅	
Payment result	✅	
Trip cancelled	✅	✅
Không nên làm MVP

Không cần triển khai ngay quá nhiều channel.

Có thể bắt đầu:

Push Notification

và thiết kế abstraction để sau này thêm:

SMS;
Email;
WhatsApp/Zalo hoặc channel khác.
11. Quản trị và vận hành
Nên làm

Operation Dashboard cần cho phép:

xem Customer;
xem Driver;
xem Vehicle;
xem Trip;
xem Trip đang diễn ra;
xem trạng thái Driver;
hỗ trợ Trip lỗi;
tra cứu transaction;
phân quyền;
xem audit log.
Không nên làm MVP
BI dashboard quá phức tạp.
AI analytics.
Forecasting.
Advanced workforce planning.
12. Báo cáo
MVP nên có báo cáo cơ bản
Tổng số chuyến.
Số chuyến hoàn thành.
Số chuyến hủy.
Doanh thu.
Tỷ lệ hoàn thành.
Tỷ lệ hủy.
Số chuyến/Driver.
Để phase sau
Driver heatmap.
Revenue forecasting.
Customer segmentation.
Predictive analytics.
AI recommendation.
13. Những gì nên làm và không nên làm
✅ NÊN LÀM trong 7 tuần
 Customer Management
 Driver Management
 Vehicle Management
 Booking
 Driver Dispatch
 Trip Management
 Driver Location
 Fare Calculation cơ bản
 Cash Payment
 Một Online Payment Provider
 Notification cơ bản
 Trip History
 Rating
 Operation Dashboard cơ bản
 Authentication
 Role/Permission
 Audit Log cơ bản
 Báo cáo cơ bản
❌ KHÔNG NÊN LÀM trong MVP
 Loyalty/Membership
 Voucher/Promotion nâng cao
 Corporate Account
 Ride Sharing
 Delivery
 Rental
 AI Driver Matching
 Advanced Analytics
 Nhiều Payment Provider
 Nhiều Notification Provider
 Dynamic Pricing phức tạp
 Multi-country
 Multi-currency
 Các tính năng chưa có Business Rule rõ ràng
14. MVP Scope đề xuất

Có thể đóng phạm vi MVP thành 8 nhóm chính:

flowchart TB
    CAB["CAB System - MVP"]


    CAB --> A["1. Customer"]
    CAB --> B["2. Driver & Vehicle"]
    CAB --> C["3. Booking & Trip"]
    CAB --> D["4. Driver Dispatch"]
    CAB --> E["5. Fare & Payment"]
    CAB --> F["6. Notification"]
    CAB --> G["7. Operation & Admin"]
    CAB --> H["8. Reporting & Audit"]


    A --> A1["Register / Login"]
    A --> A2["Profile"]
    A --> A3["Booking History"]
    A --> A4["Rating"]


    B --> B1["Driver Profile"]
    B --> B2["Vehicle"]
    B --> B3["Online / Available"]
    B --> B4["Location"]


    C --> C1["Create Booking"]
    C --> C2["Trip Status"]
    C --> C3["Cancel"]


    D --> D1["Find Driver"]
    D --> D2["Accept / Reject"]
    D --> D3["Timeout / Retry"]


    E --> E1["Fare"]
    E --> E2["Cash"]
    E --> E3["Online Payment"]


    F --> F1["Customer Notification"]
    F --> F2["Driver Notification"]


    G --> G1["Manage Customer"]
    G --> G2["Manage Driver"]
    G --> G3["Monitor Trip"]
    G --> G4["RBAC"]


    H --> H1["Basic Reports"]
    H --> H2["Audit Log"]
15. Phạm vi không làm nhưng phải thiết kế để mở rộng

Một điểm rất quan trọng trong dự án này:

Không làm trong MVP ≠ không cần quan tâm về kiến trúc.

Ví dụ:

Payment

MVP:

CAB → Payment Provider A

Nhưng nên thiết kế:

CAB
 │
Payment Interface
 │
 ├── Provider A
 ├── Provider B (future)
 └── Provider C (future)
Notification

MVP:

CAB → Push Provider

Có thể mở rộng:

Notification Service
       │
       ├── Push
       ├── SMS
       ├── Email
       └── Other Channel
Service

MVP:

CAB
 └── Ride Service

Tương lai:

CAB Platform
 ├── Ride
 ├── Delivery
 ├── Rental
 └── Other Services

Bước 5: Sau khi xác nhận với khách hàng rồi chuyển các yêu cầu thành business requirement, mỗi business requirement kí hiệu là BR, BR01 là gì, BR02 là gì, BR03 là gì, lập 1 bảng cột thứ 1 là mã với số thứ tự, cột thứ 2 là tên, cột thứ 3 là diễn giải ra
Sau khi BA đã phân tích, làm rõ và xác nhận phạm vi với khách hàng, các mục tiêu kinh doanh được chuyển thành Business Requirement (BR).

Ở cấp độ này, BR mô tả doanh nghiệp cần hệ thống đáp ứng điều gì, chưa đi sâu vào cách hệ thống thực hiện về mặt kỹ thuật.

Mã	Tên Business Requirement	Diễn giải
BR01	Quản lý khách hàng	Hệ thống phải cho phép doanh nghiệp quản lý thông tin khách hàng, đồng thời khách hàng có thể đăng ký, đăng nhập, cập nhật thông tin cá nhân và xem lịch sử chuyến đi.
BR02	Quản lý tài xế	Hệ thống phải hỗ trợ quản lý tài xế, bao gồm hồ sơ, trạng thái hoạt động và thông tin phương tiện của tài xế.
BR03	Đặt xe	Hệ thống phải cho phép khách hàng nhập điểm đón, điểm đến, lựa chọn loại xe và gửi yêu cầu đặt xe.
BR04	Tự động tìm tài xế	Hệ thống phải tự động tìm các tài xế phù hợp dựa trên vị trí, trạng thái sẵn sàng, loại xe và các tiêu chí vận hành đã được doanh nghiệp xác định.
BR05	Phân công tài xế	Hệ thống phải hỗ trợ tự động phân công tài xế phù hợp cho yêu cầu đặt xe và thông báo kết quả cho khách hàng.
BR06	Xử lý tài xế từ chối hoặc không phản hồi	Khi tài xế được đề xuất không phản hồi hoặc từ chối chuyến, hệ thống phải tiếp tục tìm tài xế khác mà không yêu cầu khách hàng tạo lại yêu cầu.
BR07	Giảm thời gian tìm tài xế	Hệ thống phải hỗ trợ rút ngắn thời gian từ khi khách hàng gửi yêu cầu đến khi chuyến được tài xế nhận, thông qua cơ chế tìm và phân công tài xế tự động.
BR08	Theo dõi chuyến đi	Hệ thống phải cho phép khách hàng và nhân viên vận hành theo dõi trạng thái chuyến đi, thông tin tài xế và thời gian dự kiến tài xế đến.
BR09	Quản lý trạng thái chuyến	Hệ thống phải hỗ trợ quản lý vòng đời chuyến đi từ lúc tạo yêu cầu, tìm tài xế, tài xế đến điểm đón, đón khách, thực hiện chuyến đến khi hoàn thành hoặc hủy.
BR10	Theo dõi vị trí tài xế	Hệ thống phải lưu và sử dụng thông tin vị trí của tài xế để hỗ trợ tìm tài xế gần khách hàng và cung cấp thông tin ETA.
BR11	Tính cước	Hệ thống phải xác định số tiền khách hàng cần thanh toán dựa trên loại dịch vụ và các thông tin của chuyến đi theo chính sách tính cước của doanh nghiệp.
BR12	Thanh toán tiền mặt	Hệ thống phải cho phép khách hàng thanh toán chuyến đi bằng tiền mặt theo chính sách của doanh nghiệp.
BR13	Thanh toán trực tuyến	Hệ thống phải hỗ trợ khách hàng thanh toán điện tử thông qua nhà cung cấp dịch vụ thanh toán bên ngoài.
BR14	Xử lý thanh toán thất bại	Khi thanh toán trực tuyến thất bại, hệ thống phải thông báo cho khách hàng và hỗ trợ xử lý lại theo chính sách thanh toán của doanh nghiệp.
BR15	Bảo vệ thông tin thanh toán	Hệ thống không được lưu trực tiếp các thông tin nhạy cảm của thẻ hoặc tài khoản thanh toán trong hệ thống CAB.
BR16	Thông báo	Hệ thống phải cung cấp cơ chế thông báo cho khách hàng và tài xế về các sự kiện quan trọng trong quá trình đặt và thực hiện chuyến.
BR17	Đánh giá tài xế	Sau khi chuyến hoàn thành, hệ thống phải cho phép khách hàng đánh giá tài xế.
BR18	Quản lý vận hành	Hệ thống phải cung cấp giao diện quản trị để nhân viên vận hành quản lý khách hàng, tài xế, phương tiện và chuyến đi.
BR19	Giám sát và xử lý sự cố	Nhân viên vận hành phải có khả năng theo dõi các chuyến đang diễn ra, kiểm tra trạng thái tài xế và hỗ trợ xử lý các trường hợp chuyến bị lỗi.
BR20	Phân quyền người dùng	Hệ thống phải kiểm soát quyền truy cập đối với các chức năng quản trị để nhân viên chỉ thực hiện được những thao tác được cấp quyền.
BR21	Báo cáo hoạt động	Hệ thống phải cung cấp báo cáo về số lượng chuyến, doanh thu, tỷ lệ hoàn thành, tỷ lệ hủy và hiệu quả hoạt động của tài xế.
BR22	Lưu vết hoạt động	Hệ thống phải lưu lại các thao tác quan trọng để phục vụ kiểm tra, truy vết và xử lý sự cố.
BR23	Khả năng mở rộng	Hệ thống phải có khả năng mở rộng để đáp ứng số lượng lớn khách hàng, tài xế và chuyến đi mà không phải thay đổi toàn bộ hệ thống.
BR24	Khả năng mở rộng dịch vụ	Hệ thống phải cho phép doanh nghiệp bổ sung các loại dịch vụ mới trong tương lai mà hạn chế ảnh hưởng đến các chức năng hiện có.
BR25	Khả năng mở rộng phương thức thanh toán	Hệ thống phải cho phép tích hợp thêm phương thức hoặc nhà cung cấp thanh toán mới trong tương lai.
BR26	Khả năng mở rộng kênh thông báo	Hệ thống phải cho phép bổ sung các kênh thông báo mới mà không phải thay đổi toàn bộ hệ thống.
BR27	Tính ổn định	Lỗi tại một thành phần như thanh toán hoặc thông báo không được làm cho toàn bộ chức năng đặt xe ngừng hoạt động.
BR28	Bảo mật dữ liệu	Hệ thống phải bảo vệ thông tin cá nhân, thông tin phương tiện, dữ liệu vị trí và dữ liệu giao dịch của người dùng.
Tóm tắt các BR cốt lõi

Nếu cần trình bày ngắn gọn trong tài liệu BA, có thể nhóm 28 BR trên thành các nhóm chính:

BR01 - BR02       → Quản lý Customer / Driver
BR03              → Đặt xe
BR04 - BR07       → Tìm và phân công Driver
BR08 - BR10       → Theo dõi và quản lý Trip
BR11 - BR15       → Fare & Payment
BR16 - BR17       → Notification & Rating
BR18 - BR22       → Operation / Admin / Reporting
BR23 - BR27       → Scalability / Reliability
BR28              → Security

Điểm quan trọng: BR là yêu cầu ở góc nhìn nghiệp vụ. Ví dụ:

BR04 – Tự động tìm tài xế: Doanh nghiệp cần hệ thống tự động tìm tài xế phù hợp.

Sau này khi chuyển sang Functional Requirement (FR), BR04 có thể được phân rã thành các yêu cầu cụ thể hơn như:

FR04.01: Hệ thống xác định các tài xế đang Available.
FR04.02: Hệ thống lọc tài xế theo loại xe.
FR04.03: Hệ thống xác định khoảng cách giữa tài xế và điểm đón.
FR04.04: Hệ thống sắp xếp tài xế theo tiêu chí ưu tiên.
FR04.05: Hệ thống gửi yêu cầu chuyến cho tài xế được chọn.

Như vậy có thể tạo được chuỗi truy xuất:

Business Goal → Business Requirement (BR) → Functional Requirement (FR) → Use Case → Test Case.

Bước 6: xây dựng business process đặt chuyến VD: grab, khách hàng muốn đặt chuyến đầu tiên tạo chuyến đi xác nhận điểm đón, 
điểm đến,hệ thống xác nhận, tìm tài xế, nếu tìm ra tài xế nếu tài xế chấp nhận thì đi
nếu tài xế không chấp nhận thì thông báo cho các tài xế khác, 
nếu chưa tìm được tài xế thì tiếp tục chờ tài xế xác nhận

1. Business Process tổng quát

Mục tiêu: Cho phép khách hàng tạo chuyến, hệ thống xác nhận thông tin, tự động tìm tài xế phù hợp và xử lý trường hợp tài xế từ chối/không phản hồi.

Quy trình
Khách hàng tạo yêu cầu đặt chuyến.
Khách hàng nhập/xác nhận:
Điểm đón.
Điểm đến.
Loại xe.
Hệ thống kiểm tra và xác nhận thông tin chuyến.
Hệ thống bắt đầu tìm tài xế phù hợp.
Nếu chưa tìm được tài xế:
Tiếp tục tìm kiếm.
Khách hàng tiếp tục chờ.
Nếu tìm được tài xế:
Gửi yêu cầu nhận chuyến cho tài xế.
Nếu tài xế chấp nhận:
Hệ thống xác nhận tài xế.
Thông báo cho khách hàng.
Chuyến được bắt đầu.
Nếu tài xế từ chối hoặc không phản hồi:
Hệ thống loại tài xế đó khỏi lượt tìm hiện tại.
Tiếp tục tìm tài xế khác.
Nếu không còn tài xế phù hợp:
Thông báo cho khách hàng rằng chưa tìm được tài xế.
Chuyến chuyển sang trạng thái phù hợp theo business rule.
2. Business Process dạng Flowchart
flowchart TD
    A([Bắt đầu]) --> B["Khách hàng tạo yêu cầu đặt chuyến"]


    B --> C["Nhập / xác nhận điểm đón"]
    C --> D["Nhập / xác nhận điểm đến"]
    D --> E["Chọn loại xe"]


    E --> F["Hệ thống kiểm tra thông tin chuyến"]


    F --> G{"Thông tin hợp lệ?"}


    G -- "Không" --> H["Thông báo lỗi và yêu cầu khách hàng chỉnh sửa"]
    H --> C


    G -- "Có" --> I["Tạo chuyến / Booking"]
    I --> J["Hệ thống tìm tài xế phù hợp"]


    J --> K{"Tìm được tài xế?"}


    K -- "Chưa tìm được" --> L["Tiếp tục tìm kiếm"]
    L --> M["Khách hàng tiếp tục chờ"]
    M --> J


    K -- "Có" --> N["Gửi yêu cầu nhận chuyến cho tài xế"]


    N --> O{"Tài xế chấp nhận?"}


    O -- "Có" --> P["Xác nhận tài xế"]
    P --> Q["Thông báo tài xế cho khách hàng"]
    Q --> R["Chuyến được xác nhận"]
    R --> S([Tiếp tục thực hiện chuyến])


    O -- "Không / Từ chối" --> T["Thông báo / chuyển sang tài xế khác"]
    T --> J
3. Business Process chi tiết theo Actor
Bước	Customer	CAB System	Driver
1	Tạo yêu cầu đặt chuyến		
2	Nhập điểm đón		
3	Nhập điểm đến		
4	Chọn loại xe		
5	Xác nhận đặt chuyến	Kiểm tra thông tin	
6	Chờ	Tạo Booking	
7	Chờ	Tìm Driver phù hợp	
8	Chờ	Chọn Driver	
9	Chờ	Gửi yêu cầu	Nhận thông báo chuyến
10	Chờ	Chờ phản hồi	Accept / Reject
11A	Nhận thông báo	Xác nhận Driver	Nhận chuyến
11B	Chờ	Nếu Reject/Timeout → tìm Driver khác	
12	Theo dõi Driver	Cập nhật trạng thái	Bắt đầu đến điểm đón
4. Các nhánh xử lý quan trọng
Trường hợp 1 – Tìm được tài xế và tài xế chấp nhận
Customer tạo chuyến
        ↓
CAB tìm Driver
        ↓
Tìm thấy Driver
        ↓
Gửi yêu cầu
        ↓
Driver ACCEPT
        ↓
CAB xác nhận Driver
        ↓
Thông báo Customer
        ↓
Bắt đầu chuyến
Trường hợp 2 – Tài xế từ chối
CAB tìm Driver A
        ↓
Gửi yêu cầu
        ↓
Driver A REJECT
        ↓
CAB tìm Driver B
        ↓
Gửi yêu cầu
        ↓
Driver B ACCEPT
        ↓
Xác nhận chuyến

Điểm quan trọng là Customer không phải tạo lại chuyến.

Trường hợp 3 – Tài xế không phản hồi
CAB gửi request
       ↓
Chờ Driver phản hồi
       ↓
Timeout
       ↓
Driver bị xem là không phản hồi
       ↓
Tìm Driver khác
Trường hợp 4 – Chưa tìm được tài xế
Customer tạo chuyến
       ↓
CAB tìm Driver
       ↓
Chưa có Driver phù hợp
       ↓
Tiếp tục tìm
       ↓
Customer tiếp tục chờ
       ↓
Tìm được Driver?
    ↙        ↘
  Chưa        Có
   ↓           ↓
Tiếp tục     Gửi request

Cần bổ sung một Business Rule quan trọng: Không nên để trạng thái "tiếp tục chờ" vô hạn. BA cần xác nhận với khách hàng thời gian tối đa tìm tài xế. Ví dụ nếu sau X phút không có tài xế thì hệ thống phải thông báo "Không tìm được tài xế" và kết thúc/hủy yêu cầu.

5. Trạng thái của Booking trong Business Process

Có thể sử dụng state flow sau:

stateDiagram-v2
    [*] --> REQUESTED


    REQUESTED --> SEARCHING_DRIVER: Xác nhận thông tin


    SEARCHING_DRIVER --> DRIVER_FOUND: Tìm thấy Driver
    SEARCHING_DRIVER --> NO_DRIVER_FOUND: Hết thời gian tìm


    DRIVER_FOUND --> WAITING_DRIVER_RESPONSE: Gửi request


    WAITING_DRIVER_RESPONSE --> DRIVER_ASSIGNED: Driver Accept
    WAITING_DRIVER_RESPONSE --> SEARCHING_DRIVER: Driver Reject
    WAITING_DRIVER_RESPONSE --> SEARCHING_DRIVER: Driver Timeout


    DRIVER_ASSIGNED --> DRIVER_ARRIVING


    NO_DRIVER_FOUND --> [*]

Bước 7: 
