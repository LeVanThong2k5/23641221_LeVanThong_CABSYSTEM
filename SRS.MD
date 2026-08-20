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

Bước 7: Busimess requirement phân rã thành các functional requirement phân rã yêu cầu dịch vụ, thiết kế các functional requirement, ví dụ FR1 tìm vị trí của khách hàng, FR2 chọn những thằng tài xế online, FR3 chọn loại xe, ưu tiên chọn những tài xế đánh giá cao, làm theo dạng markdown
Ở bước này, từ các Business Requirement (BR) đã xác định ở bước 5, BA tiếp tục phân rã thành các Functional Requirement (FR) cụ thể.

BR trả lời: Doanh nghiệp cần hệ thống đáp ứng điều gì?
FR trả lời: Hệ thống phải thực hiện chức năng gì để đáp ứng BR đó?

Ví dụ:

BR04 – Tự động tìm tài xế
↓
FR04.01 – Xác định vị trí khách hàng
FR04.02 – Lọc tài xế đang Online/Available
FR04.03 – Lọc tài xế theo loại xe
FR04.04 – Tính khoảng cách đến khách hàng
FR04.05 – Ưu tiên tài xế có rating cao
FR04.06 – Gửi yêu cầu nhận chuyến

1. Functional Requirement cho quy trình đặt chuyến
Mã FR	Tên Functional Requirement	Diễn giải
FR01	Xác định vị trí khách hàng	Hệ thống phải cho phép xác định vị trí hiện tại của khách hàng hoặc cho phép khách hàng nhập/chọn điểm đón trên bản đồ.
FR02	Nhập điểm đến	Hệ thống phải cho phép khách hàng nhập và xác nhận điểm đến của chuyến đi.
FR03	Chọn loại xe	Hệ thống phải hiển thị các loại xe/dịch vụ đang được hỗ trợ để khách hàng lựa chọn.
FR04	Tạo yêu cầu đặt chuyến	Hệ thống phải tạo Booking sau khi khách hàng xác nhận điểm đón, điểm đến và loại xe.
FR05	Kiểm tra thông tin Booking	Hệ thống phải kiểm tra tính hợp lệ của điểm đón, điểm đến và loại xe trước khi tạo Booking.
FR06	Xác định tài xế Online/Available	Hệ thống phải lọc danh sách tài xế đang ở trạng thái có thể nhận chuyến.
FR07	Lọc tài xế theo loại xe	Hệ thống chỉ được lựa chọn tài xế có phương tiện phù hợp với loại xe mà khách hàng đã chọn.
FR08	Xác định khoảng cách tài xế	Hệ thống phải xác định khoảng cách giữa vị trí tài xế và điểm đón của khách hàng.
FR09	Ưu tiên tài xế gần khách hàng	Hệ thống phải ưu tiên các tài xế có khoảng cách phù hợp/gần điểm đón theo quy tắc vận hành.
FR10	Ưu tiên tài xế có đánh giá cao	Hệ thống có thể sử dụng rating của tài xế như một tiêu chí ưu tiên khi lựa chọn tài xế.
FR11	Xếp hạng tài xế phù hợp	Hệ thống phải sắp xếp các tài xế phù hợp theo các tiêu chí được doanh nghiệp cấu hình.
FR12	Gửi yêu cầu nhận chuyến	Hệ thống phải gửi thông báo yêu cầu nhận chuyến đến tài xế được lựa chọn.
FR13	Chờ tài xế phản hồi	Hệ thống phải theo dõi thời gian tài xế phản hồi yêu cầu nhận chuyến.
FR14	Tài xế chấp nhận chuyến	Khi tài xế chấp nhận, hệ thống phải cập nhật tài xế vào Booking và xác nhận chuyến.
FR15	Tài xế từ chối chuyến	Khi tài xế từ chối, hệ thống phải loại tài xế đó khỏi lượt tìm hiện tại và tiếp tục tìm tài xế khác.
FR16	Xử lý tài xế không phản hồi	Nếu tài xế không phản hồi trong thời gian quy định, hệ thống phải xem yêu cầu là timeout và tiếp tục tìm tài xế khác.
FR17	Tìm tài xế tiếp theo	Khi tài xế từ chối hoặc timeout, hệ thống phải lựa chọn tài xế phù hợp tiếp theo mà không yêu cầu khách hàng tạo lại Booking.
FR18	Thông báo đã tìm được tài xế	Khi có tài xế nhận chuyến, hệ thống phải thông báo cho khách hàng thông tin tài xế.
FR19	Không tìm được tài xế	Nếu không còn tài xế phù hợp, hệ thống phải thông báo cho khách hàng theo chính sách của doanh nghiệp.
FR20	Theo dõi trạng thái Booking	Hệ thống phải cập nhật trạng thái Booking trong quá trình tìm và phân công tài xế.
2. Phân rã FR theo từng Business Requirement
BR01 – Quản lý khách hàng
BR01
│
├── FR01.01 – Đăng ký tài khoản
├── FR01.02 – Đăng nhập
├── FR01.03 – Đăng xuất
├── FR01.04 – Cập nhật thông tin cá nhân
├── FR01.05 – Xem thông tin tài khoản
└── FR01.06 – Xem lịch sử chuyến
BR02 – Quản lý tài xế
BR02
│
├── FR02.01 – Tạo tài khoản tài xế
├── FR02.02 – Cập nhật hồ sơ tài xế
├── FR02.03 – Quản lý thông tin phương tiện
├── FR02.04 – Chuyển trạng thái Online/Offline
├── FR02.05 – Chuyển trạng thái Available/Unavailable
└── FR02.06 – Cập nhật vị trí
BR03 – Đặt xe
BR03
│
├── FR03.01 – Xác định vị trí khách hàng
├── FR03.02 – Nhập điểm đón
├── FR03.03 – Nhập điểm đến
├── FR03.04 – Chọn loại xe
├── FR03.05 – Kiểm tra thông tin chuyến
└── FR03.06 – Tạo Booking
BR04 – Tự động tìm tài xế
BR04
│
├── FR04.01 – Lấy vị trí khách hàng
├── FR04.02 – Lấy danh sách Driver Available
├── FR04.03 – Lọc theo loại xe
├── FR04.04 – Xác định khoảng cách
├── FR04.05 – Xác định Driver phù hợp
├── FR04.06 – Xếp hạng Driver
└── FR04.07 – Chọn Driver ưu tiên
BR05 – Phân công tài xế
BR05
│
├── FR05.01 – Gửi yêu cầu cho Driver
├── FR05.02 – Nhận phản hồi Accept
├── FR05.03 – Xác nhận Driver
├── FR05.04 – Gán Driver vào Booking
└── FR05.05 – Thông báo Customer
BR06 – Xử lý Driver từ chối/không phản hồi
BR06
│
├── FR06.01 – Nhận Reject
├── FR06.02 – Theo dõi Timeout
├── FR06.03 – Loại Driver không phù hợp
├── FR06.04 – Tìm Driver tiếp theo
└── FR06.05 – Thông báo khi không còn Driver
3. Functional Requirement cho Trip
Mã	Tên	Diễn giải
FR21	Driver đã đến	Driver có thể cập nhật trạng thái đã đến điểm đón.
FR22	Đã đón khách	Driver có thể cập nhật trạng thái đã đón khách.
FR23	Bắt đầu chuyến	Driver có thể chuyển Trip sang trạng thái đang di chuyển.
FR24	Hoàn thành chuyến	Driver có thể cập nhật Trip là hoàn thành.
FR25	Hủy chuyến	Hệ thống phải hỗ trợ hủy chuyến theo chính sách đã xác nhận.
FR26	Theo dõi Trip	Customer có thể xem trạng thái hiện tại của Trip.
FR27	Hiển thị thông tin Driver	Customer có thể xem thông tin Driver được phân công.
FR28	Hiển thị ETA	Hệ thống phải cung cấp thời gian dự kiến Driver đến.
4. Functional Requirement cho Fare & Payment
Mã	Tên	Diễn giải
FR29	Tính cước	Hệ thống tính số tiền phải trả dựa trên pricing rule.
FR30	Hiển thị cước	Customer có thể xem số tiền phải thanh toán.
FR31	Thanh toán tiền mặt	Hệ thống ghi nhận chuyến được thanh toán bằng tiền mặt.
FR32	Tạo giao dịch online	Hệ thống tạo yêu cầu thanh toán tới Payment Provider.
FR33	Nhận kết quả thanh toán	Hệ thống tiếp nhận kết quả thành công/thất bại từ Payment Provider.
FR34	Xử lý payment failure	Hệ thống thông báo khi thanh toán thất bại và cho phép retry theo policy.
FR35	Lưu transaction reference	Hệ thống lưu mã tham chiếu giao dịch thay vì lưu dữ liệu nhạy cảm của thẻ/tài khoản.
5. Functional Requirement cho Notification
Mã	Tên	Diễn giải
FR36	Thông báo Booking	Thông báo cho Customer khi Booking được tiếp nhận.
FR37	Thông báo Driver nhận chuyến	Thông báo cho Customer khi có Driver nhận chuyến.
FR38	Thông báo Driver mới	Thông báo cho Driver khi có yêu cầu chuyến mới.
FR39	Thông báo Driver đến	Thông báo cho Customer khi Driver đến điểm đón.
FR40	Thông báo hoàn thành	Thông báo cho Customer khi Trip hoàn thành.
FR41	Thông báo Payment	Thông báo kết quả thanh toán cho Customer.
6. Functional Requirement cho Operation/Admin
Mã	Tên	Diễn giải
FR42	Quản lý Customer	Nhân viên có thể xem và quản lý thông tin Customer theo quyền được cấp.
FR43	Quản lý Driver	Nhân viên có thể xem và quản lý thông tin Driver.
FR44	Quản lý Vehicle	Nhân viên có thể quản lý thông tin phương tiện.
FR45	Giám sát Trip	Nhân viên có thể xem các Trip đang diễn ra.
FR46	Tra cứu giao dịch	Nhân viên có quyền có thể tra cứu lịch sử giao dịch.
FR47	Xử lý Trip lỗi	Nhân viên có thể hỗ trợ xử lý các Trip gặp vấn đề.
FR48	Phân quyền	Hệ thống kiểm tra quyền trước khi cho phép thực hiện chức năng quản trị.
FR49	Audit Log	Hệ thống ghi nhận các thao tác quan trọng của người dùng/quản trị viên.
FR50	Báo cáo	Hệ thống cung cấp các báo cáo cơ bản về Trip và doanh thu.
7. Thiết kế Functional Requirement cho chức năng tìm tài xế

Đây là phần nên đặc biệt chú trọng vì liên quan trực tiếp đến BG01 – Tự động tìm tài xế và BG02 – Giảm thời gian tìm tài xế.

flowchart TD
    A["Customer tạo Booking"] --> B["FR01: Xác định vị trí khách hàng"]
    B --> C["FR02: Xác định điểm đến"]
    C --> D["FR03: Xác định loại xe"]


    D --> E["FR06: Lấy Driver Online / Available"]
    E --> F["FR07: Lọc Driver theo loại xe"]
    F --> G["FR08: Tính khoảng cách"]
    G --> H["FR10: Xem xét Rating"]
    H --> I["FR11: Xếp hạng Driver"]


    I --> J{"Có Driver phù hợp?"}


    J -- "Có" --> K["FR12: Gửi yêu cầu nhận chuyến"]
    K --> L{"Driver phản hồi?"}


    L -- "Accept" --> M["FR14: Gán Driver"]
    M --> N["FR18: Thông báo Customer"]


    L -- "Reject" --> O["FR15: Loại Driver"]
    O --> E


    L -- "Timeout" --> P["FR16: Xử lý Timeout"]
    P --> E


    J -- "Không" --> Q["FR19: Thông báo chưa tìm được Driver"]
