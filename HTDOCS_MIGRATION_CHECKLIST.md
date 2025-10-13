## Checklist chuyển giao diện & chức năng từ htdocs sang dự án SMM

### USER (Khách hàng)
- **Auth**: Đăng ký, Đăng nhập, Quên mật khẩu, Verify email
- **Hồ sơ**: Cập nhật thông tin, timezone; Đổi mật khẩu; API key (xem/tạo lại)
- **Số dư & Nạp tiền**:
  - Xem số dư, lịch sử nạp
  - Nạp Paypal/Stripe (min/max, điều kiện new users)
  - Bonus theo bậc (nếu bật)
- **Danh mục & Dịch vụ**:
  - List danh mục; List/filter dịch vụ theo danh mục, trạng thái
  - Chi tiết dịch vụ: mô tả, min/max, giá, refill/dripfeed
  - Tìm kiếm dịch vụ
- **Tạo đơn hàng**:
  - direct/api; link/quantity/usernames/hashtags/comments/media
  - Dripfeed: runs, interval, quantity
  - Subscription (nếu dùng): sub_min/max/delay/expiry
  - Refill: yêu cầu refill nếu được
- **Theo dõi đơn hàng**: danh sách, chi tiết, filter trạng thái; hủy/hoàn trả (nếu cho phép)
- **Tickets**: tạo ticket, danh sách, chat/reply, trạng thái (new/pending/answered/closed)
- **FAQs/Trang tĩnh/News**: danh sách/chi tiết; Terms/Policy/Custom Pages; News hiệu lực
- **File manager (tuỳ chọn)**: upload, xem chi tiết ảnh/tệp
- **Ngôn ngữ**: chọn ngôn ngữ (nếu bật)
- **API Docs**: xem/copy API key; tài liệu endpoints (add order, status, services)
- **Email**: nhận các email theo cấu hình bật/tắt

### ADMIN (Quản trị)
- **Dashboard**: tổng đơn/trạng thái, doanh thu, nạp, thông báo nhanh
- **Users**: danh sách/chi tiết, khóa/mở; số dư & spent; reset API key; UserPrices
- **Categories**: CRUD tên/mô tả/ảnh/sort/trạng thái
- **Services**: CRUD; price/original_price/min/max/type/status; flags (deny_duplicates/refill/refill_type/dripfeed/add_type); liên kết Provider; đồng bộ từ Provider
- **Orders**: danh sách/filter; chi tiết; bulk actions (completed/cancel/refund/partial); dripfeed/subscription; refill
- **Providers (ApiProviders)**: CRUD; refresh balance; đồng bộ dịch vụ từ provider (manual/cron)
- **Payments**: CRUD phương thức; params JSON; min/max/new_users/status; **PaymentsBonus** CRUD; Transaction logs (nếu có)
- **Tickets**: danh sách toàn hệ thống; gán/trả lời/đóng; user_read/admin_read
- **FAQs/Custom Pages**: CRUD câu hỏi/sort/status; CRUD trang tĩnh (name/slug/image/content/position/pid/status)
- **News/Announcements**: CRUD type/description/status/expiry
- **File Manager**: danh sách tệp, xoá/quản lý
- **Options/Settings**:
  - Website: name/title/desc/keywords/logo/favicon
  - Công tắc: https, maintenance, homepage, api tab, notification popup
  - Liên hệ: email/tel/giờ; Social links
  - Email: protocol/smtp; bật template (verify/welcome/payment/ticket/order)
  - Currency: symbol/decimals/separators
  - Defaults: min/max/price_per_1k; dripfeed defaults
  - Recaptcha keys (nếu dùng)
- **Languages**: danh sách, mặc định, bật/tắt; general_lang key/value (nếu áp dụng)
- **Subscribers**: danh sách email, export
- **Staff/Admin**: quản lý admin/staff, phân quyền (nếu dùng)
- **Logs/Sessions**: theo dõi hệ thống
- **Tools**: Import dữ liệu cốt lõi từ htdocs

### Backend/Infra (đã/đang thực hiện)
- **Bảng sẵn có**: Categories, Services, Orders, Users, RefreshTokens, ...
- **Bảng mới**: ApiProviders, Payments, PaymentBonuses, UserPrices, Tickets, TicketMessages, Faqs, CustomPages, Options, FileManagers
- **Seed**: Payments mẫu (Paypal/Stripe), Options cơ bản
- **Migrations**: đã tạo và cập nhật DB
- **Jobs/Cron (tuỳ)**: sync services, check order status, refresh provider balance
- **Bảo mật**: Roles ADMIN/MEMBER; rate limit (tuỳ)
- **Uploads**: lưu tệp/ảnh per user/hệ thống

### Di chuyển dữ liệu (từ htdocs)
- Providers: import
- Services: import + map category
- Options/Settings: import theo whitelist
- Payments: import phương thức + bonus
- Users: KHÔNG import mật khẩu; dùng reset/khởi tạo lại
- Orders lịch sử (tuỳ): cân nhắc nhu cầu báo cáo

### Ưu tiên triển khai (đề xuất)
1) Backend: Providers, Payments(+bonus), Tickets(+messages), FAQs/Pages, Options; mở rộng Orders/Services (refill/dripfeed)
2) Frontend: Admin pages tương ứng; User pages: nạp tiền, tạo đơn, theo dõi đơn, tickets, FAQs/pages, settings
3) Đồng bộ Provider + import dữ liệu cốt lõi


