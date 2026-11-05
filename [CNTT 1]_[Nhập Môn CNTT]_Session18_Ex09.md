# Thiết Kế Kiến Trúc Két Sắt Số Bitwarden Và Chính Sách Mật Khẩu Game Studio

## ***PHẦN 1: BÁO CÁO PHÂN TÍCH KIẾN TRÚC AN NINH MẬT KHẨU***

***1. Rủi ro khi lưu mật khẩu trên Google Chrome đối với lập trình viên nhiễm Infostealer***

Thói quen bấm nút "Lưu mật khẩu" mặc định trên Google Chrome tạo ra một lỗ hổng chí mạng khi máy tính bị nhiễm phần mềm độc hại dòng Infostealer (như RedLine, Racoon, Lumma Stealer):  

- Cơ chế lưu trữ dễ bị khai thác: Google Chrome lưu trữ dữ liệu thông tin đăng nhập trong một cơ sở dữ liệu SQLite tại đường dẫn cục bộ (%LocalAppData%\Google\Chrome\User Data\Default\Login Data). Mặc dù mật khẩu trong trường password_value được mã hóa, Chrome phụ thuộc vào cơ chế bảo vệ cấp hệ điều hành (như DPAPI trên Windows hoặc Keychain trên macOS) để khóa mã khóa giải mã (Master Key).

- Điểm yếu trước Infostealer: Khi máy tính dính mã độc chạy dưới quyền của người dùng hiện tại (User privilege), mã độc có thể dễ dàng gọi API của hệ điều hành để giải mã Master Key, đọc toàn bộ tệp Login Data dưới dạng văn bản rõ (Clear-text) chỉ trong tích tắc.

- Mối đe dọa đặc thù với lập trình viên: Đối với dev tại PixelForge Studio, Chrome không chỉ lưu mật khẩu web thông thường mà còn lưu trữ các Personal Access Token (PAT) của GitHub, API Keys của AWS, thông tin đăng nhập Firebase hay Stripe. Khi Infostealer đánh cắp tệp này, toàn bộ hạ tầng đám mây, kho mã nguồn và cổng thanh toán của studio sẽ rơi vào tay kẻ tấn công ngay lập tức mà không cần hacker phải bẻ khóa từng mật khẩu.

***2. Bản chất kỹ thuật của Kiến trúc Zero-Knowledge và Client-side Decryption***

Nếu máy chủ đám mây của nhà cung cấp Password Manager (như Bitwarden) bị hacker tấn công xâm nhập toàn bộ (Server Compromise), dữ liệu két sắt của PixelForge Studio HOÀN TOÀN KHÔNG BỊ GIẢI Mã. Lý do xuất phát từ các nguyên lý kỹ thuật cốt lõi sau:

- Client-side Decryption (Giải mã tại máy khách): Toàn bộ quá trình mã hóa và giải mã dữ liệu diễn ra cục bộ trên thiết bị của người dùng (Laptop, điện thoại). Dữ liệu khi truyền lên máy chủ đám mây hoặc lưu trên ổ cứng của server đã ở trạng thái mã hóa đầu cuối bằng chuẩn AES-256 bit (chuẩn mã hóa quân sự).

*** - Nguyên tắc Zero-Knowledge (Không-Biết-Gì):***

- Máy chủ của nhà cung cấp chỉ đóng vai trò là "kho chứa các tệp mã hóa mù" (Blind Storage).

- Mật khẩu chính (Master Passphrase) của người dùng không bao giờ được gửi lên máy chủ, thậm chí không được lưu trữ dưới dạng thô hay dạng băm đơn thuần. Thay vào đó, máy khách dùng thuật toán dẫn xuất khóa (Argon2id hoặc PBKDF2) kết hợp Master Passphrase với chuỗi muối ngẫu nhiên (Salt) để tạo ra một Khóa Chính (Master Key) cục bộ.

- Kết luận: Kẻ tấn công khi chiếm được máy chủ Bitwarden chỉ thu được các chuỗi ký tự mã hóa hỗn độn (Ciphertext). Để giải mã được, chúng buộc phải có Master Passphrase của từng thành viên. Với độ dài và độ phức tạp chuẩn, việc vét cạn (Brute-force) mã AES-256 là bất khả thi về mặt vật lý (mất hàng tỷ năm bằng công nghệ siêu máy tính hiện tại).

## ***PHẦN 2: THIẾT KẾ CHÍNH SÁCH & KỊCH BẢN CHUYỂN ĐỔI***