8. Lưu ý về tiêu chí "tài xế đánh giá cao"

Yêu cầu "ưu tiên tài xế đánh giá cao" là một Functional Requirement hợp lý, nhưng BA không nên tự biến nó thành rule cuối cùng nếu khách hàng chưa xác nhận.

Ví dụ cần xác nhận:

Hệ thống có ưu tiên Driver có rating cao hơn Driver gần hơn không?

Có thể xảy ra:

Driver A
- Khoảng cách: 1 km
- Rating: 4.2


Driver B
- Khoảng cách: 2 km
- Rating: 4.9

Nếu chỉ ưu tiên rating → chọn B.

Nếu chỉ ưu tiên khoảng cách → chọn A.

Nếu kết hợp → cần Business Rule, ví dụ:

Driver Score =
Distance Score
+ Rating Score
+ Availability Score

Công thức và trọng số phải được Business xác nhận, không nên để Developer tự quyết định.

9. Mapping từ Business Goal đến Functional Requirement
BG01 - Tự động tìm và phân công tài xế
       ↓
BR04 - Tự động tìm tài xế
BR05 - Phân công tài xế
       ↓
FR06 - Lọc Driver Available
FR07 - Lọc loại xe
FR08 - Tính khoảng cách
FR10 - Xem xét Rating
FR11 - Xếp hạng Driver
FR12 - Gửi Request
FR14 - Assign Driver
BG02 - Giảm thời gian tìm tài xế
       ↓
BR06 - Xử lý Reject / Timeout
BR07 - Giảm thời gian tìm Driver
       ↓
FR13 - Theo dõi phản hồi
FR15 - Xử lý Reject
FR16 - Xử lý Timeout
FR17 - Tìm Driver tiếp theo
FR19 - Xử lý không tìm được Driver
BG03 - Hỗ trợ thanh toán
       ↓
BR12 - Cash Payment
BR13 - Online Payment
BR14 - Payment Failure
       ↓
FR31 - Thanh toán tiền mặt
FR32 - Tạo giao dịch online
FR33 - Nhận kết quả Payment
FR34 - Retry Payment
Kết quả của Bước 7

Có thể hiểu chuỗi phân tích của dự án hiện tại như sau:

Business Goal (BG)
↓
Business Requirement (BR)
↓
Functional Requirement (FR)
↓
Use Case
↓
User Story / Acceptance Criteria
↓
Test Case

Bước 8: Thiết kế business rule, và thiết kế Accession, ví dụ xác tài xế sẵn sàng mới được nhận chuyến, quá thời hạn tài xế không chịu access thì sẽ restar qua thằng tài xế tiếp theo, làm theo dạng markdown
1. Business Rules – Quy tắc nghiệp vụ
Mã	Business Rule	Diễn giải
BRL01	Driver phải sẵn sàng	Chỉ tài xế ở trạng thái Available/Ready mới được hệ thống đưa vào danh sách tìm tài xế.
BRL02	Driver phải phù hợp loại xe	Tài xế được chọn phải có phương tiện phù hợp với loại xe khách hàng yêu cầu.
BRL03	Driver phải có vị trí hợp lệ	Hệ thống chỉ xem xét tài xế có thông tin vị trí hợp lệ và còn trong khoảng thời gian cập nhật cho phép.
BRL04	Ưu tiên Driver phù hợp	Hệ thống ưu tiên tài xế dựa trên các tiêu chí nghiệp vụ như khoảng cách, trạng thái, loại xe và rating.
BRL05	Driver chỉ nhận một chuyến	Một tài xế không được đồng thời nhận hai chuyến đang ở trạng thái cần thực hiện.
BRL06	Driver phải phản hồi trong thời gian quy định	Sau khi nhận yêu cầu, tài xế phải Accept hoặc Reject trong thời gian do doanh nghiệp quy định.
BRL07	Timeout Driver	Nếu tài xế không phản hồi trước thời hạn, hệ thống phải xem yêu cầu là Timeout.
BRL08	Chuyển sang Driver tiếp theo	Khi Driver Reject hoặc Timeout, hệ thống phải tìm Driver phù hợp tiếp theo.
BRL09	Không yêu cầu Customer đặt lại	Khi Driver Reject/Timeout, Booking hiện tại tiếp tục được sử dụng; Customer không cần tạo Booking mới.
BRL10	Không có Driver	Nếu không còn Driver phù hợp, hệ thống phải thông báo cho Customer theo chính sách của doanh nghiệp.
BRL11	Xác nhận Driver	Chỉ khi Driver Accept thành công và hệ thống xác nhận việc phân công thì Booking mới chuyển sang trạng thái Driver Assigned.
BRL12	Cập nhật trạng thái Driver	Sau khi nhận chuyến, Driver phải chuyển sang trạng thái không nhận chuyến mới cho đến khi hoàn thành hoặc kết thúc chuyến.
BRL13	Không được gán trùng Driver	Một Booking chỉ được có một Driver chính thức tại cùng một thời điểm.
BRL14	Hủy Booking	Customer/Driver chỉ được hủy Booking ở những trạng thái được Business Policy cho phép.
BRL15	Tính cước	Fare được tính dựa trên Pricing Rule đã được doanh nghiệp xác nhận.
BRL16	Payment	Booking phải được ghi nhận trạng thái thanh toán phù hợp sau khi Trip hoàn thành.
BRL17	Không lưu dữ liệu thanh toán nhạy cảm	CAB không được lưu trực tiếp thông tin nhạy cảm của thẻ/tài khoản thanh toán.
BRL18	Rating	Customer chỉ được đánh giá Driver sau khi Trip đã hoàn thành.
BRL19	Quyền quản trị	Nhân viên chỉ được thực hiện các thao tác phù hợp với Role/Permission được cấp.
BRL20	Audit	Các thao tác quan trọng phải được lưu vết để phục vụ kiểm tra và truy xuất sự cố.
2. Business Rule quan trọng nhất – Driver Dispatch

Quy trình tìm Driver có thể thiết kế theo rule:

Customer tạo Booking
        ↓
Tìm Driver
        ↓
Driver có Available?
   ┌────┴────┐
   Không     Có
    ↓         ↓
Bỏ qua     Kiểm tra
Driver     loại xe
              ↓
        Kiểm tra vị trí
              ↓
        Xếp hạng Driver
              ↓
        Gửi Request
              ↓
        Chờ phản hồi
         /         \
    Accept       Reject/Timeout
       ↓              ↓
  Assign Driver   Driver tiếp theo
3. Quy tắc Timeout

Đây là rule cần khách hàng xác nhận rõ.

Ví dụ:

BRL06: Driver phải phản hồi trong thời gian X giây.

Nếu:

Request sent
      ↓
  X giây
      ↓
Không có response
      ↓
TIMEOUT
      ↓
Tìm Driver tiếp theo

Lưu ý: Giá trị X chưa nên tự đặt. Đây là một Business Rule cần xác nhận với khách hàng.

4. Exception / Alternative Flow
EF01 – Driver không sẵn sàng

Điều kiện: Driver đang Offline hoặc Unavailable.

Xử lý:

Hệ thống tìm Driver
        ↓
Driver không Available
        ↓
Không gửi Booking
        ↓
Bỏ qua Driver
        ↓
Tìm Driver tiếp theo
EF02 – Driver từ chối chuyến

Điều kiện: Driver nhấn Reject.

Gửi Booking cho Driver A
        ↓
Driver A Reject
        ↓
Cập nhật Request = REJECTED
        ↓
Không gán Driver A
        ↓
Tìm Driver B

Customer không cần tạo lại Booking.

EF03 – Driver không phản hồi

Điều kiện: Driver không Accept/Reject trong thời gian quy định.

Gửi Booking cho Driver A
        ↓
     Timeout
        ↓
Request = TIMEOUT
        ↓
Loại Driver A khỏi lượt tìm
        ↓
Tìm Driver B
EF04 – Driver mất kết nối

Điều kiện: Driver đang được đề xuất nhưng mất kết nối.

Driver A đang được request
        ↓
Mất kết nối
        ↓
Không nhận được response
        ↓
Hết thời gian timeout
        ↓
TIMEOUT
        ↓
Tìm Driver khác
EF05 – Không còn Driver phù hợp
Tìm Driver
    ↓
Không còn Driver phù hợp
    ↓
Kiểm tra thời gian tìm kiếm
    ↓
 ┌──────────────┴──────────────┐
 Còn thời gian              Hết thời gian
    ↓                            ↓
Tiếp tục tìm                Kết thúc tìm
                                 ↓
                      Thông báo Customer

Thông báo có thể ở mức nghiệp vụ:

"Hiện tại chưa tìm được tài xế phù hợp. Vui lòng thử lại sau."

Nội dung chính thức cần được Business xác nhận.

5. Exception – Customer hủy trong khi đang tìm Driver
flowchart TD
    A["Booking đang SEARCHING_DRIVER"] --> B{"Customer hủy?"}


    B -- "Không" --> C["Tiếp tục tìm Driver"]


    B -- "Có" --> D{"Có Driver đã được assign?"}


    D -- "Không" --> E["Hủy Booking"]
    E --> F["Dừng quá trình tìm Driver"]


    D -- "Có" --> G["Kiểm tra Cancellation Policy"]
    G --> H["Xử lý phí hủy nếu có"]
    H --> I["Hủy Booking"]
6. Exception – Hai tài xế cùng Accept

Đây là một trường hợp kỹ thuật/nghiệp vụ rất quan trọng.

Ví dụ:

Booking 001
     ↓
Driver A ── Accept ──┐
                     ├──> Hệ thống xử lý
Driver B ── Accept ──┘

Business Rule:

Chỉ một Driver được xác nhận chính thức cho một Booking.

Hệ thống phải đảm bảo:

First valid Accept
       ↓
Assign Driver
       ↓
Các Accept sau
       ↓
Reject / Ignore

Không được để một Booking có đồng thời Driver A và Driver B.

7. Exception – Driver Accept nhưng không còn Available

Ví dụ:

Driver A
Available
   ↓
Booking request
   ↓
Driver A Accept
   ↓
Kiểm tra lại trạng thái
   ↓
Driver A không còn Available
   ↓
Không assign
   ↓
Tìm Driver khác

Đây là trường hợp cần xử lý để tránh race condition khi có nhiều Booking.

8. Exception – Payment thất bại
flowchart TD
    A["Trip Completed"] --> B["Tính Fare"]
    B --> C["Customer chọn Online Payment"]
    C --> D["Gửi Payment Provider"]
    D --> E{"Payment thành công?"}


    E -- "Có" --> F["Payment = SUCCESS"]
    F --> G["Thông báo Customer"]


    E -- "Không" --> H["Payment = FAILED"]
    H --> I["Thông báo Customer"]
    I --> J{"Cho phép Retry?"}


    J -- "Có" --> C
    J -- "Không" --> K["Xử lý theo Payment Policy"]
9. Exception – Notification thất bại

Notification không nên làm Booking bị thất bại.

