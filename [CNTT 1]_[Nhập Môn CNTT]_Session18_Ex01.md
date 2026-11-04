#  Vá lỗ hổng rò rỉ API Key trên GitHub

***Tại sao tệp .env vẫn bị đẩy lên github

- .gitignore thiếu cấu hình: File .gitignore hiện tại mới chỉ chặn node_modules/ và dist/, chưa thêm .env vào danh sách loại trừ.

- Thói quen dùng git add .: Lệnh này gom toàn bộ các file mới/chỉnh sửa trong dự án vào staging area. Vì Git chưa được dặn bỏ qua .env, nó sẽ tự động theo dõi và đẩy file này lên repository công khai cùng đợt git push.

***Sửa tệp .gitignore và cơ chế hiển thị trên VS Code***

 Nội dung tệp .gitignore sau khi sửa:

 Test

.env
 
 .gitignore
 
 README 


***Cơ chế "ẩn thông tin" (làm mờ) trên VS Code***

- Nhận diện tự động: VS Code đọc tệp .gitignore trong dự án và tự động làm xám/mờ (dimmed) tên tệp .env ở thanh quản lý thư mục (Explorer).

- Cảnh báo trực quan: Màu mờ giúp người dùng nhận biết tệp đó đã bị Git bỏ qua, tránh nhầm lẫn với các tệp source code chính.

- Loại khỏi tab Source Control: Tệp .env sẽ không còn xuất hiện trong mục danh sách thay đổi (Changes) của VS Code, ngăn chặn hoàn toàn việc vô tình bấm commit hoặc push tệp nhạy cảm này lên mạng.
