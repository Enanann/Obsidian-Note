
- **Compound data type** là kiểu dữ liệu gồm nhiều kiểu dữ liệu khác (có thể cơ bản hoặc compound hoặc cả hai)
- Các kiểu compound:
	- Functions
	- C-style arrays e.g. `int* arr[100];`
	- Pointer type:
		- Pointer sang object
		- Pointer sang function 
	- Pointer sang thành viên
		- Pointer sang biến thành viên
		- Pointer sang hàm thành viên 
	- Reference
		- L-value ref
		- R-value ref
	- Enumerated type
		- Unscoped enumerations
		- Scoped enumerations
	- Class types:
		- Struct
		- Class
		- Union

- Tất cả các expression trong C++ có 2 phần: type và value 
	- Type là kiểu của dữ liệu, hàm, hay đối tượng kết quả của biểu thức
	- Value chỉ rằng biểu thức trả về một giá trị, hàm, hay đối tượng 

- Value category bao gồm 5 loại: `lvalue`, `rvalue`, `glvalue`, `prvalue`, `xvalue` 

- **lvalue** là một biểu thức được tính toán thành một đối tượng hoặc hàm có thể xác định được
- lvalue lại được phân thành 2 loại: **modifiable lvalue** và **non-modifiable lvalue** 
```cpp
int main() {
    int x{};
    const double d{};

    int y{x}; // x is a modifiable lvalue expression
    const double e{d}; // d is a non-modifiable lvalue expression

    return 0;
}
```

- **rvalue** là biểu thức mà không phải là lvalue, tức là nó là một biểu thức mà được tính toán ra một giá trị. Thường là các literal (ngoại trừ C-style string, nó là lvalue). Không xác định được rvalue, và nó chỉ tồn tại trong scope của biểu thức
```cpp
int return5() {
    return 5;
}

int main() {
    int x{5}; // 5 is an rvalue expression
    const double d{1.2}; // 1.2 is an rvalue expression

    int y{x}; // x is a modifiable lvalue expression
    const double e{d}; // d is a non-modifiable lvalue expression
    int z{return5()}; // return5() is an rvalue expression (since the result is returned by value)

    int w{x+1}; // x + 1 is an rvalue expression
    int q{static_cast<int>(d)}; // the result of static casting d to an int is an rvalue expression

    return 0;
}
```

- lvalue có thể chuyển đổi ngầm sang rvalue, trái lại rvalue không thể chuyển đổi ngầm qua lvalue 

- **Reference** là bí danh cho một object đang tồn tại. Về bản chất, reference giống hệt với object được tham chiếu

- **lvalue reference** (thường chỉ là **reference**) hoạt động như là tham chiếu của một lvalue (như là biến) 
- Reference không thể được **reseated**, tức là chuyển đối tượng mà nó đang tham chiếu đến 

- Vì lvalue reference chỉ tham chiếu đến được với modifiable lvalue, nên khi muốn tạo tham chiếu đến non-modifiable lvalue, ta cần thêm `const` vào trước ref -> **lvalue reference to const**. Nó sẽ coi object đang được reference đến là const 
- lvalue reference to const có thể được bind với một rvalue, lúc này mmoojt object tạm thời sẽ được tạo với rvalue đó, và ref sẽ được gắn với object tạm thời đó. Việc này đồng nghĩa là lvalue ref to const giúp **kéo dài thời gian sống** của object tạm thời 
- lvalue reference to const cũng có thể được bind với các kiểu dữ liệu khác, miễn là chúng có thể chuyển đổi ngầm qua kiểu dữ liệu của ref. Lúc này thì ref đó sẽ tham chiếu đến object tạm thời, chứ không phải object gốc
```cpp
short x{1};
const int& ref{x};
--x;
std::cout << ref << '\n'; // print 1;
```

- Bởi vì một số kiểu dữ liệu sẽ tốn nhiều tài nguyên khi copy e.g. `std::string`, thay vì pass by value thì ta có thể **pass by reference** 
- Pass by reference có thể thay đổi biến được pass vào, vì thế nên chỉ chấp nhận lvalue có thể thay đổi được

- Như đã nói ở trên, nếu muốn có thể cho mọi kiểu dữ liệu vào thì dùng **pass by const reference** 
- Best practice: Ưu tiên pass by const reference trừ khi ta cần thay đổi giá trị biến pass vào 

- Best practice: Ưu tiên pass `std::string` theo `std::string_view` thay vì `const std::string&`, trừ khi bạn cần làm việc với kiểu `std::string` 

- **Toán tử address-of** `&` trả về địa chỉ bộ nhớ của một toán hạng
- **Toán tử dereference** `*` trả về giá trị của một bộ nhớ như là 1 lvalue 

- **Pointer** là object chứa địa chỉ bộ nhớ (thường là của một biến) làm giá trị của nó. Pointer mà chưa được khởi tạo là **wild pointer**. Pointer chứa địa chỉ của một biến đã bị hủy là **dangling pointer** 
- Ngoài địa chỉ bộ nhớ, pointer có một giá trị đặc biệt là **null**. Khi pointer chứa giá trị là null, tức là nó đang không trỏ đến cái gì cả, gọi là **null pointer** - `nullptr` 
- Ta chỉ có thể kiểm tra một pointer có phải là nullptr hay không, chứ không kiểm tra được xem nó có đang trỏ đến một object hợp lệ hay không 

