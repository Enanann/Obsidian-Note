
- **Statement** (câu lệnh) là một kiểu hướng dẫn làm cho chương trình thực hiện một hành động gì đó
- **Data** (dữ liệu) là bất kì thông tin gì mà có thể được di chuyển, xử lý, hoặc lưu trữ bởi máy tính 
- Trong C++, việc truy cập bộ nhớ trực tiếp không được khuyến khích. Thay vào đó, ta truy cập bộ nhớ qua các object. **Object** là một vùng bộ nhớ mà có thể lưu trữ một giá trị
- Object với tên được gọi là **variable** (biến)
- **Allocation** (cấp bộ nhớ) là việc dành riêng không gian lưu trữ cho việc sử dụng một object 

- Các kiểu **initialization** (khởi tạo) trong C++
```c++
int a;       // default-initialization (no initializer) 

// Traditional
int b = 5;   // copy-initialization (initial value after equals sign)
int c(6);    // direct-initialization (initial value in parenthesis)

// Modern (prefered)
int d{7};    // direct-list-initialization (initial value in braces)
int e{}      // value-initialization (empty braces)
```

- List-initialization (hay uniform initialization) cấm narrowing conversion e.g. `int x{4.5};` bị cấm

- Để tránh việc compiler cảnh báo các biến không được dùng đến, sử dụng `[[maybe unused]]` 

- `std::cout` được **buffered**. Tức là các output trong nó không được đưa ra console ngay lập tức, mà sẽ được **flushed** (xả) định kỳ => Nếu chương trình crashes, aborts, hay paused trước khi buffer được flushed, tất cả các output đang đợi sẽ không được hiển thị 

- `std::endl` vs `\n`: `std::endl` sẽ thực hiện 2 việc là thêm xuống dòng và flush buffer -> `\n` hiệu quả hơn 

- `std::cin` cũng được buffered. Mặc định của cin sẽ là whitespace (spaces, tabs, newlines). Mỗi dòng input sẽ được chấm dứt bởi `\n` 
- Giả sử có `int x{}; std::cin >> x;`:
	- Nếu nhập `h`: `x = 0` do integer không lưu được chữ cái, cin ở trạng thái lỗi, các cin tiếp theo luôn là 0
	- Nếu nhập `123abc`: `x = 123`, `abc` sẽ được lưu trong buffer cho lần tiếp theo 
	- Nếu nhập `abc123`: `x = 0`, cin ở trạng thái lỗi, các cin tiếp theo luôn là 0
	- Khi cin ở trạng thái lỗi, sử dụng `std::cin.clear()` và `std::cin.ignore()` để xóa lỗi và buffer 

- Best practice: Giữ giới hạn độ dài dòng là 80 ký tự 

- **Literal** là một giá trị cố định được ghi thẳng vào trong mã nguồn e.g. `5` của `int x{5};`

- **Expression** là một chuỗi không rỗng gồm các hằng, biến, toán tử, và gọi hàm để tính toán một giá trị 
- **Expression statement** là một statement đi với expression và kết thúc với `;` 