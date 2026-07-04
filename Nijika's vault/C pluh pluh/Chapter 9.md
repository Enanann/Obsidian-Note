
- **Precondition** là bất kỳ điều kiện nào phải đúng trước khi thực hiện một đoạn mã (thường là body của 1 hàm)
- Precondition nên được đặt ở đầu của hàm, sử dụng kết hợp với return sớm để trở về khi điều kiện không thỏa mãn
=> Còn được gọi là **bouncer pattern** 
```cpp
void printDivision(int x, int y) {
    if (y == 0) {
        std::cerr << "Error: Could not divide by zero\n";
        return; // bounce the user back to the caller
    }

    // We now know that y != 0
    std::cout << static_cast<double>(x) / y;
}
```

- Phiên bản không có bouncer pattern 
```cpp
void printDivision(int x, int y) {
    if (y != 0) {
        std::cout << static_cast<double>(x) / y;
    } else {
        std::cerr << "Error: Could not divide by zero\n";
        return; // bounce the user back to the caller
    }
}
```
- Có thể thấy là trông nó rời rạc hơn cũng như nhiều nesting hơn 

- **Invariant** là điều kiện mà phải đúng khi một đoạn code nào đó đang thực hiện, thường dùng với loops 

- **Post condition** là điều kiện mà phải đúng sau khi một đoạn mã nào đó thực hiện xong 

- **Assertion** là một biểu thức đúng ngoại trừ khi có lỗi trong chương trình. Nếu biểu thức true, không có gì xảy ra. Nếu biểu thức false, tin nhắn lỗi hiển thị và `std::abort()` được gọi 
- Runtime assert có trong `<cassert>` và được dùng với `assert()` 
- Có cách để khiến cho assert cụ thể hơn bằng cách thêm string vào sau điều kiện với `&&`
```cpp
assert(gravity > 0.0);

assert(gravity > 0.0 && "Invalid gravity")
```
- Có thể disable toàn bộ assert với macro `#define NDEBUG`

- Trong C++ còn có assert trong thời điểm biên dịch, vì nó là keyword nên không cần header
```cpp
static_assert(gravity > 0.0, "Invalid gravity");
```

- Best practice: Ưu tiên `static_assert()` khi có thể 

- Assertions nên được dùng để kiểm tra/ ghi lại các trường hợp vô lý. Các trường hợp có thể xảy ra nên được xử lý qua các xử lý lỗi 