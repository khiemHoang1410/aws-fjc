# AWS Worklog - Week 2: High Availability & Scalability

## 🎯 Training Objectives

- **Availability:** Triển khai kiến trúc Multi-AZ (Availability Zones) để loại bỏ Single Point of Failure.
- **Scalability:** Tự động hóa việc mở rộng tài nguyên dựa trên lưu lượng thực tế (Auto Scaling).
- **Automation:** Xây dựng quy trình CI/CD hoàn chỉnh từ GitHub Repo tới hạ tầng AWS.
- **Monitoring:** Giám sát sức khỏe hệ thống và thiết lập cảnh báo tự động qua CloudWatch.

## 🛠️ Task Checklist

- [x] **Runtime Environment:** Nâng cấp Node.js v20 (via NVM) tương thích Vite 6.
- [x] **Source Management:** Cấu hình SSH kết nối GitHub và xử lý Merge Conflicts.
- [x] **Frontend Deployment:** Triển khai React + Vite, cấu hình `allowedHosts` cho Production.
- [x] **Web Orchestration:** Thiết lập Nginx Reverse Proxy (Port 80 -> 5173).

### Technical Implementation

- [x] **Web Server:** Cấu hình Nginx làm Reverse Proxy, tối ưu hóa điều hướng traffic.
- [x] **Network & DNS:** Thiết lập Route 53, cấu hình A/CNAME Record và tích hợp External Registrar.
- [x] **Security (SSL/TLS):** Triển khai HTTPS với Let's Encrypt (Certbot) đảm bảo an toàn dữ liệu.
- [x] **System Permissions:** Cấu hình Access Control List (ACL) cho phép Web Server truy cập mã nguồn.
- [x] **Domain Management:** Quản trị Custom Domain qua AWS Route 53.
- [x] **DNS Orchestration:** Cấu hình và điều hướng Name Servers từ Registrar bên thứ 3.
- [x] **Security (SSL/TLS):** Thực thi giao thức HTTPS bảo mật trên Nginx.
- [x] **Resource Optimization:** Thực hiện Cleanup toàn bộ tài nguyên cũ, tối ưu hóa Budget.

### Professional Growth

- [ ] **Technical Writing:** Cập nhật tài liệu Architecture Diagram cho tuần 2.
- [ ] **Networking:** Tham gia thảo luận về tối ưu hóa chi phí (Cost Optimization) trong cộng đồng.

---

## 🧠 Technical Deep Dive

### 🌐 Edge Networking & Web Server (Nginx)

- **Port Conflict Resolution:** Xử lý xung đột cổng 80 bằng cách terminate các tiến trình chiếm dụng trái phép, giải phóng tài nguyên cho Nginx.
- **Reverse Proxy Configuration:** Thiết lập `nginx.conf` với các chỉ thị `root` và `proxy_pass`, đảm bảo luồng dữ liệu từ Port 80 được định tuyến chính xác vào thư mục dự án.
- **Permission Hardening:** Điều chỉnh quyền truy cập hệ thống (Linux Permissions) tại thư mục người dùng, cho phép Nginx worker có quyền `read/execute` để phục vụ nội dung tĩnh mà không vi phạm quy tắc bảo mật.

### 🌐 DNS & Edge Security

