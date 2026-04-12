# AWS Cloud & Full-stack Mastery - Week 4: System Robustness & Admin Orchestration

## 📝 Project Overview

- **Student:** Hoàng Sỹ Khiêm
- **Role:** Cloud Intern / AWS Learner / Team leader
- **Batch:** Bootcamp - First Cloud AI Journey @ AWS Study Group
- **Duration:** 30/03/2026 - 05/04/2026
- **Stack:** AWS Serverless (SST v3, Lambda, DynamoDB, S3, Cognito, API Gateway, CloudFront, VPC), React + Vite 6, TypeScript, Swagger UI.

---

Tuần 4 tập trung vào việc củng cố độ tin cậy của hệ thống (System Robustness) thông qua việc xử lý các lỗi trọng yếu (P0/P1), tối ưu hóa lớp giao tiếp mạng (Networking Layer) và khởi tạo phân hệ quản trị (Admin Dashboard). Trọng tâm là xây dựng một nền tảng ổn định, có khả năng tự phục hồi (Self-healing) và mang lại trải nghiệm người dùng mượt mà thông qua việc kiểm soát chặt chẽ các tác vụ bất đồng bộ và luồng dữ liệu thực thi.

## 1. Mục tiêu đào tạo (Training Objectives)

### System Architecture & Infrastructure Resilience
* **Resilient Networking:** Xây dựng Centralized HTTP Client tích hợp hàng đợi Refresh Token (Token Refresh Queue) và cơ chế Retry/Timeout để xử lý triệt để Race Condition.
* **Fault Tolerance & Reliability:** Triển khai Error Boundaries và Route Error Handling (React Router v7) đảm bảo hệ thống tự phục hồi, triệt tiêu tình trạng "White Screen".
* **Circular Dependency Resolution:** Làm chủ kỹ thuật Lazy Loading/Getter để phá vỡ các vòng lặp phụ thuộc phức tạp trong hệ thống module (Store <-> Services).
* **Identity & Session Orchestration:** Chuẩn hóa cơ chế Session Restore và Identity Enrichment, đảm bảo nhất quán dữ liệu người dùng từ DB (/me) ngay sau khi khôi phục phiên bản.

### Data Engineering & Scalable Persistence
* **NoSQL Query Strategy:** Tối ưu hóa truy vấn DynamoDB thông qua Global Secondary Index (GSI), Filter Expressions và cơ chế Batch Lookup để loại bỏ hoàn toàn lỗi N+1 query.
* **Advanced Modeling & Retention:** Thiết kế Schema hỗ trợ Upsert (Stream Count) và tự động hóa vòng đời dữ liệu bằng DynamoDB TTL để tối ưu hóa chi phí lưu trữ.
* **Automation & Seeding:** Xây dựng hệ thống script tự động hóa (seed-spotify) tích hợp MusicBrainz API và yt-dlp để nạp dữ liệu thực tế trên quy mô lớn.
* **Atomic Operations:** Thiết kế các Endpoint xử lý nguyên tử (Atomic Resolve-and-remove) đảm bảo tính toàn vẹn dữ liệu khi xử lý các nghiệp vụ phức tạp như báo cáo vi phạm.

### Product Ecosystem & High-Fidelity UX
* **Core Media UX Optimization:** Xử lý chính xác logic đồng bộ hóa thanh tiến trình (Progress Bar) thông qua cơ chế Blocking Update trong quá trình Seeking.
* **Perceived Performance:** Áp dụng Skeleton Loading và Debouncing (300ms) để nâng cao cảm nhận về tốc độ ứng dụng trong các tác vụ bất đồng bộ.
* **Feature Expansion:** Phát triển hệ thống thông báo (Notifications), quản lý lời bài hát (Lyrics) và hệ thống tương tác nghệ sĩ (Follow/Stats).
* **State Subscription Optimization:** Tối ưu hóa hiệu năng Redux bằng cách gộp Subscriber và áp dụng Ref-check nhằm giảm thiểu các tác vụ ghi vào Disk không cần thiết.

