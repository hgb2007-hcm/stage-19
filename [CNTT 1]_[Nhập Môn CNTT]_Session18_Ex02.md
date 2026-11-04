# Xử lý sự cố an ninh từ email đáng ngờ

***Phân tích rủi ro của kỹ thuật "Đuôi file kép" (Double Extension).***

- Bản chất trò lừa: Tên tệp thực tế là Job_Offer.pdf.exe, nhưng kẻ gian đã cố tình đặt tên đánh lừa mắt người nhìn.

- Lỗ hổng từ hệ điều hành: Theo mặc định, Windows thường ẩn phần mở rộng (extension) của các tệp quen thuộc. Vì thế, bạn sẽ chỉ thấy nó hiển thị là Job_Offer.pdf kèm theo cái icon hình file PDF đỏ chót.   

- Hậu quả chết người: Bạn cứ đinh ninh đó là file tài liệu văn bản bình thường nên thản nhiên double-click vào. Nhưng thực chất, hệ thống đang kích hoạt một chương trình chạy lệnh (.exe). Ngay lúc đó, mã độc (như trojan, keylogger hoặc mã độc tống tiền ransomware) sẽ được cài cắm ngầm vào máy tính mà không hề mở lên một cái file PDF nào cả.

***Giải thích tại sao yêu cầu "Tắt Antivirus" là một cái bẫy mã độc.***

**Tại sao yêu cầu "Tắt Antivirus" là một cái bẫy mã độc?**

- Windows Defender không ngu: Khi một file .exe giả dạng file tài liệu được tải về, Windows Defender hoặc các phần mềm diệt virus sẽ ngay lập tức quét thấy hành vi bất thường (hoặc nhận diện chữ ký mã độc bên trong) và chặn đứng nó lại.

- Chiêu trò thao túng tâm lý (Social Engineering): Kẻ tấn công biết rõ file của tụi nó sẽ bị phần mềm diệt virus thịt ngay lập tức. Do đó, chúng phải bịa ra lý do "Do tệp được mã hóa bảo mật nội bộ..." để dụ dỗ nạn nhân tự tay tắt khiên bảo vệ của máy tính đi.   

- Quy tắc vàng: Không một công ty chân chính nào bắt ứng viên phải vô hiệu hóa bảo mật máy cá nhân chỉ để xem một file thư mời nhận việc (.pdf) cả. Tắt đi chẳng khác nào mở cửa cho trộm vào nhà.   

***- Đề xuất công cụ trực tuyến để quét tệp này trước khi mở.***

Nếu gặp trường hợp nghi ngờ như thế này mà lỡ tải file xuống rồi, tuyệt đối không được mở trực tiếp trên máy. Hãy dùng công cụ quét mã độc trực tuyến uy tín nhất hiện nay:

- VirusTotal (virustotal.com)

- Cách dùng: Truy cập trang web, tải tệp nghi ngờ lên.

- Cơ chế: Hệ thống sẽ dùng đồng thời hơn 60+ công cụ diệt virus hàng đầu thế giới (Kaspersky, Bitdefender, Google,...) để quét file đó cùng một lúc. Nếu file có mã độc, nó sẽ hiện cảnh báo đỏ lòm để mình né gấp.