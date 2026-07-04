
- Compiler là chương trình (hoặc tập hợp các chương trình) mà đọc mã nguồn của một ngôn ngữ (thường là bậc cao), sau đó dịch nó thành ngôn ngữ khác (thường là ngôn ngữ bậc thấp)
- Interpreter là chương trình trực tiếp chạy các yêu cầu trong mã nguồn mà không cần biên dịch -> Linh hoạt hơn, nhưng hiệu suất kém hơn do mỗi lần chạy chương trình đều phải chạy lại từ đầu 

- Các bước để biên dịch từ mã nguồn -> executable:
	- Compiler sẽ biên dịch từng file .cpp sang ngôn ngữ máy, chúng được lưu trong **object file** .o 
	- Sau đó, linker sẽ kết hợp tất cả các object file và tạo ra executable (kiểm tra xem objectfile có valid -> kiểm tra cross-file dependencies -> link các file thư viện)

- Best practice: Sử dụng debug build trong quá trình phát triển. Chuyển qua bản release build khi muốn phát hành 


