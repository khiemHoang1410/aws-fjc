# 🚀 AWS Cloud & Full-stack Mastery - Week 3  Integration & Optimization

## 📝 Project Overview
- **Student:** Hoàng Sỹ Khiêm
- **Role:** Cloud Intern / AWS Learner / Team leader
- **Batch:** Bootcamp - First Cloud AI Journey @ AWS Study Group
- **Duration:** 23/03/2026 - 22/03/2026
- **Stack:** AWS Serverless (SST v3, Lambda, DynamoDB, S3, Cognito, API Gateway, CloudFront, VPC), React + Vite 6, TypeScript, Swagger UI.

---

Tuần 3 đánh dấu giai đoạn **Full-stack Handshake Orchestration**, tập trung thiết lập mối liên kết chặt chẽ giữa hệ sinh thái Backend Serverless và ứng dụng Client-side. Trọng tâm cốt lõi bao gồm việc tối ưu hóa luồng truyền tải nội dung đa phương tiện (Music Streaming), tái cấu trúc hệ thống điều hướng sang cơ chế **URL-driven** (React Router v7) và hoàn thiện quy trình vận hành tự động **CI/CD** chuyên nghiệp, đảm bảo toàn bộ hệ thống đạt trạng thái **Production-Ready**.

---
## 1. Mục tiêu đào tạo (Training Objectives)

### Security & Identity Orchestration
* **Advanced Auth Lifecycle:** Thiết lập quy trình xác thực đa lớp (Cognito, JWT Rotation) và hệ thống Interceptor tự động xử lý Session/Authorization tại Client.
* **Network Hardening:** Triển khai kiến trúc mạng cô lập (VPC Private Subnets) kết hợp VPC Endpoints để tối ưu hóa traffic nội bộ và bảo mật tài nguyên tuyệt đối.
### Modern Frontend Architecture
* **URL-Driven Routing:** Chuyển đổi toàn diện sang React Router v7, thực thi cơ chế điều hướng URL-based giúp tối ưu UX, SEO và khả năng Deep Linking.
* **Modular Component Design:** Tái cấu trúc hệ thống Component theo hướng Atomic, phân tách Layout/Page logic để tăng khả năng tái sử dụng và hiệu suất Render.
### Backend & Data Engineering
* **Scalable Data Retrieval:** Làm chủ kỹ thuật Cursor-based Pagination trên DynamoDB và xây dựng Search Engine đa thực thể hiệu năng cao.
* **Enterprise Data Policy:** Thực thi cơ chế quản lý vòng đời dữ liệu chuyên nghiệp thông qua Soft Delete, Hard Delete (GDPR) và Higher-Order Handlers (makeAuthHandler).
### Infrastructure & DevOps
* **Media Cloud Orchestration:** Hoàn thiện luồng xử lý đa phương tiện (Audio/Image) thông qua S3 Presigned URLs và chính sách Data Retention (RetainOnDelete).
* **Quality Assurance (QA):** Chuẩn hóa quy trình kiểm thử với bộ 30+ Unit Tests (Vitest) và thiết lập Pipeline CI/CD tự động hóa triển khai toàn diện.
* **Full-stack Observability:** Xây dựng hệ thống giám sát tập trung với Structured JSON Logging, tối ưu hóa khả năng truy vết lỗi qua CloudWatch Insights.

## 📅 2. Nhật ký công việc chi tiết (Detailed Worklog)

