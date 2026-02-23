# ShopTechTPKT – Organization Profile

## Tổng quan

**ShopTechTPKT** là organization lưu trữ mã nguồn của dự án **Shop Online** – nền tảng thương mại điện tử (e-commerce) chuyên bán và trưng bày máy tính, linh kiện PC. Dự án được phát triển full-stack với backend API (Java/Spring Boot), giao diện web (React), tích hợp cổng thanh toán VNPay, hệ thống chat hỗ trợ khách hàng, quản lý đơn hàng và vận chuyển, chương trình khuyến mãi và thông báo push. Mục đích của organization là tập trung toàn bộ repository liên quan để dễ quản lý, review và trình bày trong portfolio hoặc CV.

---

## Mục tiêu và phạm vi dự án

- Xây dựng website bán hàng trực tuyến hoàn chỉnh: catalog sản phẩm, giỏ hàng, thanh toán trực tuyến qua VNPay, quản lý tài khoản và đơn hàng.
- Cung cấp API REST cho frontend và tích hợp bên thứ ba (VNPay, Google OAuth2, email, push notification).
- Hỗ trợ real-time: chat giữa khách hàng và nhân viên hỗ trợ qua WebSocket; thông báo đơn hàng qua email và FCM.
- Phân quyền rõ ràng: khách hàng, nhân viên, quản lý; khu vực admin cho quản lý sản phẩm, đơn hàng, khách hàng, khuyến mãi, thống kê.
- Đảm bảo bảo mật (JWT, OAuth2), giới hạn tần suất gọi API (rate limiting), và tài liệu API (Swagger).

---

## Kiến trúc hệ thống

- **Frontend (React):** Single Page Application chạy trên trình duyệt, gọi API REST và kết nối WebSocket tới backend; quản lý state với Redux; hỗ trợ đa ngôn ngữ (i18n).
- **Backend (Spring Boot):** API server cung cấp REST và WebSocket; xác thực JWT và OAuth2; kết nối MySQL (dữ liệu chính), Redis (cache, rate limit), RabbitMQ (hàng đợi, tùy cấu hình); tích hợp Spring AI (Gemini) cho tính năng hỗ trợ khách hàng.
- **Cổng thanh toán:** Ứng dụng Node.js (vnpay_nodejs) kết nối VNPay sandbox (tạo URL thanh toán, xử lý return/IPN); ứng dụng demo (vnpay_demo_thach) mô phỏng luồng thanh toán và gửi email/push sau khi thanh toán thành công.
- **Chat và thông báo:** WebSocket trên backend; gửi email xác nhận đơn qua Spring Mail; push notification qua Firebase Cloud Messaging (FCM) trong phần demo thanh toán.

Luồng dữ liệu: Người dùng tương tác với React frontend; frontend gọi API backend và (khi thanh toán) chuyển hướng sang VNPay hoặc demo; sau thanh toán, backend nhận callback/notification và gửi email; demo có thể gửi thêm push qua FCM.

---

## Tính năng chính theo module

**Quản lý sản phẩm và danh mục:** CRUD sản phẩm, danh mục; lọc, tìm kiếm, phân trang; hiển thị chi tiết sản phẩm, thông số, đánh giá.

**Giỏ hàng và đơn hàng:** Thêm/sửa/xóa giỏ hàng; tạo đơn hàng; chọn phương thức thanh toán (VNPay); lưu lịch sử đơn hàng; theo dõi trạng thái đơn (đang xử lý, đang giao, đã giao); cập nhật ngày giao hàng (admin).

**Người dùng và phân quyền:** Đăng ký, đăng nhập (form và Google OAuth2); JWT cho phiên đăng nhập; phân quyền theo vai trò (khách, nhân viên, quản lý); quản lý thông tin cá nhân, đơn hàng, địa chỉ; ưu đãi theo khách hàng (mã giảm giá, voucher).

**Thanh toán VNPay:** Tích hợp VNPay sandbox (Node.js): tạo URL thanh toán, xử lý return URL và IPN, truy vấn và hoàn tiền; demo (vnpay_demo_thach) mô phỏng chọn ngân hàng, nhập thẻ, OTP, trả về kết quả và gửi email/push.

**Chat và hỗ trợ:** Chat real-time giữa khách hàng và nhân viên qua WebSocket; lưu lịch sử tin nhắn; tích hợp Spring AI (Gemini) cho trợ lý ảo/hỗ trợ khách hàng; CauHinhChat chứa cấu hình và UI liên quan chat cùng component UI luồng VNPay.

**Admin và báo cáo:** Giao diện admin quản lý sản phẩm, đơn hàng, khách hàng, nhân viên, khuyến mãi, đánh giá; thống kê cơ bản; quản lý lịch hẹn (appointment); xuất/thống kê theo nhu cầu (có thể mở rộng).

**Khác:** Đa ngôn ngữ (i18n); tích hợp bản đồ (Leaflet/Mapbox) nếu có; biểu đồ (Recharts); rate limiting API (Bucket4j); tài liệu API (Swagger/OpenAPI).

---

## Công nghệ sử dụng (chi tiết)

**Backend:** Java 21, Spring Boot 3.x, Spring Security (JWT, OAuth2 Resource Server, OAuth2 Client), Spring Data JPA, Spring WebSocket, Spring Mail, Spring AI (OpenAI-compatible API với Gemini), Bucket4j, Swagger/OpenAPI (springdoc), MySQL 8, Redis, RabbitMQ, Lombok, Maven.

**Frontend:** React 19, Vite, Redux Toolkit, React Router, Tailwind CSS, Axios, i18next (đa ngôn ngữ), SockJS + STOMP (WebSocket), Leaflet / Mapbox GL, Recharts, React Toastify, các thư viện UI và icon (Lucide, Font Awesome, React Icons).

**Thanh toán và dịch vụ bên ngoài:** Node.js, Express, VNPay API (sandbox), Jade (template), Moment, QS, Crypto (HMAC); Firebase Admin SDK (FCM) trong repo demo thanh toán.

**Công cụ và môi trường:** Git, GitHub; có thể triển khai trên server Linux với Nginx, PM2 (Node), JAR (Spring Boot).

---

## Cấu trúc repository trong organization

| Repository | Mô tả ngắn |
|------------|-------------|
| **Backend_Web** | API Spring Boot: sản phẩm, đơn hàng, giỏ hàng, user, auth (JWT/OAuth2), WebSocket chat, VNPay callback, email, Swagger, rate limit, Spring AI (Gemini). |
| **FrontEnd** | Ứng dụng web React (Vite): trang chủ, catalog, giỏ hàng, checkout, thanh toán, profile, đơn hàng, chat, admin, báo cáo, i18n. |
| **vnpay_nodejs** | Ứng dụng Node.js/Express tích hợp VNPay sandbox: tạo URL thanh toán, return URL, IPN, truy vấn giao dịch, hoàn tiền. |
| **vnpay_demo_thach** | Demo/mock luồng thanh toán: chọn ngân hàng, nhập thẻ, OTP; gửi email xác nhận qua Backend_Web và push notification qua FCM. |
| **CauHinhChat** | Cấu hình chat và bộ component UI cho luồng thanh toán VNPay (layout, chọn phương thức, OTP, kết quả). |

---

## Liên kết

- Danh sách repository: [ShopTechTPKT – Repositories](https://github.com/ShopTechTPKT?q=&type=source).
- Từng repository có README riêng (nếu đã bổ sung) mô tả cách cấu hình, biến môi trường và chạy local.

---

ShopTechTPKT