***Thiết kế Master Passphrase chuẩn (Dài, dễ nhớ, chống Brute-force)***

 Để cân bằng giữa khả năng ghi nhớ của con người và sức mạnh chống vét cạn, phương pháp tối ưu là sử dụng Passphrase đa từ (Diceware / Sentence-based) thay vì chuỗi ký tự ngẫu nhiên ngắn khó nhớ.

 ***Tiêu chuẩn thiết kế:***

 - Độ dài tối thiểu: 24 ký tự trở lên.

 - Cấu trúc: Tổ hợp của 4 đến 5 từ tiếng Anh hoặc tiếng Việt không dấu có nghĩa kết hợp với ký tự đặc biệt và số ở các vị trí cố định nhưng dễ hình dung theo một câu chuyện cá nhân.

 ***Bảng cấu hình chuẩn cho công cụ Generator trong Bitwarden***

 Loại thành phần (Type)

 - Mật khẩu (Password)

 - Tạo chuỗi ngẫu nhiên toàn diện

 Độ dài (Length)

 - 24 - 32 ký tự

 - Vượt xa tiêu chuẩn tối thiểu (16), triệt tiêu hoàn toàn khả năng dò quét

 Chữ cái viết hoa (A-Z)

 - Bật (True)

 - Tăng không gian mẫu ký tự

 Chữ cái viết thường (a-z)

 - Bật (True)

 - Tăng không gian mẫu ký tự

 Chữ số (0-9)

 - Bật (True)

 - Đảm bảo tính đa dạng cấu trúc

 Ký tự đặc biệt (!@#$...)

 - Bật (True)   

-  Chống các bộ từ điển tấn công thông dụng

Tránh ký tự dễ nhầm lẫn

- Bật (True)

- Loại bỏ các ký tự như l, I, 1, O, 0 để tránh sai sót khi nhập thủ công

***Khả năng chống tấn công Phishing giả mạo tên miền của Auto-fill***

Tính năng Tự động Điền (Auto-fill) của Bitwarden chống lừa đảo giỏi hơn con người nhờ cơ chế khớp URL nghiêm ngặt dựa trên nguyên lý kỹ thuật số:

- Con người dễ bị đánh lừa bởi thị giác khi nhìn các tên miền giả mạo tinh vi (ví dụ: githúb.com dùng ký tự Unicode homograph, hay steampowered.xyz thay vì .com).

- Ngược lại, Bitwarden không hề "đọc" giao diện hay logo trang web. Nó chỉ thực hiện so khớp chính xác chuỗi tên miền (Domain matching) đã được lưu trữ an toàn trong mục URI của tài khoản đó với URL thực tế trên thanh địa chỉ của trình duyệt.

- Khi người dùng đứng trước một trang web giả mạo (Phishing site), Bitwarden nhận diện sự khác biệt về tên miền và kiên quyết từ chối tự động điền, qua đó ngăn chặn việc gửi thông tin nhạy cảm vào tay hacker ngay cả khi nạn nhân có tâm lý chủ quan.

***Quy trình thiết lập và lưu trữ Khóa Cấp cứu (Emergency Kit)***

Để đảm bảo tính liên tục trong hoạt động vận hành của studio khi Trưởng phòng Kỹ thuật gặp sự cố đột xuất, quy trình quản lý Khóa Cấp cứu (Emergency Kit) được quy định như sau:

Xuất Khóa Cấp cứu: Khi thiết lập tài khoản Bitwarden Tổ chức (Organization) cho studio, quản trị viên bắt buộc phải xuất tài liệu Emergency Kit (tệp PDF chứa thông tin tài khoản, chuỗi mã hóa khôi phục và hướng dẫn).

Lưu trữ phân tán (Split-Knowledge / Physical Safe):

- Bản cứng 1: In ra giấy, niêm phong trong phong bì bảo mật và cất vào Két sắt vật lý đặt tại văn phòng chính của PixelForge Studio (Chỉ Trưởng nhóm và Giám đốc điều hành biết mã két).

- Bản điện tử mã hóa: Lưu tệp PDF vào một thiết bị lưu trữ ngoại vi (USB mã hóa phần cứng) và cất tại địa điểm thứ hai.

Sử dụng tính năng Emergency Access tích hợp: Cấu hình trực tiếp trên hệ thống Bitwarden tính năng Quyền truy cập khẩn cấp (Emergency Access): Phân quyền cho tài khoản của Trưởng nhóm được phép yêu cầu quyền quản trị két sắt của Trưởng phòng Kỹ thuật với thời gian chờ (Waiting Period) là 48 giờ. Nếu Trưởng phòng Kỹ thuật không từ chối trong thời gian này, hệ thống sẽ tự động cấp quyền kiểm soát cho Trưởng nhóm, đảm bảo không có điểm nghẽn vận hành khi có sự cố nhân sự đột xuất.