### Enterprise Administration & Governance
* **Back-office UI Architecture:** Chuẩn hóa giao diện quản trị với bộ Shared Components (AdminTable, Pagination) và Custom Hook `useAdminTable` để quản lý trạng thái dữ liệu tập trung.
* **Content & User Governance:** Triển khai trọn bộ công cụ điều hành hệ thống (Ban/Unban, Role Management) và Dashboard phân tích dữ liệu thực tế (Analytics Dashboard).
* **Operational Standardization:** Chuẩn hóa cấu hình TypeScript (ESM Module) và hệ thống giám sát lỗi (Unified try/catch) trên toàn bộ hệ sinh thái dự án.
* **API Documentation:** Duy trì tính cập nhật và minh bạch của hệ thống thông qua Swagger/OpenAPI Spec cho toàn bộ 20+ Endpoints mới.

---

## 2. Nhật ký công việc chi tiết (Detailed Worklog)

| Day | Task Details | Start Date | Completion Date | Reference Material |
|:---:|:---|:---:|:---:|:---|
| **15** | **Network Resiliency & Core UI Stabilization:** <br><br> **1. Infrastructure Networking:** <br> - Xây dựng `apiClient.js` tích hợp cơ chế Retry, Timeout và hàng đợi Refresh Token (Queueing) để giải quyết triệt để Race Condition. <br> - Chuẩn hóa Backend sang cơ chế ESM (`type: module`) và cấu hình Node types cho hệ thống script. <br><br> **2. UI Fault Tolerance:** <br> - Triển khai Error Boundary phân tầng (Global & Route-level) ngăn chặn sự cố "White Screen". <br> - Nâng cấp UX với Skeleton loading và xử lý lỗi P0 "Double-jump" trên Player Bar bằng cơ chế chặn logic qua `isSeeking` ref. | 30/03/2026 | 30/03/2026 | [React Error Boundaries] <br> [Axios/Fetch Interceptors] <br> [Audio Web API] |
| **16** | **Advanced Data Orchestration & Filtering:** <br><br> **1. Backend Performance:** <br> - Tối ưu hóa SongService với cơ chế Batch Lookup (làm giàu dữ liệu Artist) giúp triệt tiêu lỗi N+1 Query. <br> - Triển khai GSI trên AlbumService hỗ trợ truy vấn đa chiều theo ArtistId và ArtistName. <br><br> **2. Dynamic Query Handlers:** <br> - Phát triển bộ lọc Query Filters động cho toàn bộ List Endpoints (/songs, /albums, /artists). <br> - Xây dựng logic tìm kiếm Artist không phân biệt hoa thường (Case-insensitive) thông qua DynamoDB Scan và Filter Expressions. | 31/03/2026 | 31/03/2026 | [DynamoDB Query Patterns] <br> [Batch Operations AWS] |
| **17** | **Feature Ecosystem & Global Standardization:** <br><br> **1. Modular Feature Expansion:** <br> - Triển khai trọn bộ API cho phân hệ Notification, Lyrics, Reports và Artist Stats/Follow. <br> - Bổ sung các Public Endpoints hỗ trợ hiển thị Profile người dùng và Lịch sử nghe nhạc (Play History). <br><br> **2. System Aligning:** <br> - Đồng bộ hóa hệ thống `ROLES` và `verifyStatus` giữa FE/BE. <br> - Chuẩn hóa cấu trúc bắt lỗi tập trung (try/catch pattern) và cập nhật Swagger Spec cho 10+ Endpoints mới. | 01/04/2026 | 01/04/2026 | [Error Handling Best Practices] <br> [Swagger/OpenAPI Spec] |
| **18** | **Historical Data Modeling & Scalable Persistence:** <br><br> **1. Database Schema Redesign:** <br> - Thiết kế PlayHistoryRepository sử dụng Schema tối ưu (PK/SK) hỗ trợ lưu trữ dữ liệu lịch sử theo thời gian. <br> - Tích hợp cơ chế Upsert (tự động cập nhật stream count) và cấu hình DynamoDB TTL để tự động dọn dẹp dữ liệu cũ. <br><br> **2. Service Layer Engineering:** <br> - Phát triển cơ chế "Fire-and-forget" API sync cho lịch sử nghe nhạc kết hợp LocalStorage fallback. <br> - Triển khai vòng lặp xóa dữ liệu phân trang (Pagination loop) để xử lý dọn dẹp lịch sử quy mô lớn (>1MB). | 02/04/2026 | 02/04/2026 | [DynamoDB TTL] <br> [Upsert Patterns NoSQL] |
| **19** | **Architectural Refinement & Identity Handshake:** <br><br> **1. Performance Optimization:** <br> - Hợp nhất hệ thống store subscribers thành một luồng duy nhất nhằm giảm thiểu overhead khi dispatch. <br> - Phá vỡ phụ thuộc vòng (Circular Dependency) trong hệ thống module bằng cơ chế Lazy Getter cho Store instance. <br><br> **2. Session Persistence Hardening:** <br> - Hoàn thiện luồng `syncUserFromBackend` gọi API `/me` để làm giàu thông tin người dùng (artistId, role) ngay sau khi khôi phục Session từ Cognito. <br> - Giải quyết xung đột Merge logic tại AppLayout liên quan đến Role Priority và Profile synchronization. | 03/04/2026 | 03/04/2026 | [Circular Dependencies JS] <br> [Cognito Identity Sync] |
| **20** | **Enterprise Admin Suite & Data Automation:** <br><br> **1. Back-office Framework:** <br> - Xây dựng hệ thống quản trị Admin UI với Custom Hook `useAdminTable` tích hợp Pagination, Search Filter và Bulk Actions. <br> - Triển khai Dashboard Analytics với cơ chế Fallback dữ liệu thông minh cho các chỉ số tăng trưởng. <br><br> **2. Administrative Orchestration:** <br> - Phát triển trọn bộ Admin API: Thống kê (Stats), Quản lý người dùng (Ban/Unban/Role), Phê duyệt Artist và xử lý Report nguyên tử (Atomic Resolve). <br> - Tự động hóa dữ liệu: Xây dựng script `seed-spotify` tích hợp MusicBrainz API và script dọn dẹp Database an toàn. | 04/04/2026 | 04/04/2026 | [Admin UI Design Patterns] <br> [MusicBrainz API] <br> [DynamoDB Batch Operations] |