Trip/Booking Event
       ↓
Notification Service
       ↓
   Gửi Notification
       ↓
   ┌────┴────┐
 Success    Failed
   ↓          ↓
Hoàn thành   Retry / Log
             ↓
        Không làm Booking
        bị thất bại

Business Rule:

BRL21: Lỗi Notification không được làm gián đoạn quá trình Booking/Trip.

10. Tổng hợp Business Rule cho chức năng tìm tài xế

Có thể đưa vào tài liệu BA dưới dạng bảng ngắn gọn:

Mã	Rule	Khi nào áp dụng	Kết quả
BRL01	Driver phải Available	Khi tìm Driver	Chỉ chọn Driver Available
BRL02	Đúng loại xe	Khi lọc Driver	Loại Driver không phù hợp
BRL03	Có vị trí hợp lệ	Khi tính khoảng cách	Chỉ dùng location hợp lệ
BRL04	Ưu tiên Driver phù hợp	Khi ranking	Xác định thứ tự Driver
BRL06	Có thời gian phản hồi	Sau khi gửi request	Chờ Accept/Reject
BRL07	Timeout	Driver không phản hồi	Request = Timeout
BRL08	Reject/Timeout → Driver tiếp theo	Khi request thất bại	Tiếp tục dispatch
BRL09	Không tạo Booking mới	Driver Reject/Timeout	Giữ nguyên Booking
BRL10	Không có Driver	Hết danh sách/timeout	Thông báo Customer
BRL11	Chỉ một Driver được assign	Driver Accept	Xác nhận Driver đầu tiên hợp lệ
11. Những Business Rule cần xác nhận với khách hàng

Một số rule chưa nên chốt cứng vì đề bài chưa cung cấp giá trị cụ thể:

Nội dung cần xác nhận	Câu hỏi
Driver Timeout	Tài xế có bao nhiêu giây để Accept/Reject?
Search Timeout	Hệ thống tìm tài xế tối đa bao lâu?
Ranking	Khoảng cách hay Rating có mức ưu tiên cao hơn?
Rating	Rating tối thiểu bao nhiêu? Có dùng rating làm tiêu chí bắt buộc không?
Location	Vị trí Driver được coi là hợp lệ trong bao lâu?
Reject	Driver reject có bị ảnh hưởng về sau không?
Cancellation	Khi nào Customer/Driver được hủy?
Cancellation Fee	Có phí hủy không và tính như thế nào?
No-show	Customer không xuất hiện thì xử lý ra sao?
Payment Retry	Thanh toán thất bại được retry bao nhiêu lần?

Bước 9: Xây dựng Data modeling dựa vào đó xây dựng các cái thực thể và mô hình erd, dùng code mermaid
1. Xác định các Entity chính

Có thể chia thành các nhóm:

Nhóm người dùng
Customer
Driver
Staff
Role
Nhóm phương tiện
Vehicle
VehicleType
Nhóm đặt xe/chuyến đi
Booking
Trip
DriverAssignment
Nhóm vị trí
Location
DriverLocation
Nhóm tài chính
Fare
Payment
PaymentMethod
Nhóm thông báo/đánh giá
Notification
Rating
Nhóm quản trị
AuditLog
2. Danh sách Entity và thuộc tính chính
Entity	Thuộc tính chính	Mục đích
Customer	customer_id, name, phone, email, status	Quản lý khách hàng
Driver	driver_id, name, phone, rating, status	Quản lý tài xế
Staff	staff_id, name, email, status	Nhân viên vận hành
Role	role_id, role_name	Phân quyền
Vehicle	vehicle_id, driver_id, vehicle_type_id, plate_number, status	Quản lý phương tiện
VehicleType	vehicle_type_id, name, description	Loại xe
Booking	booking_id, customer_id, pickup_location_id, destination_location_id, vehicle_type_id, status, created_at	Yêu cầu đặt xe
DriverAssignment	assignment_id, booking_id, driver_id, status, requested_at, responded_at	Lưu lịch sử tìm/gán Driver
Trip	trip_id, booking_id, driver_id, start_time, end_time, status	Chuyến đi thực tế
Location	location_id, latitude, longitude, address	Điểm đón/điểm đến
DriverLocation	location_id, driver_id, latitude, longitude, recorded_at	Theo dõi vị trí Driver
Fare	fare_id, trip_id, base_fare, distance_fee, time_fee, surcharge, total_amount	Tính cước
Payment	payment_id, trip_id, amount, method, status, transaction_ref	Quản lý thanh toán
Rating	rating_id, trip_id, customer_id, driver_id, score, comment	Đánh giá Driver
Notification	notification_id, recipient_id, type, content, status, sent_at	Quản lý thông báo
AuditLog	audit_id, actor_id, action, entity_type, entity_id, created_at	Lưu vết thao tác
3. Mô hình quan hệ chính

Có thể hiểu các quan hệ nghiệp vụ chính như sau:

Customer
   │
   │ 1:N
   ↓
Booking
   │
   ├──────────────→ Location
   │                 Pickup
   │                 Destination
   │
   │ 1:N
   ↓
DriverAssignment
   │
   ↓
Driver
   │
   ↓
Vehicle
   │
   ↓
VehicleType


Booking
   │
   │ 1:1
   ↓
Trip
   │
   ├──→ Fare
   ├──→ Payment
   └──→ Rating

Điểm quan trọng là DriverAssignment nên được tách thành Entity riêng.

Ví dụ một Booking có thể có:

Booking 001
   ↓
Driver A → REJECTED
   ↓
Driver B → TIMEOUT
   ↓
Driver C → ACCEPTED

Nếu chỉ lưu driver_id trực tiếp trong Booking, chúng ta sẽ mất lịch sử A và B.

4. ERD – Mermaid

Dưới đây là ERD đề xuất cho MVP:

