# Gỡ Bẫy Spear Phishing Đuôi File Kép Và Sự Cố Tắt Antivirus Cài Plugin Crack

## ***PHẦN 1: PHÂN TÍCH HIỂM HỌA & LỖI VI PHẠM***

***Ba sai lầm chí mạng của thực tập sinh trong 24h qua***

- Sai lầm 1 (Dính bẫy Social Engineering & Double Extension): Chủ quan mở tệp đính kèm lạ (Sponsorship_Agreement_v2.pdf.exe) chỉ vì thấy icon file PDF và nội dung email quá hấp dẫn (nhận tài trợ 50.000 USD) mà không kiểm tra kỹ phần đuôi mở rộng thật của tệp.

- Sai lầm 2 (Sử dụng phần mềm bẻ khóa trôi nổi): Tải phần mềm "chùa", công cụ Crack/Keygen từ các diễn đàn không chính thống thay vì mua bản quyền hoặc tìm giải pháp mã nguồn mở thay thế an toàn.

- Sai lầm 3 (Tự tay tước bỏ lá chắn bảo vệ): Nghe lời hướng dẫn độc hại trên mạng, tự tay tắt bỏ tính năng bảo vệ thời gian thực (Real-time Protection) của Windows Defender để cho phép file Setup_Crack.exe độc hại chạy toàn quyền trên hệ thống.

***Phân tích thủ thuật giả mạo tên miền và đuôi file kép***

- Tại sao dùng địa chỉ epig-games.com? Hacker sử dụng kỹ thuật Typosquatting (giả mạo tên miền tinh vi). Chúng cố tình đổi chữ c thành chữ g (epig thay vì epic) để đánh lừa thị giác người nhìn lúc vội vàng. Nạn nhân tưởng đại gia ngành game đang liên hệ tài trợ nên mất cảnh giác.

- Tại sao đặt tên Sponsorship_Agreement_v2.pdf.exe và kỹ thuật này gọi là gì?

  - Đây là kỹ thuật Đuôi file kép (Double Extension) lợi dụng việc hệ điều hành Windows mặc định ẩn phần mở rộng của các định dạng quen thuộc.

  - Kẻ tấn công cố tình đặt tên tệp chứa đuôi .pdf ở giữa để Windows ngụy trang icon và ẩn đi phần .exe thực sự ở phía sau. Người dùng nhìn vào chỉ thấy file PDF tưởng là hợp đồng, nhưng thực tế khi bấm đúp vào thì hệ thống kích hoạt chạy một chương trình thực thi mã độc (.exe).

***Bản chất của yêu cầu "Tắt Antivirus" và 2 giây màn hình nhấp nháy***

- Vì sao bắt buộc phải tắt Antivirus? Các file Crack/Keygen hoặc Setup giả mạo luôn bị các phần mềm diệt virus nhận diện là mã độc (Trojan/Riskware) và chặn đứng ngay lập tức khi vừa tải về hoặc giải nén. Kẻ tấn công buộc phải dùng chiêu trò thao túng tâm lý, ép người dùng tự tay vô hiệu hóa công cụ bảo mật thì chúng mới có "đất diễn".

- Bản chất 2 giây màn hình nhấp nháy (Infostealer hoạt động ngầm):

  - Khoảnh khắc màn hình nhấp nháy đen chính là lúc mã độc thuộc dòng Infostealer (như RedLine, Raccoon...) đang âm thầm chạy ngầm với quyền cao nhất.

  - Nó quét toàn bộ hệ thống để trích xuất sạch sẽ session cookies của trình duyệt (giúp đăng nhập không cần mật khẩu vào Discord, Steam, Gmail,...), đánh cắp các token xác thực, SSH keys dùng để đẩy code lên GitHub/GitLab, và các thông tin lưu trữ ví điện tử để gửi về server của hacker. Đó là lý do tài khoản Discord và Steam bỗng dưng bị chiếm đoạt dù chưa kịp cài plugin nào cả.

