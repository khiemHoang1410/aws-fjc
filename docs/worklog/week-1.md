# ☁️ AWS Cloud Journey | Week 1: Infrastructure Foundations

## 📝 Project Overview
- **Student:** [Tên của ông]
- **Role:** Cloud Intern / AWS Learner
- **Batch:** Bootcamp - First Cloud AI Journey @ AWS Study Group
- **Duration:** 10/03/2026 - 14/03/2026
- **Stack:** AWS (EC2, S3, VPC, IAM), Linux (AL2023), Apache, PM2.

---

## 🎯 Mục tiêu đào tạo (Week 1 Objectives)
* [cite_start]**Kết nối cộng đồng:** Làm quen và kết nối với các thành viên, Quản trị viên của First Cloud Journey[cite: 5].
* **Nền tảng Cloud:** Nắm vững 06 lợi ích cốt lõi của Cloud Computing và mô hình kinh doanh Pay-as-you-go.
* [cite_start]**Quản trị tài khoản:** Hiểu và sử dụng thành thạo AWS Management Console & CLI[cite: 6].
* **Bảo mật Baseline:** Triển khai môi trường AWS Account theo tiêu chuẩn bảo mật cao nhất ngay từ đầu.
* **Thương hiệu cá nhân:** Xây dựng Profile chuyên nghiệp trên LinkedIn và GitHub.

---
## 📅 Nhật ký công việc chi tiết (Worklog Table)

