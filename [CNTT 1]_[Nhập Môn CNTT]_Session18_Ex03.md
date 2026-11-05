# Khắc phục sự cố rò rỉ thông tin đăng nhập

## ***Phần 1: Báo cáo Phân tích IPO (Input - Process - Output)***

Mô hình IPO giúp hệ thống hóa toàn bộ quy trình từ khâu phát hiện sự cố, các thao tác xử lý logic đến kết quả đầu ra mong muốn.

**INPUT**

 • Mất quyền kiểm soát tài khoản cá nhân (Facebook, Gmail) liên tục.

 • Bị đăng xuất tự động (Session Hijacking) dù vừa đổi mật khẩu trên máy tính hiện tại.

 • Nhận thông báo đăng nhập bất thường từ các vị trí lạ, email/tin nhắn rác tự động gửi đi từ tài khoản cá nhân.

 • Trình duyệt xuất hiện extension lạ, máy tính hoạt động chậm hoặc phần mềm diệtไวรัส bị vô hiệu hóa.

 **PROCESS**

 Bước 1: Ngắt kết nối mạng ngay lập tức (Cô lập thiết bị).

 Bước 2: Đổi mật khẩu & Thu hồi quyền truy cập (Dùng thiết bị sạch).

 Bước 3: Quét & Xử lý Infostealer (Diệt mã độc tận gốc).

 Bước 4: Cấu hình bảo vệ nâng cao (Gia cố hệ thống).

 **OUTPUT** 

  • Mã độc Infostealer bị gỡ bỏ hoàn toàn khỏi hệ thống.

  • Toàn bộ Session Cookies và Token truy cập cũ của kẻ tấn công bị vô hiệu hóa.

  • Quyền quản lý các tài khoản (Facebook, Gmail, GitHub...) được khôi phục an toàn.

  • Hệ thống được gia cố bằng cơ chế bảo mật nhiều lớp (2FA/Passkey).

## ***Phần 2: Quy trình 4 Bước Cấp cứu (Phần mềm & Thiết bị)***

***Ngắt kết nối mạng ngay lập tức***

- Thao tác: Rút dây mạng LAN, tắt Wi-Fi hoặc bật Airplane Mode trên máy tính bị nhiễm ngay lập tức.

- Giải thích: Ngắt đường truyền Command & Control (C2) để ngăn mã độc tiếp tục gửi dữ liệu (Session Cookies, Mật khẩu lưu trong trình duyệt, Token) về máy chủ của hacker.

- Verification: Máy tính hiển thị biểu tượng mất kết nối Internet hoàn toàn, không thể tải thêm bất kỳ trang web nào.

***Đổi mật khẩu & Thu hồi Session***

- Thao tác: Chuyển sang một thiết bị an toàn (như Smartphone dùng 4G/5G riêng hoặc máy tính khác không bị nhiễm).

- Giải thích: Thực hiện đăng xuất tất cả các phiên đăng nhập (Log out of all sessions), đổi mật khẩu mới và hủy các Token truy cập đã cấp trước đó.

- Verification: Đăng nhập thử bằng mật khẩu cũ trên thiết bị khác báo lỗi không chính xác, các thiết bị cũ đều bị đẩy ra khỏi tài khoản.

***Quét & Diệt Infostealer***

- Thao tác: Restart máy tính bị nhiễm vào chế độ Safe Mode (không kết nối mạng). Dùng các công cụ chuyên dụng như Malwarebytes, Kaspersky Virus Removal Tool, hoặc Windows Defender Offline Scan để quét toàn bộ ổ đĩa.

- Giải thích: Loại bỏ các tiến trình độc hại, Registry keys và Scheduled Tasks do mã độc tạo ra để bám rễ (Persistence).

- Verification: Công cụ diệt virus báo cáo 0 mối đe dọa (0 threats found) sau khi hoàn tất quét lại. Nếu mã độc can thiệp quá sâu, giải pháp tối ưu là Backup dữ liệu thô (non-executable) và cài lại OS (Format & Reinstall).