## ***PHẦN 2: PHƯƠNG ÁN CẤP CỨU & PHÒNG NGƯỜI***

***Quy trình Cấp cứu 4 Bước ngăn chặn hacker xâm nhập kho mã nguồn chung***

Vì máy của thực tập sinh đã dính mã độc Infostealer (có khả năng đã rò rỉ SSH keys và Token truy cập GitHub/GitLab của dự án game "CyberRealm"), chúng ta phải xử lý khẩn cấp theo các bước sau:

- Bước 1: Ngắt mạng khẩn cấp lập tức

  - Yêu cầu thực tập sinh rút ngay dây mạng LAN hoặc ngắt kết nối Wi-Fi của chiếc máy tính đó ngay lập tức nhằm cắt đứt đường truyền dữ liệu mà mã độc đang cố gắng tuồn ra ngoài hoặc nhận lệnh từ hacker.

- Bước 2: Đổi mật khẩu toàn bộ tài khoản từ một thiết bị sạch khác

  - Sử dụng một thiết bị hoàn toàn khác (điện thoại cá nhân hoặc máy tính của thành viên khác chưa bị nhiễm mã độc) để tiến hành đổi mật khẩu toàn bộ tài khoản: Email công ty, Discord, Steam, mạng xã hội, và đặc biệt là tài khoản GitHub/GitLab quản lý mã nguồn game. Bật xác thực hai lớp (2FA) cho tất cả.

- Bước 3: Thu hồi Access Tokens, SSH Keys & Session Tokens

  - Vào phần cài đặt bảo mật của GitHub/GitLab và các nền tảng quản lý dự án để Revoke (Thu hồi toàn bộ) tất cả các SSH Keys, Personal Access Tokens đang có hiệu lực.

  - Đăng xuất tất cả các phiên làm việc (Log out all sessions) trên toàn bộ các dịch vụ mà thực tập sinh từng đăng nhập trên máy tính bị nhiễm để vô hiệu hóa hoàn toàn cookie đã bị hacker đánh cắp.

- Bước 4: Cài lại hệ điều hành sạch (Clean Install / Format)

   - Máy tính đã bị nhiễm Infostealer được xem như "đã hỏng hoàn toàn" vì mã độc có thể đã cài cắm sâu vào các tiến trình hệ thống (persistence).

   - Tiến hành format trắng ổ cứng và cài đặt lại hoàn toàn hệ điều hành Windows sạch sẽ trước khi cho phép kết nối lại vào hệ thống chung của nhóm PixelForge Studio.

***Hai thiết lập bắt buộc trên Windows để phòng chống đuôi file kép***

Để tránh lặp lại sự cố tương tự cho toàn bộ 8 thành viên trong nhóm, yêu cầu tất cả mọi người cấu hình ngay 2 thiết lập sau trên Windows Explorer:

Hiển thị phần mở rộng của tên tệp (File name extensions):

- Cách làm: Mở File Explorer ➔ Chọn tab View (trên thanh menu phía trên) ➔ Tìm và tích chọn ô "File name extensions" (Phần mở rộng tên tệp).

- Tác dụng: Từ nay các file độc hại có kiểu tên lừa đảo như Sponsorship_Agreement_v2.pdf.exe sẽ hiện nguyên hình đầy đủ phần .exe ở cuối, giúp anh em dễ dàng nhận diện bằng mắt thường.

Hiển thị các tệp, thư mục và ổ đĩa ẩn (Hidden files, folders, and drives):

- Cách làm: Vẫn trong tab View của File Explorer ➔ Chọn Options (hoặc nhấn vào biểu tượng 3 chấm chọn Options) ➔ Chuyển qua tab View ➔ Tìm dòng "Show hidden files, folders, and drives" và tích chọn vào đó ➔ Nhấn Apply và OK.

- Tác dụng: Giúp phát hiện các file mã độc cố tình ẩn mình dưới dạng file hệ thống hoặc file ẩn mà hacker thường lợi dụng để qua mắt người dùng.