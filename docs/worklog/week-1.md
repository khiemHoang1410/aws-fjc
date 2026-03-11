# Worklog - Week 1: Cloud Fundamentals

## 1. Mục tiêu đào tạo

- Tìm hiểu khái niệm và 6 lợi ích cốt lõi của Cloud Computing.
- Thiết lập môi trường AWS Account chuẩn cấu trúc bảo mật.
- Xây dựng mạng lưới kết nối cộng đồng và Profile chuyên nghiệp.

## 2. Danh sách nhiệm vụ (Checklist)

### Kỹ thuật

- [x] Khởi tạo Repository GitHub theo chuẩn dự án.
- [x] Hoàn tất đăng ký tài khoản AWS (Free Tier).
- [ ] Thiết lập hệ thống cảnh báo chi phí (Billing Alarms).

### Personal Branding

- [x] Cập nhật thông tin nhận diện trên các nền tảng liên lạc.
- [x] Thiết lập Job Title trên LinkedIn: **Bootcamp - First Cloud AI Journey @ AWS Study Group**.
- [x] Kết nối với đội ngũ Admin và cộng đồng học tập.

## 3. Kiến thức trọng tâm

- **Cloud Computing:** Thuê tài nguyên qua internet theo mô hình Pay-as-you-go.
- **Tính linh hoạt (Elasticity):** Khả năng mở rộng hoặc thu hẹp tài nguyên theo nhu cầu thực tế.
- **Bảo mật:** Nguyên tắc phân quyền tối thiểu khi bắt đầu với Cloud.

## 💡 Lessons Learned & Troubleshooting
- **Issue:** Thẻ Bank không thanh toán được AWS nếu như trong tài khoản không có số dư trên 1$.
- **Solution:** Phải vào App bật "Giao dịch Internet" và "Thanh toán quốc tế", đồng thời nạp dư khoảng 50k-100k để AWS verify account.
- **Key Takeaway:** Bảo mật là ưu tiên hàng đầu (Security is Job Zero). Luôn sử dụng MFA cho tài khoản Root ngay sau khi tạo.

### [2026-03-10] Milestone: Account Activated & Credits Received

- **Status:** SUCCESSFULLY ACTIVATED.
- **Update:** Đã xác thực thành công phương thức thanh toán sau khi cấu hình lại hạn mức thẻ MB Bank.
- **Bonus:** Nhận $100.00 USD AWS Credits (Hạn dùng đến tháng 09/2026).
- **Next Step:** Cấu hình CloudWatch Billing Alarms để giám sát hạn mức Credit và tránh phát sinh chi phí ngoài ý muốn.

### [2026-03-11] Update: IAM Administration Setup
- [x] **Created IAM User:** Tài khoản đã được thiết lập với quyền `AdministratorAccess`.
- [x] **Zero Spend Budget:** Thiết lập Budget thông qua Template với ngưỡng $0.01.