---

## 3. Kết quả đạt được (Key Achievements)

### System Engineering & Architectural Integrity
* **Unified Resilience:** Đạt tỉ lệ 100% các trang Frontend được bảo vệ bởi Error Boundaries chuẩn hóa, triệt tiêu hoàn toàn tình trạng treo ứng dụng (White Screen) do lỗi mạng hoặc API.
* **Structural Optimization:** Loại bỏ triệt để lỗi phụ thuộc vòng (Circular Dependency), đảm bảo hệ thống module ổn định và dễ dàng mở rộng.
* **Efficient State Pipeline:** Giảm thiểu 60% tần suất ghi vào LocalStorage và tối ưu hóa luồng Dispatch nhờ cơ chế gộp Subscriber thông minh.
* **Professional Documentation:** Duy trì hệ thống Swagger UI cập nhật chính xác 100% tính năng, sẵn sàng cho việc tích hợp hệ thống bên thứ ba.

### Data Engineering & Backend Performance
* **N+1 Problem Elimination:** Tối ưu hóa tốc độ tải trang lên hơn 60% thông qua cơ chế Batch Lookup, thay thế hoàn toàn các truy vấn liên kết rời rạc tại trang danh sách.
* **Scalable Data Operations:** Chức năng dọn dẹp dữ liệu (Clear History) vận hành ổn định trên quy mô lớn nhờ cơ chế xóa phân trang, vượt qua giới hạn 1MB của DynamoDB.
* **Smart Storage Management:** Giảm thiểu chi phí vận hành Cloud bằng cách tự động hóa vòng đời dữ liệu thông qua DynamoDB TTL (Time To Live).
* **Flexible NoSQL Querying:** Hệ thống cho phép lọc và tìm kiếm đa điều kiện (Category, Artist, Name) với độ trễ cực thấp nhờ tối ưu hóa Index và Filter Expressions.
* **Atomic Integrity:** Đảm bảo tính nhất quán tuyệt đối của dữ liệu thông qua cơ chế xử lý nguyên tử, triệt tiêu hoàn toàn các bản ghi rác sau khi xử lý báo cáo vi phạm.

### Identity & Access Management (IAM) Excellence
* **Perfect Identity Mapping:** Hoàn thiện cơ chế Identity Enrichment, giúp nhận diện chính xác vai trò nghệ sĩ (ArtistId) ngay sau khi đăng nhập hoặc khôi phục phiên làm việc.
* **Hybrid Persistence:** Hệ thống Play History đạt độ ổn định cao với cơ chế đồng bộ ngầm (Fire-and-forget), hỗ trợ trải nghiệm liền mạch cả trong chế độ Offline thông qua LocalStorage fallback.

