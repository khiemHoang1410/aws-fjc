# AWS Worklog - Week 1: Cloud Fundamentals & Infrastructure Baseline

## 🎯 Training Objectives
- **Concepts:** Nắm vững 6 lợi ích cốt lõi của Cloud Computing & mô hình Pay-as-you-go.
- **Security:** Thiết lập môi trường AWS Account theo tiêu chuẩn Landing Zone cơ bản.
- **Professionalism:** Xây dựng Profile & kết nối cộng đồng AWS Study Group.

## 🛠️ Task Checklist
### Technical Implementation
- [x] **Source Control:** Khởi tạo GitHub Repository chuẩn dự án (README, .gitignore).
- [x] **Cloud Provisioning:** Hoàn tất đăng ký AWS Free Tier (Exp: 09/2026).
- [x] **Governance:** Thiết lập CloudWatch Billing Alarms & Zero-Threshold Budget.
- [x] **Network:** Thiết lập VPC và Public Subnet cho ứng dụng.
- [x] **S3 Hosting:** Khởi tạo và cấu hình S3 Bucket cho Static Website Hosting.

### Personal Branding
- [x] **LinkedIn Profile:** Updated "Bootcamp - First Cloud AI Journey @ AWS Study Group".
- [x] **Community:** Sync-up thành công với Admin & cộng đồng học tập.

---

## 🧠 Technical Deep Dive

### 🛡️ Identity & Access Management (IAM)
- **Root Lockdown:** Thực hiện "niêm phong" tài khoản Root sau khi kích hoạt MFA.
- **IAM Hierarchy:** Triển khai cấu trúc nhóm quyền `Admins` với policy `AdministratorAccess`. 
    - *Best Practice:* Quản lý quyền qua Group thay vì gán trực tiếp cho User để đảm bảo tính Scalability.
- **Identity:** Cấu hình Account Alias `zehel-cloud` giúp chuyên nghiệp hóa quy trình login.

### 🖥️ Compute & Network (EC2)
- **Instance Provisioning:** Launch `t3.micro` (Amazon Linux 2023) tại Region `ap-southeast-1` (Singapore).
- **Security Group (SG):** Cấu hình Port 22 (SSH).
    - *Note:* Hiện mở `0.0.0.0/0` để thực hành, sẽ thu hồi về White-list IP ở phase sau để tuân thủ **Least Privilege**.
- **Key Management:** Khởi tạo RSA Key pair, thực hiện `chmod 400` và lưu trữ local an toàn.

### 🌐 Networking (VPC)
- **VPC Setup:** Khởi tạo VPC tùy chỉnh với dải IP `10.0.0.0/16`.
- **Connectivity:** Cấu hình Internet Gateway và Route Table để cho phép Traffic ra ngoài Internet.
---

### 📦 Storage & Content Delivery (S3)
- **Static Hosting:** Kích hoạt tính năng **Static Website Hosting**, cấu hình `index.html` làm entry point.
- **Access Control:** Vô hiệu hóa "Block all public access" và sẵn sàng cho việc triển khai Bucket Policy để phân phối nội dung công khai.

## 💡 Lessons Learned & Troubleshooting

| Issue | Root Cause | Solution |
| :--- | :--- | :--- |
| **AWS Registration Fail** | Tài khoản thẻ không đủ số dư verify ($1). | Nạp số dư > 50k VNĐ, bật "Thanh toán quốc tế" trên Mobile App. |
| **Security Risk** | Quên MFA cho tài khoản đặc quyền. | **Security is Job Zero:** Kích hoạt MFA ngay lập tức cho Root & Admin. |
| **Billing Management** | Lo ngại phát sinh chi phí ngoài Free Tier. | Thiết lập **Zero-Threshold Budget ($0.01)** để nhận cảnh báo tức thì. |
| **S3 403 Forbidden** | Thiếu Bucket Policy. | Cần cấu hình Policy cho phép `s3:GetObject` trên toàn bộ tài nguyên. |
---

## 📅 Timeline & Milestones

### [2026-03-10] Foundation Established
- **Status:** Account Activated.
- **Update:** Xác thực thành công phương thức thanh toán & nhận $100 AWS Credit.

### [2026-03-11] Lab 1: Infrastructure Ready
- **Status:** **FULLY COMPLETED.**
- **Environment:** Console đã được tùy chỉnh (Pinned: EC2, S3, IAM, Billing).
#### S3 Static Website Hosting (Part 1)
- **Status:** **SUCCESSFULLY DEPLOYED.**
- **Update:** Website đã có thể truy cập qua S3 Endpoint công khai.