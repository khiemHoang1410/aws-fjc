# AWS Worklog - Week 1: Cloud Fundamentals & Infrastructure Baseline

## 🎯 Training Objectives
- **Concepts:** Nắm vững 06 lợi ích cốt lõi của Cloud Computing và mô hình kinh doanh Pay-as-you-go.
- **Security:** Triển khai môi trường AWS Account theo tiêu chuẩn bảo mật Baseline.
- **Professionalism:** Xây dựng Profile chuyên nghiệp và kết nối mạng lưới cộng đồng AWS Study Group.

## 🛠️ Task Checklist
### Technical Implementation
- [x] **Source Control:** Khởi tạo GitHub Repository theo tiêu chuẩn dự án (README, .gitignore).
- [x] **Cloud Provisioning:** Hoàn tất đăng ký AWS Free Tier và kích hoạt Credit (Exp: 09/2026).
- [x] **Governance:** Thiết lập CloudWatch Billing Alarms và Zero-Threshold Budget để kiểm soát chi phí.
- [x] **Networking:** Triển khai hạ tầng Custom VPC với phân vùng Public/Private Subnet.
- [x] **S3 Hosting:** Khởi tạo và cấu hình S3 Bucket cho dịch vụ Static Website Hosting.
- [x] **Data Protection:** Kích hoạt S3 Versioning nhằm đảm bảo tính toàn vẹn và khả năng phục hồi dữ liệu.
- [x] **Web Engine:** Cài đặt và cấu hình Apache Web Server (httpd) trên thực thể EC2.
- [x] **Static Networking:** Cấp phát Elastic IP đảm bảo địa chỉ kết nối cố định cho hệ thống.
- [x] **Routing:** Cấu hình Internet Gateway và Route Table để điều phối lưu lượng mạng.
- [x] **External Connectivity:** Cấu hình Internet Gateway (IGW) và Route Table cho VPC.
- [x] **Validation:** Xác thực kết nối SSH qua Elastic IP thành công.

### Personal Branding
- [x] **LinkedIn Profile:** Cập nhật thông tin: "Bootcamp - First Cloud AI Journey @ AWS Study Group".
- [x] **Community:** Kết nối thành công với đội ngũ Quản trị viên và cộng đồng học tập.

---

## 🧠 Technical Deep Dive

### 🛡️ Identity & Access Management (IAM)
- **Root Lockdown:** Thực thi chính sách bảo mật đa lớp (MFA) cho tài khoản Root ngay sau khi khởi tạo.
- **IAM Hierarchy:** Triển khai cấu trúc nhóm quyền `Admins` với chính sách `AdministratorAccess`.
    - *Best Practice:* Quản lý quyền hạn thông qua Group thay vì gán trực tiếp cho User để tối ưu hóa khả năng mở rộng (Scalability).
- **Identity:** Thiết lập Account Alias `zehel-cloud` nhằm chuyên nghiệp hóa quy trình định danh và đăng nhập.

### 🖥️ Compute & Network (EC2)
- **Instance Provisioning:** Khởi tạo thực thể `t3.micro` (Amazon Linux 2023) tại Region Singapore (`ap-southeast-1`).
- **Security Group (SG):** Cấu hình Port 22 (SSH).
- **Key Management:** Khởi tạo RSA Key pair, thực thi phân quyền `chmod 400` và lưu trữ cục bộ an toàn.
- **Key Security:** Xử lý lỗi bảo mật file `.pem` trên Windows bằng cách cấu hình lại Access Control List (ACL), đảm bảo nguyên tắc **Private Key Privacy** trước khi thiết lập kết nối.

#### [Updated 2026-03-12]
- **Web Server Deployment:** Triển khai **Apache (httpd)** trên Amazon Linux 2023. Tối ưu hóa quy trình khởi tạo bằng script hệ thống.
- **Static Connectivity:** Gắn **Elastic IP** vào Instance, đảm bảo duy trì địa chỉ IP công cộng cố định khi thay đổi trạng thái hệ thống (Stop/Start).
- **Traffic Control:** Mở rộng Security Group hỗ trợ giao thức **HTTP (Port 80)** song song với SSH.
- **Performance Audit:** Sử dụng công cụ `lscpu` và `free -m` để giám sát tài nguyên, đảm bảo vận hành tối ưu trong giới hạn Free Tier.
- **External Routing:** Triển khai **Internet Gateway**  và cấu hình Route Table điều hướng traffic (`0.0.0.0/0 -> IGW`) cho phân vùng Public.
- **Static Access:** Gán thành công **Elastic IP** (`54.179.17.128`) cho Web Server, đảm bảo địa chỉ định danh không đổi khi khởi động lại Instance.
- **Validation:** Kiểm tra và xác nhận khả năng kết nối SSH ổn định qua IP tĩnh.

