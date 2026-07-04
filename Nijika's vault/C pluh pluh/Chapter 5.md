
- **Constant** là giá trị mà không thể thay đổi trong quá trình thực hiện chương trình 
	- **Named constant** là constant gắn với một identifier, còn gọi là **symbolic constants**
	- **Literal constant** là constant không được gắn với một identifier

- Có 3 cách định nghĩa một named constant
	- Constant variable e.g. `const int x {6};`
	- Object-like macros with substitution text  e.g. `#define MY_NAME "buh"`
	- Enumerated constants 

- Best practice: Không dùng const cho parameter (ngoại trừ pass by reference hay pass by address), và không dùng const cho trả về 

- Literal đôi khi được gọi là **literal constant** vì giá trị của chúng không thể định nghĩa lại 
- Có thể thêm suffix vào sau literal để chỉ rõ hơn về kiểu của chúng e.g. `5u` (unsigned int), `5LL` (long long)

- Thường sẽ không cần suffix, ngoại trừ float 

- "Hello, world!" là một **string literal**, ở đây nó còn được gọi là **C strings** hay **C-style strings**
- C-style string, khác với các literal khác, là một object được tạo ở đầu chương trình và đảm bảo tồn tại trong toàn bộ thời gian chương trình chạy 

- Trong C++20 ta có thêm `<format>` để format lệnh in dễ hơn e.g. `std::cout << std::format("{:b\n}", 0b1010)` `{:b}` định dạng augment là binary digit 
- Trong C++23 ta có thêm `<print>` e.g. `std::println("{:b}", 0b1010)`, có tác dụng tương tự như trên 

- **As-if rule**: Là luật nói rằng compiler có thể thay đổi chương trình theo bất cứ cách nào để tối ưu code tốt hơn, miễn là nó không làm ảnh hưởng đến "hành vi quan sát được" của chương trình 
- **Compile-time evaluation** là khi compiler tính toán tất cả hoặc một phần của một số biểu thức tại thời điểm biên dịch (thay vì thời điểm chạy)
- **Constant folding** là khi compiler thay thế các biểu thức có toán tử hằng với kết của của biểu thức đó e.g. `3 + 4` được thay bằng `7`
- **Constant propagation** là khi compiler thay thế biến mà được biết là có giá trị hằng với giá trị của chúng 
- **Dead code elimination** là khi compiler loại bỏ code mà có thể được thực hiện, nhưng không có tác dụng gì với hành vi của chương trình 

- **Constant expression** là expression mà phải được tính toán tại thời điểm biên dịch. Có thể bao gồm:
	- Literal e.g. `5`, `1.2`
	- Toán tử với toán hạng là constant expression e.g. `3 + 4`
	- Biến const kiểu nguyên với initializer là constant expression e.g. `const int x{5};`. Đây là ngoại lệ mang tính lịch sử, giờ ưu tiên dùng `constexpr`
	- Biến `constexpr`
	- Gọi hàm `constexpr` với constant expression arguments 

- **Constexpr** yêu cầu giá trị của biến (hoặc kết quả của hàm) phải được biết tại thời điểm biên dịch
- **Const** chỉ mang nghĩa là giá trị của một object không thể thay đổi sau khởi tạo 
=> constexpr luôn là const, nhưng const không chắc là constexpr

- Không nên pass by value `std::string` vì nó tạo bản sao tốn kém 
- Có thể trả về `std::string` by value. Nếu trả về là C-style string thì nên trả về `std::string_view`
- Best practice: Ưu tiên `std::string_view` hơn `std::string` khi bạn cần string chỉ đọc, đặc biệt khi dùng trong parameter của hàn 
- `std::string_view` có thể được khởi tạo bởi nhiều loại khác nhau:
	- C-style string
	- `std::string`
	- `std::string_view`
- `std::string_view` sẽ không ngầm chuyển đổi qua `std::string`

- Để tạo string/string_view literal
```c++
using namespace std::string_literals;      // access the s suffix
using namespace std::string_view_literals; // access the sv suffix

std::cout << "foo\n";   // no suffix is a C-style string literal
std::cout << "goo\n"s;  // s suffix is a std::string literal
std::cout << "moo\n"sv; // sv suffix is a std::string_view literal
```

- Khác với `std::string`, `std::string_view` có hỗ trợ đầy đủ cho constexpr 

- `std::string_view` có thể được hoặc không được null-terminated (do nó có thể view substring) 