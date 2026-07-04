
- **Program-defined types** (cũng được gọi là **user-defined types**) là kiểu dữ liệu tùy chỉnh do người lập trình tạo ra 
- Định nghĩa của một program-defined type gọi là **type definition**, cái này được miễn trừ một phần trong ODR, cụ thể là một kiểu xác định có thể được định nghĩa trong nhiều file 

- Best practice:
	- Khi dùng program-defined type trong một file, định nghĩa nó gần nơi dùng đầu tiên nhất có thể
	- Khi muốn dùng trong nhiều file, tạo một header file chứa định nghĩa và include nó khi cần 

- **Enumerations** hay **enumerated type**/**enum** là kiểu dữ liệu mà giá trị của chúng được giới hạn bởi tập các hằng tên gọi là **enumerators**

- **Unscoped enum** đặt các enumerators của nó vào cùng scope với nơi định nghĩa enum, dễ dẫn đến naming collision, cũng như làm ô nhiễm scope đó. Unscoped enumeration sẽ chuyển đổi ngầm sang số nguyên (bắt đầu từ 0)
- Thông thường thì unscoped enum sẽ có độ lớn bằng int, ta có thể đặt tùy chỉnh kiểu của nó
```cpp
enum Color : long {
	//...
};
```

- Unscoped enum không **type safe**
```cpp
enum Color {
	red,     // 0
};
enum Fruit {
	banana,  // 0
};

int main() {
	Color c{red};
	Fruit f{banana};
	
	if (c == f) { // true 
		//...
	}
}
```

- Giải pháp là dùng scoped enumeration
- **Scoped enumeration**, hay **enum class** hoạt động giống như unscoped enum, nhưng mà các enumerators sẽ ở trong scope của enum, và các enumerators sẽ không tự động chuyển qua kiểu số nguyên 
```cpp
enum class Color {
	red,
	green,
	blue,
}
```
- Thay vì có thể truy cập trực tiếp, ta sẽ cần dùng `::` 

- Trong C++20, ta có thể đưa enum class vào scope đang dùng với `using enum Name;`, giúp tránh việc phải ghi đi ghi lại nhiều lần e.g. trong switch

- **Struct** là program-defined data type cho phép ta gộp nhiều các biến khác nhau vào cùng 1 kiểu dữ liệu. Các biến trong struct là **data members**
- Để truy cập biến thành viên, sử dụng **member selection operator** `.` cho struct, hoặc **member selection from pointer operator** `->` cho pointer đến struct 

- Trong lập trình nói chung, **aggregate data type** (hay **aggregate**) là kiểu dữ liệu gồm nhiều các biến thành viên. Trong C++, array và struct chỉ gồm biến thành viên là **aggregates** 
- Để khởi tạo aggregate, sử dụng **aggregate initialization**, cho phép ta trực tiếp khởi tạo các biến thành viên
```cpp
struct Employee {
	int id{};
	int age{};
	double wage{};
}

int main() {
	Employee mixi{1, 36, 0};    // preferred 
	Employee namx = {2, 30, 0};
}
```

- Nếu bị thiếu đối số:
	- Nếu biến thành viên có giá trị mặc định -> dùng nó
	- Nếu không,  sẽ được sao chép từ danh sách khởi tạo rỗng, thường sẽ là khởi tạo giá trị (value-initialized), trong kiểu class sẽ là hàm khởi tạo mặc định 

- C++20 thêm tính năng **designated initializer**, cho phép ta chọn biến thành viên nào sẽ được khởi tạo (phải theo thứ tự)
```cpp
struct Test {
	int a{};
	int b{};
	int c{};
};

int main() {
	Test t{.a{3}, .c{6}};    // ok
	Test t1{.a = 3, .c = 6}; // ok
	Test t2{.c{6}, .a{3}};   // not ok 
}
```

- Các trường hợp giá trị mặc định của biến thành viên (**non-static member initialization**)
```cpp
struct Something {
    int x;       // no default initialization value (bad)
    int y {};    // value-initialized by default
    int z { 2 }; // explicit default value
};

int main() {
	// No initializer list: s1.x is uninitialized, s1.y and s1.z use defaults
    Something s1;
    
    // Explicit initializers: s2.x, s2.y, and s2.z use explicit values (no default values are used)
    Something s2 { 5, 6, 7 };     
    
    // Missing initializers: s3.x is value initialized, s3.y and s3.z use defaults
    Something s3 {};          

    return 0;
}
```

- Vì lý do hiệu năng, compiler đôi khi sẽ thêm các khoảng trống vào cấu trúc (**padding**), do đó kích thước của một cấu trúc có thể lớn hơn tổng kích thước của các thành viên của nó

- **Class template** là định nghĩa template cho tạo các kiểu class
- **Class template argument deduction** (CTAD) là chức năng ở C++17, cho phép compiler tự suy ra kiểu của argument ở giá trị khởi tạo 


- Để **operator overloading**:
	- Định nghĩa function với tên của hàm là tên của toán tử
	- Thêm param của kiểu toán hạng (trái sang phải). Phải có 1 kiểu là user-defined, nếu không sẽ lỗi compile 
	- Đặt kiểu trả về phù hợp
	- Sử dụng return để trả về 