erDiagram
        UUID rating_id PK
        UUID trip_id FK
        UUID customer_id FK
        UUID driver_id FK
        int score
        string comment
        datetime created_at
    }


    NOTIFICATION {
        UUID notification_id PK
        UUID customer_id FK
        UUID driver_id FK
        string notification_type
        string content
        string status
        datetime sent_at
        datetime created_at
    }


    AUDIT_LOG {
        UUID audit_id PK
        UUID staff_id FK
        string action
        string entity_type
        UUID entity_id
        string old_value
        string new_value
        datetime created_at
    }


    CUSTOMER ||--o{ BOOKING : creates


    BOOKING ||--|| LOCATION : pickup
    BOOKING ||--|| LOCATION : destination


    VEHICLE_TYPE ||--o{ VEHICLE : defines
    DRIVER ||--o{ VEHICLE : owns


    BOOKING ||--o{ DRIVER_ASSIGNMENT : has
    DRIVER ||--o{ DRIVER_ASSIGNMENT : receives


    BOOKING ||--o| TRIP : becomes
    DRIVER ||--o{ TRIP : performs


    DRIVER ||--o{ DRIVER_LOCATION : sends


    TRIP ||--o| FARE : has
    TRIP ||--o{ PAYMENT : has
    TRIP ||--o| RATING : receives


    CUSTOMER ||--o{ RATING : gives
    DRIVER ||--o{ RATING : receives


    CUSTOMER ||--o{ NOTIFICATION : receives
    DRIVER ||--o{ NOTIFICATION : receives


    STAFF ||--o{ AUDIT_LOG : creates


    ROLE ||--o{ STAFF : assigned
5. Giải thích các quan hệ quan trọng
Customer – Booking
Customer 1 ───── N Booking

Một khách hàng có thể tạo nhiều Booking.

Một Booking chỉ thuộc về một Customer.

Booking – DriverAssignment
Booking 1 ───── N DriverAssignment

Đây là quan hệ rất quan trọng.

Ví dụ:

Booking B001
│
├── Assignment A001 → Driver D001 → REJECTED
├── Assignment A002 → Driver D002 → TIMEOUT
└── Assignment A003 → Driver D003 → ACCEPTED

Nhờ đó hệ thống có thể đáp ứng Business Rule:

Driver Reject/Timeout → tìm Driver tiếp theo.

Driver – Vehicle
Driver 1 ───── N Vehicle

Về mặt nghiệp vụ, nếu ABC quy định mỗi Driver chỉ có một phương tiện đang hoạt động, thì database vẫn có thể lưu lịch sử nhiều Vehicle nhưng chỉ một Vehicle có status = ACTIVE.

Nếu doanh nghiệp xác nhận mỗi Driver chỉ có đúng một xe, có thể thiết kế thành quan hệ 1-1.

Booking – Trip
Booking 1 ───── 0..1 Trip

Booking được tạo trước.

Chỉ khi Driver được xác nhận thì Trip mới được tạo.

Do đó:

Booking
   ↓
Driver Assigned
   ↓
Trip
Trip – Fare
Trip 1 ───── 0..1 Fare

Một Trip có một kết quả tính cước cuối cùng.

Trip – Payment
Trip 1 ───── N Payment

Ở đây nên cho phép 1-N thay vì 1-1.

Ví dụ:

Trip T001
   ↓
Payment P001 → FAILED
   ↓
Payment P002 → FAILED
   ↓
Payment P003 → SUCCESS

Điều này hỗ trợ Business Rule retry payment.

6. Driver Location

DriverLocation nên tách khỏi Driver.

Ví dụ:

Driver D001
│
├── 10:00 → 10.762622, 106.660172
├── 10:01 → 10.763100, 106.661000
├── 10:02 → 10.764000, 106.662100
└── ...

Như vậy có thể:

tìm Driver gần Customer;
tính khoảng cách;
hỗ trợ ETA;
theo dõi lịch sử vị trí nếu Business yêu cầu.

Tuy nhiên, cần xác nhận thời gian lưu trữ GPS vì dữ liệu này có thể tăng rất nhanh.

7. Một điểm cần điều chỉnh trong ERD

Ở phiên bản thiết kế ban đầu, NOTIFICATION có cả:

customer_id
driver_id

Điều này phù hợp MVP nhưng về lâu dài có thể không tối ưu.

Có thể thiết kế theo hướng:

NOTIFICATION
     │
     ↓
Recipient
     │
 ┌───┴────┐
Customer  Driver

hoặc sử dụng một User/Account chung:

USER
├── Customer Profile
├── Driver Profile
└── Staff Profile

Cách này phù hợp hơn nếu hệ thống về sau có nhiều loại người dùng.

8. Data Model theo Domain

Có thể chia ERD thành các domain để dễ phát triển và mở rộng:

flowchart TB


    subgraph USER["User Management"]
        C["Customer"]
        D["Driver"]
        S["Staff"]
        R["Role"]
    end


    subgraph FLEET["Fleet Management"]
        V["Vehicle"]
        VT["Vehicle Type"]
    end


    subgraph BOOKING["Booking & Dispatch"]
        B["Booking"]
        DA["Driver Assignment"]
        L["Location"]
        T["Trip"]
    end


    subgraph LOCATION["Location Tracking"]
        DL["Driver Location"]
    end


    subgraph PAYMENT["Fare & Payment"]
        F["Fare"]
        P["Payment"]
    end


    subgraph COMM["Communication"]
        N["Notification"]
        RT["Rating"]
    end


    subgraph ADMIN["Administration"]
        AL["Audit Log"]
    end


    C --> B
    B --> DA
    DA --> D
    B --> T
    T --> F
    T --> P
    T --> RT
    D --> V
    V --> VT
    D --> DL
    B --> L
    C --> N
    D --> N
    S --> AL
    R --> S
9. Các Entity quan trọng nhất đối với MVP

Nếu thời gian chỉ có 7 tuần, không nhất thiết phải triển khai toàn bộ Entity nâng cao ngay từ đầu.

Must Have
Customer
Driver
Vehicle
VehicleType
Booking
DriverAssignment
Trip
Location
DriverLocation
Fare
Payment
Notification
Nên có
Rating
Staff
Role
AuditLog
Có thể Phase 2
Promotion
Voucher
Loyalty
CorporateAccount
AdvancedPricing
DriverIncentive
Analytics
10. Kết quả của Bước 9

Data Model của CAB hiện có thể hình thành chuỗi nghiệp vụ chính:

CUSTOMER
   │
   ↓
BOOKING
   │
   ├── Pickup / Destination
   │
   ↓
DRIVER ASSIGNMENT
   │
   ├── Driver A → Reject
   ├── Driver B → Timeout
   └── Driver C → Accept
              │
              ↓
             TRIP
          ┌────┼────┐
          ↓    ↓    ↓
        FARE PAYMENT RATING
               │
               ↓
          NOTIFICATION

Bước 10: xác định các nonfunction requimen xác định những cái chức năng không yêu cầu
Ở bước này, BA xác định Non-Functional Requirements (NFR) – các yêu cầu không mô tả hệ thống làm chức năng gì, mà mô tả hệ thống phải hoạt động như thế nào.

Ví dụ:

FR: Hệ thống tìm tài xế.
NFR: Hệ thống phải tìm tài xế trong thời gian đáp ứng cho phép.
FR: Hệ thống thanh toán online.
NFR: Thông tin thanh toán phải được bảo mật.
FR: Hệ thống gửi thông báo.
NFR: Lỗi Notification không được làm sập chức năng đặt xe.
1. Danh sách Non-Functional Requirements
Mã	Nhóm	Non-Functional Requirement	Tiêu chí đề xuất
NFR01	Performance	Thời gian phản hồi	Các API nghiệp vụ thông thường nên phản hồi trong ≤ 2 giây ở điều kiện tải bình thường.
NFR02	Performance	Tìm tài xế	Hệ thống phải bắt đầu quá trình tìm tài xế ngay sau khi Booking được xác nhận.
NFR03	Performance	Cập nhật trạng thái	Thay đổi trạng thái Booking/Trip phải được phản ánh gần thời gian thực.
NFR04	Scalability	Khả năng mở rộng	Hệ thống phải có khả năng mở rộng khi số lượng Customer, Driver và Booking tăng.
NFR05	Availability	Tính sẵn sàng	Hệ thống đặt xe phải hoạt động ổn định, đặc biệt trong thời gian cao điểm.
NFR06	Reliability	Độ tin cậy	Lỗi của một component không được làm toàn bộ hệ thống CAB ngừng hoạt động.
NFR07	Fault Tolerance	Chịu lỗi	Nếu Notification hoặc Payment gặp lỗi, chức năng Booking vẫn phải tiếp tục hoạt động theo policy.
NFR08	Security	Authentication	Customer, Driver và Staff phải được xác thực trước khi sử dụng các chức năng yêu cầu tài khoản.
NFR09	Security	Authorization	Hệ thống phải kiểm soát quyền truy cập dựa trên Role/Permission.
NFR10	Security	Bảo vệ dữ liệu cá nhân	Thông tin cá nhân phải được bảo vệ khỏi truy cập trái phép.
NFR11	Security	Bảo vệ dữ liệu vị trí	Dữ liệu GPS của Driver phải được bảo vệ và chỉ sử dụng cho mục đích được phép.
NFR12	Security	Payment Security	CAB không lưu trực tiếp dữ liệu nhạy cảm của thẻ/tài khoản thanh toán.
NFR13	Auditability	Audit Log	Các thao tác quan trọng phải được ghi log để phục vụ truy vết.
NFR14	Maintainability	Dễ bảo trì	Hệ thống phải được thiết kế để có thể sửa đổi một module mà hạn chế ảnh hưởng module khác.
NFR15	Extensibility	Khả năng mở rộng	Có thể thêm loại xe/dịch vụ mới mà không phải xây dựng lại toàn bộ hệ thống.
NFR16	Extensibility	Payment Provider	Có thể tích hợp thêm Payment Provider mới.
NFR17	Extensibility	Notification Provider	Có thể bổ sung thêm Email/SMS/Push hoặc provider khác.
NFR18	Compatibility	Integration	Hệ thống phải có khả năng tích hợp với các hệ thống bên ngoài thông qua API.
NFR19	Data Integrity	Tính toàn vẹn dữ liệu	Một Booking không được đồng thời được assign cho nhiều Driver.
NFR20	Data Integrity	Transaction	Các thao tác cập nhật dữ liệu quan trọng phải đảm bảo tính nhất quán.
NFR21	Availability	Không phụ thuộc Payment	Payment Provider gặp sự cố không được làm toàn bộ Booking System ngừng hoạt động.
NFR22	Availability	Không phụ thuộc Notification	Notification Service gặp sự cố không được làm Trip bị mất dữ liệu hoặc dừng xử lý.
NFR23	Recovery	Backup	Dữ liệu quan trọng phải được backup theo chính sách doanh nghiệp.
NFR24	Recovery	Disaster Recovery	Hệ thống phải có khả năng khôi phục dịch vụ khi xảy ra sự cố nghiêm trọng.
NFR25	Monitoring	Monitoring	Hệ thống phải giám sát tình trạng các service quan trọng.
NFR26	Monitoring	Alerting	Hệ thống phải cảnh báo khi xảy ra lỗi hoặc vượt ngưỡng vận hành.
NFR27	Usability	Dễ sử dụng	Giao diện Customer/Driver phải đơn giản, dễ hiểu và phù hợp với quy trình đặt xe.
NFR28	Usability	Admin UI	Giao diện vận hành phải hỗ trợ nhân viên nhanh chóng tra cứu và xử lý Trip.
NFR29	Localization	Ngôn ngữ	Hệ thống phải hỗ trợ tiếng Việt trong phiên bản triển khai cho khách hàng Việt Nam.
NFR30	Deployment	Triển khai độc lập	Các component có thể triển khai/cập nhật độc lập để hạn chế ảnh hưởng đến hệ thống đang chạy.
2. NFR về Performance

Đây là nhóm đặc biệt quan trọng đối với CAB vì hệ thống có chức năng tìm tài xế theo vị trí.

NFR01 – API Response Time

Các thao tác API thông thường phải có thời gian phản hồi trong giới hạn được doanh nghiệp xác nhận, ví dụ ≤ 2 giây ở điều kiện tải bình thường.

NFR02 – Driver Dispatch

Sau khi Customer xác nhận Booking:

Customer
   ↓
Create Booking
   ↓
System xác nhận
   ↓
Start Driver Search

Quá trình tìm Driver phải được khởi động ngay sau khi Booking hợp lệ, không phụ thuộc vào việc Customer phải refresh màn hình.

NFR03 – Real-time Status

Các trạng thái quan trọng như:

SEARCHING
DRIVER_ASSIGNED
DRIVER_ARRIVING
DRIVER_ARRIVED
IN_PROGRESS
COMPLETED
CANCELLED

phải được cập nhật cho các bên liên quan với độ trễ phù hợp.

Giá trị cụ thể, ví dụ ≤ 3 giây, cần được khách hàng xác nhận.

3. NFR về Scalability

CAB được kỳ vọng phục vụ số lượng lớn Customer và Driver.

Hệ thống cần có khả năng:

100 Drivers
     ↓
1,000 Drivers
     ↓
10,000 Drivers
     ↓
100,000+ Drivers

mà không phải thiết kế lại toàn bộ hệ thống.

Các component như:

Booking
Driver Dispatch
Notification
Payment
Location

nên có khả năng scale độc lập khi cần.

4. NFR về Reliability & Fault Tolerance

Đây là yêu cầu rất quan trọng từ đề bài.

Nguyên tắc

Một module lỗi không được kéo theo toàn bộ hệ thống lỗi.

Ví dụ:

flowchart LR
    A["Customer"] --> B["Booking Service"]


    B --> C["Dispatch Service"]
    B --> D["Notification Service"]
    B --> E["Payment Service"]


    D -. "Lỗi" .-> F["Booking vẫn hoạt động"]
    E -. "Lỗi" .-> G["Trip vẫn được xử lý"]

Ví dụ:

Notification Service chết:

Booking
   ↓
Driver Assigned
   ↓
Notification FAILED
   ↓
Log + Retry
   ↓
Booking vẫn tồn tại

Không được:

Notification lỗi
       ↓
Toàn bộ CAB DOWN ❌
5. NFR về Security

Hệ thống phải bảo vệ:

Thông tin Customer.
Thông tin Driver.
Thông tin Vehicle.
Vị trí Driver.
Thông tin giao dịch.
Tài khoản Staff.
Audit Log.
Authentication
Customer → Login → Authentication → Customer Functions
Driver   → Login → Authentication → Driver Functions
Staff    → Login → Authentication → Admin Functions
Authorization

Ví dụ:

Role	Xem Trip	Quản lý Driver	Quản lý Staff	Xem Payment
Customer	Chuyến của mình	❌	❌	Chuyến của mình
Driver	Chuyến được giao	Hồ sơ mình	❌	❌
Operator	Có quyền	Có quyền	❌	Có quyền
Admin	Có quyền	Có quyền	Có quyền	Có quyền

Đây là RBAC – Role-Based Access Control.

6. NFR về Data Integrity

Ví dụ quan trọng nhất:

Không được Assign 2 Driver cho một Booking
Booking B001


Driver A → ACCEPT
Driver B → ACCEPT

Hệ thống phải đảm bảo chỉ một Driver được xác nhận chính thức.

Booking B001
     ↓
Driver A → ASSIGNED ✅
Driver B → REJECTED ❌

Điều này cần được đảm bảo ở cả business logic và database/concurrency control.

7. NFR về Maintainability

Hệ thống phải dễ thay đổi.

Ví dụ doanh nghiệp muốn thay:

Payment Provider A
        ↓
Payment Provider B

Không nên phải sửa toàn bộ Booking System.

Tương tự:

Notification
      │
 ┌────┼─────┐
 ↓    ↓     ↓
Push SMS   Email

Sau này thêm Zalo hoặc một provider khác thì chỉ cần mở rộng Notification layer.

8. NFR về Extensibility

Hệ thống hiện tại có:

Car
Motorbike

Trong tương lai có thể thêm:

SUV
Van
Luxury
Electric Car
Airport Transfer
Corporate Ride

Việc thêm service mới không nên yêu cầu viết lại toàn bộ Booking System.

9. NFR về Monitoring & Logging

Hệ thống cần theo dõi tối thiểu:

Booking Success / Failed
Driver Dispatch Success / Failed
Payment Success / Failed
Notification Success / Failed
API Error
Database Error
Service Availability

Ví dụ:

flowchart LR
    A["CAB Services"] --> B["Monitoring"]
    B --> C["Metrics"]
    B --> D["Logs"]
    B --> E["Alerts"]


    C --> F["Dashboard"]
    D --> F
    E --> G["Operations Team"]
10. NFR về Backup & Recovery

Các dữ liệu quan trọng như:

Customer
Driver
Booking
Trip
Fare
Payment
Audit Log

phải có cơ chế backup và recovery.

Các thông số cần BA/IT xác nhận:

Thông số	Cần xác định
RPO	Cho phép mất tối đa bao nhiêu dữ liệu?
RTO	Cho phép hệ thống khôi phục trong bao lâu?
Backup frequency	Backup mỗi bao lâu?
Retention	Lưu backup trong bao lâu?
11. NFR theo mức độ ưu tiên

Do dự án chỉ có 7 tuần, nên nên ưu tiên:

🔴 Must Have
NFR01 – Performance
NFR04 – Scalability
NFR05 – Availability
NFR06 – Reliability
NFR08 – Authentication
NFR09 – Authorization
NFR10 – Data Security
NFR12 – Payment Security
NFR13 – Audit Log
NFR19 – Data Integrity
NFR25 – Monitoring
🟡 Should Have
NFR14 – Maintainability
NFR15 – Extensibility
NFR16 – Payment Provider Extensibility
NFR17 – Notification Extensibility
NFR23 – Backup
NFR24 – Disaster Recovery
NFR27 – Usability
🟢 Could Have / Phase 2
Advanced Analytics
Advanced Monitoring Dashboard
Multi-language
Advanced Disaster Recovery
Advanced Auto-scaling
Advanced Notification Routing
12. Những NFR cần xác nhận với khách hàng

Đề bài hiện chưa cung cấp các con số cụ thể, vì vậy BA không nên tự ý chốt.

Cần hỏi khách hàng:

Vấn đề	Câu hỏi cần xác nhận
Performance	API tối đa bao nhiêu giây?
Concurrent Users	Hệ thống phải phục vụ đồng thời bao nhiêu người?
Drivers	Tối đa bao nhiêu tài xế online cùng lúc?
Bookings	Peak có bao nhiêu Booking/phút?
Availability	Uptime yêu cầu 99.9%, 99.95% hay mức khác?
Dispatch	Bao lâu phải bắt đầu tìm Driver?
Driver Location	Bao lâu cập nhật GPS một lần?
Data Retention	Dữ liệu Booking/Payment/GPS lưu bao lâu?
Backup	Backup bao lâu một lần?
RPO/RTO	Mức mất dữ liệu và thời gian phục hồi chấp nhận được?
Security	Chính sách bảo mật nào doanh nghiệp yêu cầu?
Payment	Retry Payment tối đa bao nhiêu lần?
Kết luận Bước 10

Có thể phân biệt rất rõ:

Functional Requirement: Hệ thống làm gì.

Non-Functional Requirement: Hệ thống phải làm tốt đến mức nào / hoạt động như thế nào.

Ví dụ với chức năng tìm tài xế:

FR
→ Hệ thống tìm Driver Available gần Customer.


NFR
→ Kết quả tìm kiếm phải đáp ứng thời gian xử lý phù hợp,
  hệ thống chịu được tải cao, không bị sập khi
  Notification/Payment gặp lỗi, dữ liệu vị trí phải
  được bảo mật và hệ thống có khả năng mở rộng.

Bước 11-12: xác định và vẽ các usecase kí hiệu UC, usecase customer thì ghi là UC01 customer, đặc tả usecase 2 bước này làm liên tục với nhau 
Dựa trên các bước trước BR → FR → Business Process → Business Rule → Data Model → NFR, ta xây dựng Use Case cho hệ thống CAB.

UC (Use Case) mô tả một mục tiêu mà một Actor muốn đạt được khi tương tác với hệ thống.

1. Xác định Actor

Hệ thống CAB có 3 nhóm Actor chính:

Actor	Vai trò
Customer	Đăng ký, đặt xe, theo dõi chuyến, thanh toán, đánh giá tài xế
Driver	Nhận chuyến, cập nhật trạng thái chuyến, cập nhật vị trí
Staff/Operator	Quản lý Customer, Driver, Vehicle, Trip và xử lý sự cố
Payment Provider	Hệ thống bên ngoài xử lý thanh toán điện tử
Notification Provider	Hệ thống bên ngoài gửi Push/SMS/Email
2. Danh sách Use Case
Customer
Mã	Use Case	Actor
UC01	Customer	Customer
UC01.01	Đăng ký tài khoản	Customer
UC01.02	Đăng nhập	Customer
UC01.03	Cập nhật thông tin cá nhân	Customer
UC01.04	Đặt chuyến	Customer
UC01.05	Theo dõi chuyến	Customer
UC01.06	Xem lịch sử chuyến	Customer
UC01.07	Xem cước chuyến	Customer
UC01.08	Thanh toán	Customer
UC01.09	Đánh giá tài xế	Customer
UC01.10	Hủy chuyến	Customer

Ở đây có thể hiểu UC01 Customer là nhóm Use Case của Customer, bên dưới là các Use Case cụ thể.

Driver
Mã	Use Case	Actor
UC02	Driver	Driver
UC02.01	Đăng nhập	Driver
UC02.02	Cập nhật hồ sơ	Driver
UC02.03	Quản lý phương tiện	Driver
UC02.04	Chuyển trạng thái Online/Offline	Driver
UC02.05	Nhận yêu cầu chuyến	Driver
UC02.06	Chấp nhận chuyến	Driver
UC02.07	Từ chối chuyến	Driver
UC02.08	Cập nhật vị trí	Driver
UC02.09	Cập nhật trạng thái chuyến	Driver
UC02.10	Hoàn thành chuyến	Driver
Staff / Operator
Mã	Use Case	Actor
UC03	Staff/Operator	Staff
UC03.01	Đăng nhập Admin	Staff
UC03.02	Quản lý Customer	Staff
UC03.03	Quản lý Driver	Staff
UC03.04	Quản lý Vehicle	Staff
UC03.05	Giám sát chuyến	Staff
UC03.06	Xử lý chuyến lỗi	Staff
UC03.07	Tra cứu giao dịch	Staff
UC03.08	Quản lý quyền	Staff/Admin
UC03.09	Xem báo cáo	Staff
UC03.10	Xem Audit Log	Staff/Admin
3. Use Case của hệ thống bên ngoài
Mã	Use Case	Actor
UC04	Payment Provider	External System
UC04.01	Xử lý thanh toán điện tử	Payment Provider
UC04.02	Trả kết quả thanh toán	Payment Provider
UC05	Notification Provider	External System
UC05.01	Gửi thông báo	Notification Provider
4. Use Case Diagram tổng thể
flowchart LR


    C["👤 Customer"]
    D["🚗 Driver"]
    S["👨‍💼 Staff / Operator"]
    PP["💳 Payment Provider"]
    NP["🔔 Notification Provider"]


    subgraph CAB["CAB System"]


        UC01["UC01\nCustomer"]
        UC01A["UC01.01\nĐăng ký"]
        UC01B["UC01.02\nĐăng nhập"]
        UC01C["UC01.03\nCập nhật hồ sơ"]
        UC01D["UC01.04\nĐặt chuyến"]
        UC01E["UC01.05\nTheo dõi chuyến"]
        UC01F["UC01.06\nLịch sử chuyến"]
        UC01G["UC01.07\nXem cước"]
        UC01H["UC01.08\nThanh toán"]
        UC01I["UC01.09\nĐánh giá"]
        UC01J["UC01.10\nHủy chuyến"]


        UC02["UC02\nDriver"]
        UC02A["UC02.01\nĐăng nhập"]
        UC02B["UC02.02\nCập nhật hồ sơ"]
        UC02C["UC02.03\nQuản lý phương tiện"]
        UC02D["UC02.04\nOnline / Offline"]
        UC02E["UC02.05\nNhận yêu cầu chuyến"]
        UC02F["UC02.06\nAccept chuyến"]
        UC02G["UC02.07\nReject chuyến"]
        UC02H["UC02.08\nCập nhật vị trí"]
        UC02I["UC02.09\nCập nhật trạng thái Trip"]


        UC03["UC03\nStaff / Operator"]
        UC03A["UC03.01\nĐăng nhập Admin"]
        UC03B["UC03.02\nQuản lý Customer"]
        UC03C["UC03.03\nQuản lý Driver"]
        UC03D["UC03.04\nQuản lý Vehicle"]
        UC03E["UC03.05\nGiám sát Trip"]
        UC03F["UC03.06\nXử lý Trip lỗi"]
        UC03G["UC03.07\nTra cứu giao dịch"]
        UC03H["UC03.08\nQuản lý quyền"]
        UC03I["UC03.09\nBáo cáo"]
        UC03J["UC03.10\nAudit Log"]


        UC04["UC04\nThanh toán Online"]
        UC05["UC05\nNotification"]
    end


    C --- UC01
    D --- UC02
    S --- UC03
    PP --- UC04
    NP --- UC05
5. Use Case quan trọng nhất: UC01.04 – Đặt chuyến

Đây là Use Case trung tâm của hệ thống CAB và được xây dựng trực tiếp từ Business Process ở Bước 6.

Thông tin Use Case
Thuộc tính	Nội dung
Use Case ID	UC01.04
Tên	Đặt chuyến
Primary Actor	Customer
Supporting Actor	Driver, Notification Provider
Mục tiêu	Customer tạo yêu cầu đặt xe và được hệ thống tìm, phân công Driver
Pre-condition	Customer đã đăng nhập
Trigger	Customer chọn chức năng đặt chuyến
Post-condition	Booking được tạo và Driver được assign hoặc Booking kết thúc do không tìm được Driver
6. Main Flow – Luồng chính
1. Customer chọn "Đặt xe".
2. Hệ thống xác định vị trí hiện tại của Customer.
3. Customer nhập/xác nhận điểm đón.
4. Customer nhập điểm đến.
5. Customer chọn loại xe.
6. Customer xác nhận yêu cầu đặt chuyến.
7. Hệ thống kiểm tra thông tin Booking.
8. Hệ thống tạo Booking.
9. Hệ thống chuyển Booking sang trạng thái SEARCHING_DRIVER.
10. Hệ thống tìm các Driver Available.
11. Hệ thống lọc Driver theo loại xe.
12. Hệ thống xác định khoảng cách Driver đến điểm đón.
13. Hệ thống xếp hạng Driver theo Business Rule.
14. Hệ thống gửi yêu cầu nhận chuyến cho Driver phù hợp nhất.
15. Driver chấp nhận chuyến.
16. Hệ thống xác nhận Driver.
17. Hệ thống chuyển Booking sang DRIVER_ASSIGNED.
18. Hệ thống thông báo thông tin Driver cho Customer.
19. Use Case kết thúc.
7. Alternative Flow – Driver từ chối
AF01 – Driver Reject

Tại bước 15:

15. Driver chọn Reject.
16. Hệ thống ghi nhận Driver Assignment = REJECTED.
17. Hệ thống không assign Driver này cho Booking.
18. Hệ thống tìm Driver phù hợp tiếp theo.
19. Hệ thống gửi yêu cầu cho Driver tiếp theo.
20. Quay lại bước chờ Driver phản hồi.

Customer không phải tạo Booking mới.

8. Alternative Flow – Driver Timeout
AF02 – Driver không phản hồi
15. Hệ thống gửi request cho Driver.
16. Driver không Accept/Reject trong thời gian quy định.
17. Hệ thống đánh dấu Assignment = TIMEOUT.
18. Hệ thống loại Driver khỏi lượt tìm hiện tại.
19. Hệ thống tìm Driver tiếp theo.
20. Gửi request cho Driver mới.

Thời gian Timeout phải được xác nhận với khách hàng, ví dụ X giây.

9. Alternative Flow – Chưa tìm được Driver
AF03 – Không có Driver phù hợp
10. Hệ thống tìm Driver.
11. Không tìm thấy Driver phù hợp.
12. Hệ thống kiểm tra thời gian tìm kiếm.
13. Nếu vẫn còn trong thời gian cho phép:
       → tiếp tục tìm Driver.
14. Nếu vượt thời gian cho phép:
       → Booking = NO_DRIVER_FOUND.
15. Thông báo Customer.
16. Use Case kết thúc.
10. Exception Flow
EF01 – Điểm đón không hợp lệ
Customer nhập điểm đón
        ↓
Hệ thống kiểm tra
        ↓
Không hợp lệ
        ↓
Thông báo lỗi
        ↓
Customer nhập lại
EF02 – Payment/Notification lỗi

Payment hoặc Notification gặp lỗi không được làm mất Booking.

Booking
   ↓
Driver Assigned
   ↓
Notification Error
   ↓
Log + Retry
   ↓
Booking vẫn hoạt động
11. UC02.05 – Driver nhận yêu cầu chuyến
Thuộc tính	Nội dung
Use Case ID	UC02.05
Tên	Nhận yêu cầu chuyến
Actor	Driver
Mục tiêu	Driver nhận thông tin Booking phù hợp và quyết định Accept/Reject
Pre-condition	Driver đã đăng nhập và ở trạng thái Available
Trigger	Hệ thống tìm thấy Driver phù hợp
Post-condition	Driver Accept hoặc Reject/Timeout
Main Flow
1. Hệ thống tìm thấy Driver phù hợp.
2. Hệ thống gửi thông báo Booking.
3. Driver xem:
   - Điểm đón
   - Điểm đến
   - Loại xe
   - Thông tin cước dự kiến nếu được phép
4. Driver chọn Accept.
5. Hệ thống kiểm tra Driver vẫn Available.
6. Hệ thống Assign Driver.
7. Driver chuyển sang trạng thái BUSY.
8. Customer nhận thông báo.
Alternative Flow

Driver Reject:

Driver → Reject
       ↓
Assignment = REJECTED
       ↓
CAB tìm Driver khác

Driver Timeout:

Không phản hồi
       ↓
TIMEOUT
       ↓
CAB tìm Driver khác
12. UC02.09 – Cập nhật trạng thái Trip

Driver cập nhật vòng đời chuyến:

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
Đặc tả
Thuộc tính	Nội dung
Actor	Driver
Pre-condition	Driver đã được Assign
Main Flow	Driver cập nhật trạng thái theo thực tế
Post-condition	Trip có trạng thái mới và Customer được cập nhật
13. UC01.08 – Thanh toán
Thuộc tính	Nội dung
Use Case ID	UC01.08
Tên	Thanh toán
Actor	Customer
Supporting Actor	Payment Provider
Pre-condition	Trip đã hoàn thành và Fare đã được tính
Trigger	Customer thực hiện thanh toán
Post-condition	Payment SUCCESS hoặc FAILED
Main Flow
1. Trip = COMPLETED.
2. Hệ thống tính Fare.
3. Customer chọn Online Payment.
4. CAB tạo Payment Request.
5. Payment Provider xử lý.
6. Payment Provider trả kết quả SUCCESS.
7. CAB cập nhật Payment = SUCCESS.
8. Thông báo Customer.
Exception
Payment FAILED
      ↓
Thông báo Customer
      ↓
Retry?
 ┌────┴────┐
Có        Không
 ↓          ↓
Retry    Xử lý theo policy
14. UC01.09 – Đánh giá Driver
Thuộc tính	Nội dung
Actor	Customer
Pre-condition	Trip đã COMPLETED
Trigger	Customer chọn đánh giá
Main Flow	Chọn số sao → nhập nhận xét → Submit
Post-condition	Rating được lưu và cập nhật rating Driver
Business Rule
Trip != COMPLETED
       ↓
Không được Rating
15. UC03 – Staff/Operator
Các chức năng chính
UC03
│
├── UC03.01 Đăng nhập Admin
├── UC03.02 Quản lý Customer
├── UC03.03 Quản lý Driver
├── UC03.04 Quản lý Vehicle
├── UC03.05 Giám sát Trip
├── UC03.06 Xử lý Trip lỗi
├── UC03.07 Tra cứu giao dịch
├── UC03.08 Quản lý quyền
├── UC03.09 Báo cáo
└── UC03.10 Audit Log
Ví dụ UC03.05 – Giám sát Trip

Main Flow:

1. Staff đăng nhập Admin Portal.
2. Chọn "Giám sát Trip".
3. Hệ thống hiển thị các Trip đang diễn ra.
4. Staff lọc theo:
   - Trip ID
   - Customer
   - Driver
   - Status
5. Staff chọn Trip.
6. Hệ thống hiển thị chi tiết Trip.
7. Staff xem trạng thái và vị trí Driver.
16. Quan hệ Include / Extend

Đối với Use Case Đặt chuyến, có thể biểu diễn:

flowchart LR


    C["Customer"]


    UC1(("UC01.04\nĐặt chuyến"))
    UC2(("Xác định vị trí"))
    UC3(("Kiểm tra Booking"))
    UC4(("Tìm Driver"))
    UC5(("Phân công Driver"))
    UC6(("Thông báo"))
    UC7(("Thanh toán"))
    UC8(("Hủy chuyến"))


    C --> UC1


    UC1 -. "<<include>>".-> UC2
    UC1 -. "<<include>>".-> UC3
    UC1 -. "<<include>>".-> UC4
    UC4 -. "<<include>>".-> UC5
    UC5 -. "<<include>>".-> UC6


    UC8 -. "<<extend>>".-> UC1
Giải thích

include dùng khi chức năng con luôn được thực hiện trong quy trình.

Ví dụ:

Đặt chuyến → luôn phải kiểm tra Booking.

extend dùng cho hành vi có điều kiện.

Ví dụ:

Hủy chuyến chỉ xảy ra khi Customer muốn hủy.

17. Traceability: UC liên kết với FR
Use Case	Functional Requirement liên quan
UC01.04 – Đặt chuyến	FR01–FR20
UC02.05 – Nhận yêu cầu chuyến	FR12–FR17
UC02.09 – Cập nhật Trip	FR21–FR25
UC01.05 – Theo dõi chuyến	FR26–FR28
UC01.08 – Thanh toán	FR29–FR35
UC01.09 – Đánh giá	Rating requirement
UC03.05 – Giám sát Trip	FR45–FR47
UC03.08 – Phân quyền	FR48
UC03.10 – Audit Log	FR49
UC03.09 – Báo cáo	FR50
18. Tổng hợp Bước 11–12

Có thể đưa vào tài liệu BA theo cấu trúc:

CAB SYSTEM
│
├── UC01 – Customer
│   ├── UC01.01 – Đăng ký
│   ├── UC01.02 – Đăng nhập
│   ├── UC01.03 – Cập nhật hồ sơ
│   ├── UC01.04 – Đặt chuyến ⭐
│   ├── UC01.05 – Theo dõi chuyến
│   ├── UC01.06 – Lịch sử chuyến
│   ├── UC01.07 – Xem cước
│   ├── UC01.08 – Thanh toán
│   ├── UC01.09 – Đánh giá
│   └── UC01.10 – Hủy chuyến
│
├── UC02 – Driver
│   ├── UC02.01 – Đăng nhập
│   ├── UC02.02 – Hồ sơ
│   ├── UC02.03 – Phương tiện
│   ├── UC02.04 – Online/Offline
│   ├── UC02.05 – Nhận yêu cầu
│   ├── UC02.06 – Accept
│   ├── UC02.07 – Reject
│   ├── UC02.08 – Vị trí
│   └── UC02.09 – Trạng thái Trip
│
└── UC03 – Staff
    ├── UC03.01 – Đăng nhập
    ├── UC03.02 – Customer
    ├── UC03.03 – Driver
    ├── UC03.04 – Vehicle
    ├── UC03.05 – Giám sát Trip
    ├── UC03.06 – Xử lý Trip lỗi
    ├── UC03.07 – Giao dịch
    ├── UC03.08 – Phân quyền
    ├── UC03.09 – Báo cáo
    └── UC03.10 – Audit Log

Bước 13: Acceptance criteria những tiêu chí chấp nhận, mục đích của, xác định khi nào kết thúc và nghiệm thu, làm theo dạng markdown, code mermaid
1. Acceptance Criteria là gì?

Acceptance Criteria (AC) là tập hợp các điều kiện mà hệ thống/chức năng phải đáp ứng để Business/Customer xác nhận rằng yêu cầu đã được hoàn thành và có thể nghiệm thu.

Nói đơn giản:

Acceptance Criteria trả lời câu hỏi: "Làm thế nào để biết chức năng này đã làm đúng và có thể nghiệm thu?"

Acceptance Criteria không chỉ dùng để Developer biết cần làm gì, mà còn giúp:

BA xác định rõ phạm vi hoàn thành.
Developer hiểu điều kiện cần đáp ứng.
Tester có cơ sở viết test case.
Customer biết khi nào có thể nghiệm thu.
Tránh tranh luận "đã làm xong hay chưa".
2. Mục đích của Acceptance Criteria
Mục đích	Diễn giải
Xác định điều kiện hoàn thành	Biết chính xác khi nào một yêu cầu được xem là Done
Nghiệm thu	Customer có căn cứ xác nhận chức năng đạt yêu cầu
Kiểm thử	Tester dựa vào AC để xây dựng Test Case
Giảm hiểu nhầm	BA, Developer, Tester và Customer cùng hiểu một yêu cầu
Kiểm soát phạm vi	Tránh phát sinh chức năng ngoài phạm vi
Đo lường chất lượng	Xác định kết quả cần đạt bằng các tiêu chí cụ thể
3. Nguyên tắc xây dựng Acceptance Criteria

Acceptance Criteria nên:

Rõ ràng
Có thể kiểm thử
Có thể đo lường
Không mơ hồ
Liên kết với Business Requirement / Functional Requirement
Có điều kiện Pass/Fail

Ví dụ không tốt:

Hệ thống tìm tài xế nhanh.

Không rõ "nhanh" là bao nhiêu.

Nên viết:

Hệ thống phải bắt đầu quá trình tìm tài xế trong tối đa X giây sau khi Booking được xác nhận.

X cần được Customer xác nhận.

4. Acceptance Criteria cho các chức năng chính
AC01 – Đăng ký Customer
Mã	Acceptance Criteria
AC01.01	Customer nhập đầy đủ thông tin bắt buộc thì có thể tạo tài khoản.
AC01.02	Số điện thoại/email đã tồn tại thì hệ thống không cho đăng ký trùng.
AC01.03	Thông tin không hợp lệ phải hiển thị thông báo lỗi rõ ràng.
AC01.04	Sau khi đăng ký thành công, tài khoản được lưu vào hệ thống.
5. AC02 – Đăng nhập
Mã	Acceptance Criteria
AC02.01	Customer nhập đúng thông tin xác thực thì đăng nhập thành công.
AC02.02	Sai thông tin xác thực thì không được đăng nhập.
AC02.03	Hệ thống không hiển thị thông tin nhạy cảm trong thông báo lỗi.
AC02.04	User chưa xác thực không được truy cập chức năng yêu cầu đăng nhập.
6. AC03 – Đặt chuyến

Đây là Acceptance Criteria quan trọng nhất của CAB.

Mã	Acceptance Criteria
AC03.01	Customer phải đăng nhập trước khi đặt chuyến.
AC03.02	Customer phải cung cấp điểm đón hợp lệ.
AC03.03	Customer phải cung cấp điểm đến hợp lệ.
AC03.04	Customer phải lựa chọn loại xe hợp lệ.
AC03.05	Sau khi Customer xác nhận, hệ thống phải tạo Booking.
AC03.06	Booking mới phải chuyển sang trạng thái SEARCHING_DRIVER.
AC03.07	Hệ thống phải tìm các Driver đang AVAILABLE.
AC03.08	Driver được lựa chọn phải phù hợp với loại xe yêu cầu.
AC03.09	Hệ thống phải ưu tiên Driver theo tiêu chí Business đã được xác nhận.
AC03.10	Khi Driver Accept, hệ thống phải chuyển Booking sang DRIVER_ASSIGNED.
AC03.11	Customer phải nhận được thông tin Driver đã nhận chuyến.
AC03.12	Nếu Driver Reject, hệ thống phải tìm Driver tiếp theo.
AC03.13	Nếu Driver không phản hồi trong thời gian quy định, Assignment phải chuyển thành TIMEOUT.
AC03.14	Sau Timeout, hệ thống phải tiếp tục tìm Driver khác.
AC03.15	Customer không phải tạo lại Booking khi Driver Reject/Timeout.
AC03.16	Nếu hết thời gian tìm kiếm mà không có Driver, Customer phải nhận được thông báo rõ ràng.
7. Luồng Acceptance Criteria của việc tìm Driver

Có thể biểu diễn bằng Mermaid:

flowchart TD


    A["Customer xác nhận đặt chuyến"]
    B["Tạo Booking"]
    C["Booking = SEARCHING_DRIVER"]
    D["Tìm Driver phù hợp"]
    E{"Có Driver phù hợp?"}
    F["Gửi yêu cầu cho Driver"]
    G{"Driver phản hồi?"}
    H{"Driver Accept?"}
    I["Driver được Assign"]
    J["Booking = DRIVER_ASSIGNED"]
    K["Thông báo Customer"]
    L["Driver Reject / Timeout"]
    M{"Còn Driver khác?"}
    N["Tìm Driver tiếp theo"]
    O["Booking = NO_DRIVER_FOUND"]
    P["Thông báo Customer không tìm được Driver"]


    A --> B
    B --> C
    C --> D
    D --> E


    E -- "Có" --> F
    E -- "Không" --> O
    O --> P


    F --> G
    G -- "Có" --> H
    G -- "Không / Timeout" --> L


    H -- "Accept" --> I
    I --> J
    J --> K


    H -- "Reject" --> L
    L --> M


    M -- "Có" --> N
    N --> D


    M -- "Không" --> O
8. AC04 – Driver nhận chuyến
Mã	Acceptance Criteria
AC04.01	Chỉ Driver có trạng thái AVAILABLE mới được nhận yêu cầu chuyến.
AC04.02	Driver nhận được thông báo khi có Booking phù hợp.
AC04.03	Driver có thể Accept hoặc Reject.
AC04.04	Khi Accept thành công, Driver chuyển sang trạng thái BUSY.
AC04.05	Khi Reject, Driver không được assign vào Booking đó.
AC04.06	Driver không phản hồi quá thời gian quy định thì Assignment = TIMEOUT.
AC04.07	Một Booking chỉ được có một Driver được Assign chính thức.
9. AC05 – Thực hiện Trip
Mã	Acceptance Criteria
AC05.01	Driver được assign mới có thể bắt đầu Trip.
AC05.02	Driver có thể cập nhật DRIVER_ARRIVING.
AC05.03	Driver có thể cập nhật DRIVER_ARRIVED.
AC05.04	Driver có thể cập nhật PASSENGER_PICKED_UP.
AC05.05	Driver có thể cập nhật IN_PROGRESS.
AC05.06	Driver có thể cập nhật COMPLETED.
AC05.07	Customer nhìn thấy trạng thái Trip tương ứng.
AC05.08	Không cho phép cập nhật trạng thái sai thứ tự nếu Business Rule không cho phép.
10. AC06 – Tính cước
Mã	Acceptance Criteria
AC06.01	Fare chỉ được tính khi Trip hoàn thành hoặc theo policy đã xác nhận.
AC06.02	Hệ thống sử dụng đúng loại dịch vụ/loại xe.
AC06.03	Tổng tiền phải được tính theo Pricing Rule đã được Customer xác nhận.
AC06.04	Customer có thể xem số tiền phải thanh toán.
AC06.05	Hệ thống lưu lại kết quả tính cước.

Công thức cước cụ thể hiện chưa được khách hàng chốt, vì vậy AC này phải được cập nhật sau khi có Pricing Business Rule chính thức.

11. AC07 – Thanh toán
Mã	Acceptance Criteria
AC07.01	Customer có thể chọn tiền mặt nếu Booking/Trip cho phép.
AC07.02	Customer có thể chọn thanh toán điện tử.
AC07.03	CAB không lưu trực tiếp thông tin nhạy cảm của thẻ/tài khoản.
AC07.04	Payment Provider trả SUCCESS thì Payment = SUCCESS.
AC07.05	Payment Provider trả FAILED thì Payment = FAILED.
AC07.06	Customer nhận được thông báo khi thanh toán thất bại.
AC07.07	Customer có thể Retry theo chính sách doanh nghiệp.
AC07.08	Payment lỗi không làm mất thông tin Trip/Booking.
12. AC08 – Notification
Mã	Acceptance Criteria
AC08.01	Customer nhận thông báo khi Booking được tiếp nhận.
AC08.02	Customer nhận thông báo khi Driver Accept.
AC08.03	Customer nhận thông báo khi Driver đến điểm đón.
AC08.04	Customer nhận thông báo khi Trip hoàn thành.
AC08.05	Customer nhận thông báo kết quả Payment.
AC08.06	Driver nhận thông báo khi có Booking phù hợp.
AC08.07	Notification lỗi không làm Booking/Trip bị mất dữ liệu.
13. AC09 – Đánh giá Driver
Mã	Acceptance Criteria
AC09.01	Chỉ Customer đã thực hiện Trip mới được đánh giá Driver.
AC09.02	Chỉ Trip COMPLETED mới được đánh giá.
AC09.03	Customer phải chọn Score hợp lệ.
AC09.04	Rating được lưu thành công sau khi Submit.
AC09.05	Rating trung bình của Driver được cập nhật theo Business Rule.
14. AC10 – Staff quản lý hệ thống
Mã	Acceptance Criteria
AC10.01	Staff phải đăng nhập trước khi truy cập Admin Portal.
AC10.02	Staff chỉ được thực hiện chức năng theo Permission.
AC10.03	Staff không có quyền không được thực hiện thao tác nhạy cảm.
AC10.04	Staff có thể xem các Trip đang hoạt động.
AC10.05	Staff có thể tra cứu giao dịch.
AC10.06	Các thao tác quản trị quan trọng phải được ghi Audit Log.
15. Acceptance Criteria cho Non-Functional Requirements

Acceptance Criteria không chỉ dành cho Functional Requirement mà còn dùng cho NFR.

Ví dụ:

NFR	Acceptance Criteria
Performance	API đáp ứng trong ngưỡng thời gian đã thống nhất
Availability	Uptime đạt SLA đã thống nhất
Security	User không có quyền không thể truy cập dữ liệu
Scalability	Hệ thống đáp ứng mức tải được xác định
Reliability	Payment/Notification lỗi không làm Booking ngừng hoạt động
Audit	Thao tác quan trọng có Audit Log
Recovery	Hệ thống khôi phục trong thời gian RTO đã thống nhất

Các con số cụ thể như 2 giây, 99.9%, RTO/RPO... cần được khách hàng xác nhận trước khi đưa thành tiêu chí nghiệm thu chính thức.

16. Khi nào một Use Case được xem là "Done"?

Có thể xác định theo quy trình:

flowchart TD


    A["Business Requirement"]
    B["Functional Requirement"]
    C["Use Case"]
    D["Development"]
    E["Developer Test"]
    F["QA / SIT"]
    G{"Tất cả Acceptance Criteria đạt?"}
    H["UAT với Customer"]
    I{"Customer chấp nhận?"}
    J["DONE / ACCEPTED"]
    K["Fix / Rework"]


    A --> B
    B --> C
    C --> D
    D --> E
    E --> F
    F --> G


    G -- "Không" --> K
    K --> D


    G -- "Có" --> H
    H --> I


    I -- "Không" --> K
    I -- "Có" --> J
17. Definition of Done cho dự án CAB

Để một chức năng được nghiệm thu, nên yêu cầu tối thiểu:

 Đã implement đúng Functional Requirement.
 Tất cả Acceptance Criteria đều PASS.
 Đã hoàn thành Unit Test.
 Đã hoàn thành Integration/SIT Test.
 Không còn lỗi Critical/Blocker.
 Các lỗi còn lại được Customer chấp nhận nếu có.
 Security requirement liên quan đã được kiểm tra.
 Audit/Logging đã được kiểm tra nếu có yêu cầu.
 Documentation được cập nhật.
 Customer thực hiện UAT và xác nhận Accepted.
18. Mối liên hệ từ Requirement đến Acceptance

Toàn bộ các bước BA của CAB có thể nối thành:

flowchart LR


    BG["Business Goal"]
    BR["Business Requirement"]
    FR["Functional Requirement"]
    UC["Use Case"]
    AC["Acceptance Criteria"]
    TC["Test Case"]
    UAT["UAT"]
    DONE["Accepted / Done"]


    BG --> BR
    BR --> FR
    FR --> UC
    UC --> AC
    AC --> TC
    TC --> UAT
    UAT --> DONE
Ví dụ xuyên suốt với chức năng tìm tài xế
BG02
↓
Giảm thời gian tìm tài xế


BR
↓
Hệ thống tự động tìm và phân công Driver


FR
↓
FR01: Xác định vị trí Customer
FR02: Lọc Driver Available
FR03: Tính khoảng cách
FR04: Ưu tiên Driver
FR05: Gửi request
FR06: Xử lý Accept/Reject/Timeout


UC
↓
UC01.04 – Đặt chuyến


AC
↓
Driver Reject → tìm Driver tiếp theo
Driver Timeout → tìm Driver tiếp theo
Driver Accept → Assignment thành công
Không có Driver → thông báo Customer


TEST
↓
QA/UAT kiểm tra toàn bộ AC


DONE
↓
Customer xác nhận nghiệm thu

Mục tiêu cuối cùng: xác định rõ hệ thống phải làm gì, làm như thế nào và điều kiện nào để khách hàng xác nhận là đã yêu cầu
Bước 14: Truy xuất nguồn gốc yêu cầu, ma trận truy xuất yêu cầu, cột 1 BG, cột thứ 2 BR, cột thứ 3 FR, cột UC cột tiếp theo AC, cột tiếp theo TC
Sau khi hoàn thành các bước từ Business Goal → Business Requirement → Functional Requirement → Use Case → Acceptance Criteria, bước 14 xây dựng Requirement Traceability Matrix (RTM) để đảm bảo:

Mỗi mục tiêu Business đều được chuyển thành yêu cầu, chức năng, Use Case, tiêu chí nghiệm thu và Test Case tương ứng.

RTM giúp trả lời 3 câu hỏi:

Hệ thống phải làm gì? → FR / UC
Làm như thế nào để đáp ứng Business Goal? → BR → FR → UC
Làm sao biết đã làm đúng? → AC → TC
2. Cấu trúc RTM

Theo yêu cầu, ma trận gồm:

BG	BR	FR	UC	AC	TC

Trong đó:

BG = Business Goal
BR = Business Requirement
FR = Functional Requirement
UC = Use Case
AC = Acceptance Criteria
TC = Test Case
3. Business Goal của CAB

Trước tiên xác định các BG chính:

Mã	Business Goal
BG01	Xây dựng nền tảng CAB cho phép Customer đặt và theo dõi chuyến xe một cách thuận tiện.
BG02	Giảm thời gian và công sức trong việc tìm kiếm, phân công Driver.
BG03	Quản lý và theo dõi toàn bộ quá trình thực hiện Trip.
BG04	Hỗ trợ tính cước và thanh toán tiền mặt hoặc thanh toán điện tử an toàn.
BG05	Cung cấp hệ thống thông báo kịp thời cho Customer và Driver.
BG06	Cung cấp công cụ vận hành và quản trị cho doanh nghiệp.
BG07	Xây dựng nền tảng có khả năng mở rộng, bảo mật và hoạt động ổn định.
4. Business Requirement
Mã	Business Requirement
BR01	Hệ thống cho phép Customer đăng ký, đăng nhập và quản lý thông tin cá nhân.
BR02	Hệ thống cho phép Customer tạo và quản lý yêu cầu đặt xe.
BR03	Hệ thống tự động tìm kiếm và phân công Driver phù hợp.
BR04	Hệ thống cho phép Driver nhận, từ chối và thực hiện Trip.
BR05	Hệ thống cho phép Customer theo dõi trạng thái Trip.
BR06	Hệ thống hỗ trợ tính cước và thanh toán bằng tiền mặt hoặc điện tử.
BR07	Hệ thống cung cấp Notification cho Customer và Driver.
BR08	Hệ thống cho phép Customer đánh giá Driver sau Trip.
BR09	Hệ thống cung cấp chức năng quản trị và vận hành.
BR10	Hệ thống phải bảo mật, ghi nhận Audit và kiểm soát quyền truy cập.
BR11	Hệ thống phải có khả năng mở rộng và tích hợp với các hệ thống bên ngoài.
5. Functional Requirement

Một số FR chính:

Mã	Functional Requirement
FR01	Xác thực Customer
FR02	Quản lý thông tin Customer
FR03	Xác định vị trí Customer
FR04	Nhập điểm đón và điểm đến
FR05	Chọn loại xe
FR06	Tạo Booking
FR07	Tìm Driver Available
FR08	Lọc Driver theo loại xe
FR09	Xác định khoảng cách Driver
FR10	Ưu tiên Driver theo tiêu chí vận hành
FR11	Gửi yêu cầu chuyến cho Driver
FR12	Xử lý Driver Accept
FR13	Xử lý Driver Reject
FR14	Xử lý Driver Timeout
FR15	Tìm Driver tiếp theo
FR16	Thông báo không tìm được Driver
FR17	Cập nhật trạng thái Trip
FR18	Theo dõi vị trí Driver
FR19	Tính Fare
FR20	Thanh toán tiền mặt
FR21	Thanh toán điện tử
FR22	Retry Payment
FR23	Gửi Notification
FR24	Đánh giá Driver
FR25	Quản lý Customer/Driver/Vehicle
FR26	Giám sát Trip
FR27	Tra cứu giao dịch
FR28	Báo cáo hoạt động
FR29	RBAC
FR30	Audit Log
6. Requirement Traceability Matrix

Dưới đây là RTM cấp Business → Test cho CAB:

BG	BR	FR	UC	AC	TC
BG01	BR01	FR01, FR02	UC01.01, UC01.02, UC01.03	AC01.01–AC01.04, AC02.01–AC02.04	TC01–TC06
BG01	BR02	FR03–FR06	UC01.04	AC03.01–AC03.06	TC07–TC14
BG02	BR03	FR07–FR16	UC01.04	AC03.07–AC03.16	TC15–TC28
BG02	BR04	FR11–FR15	UC02.05–UC02.07	AC04.01–AC04.07	TC29–TC38
BG03	BR05	FR17–FR18	UC01.05, UC02.09	AC05.01–AC05.08	TC39–TC48
BG04	BR06	FR19–FR22	UC01.07, UC01.08	AC06.01–AC06.05, AC07.01–AC07.08	TC49–TC62
BG05	BR07	FR23	UC01.05, UC02.05	AC08.01–AC08.07	TC63–TC72
BG01	BR08	FR24	UC01.09	AC09.01–AC09.05	TC73–TC77
BG06	BR09	FR25–FR28	UC03.02–UC03.07, UC03.09	AC10.01–AC10.06	TC78–TC90
BG06	BR10	FR29–FR30	UC03.01, UC03.08, UC03.10	AC10.01–AC10.06	TC91–TC98
BG07	BR11	FR29–FR30 + NFR	UC03.08, UC03.10	AC NFR	TC99–TC110
7. Traceability chi tiết cho chức năng đặt xe

Đây là phần quan trọng nhất nên có trong tài liệu.

BG	BR	FR	UC	AC	TC
BG01	BR02	FR03	UC01.04	AC03.02	TC07 – Kiểm tra điểm đón
BG01	BR02	FR04	UC01.04	AC03.03	TC08 – Kiểm tra điểm đến
BG01	BR02	FR05	UC01.04	AC03.04	TC09 – Chọn loại xe
BG01	BR02	FR06	UC01.04	AC03.05	TC10 – Tạo Booking
BG02	BR03	FR07	UC01.04	AC03.07	TC15 – Tìm Driver Available
BG02	BR03	FR08	UC01.04	AC03.08	TC16 – Lọc loại xe
BG02	BR03	FR09	UC01.04	AC03.09	TC17 – Tính khoảng cách
BG02	BR03	FR10	UC01.04	AC03.09	TC18 – Ưu tiên Driver
BG02	BR03	FR11	UC01.04	AC03.10	TC19 – Driver Accept
BG02	BR03	FR13	UC01.04	AC03.12	TC20 – Driver Reject
BG02	BR03	FR14	UC01.04	AC03.13	TC21 – Driver Timeout
BG02	BR03	FR15	UC01.04	AC03.14	TC22 – Tìm Driver tiếp theo
BG02	BR03	FR16	UC01.04	AC03.16	TC23 – Không có Driver
8. Mermaid – Traceability Flow

Có thể vẽ mối quan hệ từ BG → BR → FR → UC → AC → TC bằng Mermaid:

flowchart LR


    BG02["BG02\nGiảm thời gian tìm Driver"]


    BR03["BR03\nTự động tìm & phân công Driver"]


    FR07["FR07\nTìm Driver Available"]
    FR08["FR08\nLọc theo loại xe"]
    FR09["FR09\nXác định khoảng cách"]
    FR10["FR10\nƯu tiên Driver"]
    FR11["FR11\nGửi yêu cầu"]
    FR13["FR13\nXử lý Reject"]
    FR14["FR14\nXử lý Timeout"]
    FR15["FR15\nTìm Driver tiếp theo"]


    UC["UC01.04\nĐặt chuyến"]


    AC01["AC03.07\nDriver phải Available"]
    AC02["AC03.08\nDriver phù hợp loại xe"]
    AC03["AC03.09\nƯu tiên Driver"]
    AC04["AC03.10\nDriver Accept"]
    AC05["AC03.12\nDriver Reject"]
    AC06["AC03.13\nDriver Timeout"]
    AC07["AC03.14\nTìm Driver tiếp theo"]
    AC08["AC03.16\nKhông tìm được Driver"]


    TC01["TC15\nTest Available Driver"]
    TC02["TC16\nTest Vehicle Type"]
    TC03["TC17\nTest Distance"]
    TC04["TC18\nTest Priority"]
    TC05["TC19\nTest Accept"]
    TC06["TC20\nTest Reject"]
    TC07["TC21\nTest Timeout"]
    TC08["TC22\nTest Next Driver"]
    TC09["TC23\nTest No Driver"]


    BG02 --> BR03


    BR03 --> FR07
    BR03 --> FR08
    BR03 --> FR09
    BR03 --> FR10
    BR03 --> FR11
    BR03 --> FR13
    BR03 --> FR14
    BR03 --> FR15


    FR07 --> UC
    FR08 --> UC
    FR09 --> UC
    FR10 --> UC
    FR11 --> UC
    FR13 --> UC
    FR14 --> UC
    FR15 --> UC


    UC --> AC01
    UC --> AC02
    UC --> AC03
    UC --> AC04
    UC --> AC05
    UC --> AC06
    UC --> AC07
    UC --> AC08


    AC01 --> TC01
    AC02 --> TC02
    AC03 --> TC03
    AC04 --> TC05
    AC05 --> TC06
    AC06 --> TC07
    AC07 --> TC08
    AC08 --> TC09
9. Mermaid – Tổng thể Requirement Traceability
flowchart TD


    BG["Business Goals"]


    BG01["BG01\nĐặt & theo dõi chuyến"]
    BG02["BG02\nGiảm thời gian tìm Driver"]
    BG03["BG03\nQuản lý Trip"]
    BG04["BG04\nTính cước & Thanh toán"]
    BG05["BG05\nThông báo"]
    BG06["BG06\nVận hành & Quản trị"]
    BG07["BG07\nMở rộng & Bảo mật"]


    BR["Business Requirements"]
    FR["Functional Requirements"]
    UC["Use Cases"]
    AC["Acceptance Criteria"]
    TC["Test Cases"]


    BG --> BG01
    BG --> BG02
    BG --> BG03
    BG --> BG04
    BG --> BG05
    BG --> BG06
    BG --> BG07


    BG01 --> BR
    BG02 --> BR
    BG03 --> BR
    BG04 --> BR
    BG05 --> BR
    BG06 --> BR
    BG07 --> BR


    BR --> FR
    FR --> UC
    UC --> AC
    AC --> TC


    TC --> RESULT["UAT / Acceptance"]


    RESULT --> PASS{"All criteria PASS?"}


    PASS -- "YES" --> DONE["ACCEPTED / DONE"]
    PASS -- "NO" --> FIX["REWORK"]
    FIX --> FR
10. Ý nghĩa của RTM

RTM giúp kiểm tra không bị mất yêu cầu trong quá trình phát triển.

Ví dụ:

BG02
↓
BR03
↓
FR07
↓
UC01.04
↓
AC03.07
↓
TC15
↓
PASS

Nếu có một BR nhưng không có FR:

BR03
↓
❌ Không có FR

→ Có khả năng yêu cầu chưa được thiết kế/triển khai.

Nếu có FR nhưng không có AC:

FR07
↓
❌ Không có AC

→ Chưa xác định rõ điều kiện để Customer nghiệm thu.

Nếu có AC nhưng không có TC:

AC03.07
↓
❌ Không có TC

→ Chưa có Test Case để chứng minh yêu cầu đạt.

11. Coverage cuối cùng

Mục tiêu của Bước 14 là đạt được chuỗi:

BG
↓
BR
↓
FR
↓
UC
↓
AC
↓
TC
↓
UAT
↓
Customer Acceptance
