
- Đơn vị bộ nhớ nhỏ nhất là **binary digit**, hay **bit**
- Đơn vị bộ nhớ nhỏ nhất có thể truy cập trực tiếp là **byte**. 1 byte = 8 bits

- Dùng `sizeof()` để xem độ lớn của một kiểu dữ liệu (byte)

- Do kiểu dữ liệu có thể khác nhau tùy vào hệ thống (int có thể tối thiểu là 16, nhưng thường là 32 bit)
- Để muốn đặt độ lớn cố định, sử dụng **fixed-width integers** trong `<cstdint>` e.g. `std::int8_t`, `std::uint32_t`,...
- `std::int8_t` sẽ được coi như là một signed char
- `std::uint8_t` sẽ được coi như là một unsinged char
- Best practice: Sử dụng fixed-width integer khi bạn cần kiểu dữ liệu nguyên có độ lớn trong khoảng cố định nào đó

- Best practice:
	- Dùng `int` khi size không quan trọng
	- Dùng `std::int#_t` khi cần độ lớn trong một khoảng nhất định
	- Dùng `std::uint#_t` khi làm việc với bit manipulation hay khi hành vi wrap-around cần được định nghĩa tốt 

- `size_t` là kiểu dữ liệu nguyên usigned dùng để biểu diễn độ lớn hoặc độ dài object (trong header `<cstddef>`)

- **Scientific notation** là cách viết tắt các số dài. Các số trước `e` là **significant digits**

- `<>` trong C++ thường được dùng để biểu diễn một cái gì đó cần một tham số có dạng kiểu
- Dùng với `static_cast` để quyết định kiểu dữ liệu mà argument nên được chuyển về