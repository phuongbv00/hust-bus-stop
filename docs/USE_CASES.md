# **Đặc tả Use Case (UC) \- Hệ thống Quản lý Xe buýt Sinh viên**

Tài liệu này mô tả chi tiết các trường hợp sử dụng (Use Cases) của hệ thống, được phân loại theo từng tác nhân (Actor) tương tác. Mỗi UC được phân tích sâu hơn về mục tiêu, luồng sự kiện, và các điều kiện liên quan để phục vụ cho việc thiết kế và phát triển phần mềm.

## **A. Tác nhân: Sinh viên**

Đại diện cho người dùng cuối của dịch vụ, sử dụng ứng dụng di động để đăng ký, theo dõi và tương tác với hệ thống xe buýt.

### **UC-01: Quản lý tài khoản và dịch vụ đưa đón**

* **Mô tả gốc:** Cho phép sinh viên đăng ký, cập nhật thông tin cá nhân, địa chỉ, lịch học và trạng thái sử dụng dịch vụ (sử dụng, tạm ngưng, hủy).  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Cung cấp cho sinh viên khả năng tự quản lý (CRUD) thông tin cá nhân và trạng thái đăng ký dịch vụ.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng.  
  * **Luồng sự kiện chính:**  
    1. Sinh viên chọn chức năng "Tài khoản" hoặc "Đăng ký dịch vụ" sau khi đăng nhập.  
    2. Hệ thống hiển thị giao diện quản lý thông tin, bao gồm: thông tin cá nhân (Họ tên, Mã sinh viên, SĐT), địa chỉ đón, lịch học.  
    3. Sinh viên thực hiện một trong các thao tác: Đăng ký mới, Cập nhật, Thay đổi trạng thái.  
    4. Hệ thống xác thực dữ liệu và lưu các thay đổi vào cơ sở dữ liệu.  
    5. Hệ thống gửi thông báo xác nhận thao tác thành công.  
  * **Điều kiện tiên quyết:** Sinh viên đã hoàn thành UC-16.  
  * **Kết quả:** Thông tin và trạng thái đăng ký của sinh viên được cập nhật.

### **UC-02: Xem lịch trình và theo dõi xe buýt theo thời gian thực**

* **Mô tả gốc:** Sinh viên xem được giờ đón, điểm đón, lộ trình và vị trí hiện tại của xe trên bản đồ.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Cung cấp giao diện bản đồ trực quan để sinh viên theo dõi vị trí chính xác của xe buýt.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng, UC-18: Xử lý dữ liệu vị trí GPS.  
  * **Luồng sự kiện chính:**  
    1. Sinh viên mở chức năng "Theo dõi xe".  
    2. Hệ thống hiển thị bản đồ với lộ trình, các điểm đón, và vị trí xe buýt được cập nhật liên tục.  
  * **Điều kiện tiên quyết:** Sinh viên đã được phê duyệt đăng ký. Chuyến đi đang hoạt động.  
  * **Kết quả:** Sinh viên chủ động nắm bắt thông tin di chuyển của xe.

### **UC-03: Nhận thông báo tự động**

* **Mô tả gốc:** Hệ thống tự động gửi các thông báo quan trọng như nhắc giờ đón, xe sắp đến, hoặc các thay đổi đột xuất.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Chủ động cung cấp thông tin kịp thời cho sinh viên.  
  * **Bao gồm (Includes):** UC-17: Gửi thông báo đẩy.  
  * **Các sự kiện kích hoạt thông báo:** Nhắc lịch, Xe sắp đến, Thông báo từ QTV, Cập nhật từ tài xế.  
  * **Điều kiện tiên quyết:** Sinh viên đã cài đặt ứng dụng và cấp quyền nhận thông báo.  
  * **Kết quả:** Sinh viên nhận được thông tin quan trọng mà không cần mở ứng dụng.

### **UC-04: Check-in khi lên xe**