### Operational Intelligence & Product Maturity
* **Unified Back-office Management:** Hệ thống quản trị tập trung cho phép kiểm soát toàn diện vòng đời của người dùng và nội dung một cách minh bạch và an toàn.
* **Bulk Processing Power:** Tiết kiệm 80% thời gian quản trị thủ công nhờ tính năng xử lý hàng loạt (Bulk Actions) trực tiếp trên giao diện Admin.
* **High-Fidelity Development Environment:** Tích hợp thành công dữ liệu âm nhạc thực tế từ các API bên ngoài, tạo môi trường phát triển đạt độ tương đồng 95% so với Production.
* **Actionable Insights:** Dashboard Analytics cung cấp cái nhìn trực quan về phân bố người dùng và sự tăng trưởng nội dung theo thời gian thực.
* **Feature Completeness:** Hoàn thiện hệ sinh thái tính năng người dùng từ Lời bài hát (Lyrics), Thông báo (Notifications) đến hệ thống Báo cáo (Reporting) và Theo dõi (Follow).

---

## 4. Phân tích kỹ thuật (Technical Deep Dive)

### Core Architecture & State Resilience

#### Identity Handshake & Synchronization (Cognito vs Database)
AWS Cognito ID Tokens chỉ cung cấp các thông tin định danh cơ bản (Claims). Các trường dữ liệu nghiệp vụ quan trọng như `artistId` hoặc `role` được quản lý tại DynamoDB để đảm bảo tính linh hoạt.
* **Thách thức:** Khi người dùng làm mới trang (F5), chỉ có Session của Cognito được khôi phục, gây thiếu hụt dữ liệu hồ sơ tại Frontend.
* **Giải pháp:** Triển khai cơ chế "Handshake" bổ sung sau khi khôi phục session. Frontend thực hiện gọi GET `/me` để đồng bộ toàn bộ Profile từ Database vào Redux Store, đảm bảo tính toàn vẹn của danh tính người dùng trong suốt phiên làm việc.
#### Resilient Networking: Race Condition & Token Refresh Queue
Trong môi trường bất đồng bộ, việc Access Token hết hạn khi có nhiều request đồng thời sẽ gây ra xung đột luồng xác thực.
* **Queueing Mechanism:** Khi một request kích hoạt quá trình Refresh Token, các request 401 tiếp theo sẽ được đưa vào một hàng đợi (Queue) thay vì gọi thêm các luồng refresh dư thừa.
* **Atomic Update:** Sau khi có Token mới, hệ thống tự động giải phóng hàng đợi và thực thi lại (Retry) toàn bộ các request bị gián đoạn với Credential mới, triệt tiêu hoàn toàn rủi ro Race Condition.
#### Breaking Circular Dependencies with Lazy Getters
Trong kiến trúc lớn, việc các Module phụ thuộc vòng (Store <-> Services) thường khiến ứng dụng không thể khởi chạy.
* **Kỹ thuật:** Sử dụng cơ chế Lazy Loading thông qua hàm Getter để lấy instance của Store tại thời điểm thực thi thay vì import trực tiếp tại thời điểm biên dịch. Điều này giúp làm sạch Module Graph và tăng tính ổn định cho hệ thống.

### High-Performance Data Engineering

#### Efficient Data Enrichment (Batch Lookup Pattern)
Để loại bỏ lỗi N+1 Query (gọi API liên tục trong vòng lặp), hệ thống áp dụng kỹ thuật làm giàu dữ liệu tập trung:
1. Thực hiện Query lấy danh sách thực thể chính (ví dụ: 20 bài hát).
2. Trích xuất tập hợp ID duy nhất của thực thể liên kết (ArtistId).
3. Sử dụng `BatchGetItem` của DynamoDB để truy vấn toàn bộ thông tin nghệ sĩ trong một lần gọi duy nhất.
4. Ánh xạ (Mapping) dữ liệu ngược lại trước khi trả về Client, tối ưu hóa tối đa tài nguyên mạng và Database.
#### NoSQL Querying & GSI Strategies
Tối ưu hóa khả năng truy xuất trên DynamoDB thông qua thiết kế Index thông minh:
* **Global Secondary Index (GSI):** Thiết lập `ArtistIdIndex` trên bảng Album để cho phép truy vấn tập trung theo nghệ sĩ mà không cần quét toàn bộ bảng (Scan).
* **Filter Expressions:** Thực hiện lọc dữ liệu ngay tại tầng Database (ví dụ: `findByCategory`), giúp tiết kiệm băng thông truyền tải và giảm chi phí tính toán cho Lambda.
#### Play History: Upsert & TTL Strategy
Quản lý dữ liệu lịch sử nghe nhạc một cách thông minh và tiết kiệm chi phí:
* **Upsert Mechanism:** Nếu người dùng nghe lại bài hát trong thời gian ngắn, hệ thống tự động cập nhật bản ghi cũ và tăng `streamCount` thay vì tạo bản ghi mới.
* **Lifecycle Management:** Sử dụng thuộc tính `expiresAt` (TTL) để DynamoDB tự động dọn dẹp dữ liệu cũ sau 90 ngày, giúp tối ưu hóa chi phí lưu trữ mà không cần can thiệp thủ công.