| Day | Task Details | Start Date | Completion Date | Reference Material |
|:---:|:---|:---:|:---:|:---|
| **11** | **Deep Integration: Frontend Auth & API Security** <br> <br> **Setup & Config** <br> - Cấu hình AWS Amplify SDK v6, khởi tạo Instance kết nối với `UserPoolId` và `ClientId` từ Backend. <br> - Xây dựng `AuthContext` và `useAuth` hook để quản lý trạng thái `user`, `loading`, và `isAuthenticated`. <br> <br> **Logic & Interceptor** <br> - Triển khai luồng Login/Logout/Register đồng bộ với DynamoDB persistence. <br> - Viết **Axios Interceptor** để tự động "inject" JWT vào `Authorization: Bearer <Token>`. <br> - Xử lý logic **Protected Routes** (ngăn chặn User chưa login vào trang `/admin` hoặc `/upload`). <br> **System Hardening & Feature Expansion:** <br> - Triển khai `/auth/refresh` và `/auth/logout` (GlobalSignOut). <br> - Xây dựng Search Engine và Pagination (Cursor-based). <br> - Cấu hình `/media/upload-image` (Presigned URL cho JPEG/PNG/WEBP). <br> - Refactor Handlers hỗ trợ Query Params nâng cao.| 03/24/2026 | 03/24/2026 | [AWS Amplify Auth](https://docs.amplify.aws/lib/auth/getting-started/) <br> [Axios Interceptors](https://axios-http.com/docs/interceptors) |
| **12** | **Enterprise Infrastructure Hardening & Backend Excellence:** <br><br> **1. Infrastructure & Networking:** <br> - Thiết kế kiến trúc VPC `10.0.0.0/16` (DNS Hostnames), cô lập Lambda vào Private Subnet nhằm triệt tiêu bề mặt tấn công. <br> - Triển khai NAT Gateway cho luồng Outbound an toàn và hệ thống VPC Endpoints (S3, DynamoDB Gateway & Cognito Interface) để tối ưu hóa traffic trên mạng xương sống của AWS. <br><br> **2. Quality Assurance & Logic:** <br> - Xây dựng bộ 30+ Unit Tests chuyên sâu với **Vitest**, đạt độ bao phủ cao cho các Service cốt lõi: `SongService`, `ArtistService`, `SearchService`. <br> - Triển khai lớp Input Validation toàn diện (Zod-like utility) và cơ chế quản lý dữ liệu đa tầng: Soft Delete (bảo toàn dữ liệu) và Hard Delete (tuân thủ GDPR). <br><br> **3. Observability & Operations:** <br> - Chuẩn hóa hệ thống Structured JSON Logging, cho phép thực hiện các truy vấn SQL-like phức tạp thông qua CloudWatch Logs Insights để giám sát hệ thống thời gian thực. | 03/25/2026 | 03/25/2026 | [AWS VPC Networking](https://docs.aws.amazon.com/vpc/) <br> [Vitest Guide](https://vitest.dev/) |
| **13** | **System Archetype Reconstruction & Logic Decoupling:** <br><br> **1. Frontend Modularization:** <br> - Thực thi tái cấu trúc toàn diện hệ sinh thái `src/` theo triết lý **Modular Design**; phân tách rạch ròi các lớp: `layout/`, `cards/`, `search/`, `ui/` và `services/api/`. <br> - Tiến hành **Migration** hàng loạt hệ thống Import Path trên toàn bộ dự án, đảm bảo tính nhất quán (Strict Path Consistency) sau khi tái định vị tài nguyên. <br><br> **2. Backend Orchestration:** <br> - Hợp nhất Runtime Configuration vào kiến trúc **Single Source of Truth (SSOT)** tại `src/config/index.ts`. <br> - Trích xuất hoàn toàn Hardcoded Routes từ hạ tầng (SST) sang các **Dedicated Route Files** chuyên biệt. <br> - Áp dụng cơ chế **Route Registration** tự động thông qua `Object.entries()` để tối ưu hóa quy trình mở rộng Endpoint. | 03/26/2026 | 03/26/2026 | [Refactoring Best Practices] <br> [Modular Architecture] |
| **14** | **Full-stack Handshake & DevOps Pipeline Deployment:** <br><br> **1. Data Mapping & Integration:** <br> - Thiết lập tầng **Adapter Layer** trung gian để Mapping dữ liệu phức tạp giữa Backend API và Frontend Services, triệt tiêu sự phụ thuộc cứng (Hard-coupling). <br> - Khởi tạo luồng **Asynchronous Handshake** kết nối logic thực tế, thay thế hoàn toàn MockData bằng dữ liệu thời gian thực từ DynamoDB. <br><br> **2. DevOps & Enterprise Patterns:** <br> - Cấu hình và chuẩn hóa quy trình **CI/CD Automated Deployment**; tích hợp cơ chế kiểm thử tự động trước khi triển khai. <br> - Nhúng các **Enterprise Design Patterns** (Soft Delete, Result Wrapper) vào Base Repository để xử lý lỗi và quản lý vòng đời dữ liệu chuyên sâu. <br> - Thực hiện **Patching & Debugging** triệt để cho module Authentication, đảm bảo luồng Login/Register vận hành ổn định. | 03/27/2026 | 03/27/2026 | [SST CI/CD Guide] <br> [Adapter Pattern] <br> [Enterprise Patterns] |
| **15** | **Architectural Migration to React Router v7 & UI Decoupling:** <br><br> **1. Routing & Navigation Overhaul:** <br> - Thực thi Migration toàn bộ logic điều hướng từ Redux `uiSlice` sang cơ chế **Declarative Routing** sử dụng React Router v7. <br> - Áp dụng **Centralized Route Definitions** tại `src/routes/index.jsx`, thiết lập ánh xạ (Mapping) từ 16+ trạng thái View cũ sang các URL Path tương ứng (Home, Search, Artist, Album, Admin, v.v.). <br> - Triển khai Higher-order Component `ProtectedRoute` để thực thi chính sách bảo mật và phân quyền truy cập dựa trên Cognito Roles. <br><br> **2. Layout Refactoring & State Purging:** <br> - Loại bỏ hoàn toàn `MainContent.jsx`, phân tách logic vào hệ thống **Atomic Pages** và `AppLayout` shell. <br> - Tiến hành **Redux Store Cleanup**, giải phóng 8+ redundant states (currentView, activePlaylistId...) giúp giảm bộ nhớ và tránh Side-effects không mong muốn. <br> - Refactor toàn bộ các UI Components (Sidebar, PlayerBar, Navbar) chuyển từ `dispatch(setView)` sang cơ chế điều hướng chuẩn `Maps()`. | 03/28/2026 | 03/28/2026 | [React Router v7 Docs] <br> [Clean Architecture] |
| **16** | **Data Integrity & End-to-End Integration Stabilization:** <br><br> **1. Infrastructure Resilience Policy:** <br> - Thiết lập cơ chế **Pin Resource Names** và kích hoạt `retainOnDelete` cho DynamoDB và S3 Bucket nhằm bảo vệ dữ liệu vĩnh viễn (Data Persistence) khi thực hiện lệnh `sst remove`. <br> - Kích hoạt `deletionProtectionEnabled` cho môi trường Production, ngăn chặn các thao tác xóa hạ tầng ngoài ý muốn. <br><br> **2. Integration & Functional Fixes:** <br> - Loại bỏ 100% Mock Data tại toàn bộ hệ thống Services (Song, Artist, Album, Admin), chuyển dịch sang giao tiếp hoàn toàn với API Backend. <br> - Đồng bộ hóa luồng **Upload Orchestration**; xử lý đồng thời Audio và Cover Image qua Presigned URL Flow với cơ chế Validate Duration chính xác. <br> - Nâng cấp `ArtistRepository` với cơ chế tìm kiếm qua **Global Secondary Index (GSI)** và xử lý lỗi tương thích ESM (`__dirname`) cho Seed-data script. | 03/29/2026 | 03/29/2026 | [AWS Data Persistence] <br> [S3 Presigned URLs] <br> [DynamoDB GSI] |

---

## 🏆 3. Kết quả đạt được (Key Achievements)

### Security & Identity Management Excellence
* **Full-stack Auth Orchestration:** Hoàn thiện luồng xác thực khép kín từ Login, Refresh đến Global Logout. Hệ thống tự động đính kèm Security Headers và duy trì trạng thái đăng nhập (Persistence) đồng bộ giữa Cognito và Local State.
* **Unified Security Framework:** Triển khai thành công bộ đôi `makeHandler` và `makeAuthHandler` thế hệ mới, giúp chuẩn hóa logic bảo mật và rút gọn 40% mã nguồn xử lý API.
### High-Performance API & Backend Engineering
* **Scalable Data Retrieval:** 100% các list endpoints (`/songs`, `/artists`, `/albums`) đã hỗ trợ **Cursor-based Pagination**, đảm bảo hiệu năng truy vấn ổn định bất kể quy mô dữ liệu và giảm tải tối đa cho DynamoDB.
* **Smart Content Discovery:** Tích hợp thành công Multi-type Search Engine với tốc độ phản hồi tối ưu, đi kèm cơ chế đăng ký Route tự động qua `Object.entries()` giúp hệ thống cực kỳ linh hoạt khi mở rộng.
### Modern Frontend & UX Evolution
* **URL-Driven Architecture:** Chuyển đổi toàn diện sang React Router v7, hỗ trợ Deep Linking và tối ưu UX thông qua cơ chế điều hướng URL-based thay thế hoàn toàn cho Redux view-state cũ.
* **Modular Codebase & State Optimization:** Tái cấu trúc `src/` theo hướng Atomic Design, tinh gọn Redux Store và chuẩn hóa hệ thống Page-based, sẵn sàng cho việc triển khai Lazy Loading và Code Splitting.
### Production Readiness & Resilience
* **Zero Data Loss Infrastructure:** Thiết lập chính sách bảo mật dữ liệu nghiêm ngặt (`retainOnDelete`, Deletion Protection), đảm bảo an toàn tuyệt đối cho tài nguyên S3 và DynamoDB ngay cả khi thay đổi hạ tầng.
* **E2E Stability & Documentation:** Hoàn thiện luồng dữ liệu thực 100% (Upload, Admin Approval) đi kèm hệ thống tài liệu Swagger UI và bộ cấu hình môi trường (.env) chuẩn hóa cho Production.
---

## 🧠 4. Phân tích kỹ thuật (Technical Deep Dive)

### 🔐 1. Identity & Access Orchestration (Cognito + RBAC)
Hệ thống chuyển dịch từ cơ chế xác thực cơ bản sang mô hình quản lý định danh chuyên sâu:
* **Identity Handshake:** Khi xác thực thành công, Cognito cấp phát bộ 3 Token (Id, Access, Refresh). Frontend thực hiện bóc tách `groups` claim từ JWT để thực thi phân quyền (RBAC) ngay tại lớp giao diện.
* **Security Interceptor Workflow:** Triển khai Middleware tự động đánh chặn Request để gắn `Authorization` header. Hệ thống có khả năng tự phục hồi phiên đăng nhập thông qua cơ chế **Token Rotation (Refresh Flow)** và thu hồi quyền truy cập tức thì bằng **GlobalSignOut**.

### 🌐 2. Secure Hybrid Networking (VPC Hardening)
Kiến trúc mạng được thiết kế theo tiêu chuẩn "Defense in Depth" (Phòng thủ chiều sâu):
* **Network Isolation:** Toàn bộ logic xử lý (Lambda) được cô lập trong Private Subnet, giao tiếp với Internet qua NAT Gateway để ẩn danh hạ tầng.
* **Backbone Traffic Optimization:** Sử dụng **VPC Endpoints** (S3/DynamoDB Gateway & Cognito Interface) để giữ dữ liệu nhạy cảm lưu thông hoàn toàn trong mạng nội bộ AWS, giúp tối ưu chi phí và triệt tiêu độ trễ Internet.

### ⚡ 3. High-Performance Data Engineering
Tối ưu hóa khả năng truy xuất dữ liệu lớn trên nền tảng NoSQL:
* **Cursor-based Pagination:** Thay thế cơ chế `offset` truyền thống bằng `ExclusiveStartKey` của DynamoDB. Kỹ thuật này đảm bảo tốc độ phản hồi `O(1)` bất kể quy mô bản ghi (Dataset size), cung cấp luồng dữ liệu mượt mà cho trải nghiệm người dùng.
* **Resilient Data Policy:** Thực thi chính sách `retainOnDelete: true`. Đây là lớp bảo hiểm quan trọng trong Cloud, đảm bảo dữ liệu trong S3 và DynamoDB luôn tồn tại vĩnh viễn (Data Persistence) kể cả khi hạ tầng compute bị gỡ bỏ.

### 🏗️ 4. Scalable Software Design Patterns
Áp dụng các chuẩn mực thiết kế phần mềm hiện đại để tăng khả năng bảo trì:
* **URL-driven Architecture:** Chuyển đổi từ Redux-state sang **React Router v7**. Việc đồng bộ trạng thái ứng dụng với URL giúp hỗ trợ Deep Linking, tối ưu SEO và tận dụng tối đa cơ chế Native Navigation của trình duyệt.
* **Adapter & Router Decoupling:** - **Adapter Layer:** Đóng vai trò "người phiên dịch", chuẩn hóa dữ liệu từ API thô sang cấu trúc Object phù hợp cho UI, triệt tiêu sự phụ thuộc cứng (Hard-coupling) giữa FE và BE.
    - **Router Extraction:** Tách biệt định tuyến khỏi cấu hình hạ tầng, cho phép nhà phát triển mở rộng API theo hướng Modular hóa.

### 🧪 5. Quality Assurance & Observability
* **Automated Testing (Vitest):** Duy trì bộ 30+ Unit Tests cho các Service cốt lõi, đảm bảo tính đúng đắn của logic nghiệp vụ trước khi triển khai (Production Readiness).
* **Structured JSON Logging:** Chuẩn hóa Log đầu ra dưới dạng JSON. Điều này biến CloudWatch từ một kho chứa text vô tri thành một công cụ phân tích mạnh mẽ, hỗ trợ truy vấn SQL-like qua Logs Insights để xử lý sự cố trong vài giây.

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
| **addAuthorizer Name Fix** | Thuộc tính `name` trong `addAuthorizer` bị deprecated ở phiên bản mới. | Chuyển đổi sang tham số vị trí (positional argument) theo đúng chuẩn API Gateway V2. |
| **VPC Lambda Latency** | Lambda trong VPC gặp tình trạng Cold Start lâu do khởi tạo ENI. | Sử dụng cấu hình SST build-time và tối ưu hóa Security Groups để giảm overhead. |
| **Input Validation Overload** | Việc validate thủ công tại mỗi handler gây lặp code và dễ sai sót. | Xây dựng `validate.ts` utility trung tâm để chuẩn hóa việc kiểm tra dữ liệu đầu vào. |
| **SST Data Loss** | Mặc định SST sẽ xóa Bucket/Table khi gỡ bỏ Stack. | Cấu hình `retainOnDelete` và `fixed name` cho các Resource lưu trữ dữ liệu. |
| **ESM Directory Error** | Biến `__dirname` không khả dụng trong môi trường ES Modules của Node.js. | Sử dụng giải pháp thay thế qua `fileURLToPath` và `path.dirname` để xác định đường dẫn seed-data. |
| **Artist-User Mapping** | Không thể truy vấn nhanh Artist dựa trên UserId của Cognito. | Bổ sung **Global Secondary Index (GSI)** trên bảng Artist với Partition Key là `userId`. |
| **Import Path Hell** | Việc di chuyển thư mục khiến hàng loạt đường dẫn `import` bị hỏng. | Sử dụng công cụ Refactor của VS Code kết hợp với `tsconfig` paths để chuẩn hóa. |
| **Merge Conflicts** | Xung đột khi tích hợp cơ chế Soft Delete vào Repository cũ. | Sử dụng **Result Wrapper** để thống nhất kiểu dữ liệu trả về, giải quyết xung đột logic. |
---

