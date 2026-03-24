# 🚀 AWS Cloud & Full-stack Mastery - Week 3  Integration & Optimization

## 📝 Project Overview
- **Student:** Hoàng Sỹ Khiêm
- **Role:** Cloud Intern / AWS Learner / Team leader
- **Batch:** Bootcamp - First Cloud AI Journey @ AWS Study Group
- **Duration:** 23/03/2026 - 22/03/2026
- **Stack:** AWS Serverless (SST v3, Lambda, DynamoDB, S3, Cognito, API Gateway, CloudFront, VPC), React + Vite 6, TypeScript, Swagger UI.

---

## 📝 Project Overview
Tuần 3 tập trung vào việc kết nối hệ sinh thái Backend Serverless với giao diện người dùng (Frontend), đồng thời tối ưu hóa tốc độ truyền tải nội dung (Music Streaming) và thiết lập quy trình vận hành tự động chuyên nghiệp.

---

## 🎯 1. Mục tiêu đào tạo (Training Objectives)

* **Identity Handshake Orchestration:** Xây dựng quy trình xác thực đa lớp, kết nối đồng bộ giữa React Frontend và AWS Cognito User Pool.
* **State Management for Auth:** Quản lý trạng thái đăng nhập tập trung (Global State), đảm bảo tính nhất quán của dữ liệu người dùng trên toàn bộ ứng dụng.
* **Security Interceptor Design:** Thiết kế hệ thống đánh chặn (Interceptors) tự động xử lý bài toán "Authorization" và "Session Expired" mà không cần can thiệp thủ công vào từng Request.
* **Secure Token Storage:** Nghiên cứu và triển khai cơ chế lưu trữ JWT an toàn, chống lại các cuộc tấn công XSS và CSRF cơ bản tại phía Client.
* **Token Rotation Strategy:** Triển khai cơ chế xoay vòng Token (Refresh Token) để tối ưu bảo mật và trải nghiệm người dùng.
* **Advanced Data Retrieval:** Làm chủ kỹ thuật **Pagination (Cursor-based)** để xử lý tập dữ liệu lớn trên DynamoDB.
* **Functional Refactoring:** Nâng cao tính tái sử dụng code thông qua Higher-Order Functions (`makeHandler`, `makeAuthHandler`).

## 📅 2. Nhật ký công việc chi tiết (Detailed Worklog)

