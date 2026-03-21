# AWS Cloud Infrastructure & Serverless Implementation - Week 2

## 📝 Project Overview
- **Student:** [Tên của ông]
- **Role:** Cloud Intern / AWS Learner
- **Batch:** Bootcamp - First Cloud AI Journey @ AWS Study Group
- **Duration:** 10/03/2026 - 14/03/2026
- **Stack:** AWS (EC2, S3, VPC, IAM), Linux (AL2023), Apache, PM2.

## 📝 Project Overview
Tài liệu này tổng hợp chi tiết lộ trình triển khai, cấu hình và tối ưu hóa hạ tầng điện toán đám mây trên nền tảng **Amazon Web Services (AWS)** trong tuần thứ 2. Trọng tâm của giai đoạn này là sự dịch chuyển mang tính chiến lược từ kiến trúc Monolithic truyền thống sang mô hình **Serverless (SST v3 - Ion)**. Mục tiêu cuối cùng là thiết lập một hệ thống có khả năng tự động mở rộng (Scalability), tối ưu hóa chi phí vận hành và đảm bảo tính sẵn sàng cao (High Availability) trên nhiều vùng khả dụng (Multi-AZ).

---

# 🎯 1. Mục tiêu đào tạo (Training Objectives)

Trong tuần này, các mục tiêu chiến lược được đề ra bao gồm:

* **High Availability & Fault Tolerance:** Thiết kế và triển khai kiến trúc trên nhiều Availability Zones (Multi-AZ) nhằm loại bỏ hoàn toàn các điểm nghẽn đơn lẻ (Single Point of Failure), đảm bảo hệ thống vẫn vận hành ổn định ngay cả khi một vùng gặp sự cố.
* **Elastic Scalability:** Xây dựng cơ chế tự động hóa việc co giãn tài nguyên (Auto Scaling) dựa trên phân tích lưu lượng truy cập thực tế, giúp cân bằng giữa hiệu năng và chi phí.
* **DevOps Automation:** Thiết lập và chuẩn hóa quy trình CI/CD (Continuous Integration/Continuous Deployment) khép kín, từ việc đẩy mã nguồn lên GitHub đến việc tự động triển khai trực tiếp lên hạ tầng AWS.
* **Infrastructure Monitoring:** Triển khai giải pháp giám sát sức khỏe hệ thống toàn diện thông qua **Amazon CloudWatch**, thiết lập các ngưỡng cảnh báo tự động để phát hiện và xử lý sự cố kịp thời.
* **Serverless Paradigm:** Tiếp cận và làm chủ công nghệ SST v3 (Ion) để quản lý tài nguyên Cloud thông qua mã nguồn (Infrastructure as Code).

---

## 📅 2. Nhật ký công việc chi tiết (Detailed Worklog)

Dưới đây là bảng tổng hợp các đầu việc đã được thực hiện xuyên suốt từ ngày 16/03 đến 21/03/2026:

