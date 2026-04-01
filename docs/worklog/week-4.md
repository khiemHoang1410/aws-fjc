# AWS Cloud & Full-stack Mastery - Week 4: System Robustness & Admin Orchestration

## 📝 Project Overview
- **Student:** Hoàng Sỹ Khiêm
- **Role:** Cloud Intern / AWS Learner / Team leader
- **Batch:** Bootcamp - First Cloud AI Journey @ AWS Study Group
- **Duration:** 23/03/2026 - 29/03/2026
- **Stack:** AWS Serverless (SST v3, Lambda, DynamoDB, S3, Cognito, API Gateway, CloudFront, VPC), React + Vite 6, TypeScript, Swagger UI.

---

Tuần 4 tập trung vào việc củng cố độ tin cậy của hệ thống (System Robustness) thông qua việc xử lý các lỗi trọng yếu (P0/P1), tối ưu hóa lớp giao tiếp mạng (Networking Layer) và khởi tạo phân hệ quản trị (Admin Dashboard). Trọng tâm là xây dựng một nền tảng ổn định, có khả năng tự phục hồi (Self-healing) và mang lại trải nghiệm người dùng mượt mà thông qua việc kiểm soát chặt chẽ các tác vụ bất đồng bộ và luồng dữ liệu thực thi.

## 1. Mục tiêu đào tạo (Training Objectives)

### Advanced Networking & Resilience
* **Resilient API Client:** Xây dựng Centralized HTTP Client tích hợp cơ chế Retry, Timeout và hàng đợi Refresh Token (Token Refresh Queue) nhằm giải quyết triệt để bài toán Race Condition trong xác thực.
* **Fault Tolerance:** Triển khai Error Boundaries và Route Error Handling (React Router v7) để đảm bảo ứng dụng không bị tình trạng "White Screen" khi xảy ra lỗi cục bộ.
### Admin Systems & Analytics
* **Back-office Infrastructure:** Thiết lập hệ thống Endpoint quản trị để truy xuất thống kê hệ thống (Stats), quản lý báo cáo (Reports) và kiểm soát tài nguyên (Content Moderation).
* **Environment Standardization:** Chuẩn hóa cấu hình TypeScript và ESM Module trên toàn bộ hạ tầng Backend để đảm bảo tính nhất quán khi thực thi các script quản trị và hệ thống Type-checking.
### Core UX & Performance Optimization
* **Audio Engineering Precision:** Xử lý triệt để logic đồng bộ hóa thanh tiến trình (Progress Bar) thông qua cơ chế Blocking Update trong quá trình Seeking để đảm bảo tính mượt mà của trình phát nhạc.
* **Perceived Performance:** Nâng cao cảm nhận tốc độ ứng dụng thông qua kỹ thuật Skeleton Loading và Debouncing (300ms) trong các thao tác truy vấn dữ liệu bất đồng bộ.

---

## 2. Nhật ký công việc chi tiết (Detailed Worklog)

| Day | Task Details | Start Date | Completion Date | Reference Material |
|:---:|:---|:---:|:---:|:---|
| **15** | **System Hardening, Admin Integration & UX Stabilization:** <br><br> **1. Networking & Resilience:** <br> - Phát triển `apiClient.js` tập trung xử lý Typed Errors, Retry và Token Refresh Queue; giải quyết triệt để Race Condition khi Refresh Token đồng thời. <br> - Triển khai Error Boundary toàn cục và Route-level Error Handling cho AppLayout. <br><br> **2. Admin Module & Backend Core:** <br> - Khởi tạo hệ thống Admin Backend: GET /admin/stats, GET /admin/reports, DELETE /admin/songs. <br> - Chuẩn hóa hạ tầng Backend: Cấu hình `type: module` và `tsconfig` hỗ trợ Node types cho các script quản trị. <br><br> **3. Logic P0 & UX Refinement:** <br> - Xử lý lỗi "Double-jump" trên Player Bar bằng `isSeeking` ref; đồng bộ hóa `artistId` trong luồng Upload thực tế. <br> - Nâng cấp trải nghiệm người dùng: Skeleton loading, 300ms debounce cho Search và chuẩn hóa thông báo Toast (5s duration). | 04/01/2026 | 04/01/2026 | [React Error Boundaries] <br> [Axios/Fetch Interceptors] <br> [Audio Web API] |

---

## 3. Phân tích kỹ thuật (Technical Deep Dive)

### Networking: Race Condition & Token Refresh Queue
Trong một hệ thống phân tán, khi Access Token hết hạn, nhiều Request gọi cùng lúc sẽ dẫn đến việc kích hoạt nhiều luồng Refresh Token đồng thời. `apiClient` được thiết kế để giải quyết bài toán này:
* **Queueing Mechanism:** Khi một Request đang thực hiện Refresh Token, tất cả các Request bị lỗi 401 tiếp theo sẽ được đẩy vào một hàng đợi (Queue).
* **Atomic Update:** Ngay khi Token mới được cấp phát thành công, toàn bộ hàng đợi sẽ được giải phóng và thực thi lại (Retry) với Credential mới, đảm bảo phiên làm việc không bị gián đoạn.

### UI Persistence: The "Double-jump" Seeking Fix
Vấn đề phát sinh khi sự kiện `onTimeUpdate` của HTML5 Audio Conflict với thao tác kéo thả của người dùng, khiến UI bị nhảy về vị trí cũ (Snap back).
* **Giải pháp:** Sử dụng `useRef` để quản lý trạng thái `isSeeking`. Khi người dùng tương tác, hệ thống sẽ chặn (Block) mọi cập nhật từ Audio Element trong 300ms, đủ thời gian để Buffer hoàn tất việc nhảy tới vị trí mới mà không gây giật lag giao diện.

### Infrastructure: ESM & TypeScript Standardization
Việc chuyển dịch sang `type: module` trong `package.json` Backend yêu cầu sự thay đổi trong cách xử lý `__dirname` và `path`.
* **Standardization:** Hợp nhất `scripts/` vào luồng Type-checking của `tsconfig`, đảm bảo các công cụ quản trị (như Seed-data) luôn được kiểm soát chặt chẽ về kiểu dữ liệu và tương thích hoàn toàn với môi trường thực thi của Lambda.