* **Mô tả gốc:** Sinh viên thực hiện check-in khi lên xe để hệ thống ghi nhận sự có mặt, từ đó thu thập dữ liệu về nhu cầu sử dụng thực tế so với đăng ký.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** So sánh dữ liệu đăng ký và dữ liệu sử dụng thực tế để tối ưu hóa vận hành. Ghi nhận chính xác danh sách sinh viên có mặt trên mỗi chuyến đi.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng.  
  * **Luồng sự kiện chính (Check-in bằng QR Code):**  
    1. Trên mỗi xe buýt có dán một mã QR code được tạo ra và gán cho chuyến đi đó.  
    2. Sinh viên mở ứng dụng, chọn chức năng "Check-in".  
    3. Ứng dụng mở camera để quét mã QR.  
    4. Sau khi quét thành công, hệ thống xác thực mã QR hợp lệ (đúng chuyến, đúng giờ) và ghi nhận sinh viên đã lên xe thành công.  
    5. Hệ thống hiển thị thông báo check-in thành công trên ứng dụng của sinh viên và có thể gửi tín hiệu đến một thiết bị của tài xế.  
  * **Luồng sự kiện thay thế (Mất kết nối mạng):**  
    1. Nếu không có mạng, ứng dụng lưu lại thông tin check-in (mã sinh viên, mã chuyến đi, thời gian) tạm thời trên thiết bị.  
    2. Khi có kết nối mạng trở lại, ứng dụng tự động đồng bộ dữ liệu check-in lên máy chủ.  
  * **Điều kiện tiên quyết:** Sinh viên đã đăng nhập. Chuyến đi đang hoạt động và sinh viên có đăng ký cho chuyến đi này.  
  * **Kết quả:** Hệ thống có dữ liệu chính xác về số lượng và danh sách sinh viên trên mỗi chuyến đi, làm cơ sở cho việc phân tích ở UC-12.

## **B. Tác nhân: Quản trị viên**

Người dùng quản lý toàn bộ hoạt động của hệ thống thông qua một giao diện web (dashboard).

### **UC-05: Quản lý đăng ký của sinh viên**

* **Mô tả gốc:** Xem danh sách, phê duyệt và quản lý thông tin của các sinh viên đã đăng ký dịch vụ.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Xử lý các yêu cầu đăng ký dịch vụ từ sinh viên.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng, UC-17: Gửi thông báo đẩy.  
  * **Luồng sự kiện chính:** QTV xem danh sách, chọn một yêu cầu, và thực hiện "Phê duyệt" hoặc "Từ chối". Hệ thống cập nhật trạng thái và gửi thông báo cho sinh viên.  
  * **Kết quả:** Trạng thái đăng ký của sinh viên được cập nhật.

### **UC-06: Phân tích và thiết lập điểm đón tự động**

* **Mô tả gốc:** Hệ thống tự động đề xuất các điểm đón tối ưu. Quản trị viên có thể tinh chỉnh và phê duyệt.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Tự động hóa việc xác định các điểm đón tối ưu dựa trên dữ liệu.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng.  
  * **Luồng sự kiện chính:** QTV ra lệnh thực thi phân tích. Hệ thống chạy tác vụ nền, gom cụm địa chỉ và đề xuất điểm đón. QTV xem xét, tinh chỉnh và phê duyệt.  
  * **Kết quả:** Danh sách các điểm đón tối ưu được tạo ra.

### **UC-07: Quản lý phương tiện và tài xế**

* **Mô tả gốc:** Quản lý danh sách xe và thông tin tài xế.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Quản lý tập trung thông tin về nguồn lực.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng.  
  * **Chức năng:** Cung cấp giao diện CRUD cho đối tượng Phương tiện và Tài xế.  
  * **Kết quả:** Dữ liệu về xe và tài xế luôn được cập nhật.

### **UC-08: Tự động tạo lộ trình và lịch trình**

* **Mô tả gốc:** Dựa trên dữ liệu điểm đón đã được thiết lập, hệ thống tự động tạo ra các lộ trình tối ưu và ước tính khung giờ hoạt động. Quản trị viên xem xét, tinh chỉnh và phê duyệt.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Tự động hóa việc xây dựng các tuyến đường và lịch trình một cách khoa học, giảm thiểu thời gian di chuyển và chi phí vận hành.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng.  
  * **Luồng sự kiện chính:**  
    1. QTV truy cập chức năng "Tạo lộ trình tự động".  
    2. Hệ thống chạy thuật toán tối ưu hóa (ví dụ: giải bài toán Traveling Salesperson Problem \- TSP) dựa trên tập hợp các điểm đón đã được phê duyệt ở UC-06.  
    3. Hệ thống tạo ra các phương án lộ trình (ví dụ: Tuyến A, Tuyến B) và sắp xếp thứ tự các điểm đón trong mỗi lộ trình.  
    4. Dựa vào dữ liệu giao thông thực tế (từ API bản đồ), hệ thống ước tính thời gian di chuyển và đề xuất các khung giờ hoạt động cho mỗi lộ trình.  
    5. Hệ thống trình bày các lộ trình và lịch trình đề xuất cho QTV dưới dạng bản đồ và bảng biểu trực quan.  
    6. QTV xem xét, có thể tinh chỉnh (thay đổi thứ tự điểm đón, điều chỉnh giờ xuất phát) và phê duyệt phương án cuối cùng.  
  * **Điều kiện tiên quyết:** Đã hoàn thành UC-06 (có danh sách điểm đón đã được phê duyệt).  
  * **Kết quả:** Các tuyến xe và lịch hoạt động tối ưu được định nghĩa trong hệ thống.