| Day | Task Details | Start Date | Completion Date | Reference Material |
|:---:|:---|:---:|:---:|:---|
| **9** | **Deep Integration: Frontend Auth & API Security** <br> <br> **Buổi sáng: Setup & Config** <br> - Cấu hình AWS Amplify SDK v6, khởi tạo Instance kết nối với `UserPoolId` và `ClientId` từ Backend. <br> - Xây dựng `AuthContext` và `useAuth` hook để quản lý trạng thái `user`, `loading`, và `isAuthenticated`. <br> <br> **Buổi chiều: Logic & Interceptor** <br> - Triển khai luồng Login/Logout/Register đồng bộ với DynamoDB persistence. <br> - Viết **Axios Interceptor** để tự động "inject" JWT vào `Authorization: Bearer <Token>`. <br> - Xử lý logic **Protected Routes** (ngăn chặn User chưa login vào trang `/admin` hoặc `/upload`). <br> **System Hardening & Feature Expansion:** <br> - Triển khai `/auth/refresh` và `/auth/logout` (GlobalSignOut). <br> - Xây dựng Search Engine và Pagination (Cursor-based). <br> - Cấu hình `/media/upload-image` (Presigned URL cho JPEG/PNG/WEBP). <br> - Refactor Handlers hỗ trợ Query Params nâng cao.| 03/24/2026 | 03/24/2026 | [AWS Amplify Auth](https://docs.amplify.aws/lib/auth/getting-started/) <br> [Axios Interceptors](https://axios-http.com/docs/interceptors) |

---

## 🏆 3. Kết quả đạt được (Key Achievements)
* **Persistent Identity:** Hệ thống duy trì trạng thái đăng nhập sau khi Refresh trang nhờ cơ chế đồng bộ giữa Cognito Session và Local State.
* **Centralized Auth Configuration:** Đóng gói toàn bộ thông số AWS (Region, Identity Pool, User Pool) vào một file cấu hình duy nhất, sẵn sàng cho việc thay đổi Environment (Dev/Staging/Prod).
* **Automated Security Headers:** Thành công trong việc tự động đính kèm `Access Token` vào Header cho tất cả các request gọi tới các endpoint được bảo vệ (như `/getUploadUrl` hay CRUD Song/Artist).
* **Swagger Sync:** Xác thực thành công khả năng tương thích giữa JWT được lấy từ giao diện và việc Test API trực tiếp trên Swagger UI đã cài đặt ở Tuần 2.
* **Robust Auth Lifecycle:** Hoàn thiện luồng xác thực từ Login, Refresh đến Logout an toàn trên toàn hệ thống.
* **Performance Optimized:** 100% các list endpoints (`/songs`, `/artists`, `/albums`) đã hỗ trợ phân trang Cursor-based, giảm tải cho Database.
* **Smart Search:** Triển khai thành công tính năng tìm kiếm đa thực thể (multi-type) với tốc độ phản hồi tối ưu.
* **Clean Code Architecture:** Rút gọn logic xử lý API nhờ bộ đôi `makeHandler` và `makeAuthHandler` thế hệ mới.

---

## 🧠 4. Phân tích kỹ thuật (Technical Deep Dive)

### 🔐 Kiến trúc xác thực JWT Claims & RBAC
Việc tích hợp Cognito ở lớp Frontend không chỉ là đăng nhập, mà còn là quản lý phân quyền (Role-Based Access Control):
* **Identity Handshake:** Khi User login thành công, Cognito trả về 3 loại Token: `IdToken` (chứa thông tin User), `AccessToken` (dùng để gọi API), và `RefreshToken`.
* **Claims Validation:** Frontend bóc tách `groups` claim từ JWT để hiển thị giao diện phù hợp (Ví dụ: Chỉ hiện nút "Upload" cho người dùng thuộc group `Artists`).
* **Interceptor Workflow:** 1. Interceptor chặn Request.
    2. Lấy `AccessToken` từ session.
    3. Gắn vào Header.
    4. Nếu API trả về 401 (Unauthorized), tự động kích hoạt luồng Logout hoặc Refresh Token.
    
#### 🔄 Token Rotation & Security
Hệ thống sử dụng cơ chế **Refresh Token Auth Flow**:
- **Refresh:** Khi Access Token hết hạn, hệ thống tự động dùng Refresh Token để lấy cặp Token mới, giúp User không phải đăng nhập lại nhiều lần.
- **Global Logout:** Sử dụng `GlobalSignOut` để vô hiệu hóa (revoke) toàn bộ các Token đã cấp, bảo vệ tài khoản ngay lập tức khi User yêu cầu thoát.

#### 📑 Cursor-based Pagination
Thay vì dùng `offset` (chậm khi data lớn), hệ thống sử dụng `ExclusiveStartKey` của DynamoDB làm **Cursor**:
- **Ưu điểm:** Tốc độ truy vấn không đổi bất kể kích thước bảng dữ liệu.
- **Response:** Trả về `nextCursor` cho Client để thực hiện các yêu cầu tiếp theo, đảm bảo luồng dữ liệu mượt mà.

---
## 💡 5. Xử lý sự cố & Bài học kinh nghiệm (Troubleshooting)

| Vấn đề (Issue) | Nguyên nhân (Root Cause) | Giải pháp (Solution) |
| :--- | :--- | :--- |
| **CORS Preflight Error (403)** | Trình duyệt gửi request `OPTIONS` trước khi gửi `POST/GET` nhưng API Gateway chưa được cấu hình cho phép các Headers tùy chỉnh. | Bổ sung `Authorization` và `Content-Type` vào danh sách `allowHeaders` trong cấu hình CORS của SST API construct. |
| **Amplify "No User Pool" Error** | File cấu hình `aws-exports` hoặc thông số truyền vào `Amplify.configure()` bị sai lệch giữa Web Client và Console. | Kiểm tra lại `ClientId` (đảm bảo không có Secret Key nếu là Web Client) và Region của User Pool. |
| **Token Payload Desync** | Thông tin hiển thị trên giao diện (Username, Email) không cập nhật ngay sau khi Login. | Sử dụng `Hub` listener của Amplify để lắng nghe sự kiện `signIn` và cập nhật Global State kịp thời. |
| **Refresh Token Expiry** | User bị văng ra sau một thời gian dài không hoạt động. | Cấu hình thời gian sống của Refresh Token trong Cognito phù hợp với yêu cầu UX. |
| **Cursor Encoding** | Cursor chứa ký tự đặc biệt gây lỗi khi truyền qua URL. | Thực hiện Base64 Encode/Decode cho Cursor để đảm bảo an toàn khi truyền tải. |
| **Search Performance** | Query trên DynamoDB tốn nhiều tài nguyên khi tập dữ liệu lớn. | Sử dụng GSI (Global Secondary Index) kết hợp với Filter Expression để tối ưu hóa chi phí. |
---