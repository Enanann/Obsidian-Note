
- **Implicit type conversion** (**automatic type conversion** hay **coercion**) được thực hiện khi một kiểu dữ liệu được mong đợi, nhưng một kiểu dữ liệu khác được cung cấp. Nếu compiler biết cách chuyển đổi giữa chúng thì sự chuyển đổi sẽ được thực hiện, nếu không sẽ báo lỗi 

- C++ định nghĩa một số kiểu chuyển đổi giữa các kiểu cơ bản -> **standard conversion**:
	- **Numeric promotion**: chuyển từ kiểu dữ liệu số nhỏ hơn lên kiểu dữ liệu số lớn hơn (thường là `int` hoặc `double`), đây là kiểu c huyển đổi **value-preserving** (không gây mất dữ liệu)
	- **Numeric conversion**: chuyển kiểu dữ liệu số không phải là numeric promotion. **Narrowing conversion** là numeric conversion có thể gây mất dữ liệu 
	- **Explicit type conversion**: Được thực hiện bởi người lập trình qua một cast 

| Cast             | Description                                                                                           | Safe?                 |
| ---------------- | ----------------------------------------------------------------------------------------------------- | --------------------- |
| static_cast      | Performs compile-time type conversions between related types                                          | Yes                   |
| dynamic_cast     | Performs runtime type conversions on pointers or references in an polymorphic (inheritance) hierarchy | Yes                   |
| const_cast       | Adds or removes const                                                                                 | Only for adding const |
| reinterpret_cast | Reinterprets the bit-level representation of one type as if it were another type                      | No                    |
| C-style casts    | Performs some combination of `static_cast`, `const_cast`, or `reinterpret_cast`                       | No                    |

- **Typedef** và **type aliases** cho phép tạo bí danh cho các kiểu dữ liệu 
```cpp
// identical
typedef long Miles;
using Miles = long; // preferred
```

- **Type deduction** (**type inference**) là chức năng cho phép compiler tự suy ra kiểu dữ liệu của biến dựa vào giá trị của nó, được dùng với từ khóa `auto` 
- Type deduction sẽ bỏ `const` nếu có, và cần phải được áp dụng lại `const auto x{y};` \

- Type deduction cho string sẽ cần phải thêm suffix `s` hoặc `sv` cho string_view qua `using std::string::literals`, nếu không sẽ có dạng `const char*` 

- `auto` cũng có thể được dùng với hàm, tuy nhiên kiểu giá trị trả về cần phải giống nhau
- `auto` còn có thể dùng cho cấu trúc **trailing return**, giúp dễ đọc/căn code hơn
```cpp
auto add(int x, int y) -> int;
auto divise(double x, double y) -> double;

auto someFunc() -> Complicated::Type {
	//...
}
```