### **UC-09: Tự động điều phối phương tiện**

* **Mô tả gốc:** Hệ thống tự động phân công tài xế và xe cho các chuyến đi đã có lịch trình. Quản trị viên chỉ cần xem xét, tinh chỉnh lại khi cần thiết và phê duyệt.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Tối ưu hóa việc sử dụng nguồn lực (xe, tài xế) bằng cách tự động hóa quy trình phân công, đảm bảo phù hợp về tải trọng và lịch làm việc.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng, UC-17: Gửi thông báo đẩy.  
  * **Luồng sự kiện chính:**  
    1. Đến một thời điểm định trước (ví dụ: 4:00 PM hàng ngày), hệ thống tự động chạy tác vụ điều phối cho ngày hôm sau.  
    2. Hệ thống tổng hợp dữ liệu: các chuyến đi theo lịch trình (từ UC-08), số lượng sinh viên đăng ký cho mỗi chuyến, danh sách xe và tài xế khả dụng.  
    3. Thuật toán sẽ thực hiện việc ghép cặp tối ưu: chọn xe có số ghế phù hợp nhất với lượng khách, gán tài xế có lịch trống và phù hợp.  
    4. Hệ thống tạo ra một "Kế hoạch điều phối đề xuất" và hiển thị trên dashboard của QTV.  
    5. QTV xem xét kế hoạch. Nếu cần, QTV có thể can thiệp thủ công (ví dụ: đổi tài xế cho một chuyến vì lý do đặc biệt).  
    6. QTV phê duyệt kế hoạch điều phối.  
    7. Sau khi phê duyệt, hệ thống chính thức gán nhiệm vụ và gửi thông tin chi tiết đến ứng dụng của từng tài xế.  
  * **Điều kiện tiên quyết:** Đã có lịch trình các chuyến đi (từ UC-08) và dữ liệu về xe/tài xế khả dụng (từ UC-07).  
  * **Kết quả:** Tất cả các chuyến đi trong ngày được phân công tài xế và xe một cách tối ưu.

### **UC-10: Giám sát hoạt động theo thời gian thực**

* **Mô tả gốc:** Theo dõi vị trí, trạng thái của tất cả các xe trên một dashboard.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Cung cấp cái nhìn tổng quan về hoạt động của đội xe.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng, UC-18: Xử lý dữ liệu vị trí GPS.  
  * **Chức năng:** Dashboard hiển thị bản đồ vị trí xe, danh sách chuyến đi và các cảnh báo tự động.  
  * **Kết quả:** QTV kiểm soát được tình hình hoạt động.

### **UC-11: Gửi thông báo khẩn cấp**

* **Mô tả gốc:** Gửi thông báo hàng loạt tới sinh viên và tài xế.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Cung cấp công cụ truyền thông để xử lý các tình huống khẩn cấp.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng, UC-17: Gửi thông báo đẩy.  
  * **Luồng sự kiện chính:** QTV chọn đối tượng nhận, soạn nội dung và gửi đi.  
  * **Kết quả:** Thông tin quan trọng được truyền tải nhanh chóng.

### **UC-12: Xem báo cáo và thống kê**

* **Mô tả gốc:** Xem các báo cáo về hiệu suất hoạt động.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Cung cấp các chỉ số đo lường hiệu suất (KPIs) để đánh giá.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng.  
  * **Các báo cáo chính:** Hiệu suất chuyến đi, hiệu quả sử dụng (so sánh đăng ký vs. check-in), người dùng, phản hồi.  
  * **Kết quả:** QTV có thông tin để tối ưu hóa vận hành.

### **UC-13: Quản lý phản hồi của người dùng**

* **Mô tả gốc:** Tiếp nhận, xem xét và xử lý các phản hồi do sinh viên gửi đến.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Đảm bảo mọi phản hồi từ sinh viên đều được xử lý.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng.  
  * **Luồng sự kiện chính:** QTV xem danh sách phản hồi, xem chi tiết và thay đổi trạng thái.  
  * **Kết quả:** Vòng lặp phản hồi được khép kín.