### 🌐 Networking (VPC Architecture)
- **VPC Customization:** Triển khai VPC với dải CIDR `10.0.0.0/16`, cô lập hoàn toàn với môi trường mặc định.
- **Subnet Segmentation:** - **Public Subnet (`10.0.1.0/24`):** Thiết lập phân vùng biên (DMZ) cho các dịch vụ hướng ngoại.
- **Private Subnet (`10.0.2.0/24`):** Thiết lập vùng an toàn cho Database/Backend, ngăn chặn truy cập trực tiếp từ Internet.
- **Gateway & Routing:** Attach **Internet Gateway (IGW)** và cấu hình Route Table (`0.0.0.0/0 -> IGW`) để kích hoạt kết nối Internet cho phân vùng Public.

### 📦 Storage & Content Delivery (S3)
- **Static Hosting:** Kích hoạt tính năng **Static Website Hosting**, thiết lập `index.html` làm entry point cho ứng dụng.
- **Access Control:** Triển khai **Bucket Policy** (JSON) cấp quyền `s3:GetObject` cho Public Access, cho phép người dùng truy cập nội dung qua Internet.
- **Data Reliability:** Kích hoạt **Versioning** để quản lý đa phiên bản Object, hỗ trợ khả năng Rollback dữ liệu và ngăn ngừa rủi ro ghi đè ngoài ý muốn.

---

## 💡 Lessons Learned & Troubleshooting

| Issue | Root Cause | Solution |
| :--- | :--- | :--- |
| **AWS Registration Fail** | Tài khoản thanh toán không đủ số dư xác thực ($1). | Đảm bảo số dư tối thiểu (> 50k VNĐ) và kích hoạt giao dịch quốc tế. |
| **Security Risk** | Thiếu lớp bảo mật cho tài khoản đặc quyền. | **Security is Job Zero:** Kích hoạt MFA ngay lập tức cho Root & Admin. |
| **Billing Management** | Rủi ro phát sinh chi phí ngoài dự kiến. | Thiết lập **Zero-Threshold Budget ($0.01)** để nhận cảnh báo tức thì. |
| **S3 403 Forbidden** | Thiếu chính sách truy cập (Bucket Policy). | Cấu hình Policy cho phép `s3:GetObject` trên toàn bộ tài nguyên công khai. |
| **SSH Timeout** | Chưa cấu hình Route Table trỏ ra IGW. | Thiết lập bản ghi định tuyến `0.0.0.0/0` trỏ về Internet Gateway trong VPC. |
| **SSH Permission Denied** | File `.pem` trên Windows có quyền quá hở (`Unprotected Private Key`). | Sử dụng `icacls` để gỡ bỏ quyền kế thừa và chỉ cấp quyền Read cho User hiện hành. |
---

## 📅 Timeline & Milestones

### [2026-03-10] Foundation Established
- **Status:** **ACCOUNT ACTIVATED.**
- **Update:** Hoàn tất xác thực thanh toán và nhận $100 AWS Credit.

### [2026-03-11] Lab 1: Infrastructure Ready
- **Status:** **FULLY COMPLETED.**
- **Environment:** Tùy chỉnh Console điều hướng (Pinned: EC2, S3, IAM, Billing).

#### S3 Static Website Hosting (Part 1)
- **Status:** **SUCCESSFULLY DEPLOYED.**
- **Update:** Hoàn tất cấu hình Hosting và Endpoint truy cập công khai.


### [2026-03-12] S3 Static Website Hosting - SUCCESS
- **Status:** **WEBSITE IS LIVE.**
- **Update:** Triển khai thành công Access Policy và cơ chế bảo vệ dữ liệu Versioning.
#### Deploying Web Server on EC2
- **Status:** **SUCCESSFULLY PROVISIONED.**
- **Update:** Server vận hành ổn định trên nền tảng Elastic IP và Apache Engine.
- **Next Step:** Tích hợp quy trình CI/CD hoặc triển khai tầng dữ liệu (RDS).

### [2026-03-14] Networking with VPC - COMPLETED
- **Status:** **INFRASTRUCTURE READY.**
- **Update:** Hoàn tất thiết lập hạ tầng mạng Custom VPC, sẵn sàng triển khai mô hình Multi-tier Architecture.