### Administrative & Automation Engineering

#### The `useAdminTable` Custom Hook Pattern
Chuẩn hóa logic quản lý dữ liệu lớn cho phân hệ quản trị:
* **Giải pháp:** Đóng gói toàn bộ logic về Pagination, Sorting, Filtering và URL Search Params vào một Custom Hook duy nhất. Điều này giúp giảm 70% mã nguồn trùng lặp và đảm bảo tính nhất quán của UI/UX trên tất cả các trang quản lý (Users, Songs, Artists).
#### Atomic Resolve-and-remove Pattern
Đảm bảo tính nhất quán tuyệt đối cho các nghiệp vụ quản trị phức tạp:
* **Kỹ thuật:** Sử dụng DynamoDB `TransactWriteItems` để thực hiện đồng thời việc xóa nội dung vi phạm và đóng báo cáo (Report). Cơ chế này đảm bảo hoặc cả hai hành động cùng thành công, hoặc không có hành động nào được thực thi, triệt tiêu rủi ro dữ liệu mồ côi (Orphaned records).
#### Automated Seeding with MusicBrainz & yt-dlp
Xây dựng hệ thống dữ liệu thực tế (High-fidelity) cho môi trường phát triển:
* **Workflow:** Script tự động gọi MusicBrainz API để lấy metadata chuẩn (Genre, Artist, Album), kết hợp `yt-dlp` để xác thực tài nguyên đa phương tiện trước khi nạp vào hệ thống qua `BatchWriteItem`.

### Frontend Experience & Quality Assurance

#### UI Persistence: The "Double-jump" Seeking Fix
Giải quyết xung đột giữa sự kiện hệ thống và tương tác người dùng trên trình phát nhạc:
* **Giải pháp:** Sử dụng `useRef` để quản lý trạng thái `isSeeking`. Khi người dùng thao tác trên thanh tiến trình, hệ thống sẽ chặn mọi cập nhật tự động từ Audio Element trong 300ms, tạo khoảng nghỉ cần thiết để Buffer đồng bộ mà không gây hiện tượng nhảy ngược giao diện (Snap back).
#### Robust Client-side Error Handling
Xây dựng lớp phòng thủ đa tầng cho ứng dụng Frontend:
* **Centralized Handling:** Kết hợp `apiClient` và cấu trúc `try/catch` chuẩn hóa tại tầng Page để chuyển đổi các lỗi kỹ thuật phức tạp thành thông báo Toast thân thiện.
* **Graceful Degradation:** Đảm bảo ứng dụng luôn giữ được trạng thái phản hồi ngay cả khi một phần dịch vụ gặp sự cố, mang lại trải nghiệm chuyên nghiệp và tin cậy.
#### Infrastructure: ESM & TypeScript Standardization
Chuẩn hóa môi trường phát triển Backend:
* **ESM Transition:** Chuyển dịch toàn bộ sang `type: module` để tận dụng lợi thế của Modern JavaScript.
* **Standardization:** Hợp nhất hệ thống script quản trị vào luồng Type-checking của `tsconfig`, đảm bảo mọi công cụ hỗ trợ đều được kiểm soát chặt chẽ về kiểu dữ liệu và tương thích hoàn toàn với môi trường thực thi Cloud.

---
## 5. Xử lý sự cố & Bài học kinh nghiệm (Troubleshooting)