## **C. Tác nhân: Tài xế**

Người trực tiếp vận hành phương tiện, sử dụng ứng dụng di động chuyên dụng.

### **UC-14: Xem nhiệm vụ và lộ trình được phân công**

* **Mô tả gốc:** Tài xế đăng nhập để xem chi tiết chuyến đi được giao trong ngày.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Cung cấp đầy đủ thông tin cần thiết cho tài xế.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng.  
  * **Luồng sự kiện chính:** Tài xế đăng nhập, xem danh sách chuyến đi, chọn một chuyến để xem chi tiết lộ trình, điểm đón.  
  * **Điều kiện tiên quyết:** Tài xế đã được QTV phân công.  
  * **Kết quả:** Tài xế nắm rõ nhiệm vụ cần thực hiện.

### **UC-15: Cập nhật trạng thái chuyến đi**

* **Mô tả gốc:** Tài xế cập nhật các trạng thái chính của chuyến đi.  
* **Phân tích chi tiết:**  
  * **Mục tiêu:** Ghi nhận các cột mốc quan trọng của chuyến đi theo thời gian thực.  
  * **Bao gồm (Includes):** UC-16: Xác thực người dùng, UC-18: Xử lý dữ liệu vị trí GPS.  
  * **Luồng sự kiện chính:** Tài xế nhấn các nút "Bắt đầu", "Đã đến điểm đón", "Kết thúc" trên ứng dụng.  
  * **Điều kiện tiên quyết:** Tài xế đang trong màn hình chi tiết của một chuyến đi.  
  * **Kết quả:** Trạng thái và vị trí của chuyến đi được cập nhật lên hệ thống.

## **D. Use Cases Phụ thuộc (Supporting Use Cases)**

Đây là các Use Case nền tảng, cung cấp các chức năng chung được các Use Case chính sử dụng lại (thông qua quan hệ \<\<include\>\>).

### **UC-16: Xác thực người dùng**

* **Mô tả:** Cung cấp cơ chế đăng nhập và xác thực danh tính cho tất cả các tác nhân. Hệ thống có thể tích hợp với các nhà cung cấp danh tính của nhà trường (ví dụ: Google Workspace, Microsoft Azure AD) thông qua các giao thức chuẩn như **OAuth2/OpenID Connect** để mang lại trải nghiệm đăng nhập một lần (Single Sign-On).  
* **Tác nhân:** Sinh viên, Quản trị viên, Tài xế.  
* **Luồng sự kiện chính (Ví dụ với OAuth2):**  
  1. Người dùng chọn "Đăng nhập bằng tài khoản nhà trường".  
  2. Hệ thống chuyển hướng người dùng đến trang đăng nhập của nhà cung cấp danh tính.  
  3. Người dùng nhập thông tin xác thực.  
  4. Sau khi thành công, người dùng được chuyển hướng trở lại ứng dụng kèm theo thông tin xác thực.  
  5. Hệ thống cấp cho người dùng một phiên làm việc (session).  
* **Được bao gồm bởi (Included by):** Hầu hết các UC chính, là bước tiền đề để người dùng có thể tương tác với các chức năng được bảo vệ.

### **UC-17: Gửi thông báo đẩy (Push Notification)**

* **Mô tả:** Cung cấp một dịch vụ trung tâm để gửi thông báo đẩy đến ứng dụng di động của sinh viên và tài xế. Dịch vụ này tương tác với các nền tảng của Apple (APNS) và Google (FCM).  
* **Mô tả chi tiết:** Khi một sự kiện trong hệ thống cần thông báo cho người dùng, nó sẽ gọi đến dịch vụ này với các tham số (người nhận, nội dung). Dịch vụ sẽ tìm thiết bị tương ứng của người nhận và gửi thông báo qua cổng phù hợp.  
* **Được bao gồm bởi (Included by):** UC-03, UC-05, UC-09, UC-11.

### **UC-18: Xử lý dữ liệu vị trí GPS**

* **Mô tả:** Tiếp nhận, lưu trữ và cung cấp dữ liệu vị trí (kinh độ, vĩ độ) được gửi từ ứng dụng của tài xế.  
* **Mô tả chi tiết:** Dịch vụ này lắng nghe các cập nhật vị trí từ tài xế. Dữ liệu sau khi được xác thực sẽ được lưu và đồng thời phát (broadcast) đến các client đang kết nối (sinh viên, QTV) để cập nhật vị trí xe trên bản đồ theo thời gian thực.  
* **Được bao gồm bởi (Included by):** UC-02, UC-10, UC-15.

