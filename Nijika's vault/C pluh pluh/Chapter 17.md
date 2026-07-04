
# `std::array`

- Khác với `std::vector`, `std::array` là mảng tĩnh (**fixed-length array**). Tức là độ dài của mảng đó phải được biết tại thời điểm khởi tạo 
- C-style array cũng là mảng tĩnh 
- Chính vì là mảng tĩnh nên `std::array` có hỗ trợ đầy đủ của constexpr 
- Best practice: Dùng `std::array` cho mảng constexpr, `std::vector` cho mảng non-constexpr 

- Định nghĩa array với `std::array<type, size_t>` 
- `size_t` phải là một constant expression, tức là không dùng với cin được 
- Array có thể khởi tạo với độ lớn 0 -> undefined 
- Khác với vector, array là **aggregate**, tức là nó không có hàm khởi tạo

- Trong C++17, CTAD có hỗ trợ cho `std::array`
```cpp
constexpr std::array a1 { 9, 7, 5, 3, 1 }; // deduced to std::array<int, 5>
constexpr std::array a2 { 9.7, 7.31 };     // deduced to std::array<double, 2>
```
- CTAD **không hỗ trợ bỏ một phần** e.g. `<int>`, `<5>`

- Ta có thể bỏ qua phần độ dài của mảng trong C++20 nhờ TAD (template argument deduction) với `std::to_array`
```cpp
constexpr auto myArray1 { std::to_array<int, 5>({ 9, 7, 5, 3, 1 }) }; 
// Specify type and size

constexpr auto myArray2 { std::to_array<int>({ 9, 7, 5, 3, 1 }) };    
// Specify type only, deduce size

constexpr auto myArray3 { std::to_array({ 9, 7, 5, 3, 1 }) };         
// Deduce type and size
```
- Tuy nhiên `std::to_array` tốn kém hơn tạo `std::array` trực tiếp -> Chỉ nên dùng khi kiểu dữ liệu không thể được xác định một cách hiệu quả từ các giá trị khởi tạo, hoặc khi dùng trong vòng lặp để tạo nhiều mảng 
- Ví dụ khi muốn tạo mảng short -> không có hậu tố để chỉ riêng như LL, s, sv -> nếu là `std::array<short, 4>` thì kiểu int trong sẽ bị narrow conversion 
```cpp
constexpr auto shortArray{std::to_array<short>({1, 3, 5, 7, 9})};
```

- Để lấy độ lớn của array: 
	- `.size()`: trả về `size_type` (alias của `std::size_t`)
	- `std::size()`: trả về `size_type` (gọi `.size()`)
	- `std::ssize()`: trả về large signed integral (C++20), thường là `std::ptrdiff_t`

- Do array hỗ trợ constexpr, có thể dùng 3 hàm trên trong constant expression 

- Để lấy một thành phần:
	- `[]`: Không bound checking
	- `.at()`: Bound checking trong runtime
	- `std::get<index>()`: Bound checking trong compile time (nếu ta có index là constexpr)

- Khi muốn pass array vào hàm, phải chỉ rõ cả kiểu dữ liệu và số thành phần
```c++
void passByRef(const std::array<int, 5>& arr) {
    //...
}
```
- CTAD không hoạt động với tham số của hàm, vì thế nếu muốn chấp nhận mọi kiểu cũng như mọi độ dài thì nên tạo template
```c++
template <typename T, std::size_t N>
void passByRef(const std::array<T, N>& arr) {
    static_assert(N != 0);
	//...
}
```
- C++20 có thể thay `std::size_t` thành `auto`

- `std::array` không **move-capable** được như `std::vector`, nên vì thế khi trả về `std::array`:
	- Có thể trả về theo giá trị nếu: mảng không lớn, kiểu dữ liệu rẻ để copy, code không yêu cầu hiệu năng cao
	- Có thể sử dụng out parameter, tức là pass array vào theo reference
	- Trả về `std::vector` (do nếu bạn muốn trả về `std::array` thì thà dùng vector còn hơn)

