
- Trong function overloading, **overload resolution** là quá trình compiler tìm match tốt nhất của hàm khi không có exact match của đối số truyền vào (ưu tiên **numeric promotion** hơn **numeric conversion**)
- **Ambiguous match** xảy ra khi compiler tìm được 2 hay nhiều hàm có thể match với đối số được truyền vào và không thể quyết định được cái nào tốt nhất 

- Trong trường hợp chúng ta muốn hàm không thể thực hiện được với kiểu dữ liệu nhất định, có thể sử dụng `= delete`
```cpp
void printInt(int x) {
    std::cout << x << '\n';
}

void printInt(char) = delete; // calls to this function will halt compilation
void printInt(bool) = delete; // calls to this function will halt compilation
```

- Để xóa tất cả kiểu dữ liệu không phù hợp, có thể dùng cùng template
```cpp
void printInt(int x) {
	std::cout << x << '\n';
}

template <typename T>
void printInt(T x) = delete;
```

- **Default argument** là giá trị mặc định của một đối số của hàm, nó phải nằm ở bên phải cùng của hàm 

- **Function template** cho phép ta tạo một khuôn mẫu cho hàm với kiểu dữ liệu của tham số là generic
- Ta sử dụng **type template parameters** làm placeholder cho kiểu dữ liệu
- Cấu trúc của lệnh này gọi là **template parameter declaration**
- Quá trình tạo hàm với kiểu dữ liệu cụ thể từ khuôn mẫu là **function template instantiation** hay **instantiation**. Khi quá trình này xảy ra do gọi hàm, gọi là **implicit instantiation** 
- Hàm được tạo bởi quá trình trên là **function instance** hay **instance**, **template function**

- **Template argument deduction** cho phép compiler tự suy ra kiểu dữ liệu nên được dùng cho một instance của hàm. TAD không chuyển kiểu dữ liệu
```cpp
template <typename T>
void print(T x, T y) {
    std::cout << x << ' ' << y << '\n';
}

print(10, 2);           // ok
print(10, 2.5);         // error: int is not the same type as double
print<double>(10, 2.5); // ok, convert 10 to double
```

- Khi template chứa biến static có thể thay đổi, thì mỗi hàm được tạo từ template sẽ là một phiên bản khác nhau của biến static đó
```cpp
template <typename T>
void printIDAndValue(T value) {
	static int id{0};
	std::cout << ++id << ") " << value << '\n';
}

int main() {
	printIDAndValue(12);   // 1) 12
	printIDAndValue(13);   // 2) 13
	printIDAndValue(14.5); // 1) 14.5
}
```
- Do hàm kiểu int là 1 phiên bản, hàm kiểu double là 1 phiên bản


- Template đôi khi được gọi là **generic type**, và lập trình sử dụng template gọi là **generic programming**

- Nếu ta muốn forward declared hàm template, ta cần chỉ rõ kiểu trả về, giả sử hàm có 2 kiểu `T` và `U`, ta sẽ cần kiểu chung giữa chúng, có thể sử dụng `std::common_type_t` trong `<type_traits>`
```cpp
template <typename T, typename U>
auto max(T x, U y) -> std::common_type_t<T, U>;

int main() {
	//...
	return 0;
}

template <typename T, typename U>
auto max(T x, U y) -> std::common_type_t<T, U> {
	return (x > y) ? x : y;
}
```

- C++20 cung cấp thêm chức năng mới cho `auto`, khi được dùng cho parameter của hàm, compiler sẽ tự động template hóa hàm đó, cách này gọi là **abbreviated function template**
```cpp
auto max(auto x, auto y) {
    return (x < y) ? y : x;
}
```
là rút gọn C++20 của
```cpp
template <typename T, typename U>
auto max(T x, U y) {
    return (x < y) ? y : x;
}
```
- Best practice: Thoải mái dùng AFT với parameter đơn, hay với khi mỗi parameter nên là một kiểu riêng biệt 

- Function template cũng có thể được overload 

- **Non-type template parameters** là template parameter với kiểu dữ liệu cố định, đóng vai trò là placeholder cho constexpr được truyền vào dưới dạng template argument. Thường để tên là `N`
```cpp
template <int N> // declare a non-type template parameter of type int named N
void print() {
    std::cout << N << '\n'; // use value of N here
}
```
- Có thể thích hợp để dùng với `static_assert()` 
```cpp
template<int N>
class Buffer {
    static_assert(N % 16 == 0,
                  "Buffer size must be multiple of 16");
};
```

- C++17, `auto` cũng có thể được dùng để compiler tự suy ra kiểu dữ liệu của non-template parameter 

- Để dùng template trong nhiều file khác nhau, có thể định nghĩa luôn template trong header file do template không vi phạm ODR 