| Day | Task Details | Start Date | Completion Date | Reference Material |
|:---:|:---|:---:|:---:|:---|
| **1** | **Edge Networking & Security Hardening:** <br> - Cấu hình Nginx làm Reverse Proxy. <br> - Chuyển đổi quyền quản trị DNS từ Registrar bên thứ 3 về **AWS Route 53**. <br> - Triển khai HTTPS bằng Let's Encrypt (Certbot). | 03/16/2026 | 03/16/2026 | [AWS Route 53 Docs](https://docs.aws.amazon.com/route53/) |
| **2** | **Infrastructure Re-engineering & CLI Mastery:** <br> - Thực hiện Cleanup tài nguyên cũ để tối ưu hóa Budget. <br> - Tái cấu hình toàn bộ hạ tầng mạng và server thông qua AWS CLI. <br> - Gán Elastic IP (`54.251.43.8`) và ánh xạ DNS cho `hskhiem.io.vn`. | 03/17/2026 | 03/17/2026 | [AWS CLI Reference](https://awscli.amazonaws.com/v2/documentation/api/latest/index.html) |
| **3** | **Frontend Orchestration & Modern Runtime:** <br> - Nâng cấp môi trường thực thi lên Node.js v20 (LTS). <br> - Triển khai React + Vite 6 trên nền tảng Nginx Proxy. <br> - Cấu hình SSH Key kết nối an toàn giữa EC2 và GitHub. | 03/18/2026 | 03/18/2026 | [Vite 6 Guide](https://vitejs.dev/guide/) |
| **4** | **System Permission & Ownership:** <br> - Cấu hình Access Control List (ACL) cho Web Server. <br> - Xử lý Merge Conflicts phức tạp khi tích hợp các nhánh mã nguồn. <br> - Tối ưu hóa bảo mật hệ thống Linux (Permissions/Ownership). | 03/19/2026 | 03/20/2026 | [Linux Permissions](https://linux.die.net/man/1/chmod) |
| **5** | **Live API & Serverless Implementation:** <br> - Triển khai **SST v3 (Ion)** kết hợp AWS Lambda và API Gateway. <br> - Can thiệp vào **SSM Parameter Store** để khôi phục Metadata hệ thống. <br> - Kích hoạt Endpoint Health Check và hoàn tất dự án. | 03/21/2026 | 03/21/2026 | [SST v3 Documentation](https://sst.dev/docs/) |

---


## 🏆 3. Kết quả đạt được (Key Achievements)

### Kỹ thuật & Hạ tầng
* **Runtime Environment:** Nâng cấp thành công môi trường Node.js v20 qua NVM, đảm bảo tương thích hoàn toàn với các tính năng mới nhất của Vite 6.
* **Web Orchestration:** Triển khai hệ thống Nginx làm Reverse Proxy ổn định, điều hướng mượt mà traffic từ Port 80 về ứng dụng nội bộ.
* **Security (SSL/TLS):** 100% lưu lượng truy cập được mã hóa qua HTTPS với chứng chỉ Let's Encrypt, thực thi chính sách HSTS và Force HTTPS để bảo mật dữ liệu người dùng.
* **Serverless Success:** Triển khai thành công API Serverless với SST v3, tích hợp Lambda và API Gateway tại Region Singapore (`ap-southeast-1`).
* **Domain & DNS:** Làm chủ hoàn toàn luồng quản trị tên miền thông qua Route 53 Hosted Zones với các bản ghi A và CNAME chuẩn xác.

### Phát triển chuyên môn
* **Problem Solving:** Khả năng xử lý các xung đột mã nguồn (Merge Conflicts) và lỗi hệ thống (Permissions, Port Conflict) một cách chuyên nghiệp.
* **IaC Mastery:** Hiểu sâu về cơ chế Resource Linking của SST v3, thay thế các biến môi trường thủ công bằng hệ thống Type-safe mạnh mẽ.

---
## 🧠 4. Phân tích kỹ thuật (Technical Deep Dive)

### 🌐 Edge Networking & Nginx Reverse Proxy
Hệ thống sử dụng Nginx không chỉ như một Web Server mà còn đóng vai trò "người tiền trạm" (Reverse Proxy).
* **Port Forwarding:** Mọi yêu cầu HTTP (Port 80) được chuyển tiếp ngầm đến Port 5173 của Vite. Điều này giúp bảo vệ cổng vận hành ứng dụng bên trong và tạo ra URL thân thiện với người dùng (`hskhiem.io.vn`).
* **Permission Hardening:** Giải quyết bài toán bảo mật bằng cách điều chỉnh ACL cho thư mục dự án, cho phép tiến trình `nginx` hoặc `www-data` có quyền đọc nhưng không vi phạm nguyên tắc đặc quyền tối thiểu.

### 🔐 DNS & Security Infrastructure
* **Route 53 Orchestration:** Việc chuyển Name Servers về AWS Route 53 giúp tận dụng khả năng phân giải DNS độ trễ thấp toàn cầu. Các bản ghi A Record được ánh xạ trực tiếp tới Elastic IP cố định.
* **SSL Automation:** Sử dụng **Certbot** để tự động hóa quy trình cấp phát và gia hạn chứng chỉ. Nginx được cấu hình để tự động redirect toàn bộ traffic không bảo mật (HTTP) sang giao thức bảo mật (HTTPS).

### 🚀 Modern Frontend & Serverless Integration
* **Vite 6 Configuration:** Đặc biệt chú trọng vào việc cấu hình `allowedHosts` trong `vite.config.ts`. Đây là cơ chế bảo mật quan trọng của Vite nhằm ngăn chặn các cuộc tấn công giả mạo Host.
* **SST v3 (Ion) Architecture:**
    * **Resource Linking:** Tận dụng cơ chế link mới giúp Lambda truy cập trực tiếp vào các tài nguyên khác (S3, DynamoDB) mà không cần ARN.
    * **State Recovery:** Khi Metadata bị lỗi, việc can thiệp trực tiếp vào **SSM Parameter Store** là kỹ thuật cao cấp để khôi phục trạng thái hệ thống mà không cần phá hủy và xây dựng lại từ đầu.

---

## 💡 5. Xử lý sự cố & Bài học kinh nghiệm (Troubleshooting)

| Tình huống (Issue) | Nguyên nhân (Root Cause) | Giải pháp (Solution) |
| :--- | :--- | :--- |
| **Port 80 Conflict** | Tiến trình PM2 cũ chưa được dừng, chiếm dụng cổng 80. | Sử dụng `lsof -i :80` để truy tìm PID và thực hiện `kill -9` để giải phóng tài nguyên. |
| **Nginx 403 Forbidden** | User chạy Nginx không có quyền `x` (execute) trên các thư mục cha. | Cấu hình lại `chmod` và đảm bảo thư mục gốc dự án có phân quyền phù hợp cho Web Server. |
| **SSL Challenge Fail** | DNS chưa kịp cập nhật hoặc Security Group chặn Inbound Port 80. | Kiểm tra trạng thái phân giải tên miền và mở Port 80 trong SG trước khi chạy lại Certbot. |
| **Vite Access Denied** | Chính sách bảo mật mặc định của Vite chặn truy cập từ IP/Domain ngoại vi. | Bổ sung mảng `allowedHosts` chứa domain của dự án vào file cấu hình `vite.config.ts`. |
| **Missing Bootstrap Bucket** | SST v3 mất dấu Metadata sau quá trình dọn dẹp tài nguyên. | Can thiệp thủ công vào **AWS SSM Parameter Store** để tái thiết lập liên kết cho Metadata. |
| **Lambda Outbound Timeout** | Lambda nằm trong Private Subnet nhưng thiếu NAT Gateway để ra Internet. | Triển khai NAT Gateway hoặc chuyển cấu hình mạng phù hợp để Lambda có thể gửi Request ra ngoài. |

---