- Khi làm việc với struct trong array 
```c++
struct House {
	int number{};
	int stories{};
	int roomsPerStory{};
};

constexpr House h1{13, 2, 6};
constexpr House h2{14, 3, 5};
constexpr House h3{36, 36, 36};
constexpr std::array<House, 3> houses{h1, h2, h3};

constexpr std::array houses { // use CTAD to deduce template arguments <House, 3>
            House{ 13, 1, 7 },
            House{ 14, 2, 5 },
            House{ 15, 2, 4 }
        };
```
- Nếu ta muốn khai báo dạng này
```c++
constexpr std::array<House, 3> houses { // we're telling the compiler that each element is a House
        { 13, 1, 7 }, // but not mentioning it here
        { 14, 2, 5 },
        { 15, 2, 4 }
    };
```
- Cái này sẽ gây lỗi do array trong C++ có dạng là 1 struct với thành viên là 1 C-style array
```cpp
template<typename T, std::size_t N>
struct array {
    T implementation_defined_name[N]; //a C-style array with N elements of type T
}
```
- Vì thế nên thực tế để khai báo một array phải làm như sau
```cpp
std::array arr{{1, 2, 3}};
```
- Một `{}` để cho bản thân array, một `{}` để cho c-style array ở trong 

- Tuy nhiên C++ có thêm khái niệm là **brace elision**, giúp tránh phải **double braces** trong mọi trường hợp
- Thông thường, có thể bỏ một cặp `{}` khi giá trị là đơn (**single/scalar**), hoặc khi bạn nói rõ kiểu đối với từng thành viên 

- Ta không thể tạo mảng gồm các tham chiếu do bản chất của tham chiếu nó không phải là một đối tượng độc lập, nó chỉ là bí danh 
- Để tạo một array gồm các tham chiếu -> sử dụng `std::reference_wrapper` từ thư viện `<functional>` 
	- Lấy một tham số template T và nó hoạt động như là một tham chiếu lvalue của T 
	- `=` sẽ reseat một `std::reference_wrapper` (như là 1 pointer)
	- `std::reference_wrapper<T>` sẽ ngầm chuyển đổi thành `T&`
	- Hàm thành viên `get()` có thể được sử dụng để lấy `T&`. Điều này hữu ích khi chúng ta muốn cập nhật giá trị của đối tượng được tham chiếu.
```cpp
#include <array>
#include <functional> // for std::reference_wrapper
#include <iostream>

int main() {
    int x { 1 };
    int y { 2 };
    int z { 3 };
    
    std::array<std::reference_wrapper<int>, 3> arr { x, y, z };
    
    arr[1].get() = 5; // modify the object in array element 1
    
    std::cout << arr[1] << y << '\n'; 
	// show that we modified arr[1] and y, prints 55
    return 0;
}
```

- Trước C++17, chưa có CTAD nên phải tạo thủ công 
```cpp
std::reference_wrapper<int> ref{x};
```
- `std::ref()`, `std::cref()` được đưa vào là shortcut để tạo `std::reference_wrapper` hoặc `const std::reference_wrapper`  
```cpp
int x { 5 };

// C++11
std::reference_wrapper<int> ref{x};

auto ref{std::ref(x)};   // C++11, deduces to std::reference_wrapper<int>
auto cref{std::cref(x)}; // C++11, deduces to std::reference_wrapper<const int>

std::reference_wrapper ref1{x};        // C++17
auto ref2 {std::reference_wrapper{x}}; // C++17
```

- Dùng `static_assert` để kiểm tra constexpr array có valid hay không 

# C-style array

- C-style array là được thừa hưởng từ C, và được build vào phần lõi của C++ 
- Để khai báo C-style array
```cpp
int arr[5]; // array of 5 int values
```
- Độ lớn của C-style array phải là constant expression, mặc dù một số compiler cho phép array với non-constant expression length vì lí do tương thích với tính năng của C99 là **VLAs** - variable-length array => Không đúng với chuẩn C++
- C-style array là aggregate -> có thể khởi tạo dùng aggregate initialization 

- Best practice: Ưu tiên bỏ trống phần độ dài khi khởi tạo C-style array với mọi thành phần có giá trị
```cpp
const int prime1[5] {2, 3, 5, 7, 11};
// the same
const int prime2[] {2, 3, 5, 7, 11};
```

- Để lấy độ dài của C-style array:
	- C++17, dùng `std::size()`, trả về độ dài unsigned `std::size_t`
	- C++20, dùng `std::sszie()`, trả về độ dài signed, thường là `std::ptrdiff_t`