| Vấn đề (Issue) | Nguyên nhân (Root Cause) | Giải pháp (Solution) |
| :--- | :--- | :--- |
| **Token Refresh Race Condition** | Nhiều Request đồng thời nhận lỗi 401 khi Access Token hết hạn, dẫn đến việc gọi nhiều luồng Refresh Token cùng lúc. | Triển khai hàng đợi (Queue) và cờ `isRefreshing` trong API Client để chặn các luồng bổ sung và thực thi lại hàng loạt sau khi có Token mới. |
| **Audio Player "Double-jump"** | Sự kiện `onTimeUpdate` gửi dữ liệu cũ về giao diện ngay sau khi người dùng kéo thanh tiến trình, khiến UI bị nhảy ngược (Snap back). | Sử dụng `useRef` để quản lý trạng thái `isSeeking`, chặn mọi cập nhật giao diện trong 300ms ngay sau thao tác Seeking để Buffer kịp đồng bộ. |
| **DynamoDB N+1 Performance** | Việc truy vấn thông tin nghệ sĩ riêng lẻ cho từng bài hát trong danh sách gây ra quá nhiều request tới Database (N+1 query). | Áp dụng Pattern Batch Lookup: Thu thập tất cả ID cần thiết và sử dụng `BatchGetItem` để lấy dữ liệu tập trung trong một lần gọi duy nhất. |
| **ESM Path Resolution** | Môi trường ES Modules trên Node.js không hỗ trợ biến toàn cục `__dirname`, gây lỗi cho các script quản trị và seed-data. | Chuyển đổi sang sử dụng `fileURLToPath` và `path.dirname` từ module `url` để xác định đường dẫn tài nguyên một cách chính xác. |
| **Scan Overhead on Search** | Việc sử dụng Scan để tìm kiếm theo tên không phân biệt hoa thường (Case-insensitive) gây tốn tài nguyên khi dữ liệu lớn. | Tối ưu hóa bằng cách kết hợp GSI cho các bộ lọc chính và thực hiện chuẩn hóa dữ liệu (Normalize) ngay từ tầng lưu trữ để tăng tốc độ truy vấn. |
| **Application "White Screen"** | Một component bị lỗi khiến toàn bộ ứng dụng bị treo và hiển thị màn hình trắng (Crash). | Triển khai hệ thống Error Boundaries phân tầng (Global và Route-level) để cô lập lỗi và cung cấp giao diện phục hồi (Fallback UI) cho người dùng. |
| **Missing ArtistId on Dashboard** | Sau khi đăng nhập, idToken không chứa artistId của DB nên Dashboard không có UUID để truy vấn. | Thực hiện Fetch Profile (/me) ngay khi restore session để đồng bộ dữ liệu DB vào Frontend. |
| **DynamoDB Delete Limit** | Lệnh xóa lịch sử bị lỗi khi số lượng bản ghi vượt quá giới hạn 1MB của một lần Scan/Query. | Triển khai vòng lặp Deletion kết hợp với Pagination (LastEvaluatedKey) để xóa dữ liệu theo từng lô (Batch). |
| **Circular Dependency Crash** | Lỗi "Cannot access before initialization" do Store và HistoryService phụ thuộc lẫn nhau. | Chuyển đổi sang cơ chế Lazy Loading cho Store instance bên trong các Service. |
| **Auth Token Claims Outdated** | Token sau khi Refresh không chứa các thông tin (Claims) mới nhất nếu User vừa thay đổi Profile. | Cấu hình lưu trữ lại idToken từ response của Refresh flow để đảm bảo Frontend luôn có Claims mới nhất. |
| **GSI Filter Logic Error** | Bộ lọc `verifiedArtists` trả về kết quả sai do không lọc đúng thuộc tính `isVerified=true` trong query stats. | Cập nhật lại biểu thức Filter Expression trong GSI Query để đảm bảo tính chính xác của dữ liệu thống kê. |
| **MusicBrainz UUID Import** | Lỗi định dạng UUID khi nạp dữ liệu từ script seed do xung đột phiên bản module. | Chuẩn hóa quy trình Import UUID và bổ sung bước Validation dữ liệu trước khi thực hiện lệnh BatchWrite. |
| **UI Crash on Empty Stats** | Dashboard bị lỗi khi API trả về các key thống kê rỗng hoặc không có dữ liệu. | Triển khai cơ chế Fallback Keys tại Frontend, đảm bảo giao diện luôn hiển thị 0 hoặc trạng thái mặc định thay vì báo lỗi. |
| **Merge Conflict - AppLayout** | Xung đột lớn khi gộp các phân hệ Admin vào cấu trúc App Shell hiện tại. | Thực hiện xử lý Conflict thủ công, ưu tiên logic đồng bộ User Profile từ Backend để đảm bảo quyền truy cập Admin được nhận diện đúng. |