| Day | Task | Start Date | Completion Date | Reference Material |
|:---:|:---|:---:|:---:|:---|
| **1** | **Project Initiation & Governance:** <br> - Khởi tạo GitHub Repo (.gitignore, README). <br> - Kích hoạt AWS Free Tier & $100 Credit. <br> - Thiết lập Billing Alarms & Zero-Threshold Budget. | 03/10/2026 | 03/10/2026 | [AWS Billing Guide](https://aws.amazon.com/aws-cost-management/aws-budgets/) |
| **2** | **Security & Static Storage:** <br> - IAM: Root Lockdown (MFA), tạo Group Admins. <br> - S3: Hosting Static Website, cấu hình Versioning & Bucket Policy. | 03/11/2026 | 03/11/2026 | [S3 Documentation](https://docs.aws.amazon.com/s3/) |
| **3** | **Compute Provisioning:** <br> - Launch EC2 `t3.micro` (AL2023). <br> - Cài đặt Apache Web Server (httpd). <br> - Gán Elastic IP & cấu hình Security Group (Port 22, 80). | 03/12/2026 | 03/12/2026 | [EC2 User Guide](https://docs.aws.amazon.com/ec2/) |
| **4** | **Advanced Network Architecture:** <br> - Triển khai Custom VPC (`Zehel-VPC`). <br> - Phân chia Public/Private Subnet. <br> - Cấu hình Internet Gateway (IGW) & Route Table. | 03/14/2026 | 03/14/2026 | [VPC Masterclass](https://docs.aws.amazon.com/vpc/) |
| **5** | **Service Optimization:** <br> - Triển khai **PM2** quản lý tiến trình ngầm. <br> - Thiết lập Auto-restart & Log Monitoring cho dịch vụ. | 03/14/2026 | 03/14/2026 | [PM2 Quick Start](https://pm2.keymetrics.io/) |

---
## 🏆 Kết quả đạt được (Week 1 Achievements)

### 1. Kiến thức nền tảng (Cloud Fundamentals)
* [cite_start]Nắm vững các nhóm dịch vụ chính: Compute, Storage, Networking, Database [cite: 20-24].
* Hiểu sâu về mô hình trách nhiệm chung (Shared Responsibility Model).

### 2. Kỹ năng thực hành AWS CLI & Console
* [cite_start]Thành thạo thao tác trên AWS Console: tìm kiếm, truy cập và cấu hình dịch vụ nhanh chóng[cite: 26].
* [cite_start]Cài đặt và cấu hình AWS CLI hoàn chỉnh: Access Key, Secret Key, Default Region [cite: 27-30].
* [cite_start]Sử dụng CLI để thực hiện các lệnh nâng cao: Kiểm tra account, liệt kê Regions, quản lý Key Pairs và giám sát tài nguyên đang chạy [cite: 31-36].

### 3. Quản trị hạ tầng (Infrastructure Management)
* **Networking:** Tự thiết kế và triển khai VPC Custom thay vì sử dụng cấu hình mặc định, đảm bảo tính cô lập và bảo mật cao.
* [cite_start]**Compute:** Triển khai Web Server ổn định, xử lý thành công các vấn đề về Key Security (`chmod 400` và ACL trên Windows)[cite: 12].
* **Storage:** Làm chủ S3 với các tính năng nâng cao như Versioning (chống ghi đè) và Bucket Policy (JSON access control).

### 4. Personal Branding
* Cập nhật LinkedIn chuyên nghiệp: "Bootcamp - First Cloud AI Journey @ AWS Study Group".
* Kết nối thành công với mạng lưới chuyên gia trong cộng đồng.

---

## 🧠 Phân tích kỹ thuật (Technical Deep Dive)

### 🛡️ Identity & Access Management (IAM)
* **Root Lockdown:** Bảo vệ tuyệt đối tài khoản gốc bằng MFA.
* **IAM Groups:** Quản lý quyền hạn theo nhóm thay vì gán trực tiếp cho User để tối ưu hóa khả năng mở rộng (Scalability).
* **Account Alias:** Chuyên nghiệp hóa quy trình đăng nhập với định danh `zehel-cloud`.

### 🌐 Networking (VPC Architecture)
* **Segmentation:** Việc phân chia Public/Private Subnet giúp bảo vệ các tài nguyên nhạy cảm (như Database) khỏi sự tiếp cận trực tiếp từ Internet.
* **Routing:** Internet Gateway đóng vai trò là cửa ngõ duy nhất kết nối VPC với thế giới bên ngoài thông qua bảng định tuyến (Route Table).

### 🔄 Service Optimization & Daemonization
* **PM2:** Thay thế phương thức chạy script thủ công, cho phép ứng dụng tự hồi phục sau khi crash và quản lý log tập trung, giúp giảm thiểu thời gian gián đoạn dịch vụ.

---

---

# 💡 Xử lý sự cố & Bài học kinh nghiệm (Troubleshooting)

| Vấn đề (Issue) | Nguyên nhân (Root Cause) | Giải pháp (Solution) |
| :--- | :--- | :--- |
| **AWS Registration Fail** | Số dư tài khoản không đủ $1 để xác thực. | Đảm bảo số dư > 50.000 VNĐ và mở khóa thanh toán quốc tế. |
| **Security Risk** | Tài khoản đặc quyền thiếu lớp bảo mật. | Kích hoạt MFA ngay lập tức cho Root & Admin. |
| **Billing Management** | Rủi ro phát sinh phí ngoài dự kiến. | Thiết lập **Zero-Threshold Budget ($0.01)** để nhận cảnh báo sớm nhất. |
| **S3 403 Forbidden** | Thiếu chính sách truy cập (Bucket Policy). | Cấu hình Policy JSON cho phép hành động `s3:GetObject`. |
| **SSH Timeout** | Route Table chưa trỏ ra Internet Gateway (IGW). | Thêm bản ghi định tuyến `0.0.0.0/0` trỏ về IGW của VPC. |
| **SSH Permission Denied** | File `.pem` trên Windows có quyền quá rộng. | Dùng `icacls` gỡ quyền kế thừa, chỉ cấp quyền Read cho User hiện hành. |

---

## 🚀 Định hướng tuần tiếp theo (Next Steps)
* Nghiên cứu tích hợp quy trình CI/CD tự động từ GitHub.
* Triển khai Database Layer với AWS RDS.
* Thiết lập quy trình đồng bộ mã nguồn tự động trực tiếp lên máy chủ EC2.