- **Route 53 Integration:** Chuyển đổi quyền quản lý bản ghi từ Registrar bên thứ ba về **AWS Route 53**. Thiết lập hệ thống **Hosted Zone** với các bản ghi **A Record** (trỏ về Elastic IP) và **CNAME**, tối ưu hóa tốc độ phân giải tên miền toàn cầu.
- **SSL/TLS Implementation:** Triển khai chứng chỉ bảo mật (Let's Encrypt) thông qua Certbot. Cấu hình Nginx để thực thi chính sách **HSTS** và **Force HTTPS**, đảm bảo toàn bộ dữ liệu người dùng được mã hóa trên đường truyền.

### 🔐 Security & Domain Management

- **DNS Infrastructure:** Triển khai **Route 53 Hosted Zones**. Thực hiện cấu hình **A Record** trỏ về Elastic IP và **CNAME** cho các sub-domain. Tích hợp thành công với NameServer của bên thứ 3.
- **SSL/TLS Encryption:** Sử dụng **Certbot** để tự động hóa quy trình cấp phát và gia hạn chứng chỉ **Let's Encrypt**. Cấu hình Force HTTPS để mã hóa toàn bộ lưu lượng giữa Client và Server.

### 🚀 Modern Frontend Deployment (React + Vite 6)

- **Runtime Optimization:** Sử dụng **NVM (Node Version Manager)** để quản trị đa phiên bản Node.js. Nâng cấp lên **v20 (LTS)** nhằm đáp ứng các yêu cầu khắt khe về hiệu năng và bảo mật của **Vite 6**.
- **DevOps Workflow:** Thiết lập kết nối an toàn qua **SSH Key** giữa EC2 và GitHub. Xử lý thành công các xung đột mã nguồn (Merge Conflicts) trong quá trình tích hợp nhánh `huy` vào `main`, đảm bảo tính toàn vẹn của Repo.
- **Vite Production Config:** Cấu hình `allowedHosts` trong Vite để server chấp nhận các Request từ Domain định danh thay vì chỉ giới hạn ở `localhost`.

### 🛰️ Network & Proxy Management (Nginx)

- **Security Group Hardening:** Tối ưu hóa Firewall lớp mạng (Port 22, 80, 5173), cân bằng giữa khả năng truy cập và tính bảo mật.
- **Reverse Proxy Implementation:** Cấu hình Nginx đóng vai trò là "người tiền trạm". Mọi yêu cầu gửi đến Port 80 (HTTP) sẽ được điều hướng ngầm về Port 5173 của ứng dụng Vite.
  - **Benefit:** Giúp người dùng truy cập trực tiếp qua `hskhiem.io.vn` mà không cần lộ thông tin về Port vận hành nội bộ, tăng tính thẩm mỹ và bảo mật cho ứng dụng.

---

## 💡 Lessons Learned & Troubleshooting

| Issue                   | Root Cause                                       | Solution                                                               |
| :---------------------- | :----------------------------------------------- | :--------------------------------------------------------------------- |
| **Port 80 Conflict**    | Tiến trình PM2 cũ chưa được terminate hoàn toàn. | Sử dụng `lsof -i :80` để tìm PID và `kill` tiến trình đang chiếm dụng. |
| **Nginx 403 Forbidden** | Thiếu quyền truy cập thư mục gốc (Permissions).  | Cấu hình `chmod` và `chown` phù hợp cho user `nginx` hoặc `www-data`.  |
| **SSL Challenge Fail**  | DNS chưa cập nhật hoặc Port 80 bị chặn.          | Kiểm tra bản ghi A Record và Security Group, sau đó chạy lại Certbot.  |
**Merge Conflict** | Sai lệch lịch sử Commit giữa các nhánh local và remote. | Sử dụng `git merge`, giải quyết thủ công các file xung đột và commit lại. |
| **Vite Access Denied** | Chính sách bảo mật của Vite ngăn chặn truy cập từ Host bên ngoài. | Bổ sung cấu hình `server: { allowedHosts: [...] }` trong file `vite.config.ts`. |
| **Node.js Incompatibility** | Phiên bản mặc định của OS quá cũ cho Vite 6. | Sử dụng NVM để cài đặt và `nvm use 20` làm phiên bản thực thi chính thức. |

---

## 📅 Timeline & Milestones

### [2026-03-16] Phase 7: Edge Networking & Security Hardening

- **Status:** **SUCCESSFULLY SECURED.**
- **Update:** Hoàn tất cấu hình Nginx, trỏ Domain thành công qua Route 53 và kích hoạt HTTPS.
- **Current State:** Hệ thống đã live với giao thức bảo mật SSL, sẵn sàng cho người dùng truy cập.

### [2026-03-17] Phase 8: Infrastructure Re-engineering & CLI Mastery

- **Status:** **SUCCESSFULLY RE-PROVISIONED.**
- **Cleanup:** Giải phóng tài nguyên cũ để tối ưu hóa hạn mức tín dụng .
- **Execution:** Xây dựng lại toàn bộ hạ tầng mạng và server qua CLI.
- **Connectivity:** Gán Elastic IP (`54.251.43.8`) và hoàn tất ánh xạ DNS cho `hskhiem.io.vn`. Hệ thống hiện đã sẵn sàng phục vụ traffic thực tế.

### [2026-03-18] Phase 9: Frontend Orchestration & Modern Runtime
- **Status:** **OPERATIONAL.**
- **Update:** Hoàn tất triển khai ứng dụng React/Vite 6 trên nền tảng Node v20.
- **Infrastructure:** Hệ thống đã thông suốt từ GitHub -> EC2 -> Nginx -> Domain. Người dùng có thể truy cập qua URL chuẩn mà không cần chỉ định Port.