- C-style array không hỗ trợ assignment sang một C-style array khác, assignment cho thành viên thì được
```cpp
int arr[] {1, 2, 3};

arr[0] = 36;          // ok
arr = {5, 6, 7};      // compile error
```
- Không được vì gán yêu cầu vế trái là modifiable lvalue, C-style array không được coi là modifiable lvalue

- Nên dùng `std::vector` nếu muốn gán danh sách giá trị mới cho C-style array. Ngoài ra, có thể gán giá trị mới cho C-style array theo từng thành phần, hoặc dùng `std::copy` trong `<algorithm>`
```cpp
int arr[] {1, 2, 3};
int src[] {4, 5, 6};

// Copy src into arr
std::copy(std::begin(src), std::end(src), std::begin(arr));
```

- Trong hầu hết trường hợp, khi C-style array được sử dụng trong một biểu thức, nó sẽ bị ngầm chuyển thành pointer của kiểu dữ liệu của nó, được khởi tạo với giá trị của thành phần đầu tiên (index 0), cái này gọi là **array decay**
```cpp
// can also do const int* arr instead (not preffered!)
void printElementZero(const int arr[]) { 
	std::cout << arr[0];
}

int main() {
	const int prime[] {2, 3, 5, 7, 11};
	
	printElementZero(prime); // decay to const int* pointer 
}
```

- Một số trường hợp không bị decay:
	- Dùng là đối số của `sizeof()` hay `typeid()`
	- Lấy địa chỉ bằng `&`
	- Pass như là thành viên của kiểu class
	- Pass theo reference 

```cpp
void printArraySize(int arr[]) {
    std::cout << sizeof(arr) << '\n'; // prints 4 (assuming 32-bit addresses)
}

int main() {
    int arr[]{ 3, 2, 1 };
    std::cout << sizeof(arr) << '\n'; // prints 12 (assuming 4 byte ints)
    printArraySize(arr);
    return 0;
}
```

- Best practice:
	- Ưu tiên `std::string_view` cho xâu chỉ đọc (string literal có tên và tham số xâu)
	- Ưu tiên `std::string` cho xâu có thể thay đổi
	- Ưu tiên `std::array` cho non-global constexpr arrays
	- Ưu tiên `std::vector` cho non-constexpr arrays

- Trong C++ hiện đại, C-style array thường được dùng trong
	- Dùng để lưu dữ liệu constexpr global (hoặc constexpr static local). Do có thể truy cập trực tiếp ở bất cứ đâu + indexing không bị vấn đề chuyển đổi dấu 
	- Như là tham số cho hàm hoặc lớp muốn sử dụng trực tiếp non-constexpr C-style string (do chuyển đổi đi chuyển đổi lại giữa `std::string_view` để dùng hàm của C-style string tốn tài nguyên)

- **Pointer arithmetic** là tính năng cho phép ta thực hiện một số phép toán số nguyên nhất định (addtion, subtraction, increment, hoặc decrement) lên một pointer để sinh ra địa chỉ bộ nhớ mới
- Cho một pointer `ptr`, `ptr + 1` sẽ trả về địa chỉ bộ nhớ của object tiếp theo trong bộ nhớ (dựa vào kiểu dữ liệu của `ptr`) 

- Đối với C-style array, subscripting `[]` và sử dụng phép toán lên pointer là như nhau (subscripting được triển khai qua phép toán pointer)
```cpp
const int arr[] {1, 2, 3, 4, 5, 6};
const int* ptr{arr};

std::cout << arr[1];  // 2
std::cout << ptr + 1; // 2

// ptr[n] = *((ptr) + (n))
```

- Khi dùng increment `++` hay decrement `--`, nó sẽ làm thay đổi địa chỉ của pointer đó -> dễ lỗi out-of-bound hay là mất địa chỉ gốc
```cpp
++x;    // x   = x + 1
++ptr;  // ptr = ptr + 1
```

- Best practice:
	- Ưu tiên subscripting khi indexing từ thành phần đầu tiên của array (index 0)
	- Ưu tiên pointer arithmetic khi làm việc với vị trí tương đối của một phần tử xác định 

- C-style string chính là C-style array mà thành phần nó là `char` hoặc `const char` -> sẽ decay 

