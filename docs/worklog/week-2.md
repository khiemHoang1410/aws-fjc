# AWS Worklog - Week 2: High Availability & Scalability

## 🎯 Training Objectives
- **Availability:** Triển khai kiến trúc Multi-AZ (Availability Zones) để loại bỏ Single Point of Failure.
- **Scalability:** Tự động hóa việc mở rộng tài nguyên dựa trên lưu lượng thực tế (Auto Scaling).
- **Automation:** Xây dựng quy trình CI/CD hoàn chỉnh từ GitHub Repo tới hạ tầng AWS.
- **Monitoring:** Giám sát sức khỏe hệ thống và thiết lập cảnh báo tự động qua CloudWatch.

## 🛠️ Task Checklist
### Technical Implementation
- [x] **Web Server:** Cấu hình Nginx làm Reverse Proxy, tối ưu hóa điều hướng traffic.
- [x] **Network & DNS:** Thiết lập Route 53, cấu hình A/CNAME Record và tích hợp External Registrar.
- [x] **Security (SSL/TLS):** Triển khai HTTPS với Let's Encrypt (Certbot) đảm bảo an toàn dữ liệu.
- [x] **System Permissions:** Cấu hình Access Control List (ACL) cho phép Web Server truy cập mã nguồn.

### Professional Growth
- [ ] **Technical Writing:** Cập nhật tài liệu Architecture Diagram cho tuần 2.
- [ ] **Networking:** Tham gia thảo luận về tối ưu hóa chi phí (Cost Optimization) trong cộng đồng.

---

## 🧠 Technical Deep Dive

### 🌐 Edge Networking & Web Server (Nginx)
- **Port Conflict Resolution:** Xử lý xung đột cổng 80 bằng cách terminate các tiến trình chiếm dụng trái phép, giải phóng tài nguyên cho Nginx.
- **Reverse Proxy Configuration:** Thiết lập `nginx.conf` với các chỉ thị `root` và `proxy_pass`, đảm bảo luồng dữ liệu từ Port 80 được định tuyến chính xác vào thư mục dự án.
- **Permission Hardening:** Điều chỉnh quyền truy cập hệ thống (Linux Permissions) tại thư mục người dùng, cho phép Nginx worker có quyền `read/execute` để phục vụ nội dung tĩnh mà không vi phạm quy tắc bảo mật.

### 🔐 Security & Domain Management
- **DNS Infrastructure:** Triển khai **Route 53 Hosted Zones**. Thực hiện cấu hình **A Record** trỏ về Elastic IP và **CNAME** cho các sub-domain. Tích hợp thành công với NameServer của bên thứ 3.
- **SSL/TLS Encryption:** Sử dụng **Certbot** để tự động hóa quy trình cấp phát và gia hạn chứng chỉ **Let's Encrypt**. Cấu hình Force HTTPS để mã hóa toàn bộ lưu lượng giữa Client và Server.

---

## 💡 Lessons Learned & Troubleshooting

| Issue | Root Cause | Solution |
| :--- | :--- | :--- |
| **Port 80 Conflict** | Tiến trình PM2 cũ chưa được terminate hoàn toàn. | Sử dụng `lsof -i :80` để tìm PID và `kill` tiến trình đang chiếm dụng. |
| **Nginx 403 Forbidden** | Thiếu quyền truy cập thư mục gốc (Permissions). | Cấu hình `chmod` và `chown` phù hợp cho user `nginx` hoặc `www-data`. |
| **SSL Challenge Fail** | DNS chưa cập nhật hoặc Port 80 bị chặn. | Kiểm tra bản ghi A Record và Security Group, sau đó chạy lại Certbot. |

---

## 📅 Timeline & Milestones

### [2026-03-16] Phase 7: Edge Networking & Security Hardening
- **Status:** **SUCCESSFULLY SECURED.**
- **Update:** Hoàn tất cấu hình Nginx, trỏ Domain thành công qua Route 53 và kích hoạt HTTPS.
- **Current State:** Hệ thống đã live với giao thức bảo mật SSL, sẵn sàng cho người dùng truy cập.