- Các loại pointer:
	- **Non-const pointer**: Có thể thay đổi địa chỉ nó đang chỉ đến e.g. `int* ptr`
	- **Const pointer**: Không thể thay đổi địa chỉ nó đang chỉ đến e.g. `int* const ptr`
	
	- **Pointer to non-const**: Có thể thay đổi giá trị của biến đang chỉ đến e.g. `int* ptr`
	- **Pointer to const**: Không thể thay đổi giá trị biến đang chỉ đến e.g. `const int* ptr`
- **Const pointer to const**: Không thể thay đổi giá trị của biến đang chỉ đến, cũng như địa chỉ đang chỉ đến e.g. `const int* const ptr` 

- **Pass by address** là cung cấp cho hàm địa chỉ của đối tượng qua pointer thay vì object, nó sẽ tạo bản sao của address thay vì bản sao của object (luôn nhanh)
```cpp
#include <iostream>
#include <string>
// The function parameter is a copy of str
void printByValue(std::string val)  {
    std::cout << val << '\n'; // print the value via the copy
}

// The function parameter is a reference that binds to str
void printByReference(const std::string& ref) {
    std::cout << ref << '\n'; // print the value via the reference
}

// The function parameter is a pointer that holds the address of str
void printByAddress(const std::string* ptr) {
    std::cout << *ptr << '\n'; // print the value via the dereferenced pointer
}

int main() {
    std::string str{ "Hello, world!" };

    printByValue(str); // pass str by value, makes a copy of str
    printByReference(str); // pass str by reference, does not make a copy of str
    printByAddress(&str); // pass str by address, does not make a copy of str

    return 0;
}
```

- Best practice: Ưu tiên pass by (const) reference hơn pass by address 

- Vì pass by address là copy địa chỉ, nếu ta muốn hàm thay đổi địa chỉ con trỏ đang trỏ đến, cần **pass by address by reference**
```cpp
void nullify(int*& ptr2) {
	ptr2 = nullptr;
} 

int main() {
	int x{6};
	int* ptr{&x};
	
	nullify(ptr)
}
```

- **Return by reference** trả về một tham chiếu được gắn với object trả về -> tránh tạo bản sao của object được trả về
- Tuy nhiên việc này cần đảm bảo rằng object được trả về phải **outlive** hàm trả về đó, nếu không tham chiếu trả về sẽ là dangling, gây undefined behaviour 
- Best practice: Tránh trả về reference cho biến cục bộ non-const static 

- Nếu kết quả của return by reference được dùng để khởi tạo một biến không phải reference, thì copy sẽ được tạo 
```cpp
const int& getNextId() {
    static int s_x{ 0 };
    ++s_x;
    return s_x;
}

int main() {
    const int id1 { getNextId() }; // id1 is a normal variable now and receives a copy of the value returned by reference from getNextId()
    const int id2 { getNextId() }; // id2 is a normal variable now and receives a copy of the value returned by reference from getNextId()

    return 0;
}
```

- **Return by address** y hệt return by reference nhưng địa chỉ được trả về thay vì tham chiếu

- Tương tự với const, type deduction sử dụng `auto` sẽ bỏ reference hoặc là bỏ top-level const từ kiểu được suy ra, có thể được áp đặt lại trong khai báo 
	- **Top-level const**: Const áp dụng cho object e.g. `const int x`, const được áp dụng vào `x` 
	- **Low-level const**: Const áp dụng cho object được tham chiếu hoặc trỏ đến e.g. `const int* x`, const được áp dụng vào object được chỉ đến, chứ không phải chính pointer đó 

- Khác với reference, type deduction sẽ không bỏ pointer, có thể dùng `auto*` để dễ đọc hơn nó là dạng pointer
```cpp
#include <string>

std::string* getPtr(); // some function that returns a pointer

int main() {
    auto ptr1{ getPtr() };  // std::string*
    auto* ptr2{ getPtr() }; // std::string*

    return 0;
}
```

- `std::optional<T>` có thể có kiểu `T` hoặc không có (`std::nullopt`). Được dùng cho những hàm có thể không trả về giá trị e.g.
```cpp
double divise(double x, double y) {
	if (y == 0) {
		return 0.0;
	}
	return x / y;
}
```
- Tuy nhiên cái trên thì có thể trả về mọi giá trị được, nếu x=0 thì trả về 0 -> ambiguous, tức là không phân biệt được trừ khi biết test case 
- Có thể dùng `std::optional`
```cpp
std::optional<double> divise(double x, double y) {
	if (y == 0) {
		return {}; // or return std::nullopt;
	}
	return x / y;
}
```

- Để kiểm tra xem có giá trị hay không dùng `.has_value()`
- Để xem giá trị, dereference hoặc `.value()`

| Behavior           | Pointer                                  | `std::optional`                              |
| ------------------ | ---------------------------------------- | -------------------------------------------- |
| Hold no value      | initialize/assign `{}` or `std::nullptr` | initialize/assign `{}` or `std::nullopt`     |
| Hold a value       | initialize/assign an address             | initialize/assign a value                    |
| Check if has value | implicit conversion to bool              | implicit conversion to bool or `has_value()` |
| Get value          | dereference                              | dereference or `value()`                     |

- Tuy nhiên `std::optional` không có cách để trả về nguyên nhân cụ thể tại sao hàm fail

- Để khắc phục khuyết điểm trên, có thể dùng `std::expected<T, E>` (C++23)
```cpp
enum class Error {
    NotFound,
    OutOfMemory,
    InvalidFormat
};

std::expected<int, Error> loadValue() {
    if (fail)
        return std::unexpected(Error::NotFound);
    return 42;
}
```