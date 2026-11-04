# Vá Lỗ Hổng Hardcode Secrets Và Thiết Lập Lá Chắn

## ***Phần 1: Phân tích hậu quả & Sai lầm kỹ thuật***

***1. 4 Secrets bị lộ và hậu quả thảm họa***

Trong đoạn code server.js vừa đẩy lên public repository, nhóm mình đã vô tình phơi bày 4 chìa khóa chí mạng sau:

***OPENAI_API_KEY (sk-proj-...):***

  - Hậu quả: Đây là nguyên nhân trực tiếp khiến thẻ tín dụng của Trưởng nhóm bị trừ sạch 1.200 USD. Bất kỳ ai có key này đều có thể tha hồ gọi các mô hình AI đắt tiền của OpenAI (như GPT-4) để làm dịch vụ bên ngoài, viết tool spam, hoặc huấn luyện mô hình trái phép mà tiền thì tài khoản của studio mình phải gánh. 

 ***STEAM_WEB_API_KEY (STEAM_SECRET_KEY_882910AAFFBBDD):***

  - Hậu quả: Kẻ tấn công có thể giả mạo ứng dụng game CyberRealm để can thiệp vào hệ thống dịch vụ của Steam, đọc lén thông tin tài khoản người chơi, lấy cắp dữ liệu inventory, hoặc thao túng các yêu cầu xác thực API liên quan đến game trên Steam.

 ***MONGO_URI (mongodb+srv://admin_root:SuperSecretPass2026@...):***

  - Hậu quả: Lộ toàn bộ tài khoản admin_root cùng mật khẩu truy cập trực tiếp vào cơ sở dữ liệu MongoDB Atlas trên mây. Kẻ xấu có thể truy cập, xem trộm, sửa đổi hoặc xóa sạch toàn bộ dữ liệu game (thông tin người chơi, tiến trình, vật phẩm) trong database cyberrealm_db.

***JWT_SECRET (pixel_forge_super_private_token_key_9988):***

  - Hậu quả: Khóa bí mật dùng để ký và xác thực mã thông báo đăng nhập của người dùng. Khi lộ key này, hacker có thể tự tạo ra các token giả mạo với quyền quản trị viên cao nhất (Admin), qua mặt toàn bộ hệ thống xác thực để đăng nhập vào bất kỳ tài khoản nào trong game mà không cần mật khẩu.

  ***2. Tại sao xóa commit hoặc đổi sang Private sau 10 phút vẫn vô tác dụng?***

  ## ***Phần 2: Sửa lỗi & Chuẩn hóa an ninh***

 (khúc này em không biết làm)