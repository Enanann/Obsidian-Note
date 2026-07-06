
- Trong tất cả các hàm thành viên non-static, từ khóa `this` là const pointer chứa địa chỉ của implicit object hiện tại 
- Giả sử có class như sau
```cpp
class Foo {
public:
	void setID(int id) {
		m_id = id;
	}

private:
	int m_id{};
};

int main() {
	Foo f{};
}
```
- Khi ta gọi `f.setID(2)`, compiler sẽ viết lại lời gọi hàm là `Foo::setID(&f, 2)` 
- Hàm thành viên `setID` cũng sẽ được viết lại (tùy cách implement), nhưng thường sẽ có dạng
```cpp
static void setID(Foo* const this, int id) {
	this->m_id = id;
}
```

- Có thể để hàm trả về `*this` theo reference để thực hiện **method chaining**, khi mà nhiều hàm thành viên có thể được gọi trong một expression duy nhất 
```cpp
class Calc {
public:
    Calc& add(int value) { m_value += value; return *this; }
    Calc& sub(int value) { m_value -= value; return *this; }
    Calc& mult(int value) { m_value *= value; return *this; }

    int getValue() const { return m_value; }
};

private:
    int m_value{};

// main
Calc c{};
c.add(5).sub(2).mul(2);
```

- Như ta đã biết là không nên gọi hàm khởi tạo trong hàm thành viên, một cách để reset lại object là tạo một hàm thành viên tạo một object mới (dùng hàm khởi tạo mặc định) và gán nó vào object hiện tại
```cpp
void reset() {
	*this = {};
}
```

- Về cách chia class vào header và source file:
	- Định nghĩa class trong header file, các hàm cơ bản (như getter, setter, hàm khởi tạo với phần thân trống) có thể định nghĩa luôn trong header file
	- Định nghĩa các hàm không cơ bản khác trong source file cùng tên với header file 
```cpp
//Foo.h
#pragma once
#include <iostream>
Foo {
public:
	void print() const; // one line function can be defined here instead!

private:
	int m_x{};
};

//Foo.cpp
#include "Foo.h"

void Foo::print() const {
	std::cout << m_x << '\n';
}
```

- Member function định nghĩa trong class mặc định là inline để được ngoại lệ khỏi ODR 
- Member function định nghĩa ngoài class không được mặc định là inline. Vì thế nên chúng thường được định nghĩa trong code file -> chỉ tạo 1 translation unit 
- Tương ứng, member function định nghĩa ngoài class có thể được để vào header file nếu chúng được làm `inline` (dùng từ khóa `inline`)

- Kiểu dữ liệu được định nghĩa trong class type là **nested type** (**member type**). Type aliases cũng có thể được nested 
- Nested type sẽ không thể truy cập con trỏ `this` của class ngoài, tuy nhiên nó có thể truy cập trực tiếp các biến thành viên private của class ngoài (qua việc pass by reference)

- Ngược với hàm khởi tạo, có **destructor** (hàm hủy) -> Tự động chạy khi đối tượng bị phá hủy:
	- Phải có cùng tên với lớp, bắt đầu bằng `~`
	- Không có tham số
	- Không có kiểu trả về
	- Mỗi lớp chỉ có 1 hàm hủy
- Lưu ý: Với `std::exit()` -> hàm hủy sẽ không được gọi

- **Static member variables** là biến được chia sẻ bởi tất cả object của một class
- Static member variables không liên quan đến class object, bản chất nó chỉ là một biến global trong phạm vi scope của class đó => Truy cập bằng scope là tên class + `::`
- Do bản chất là biến global, phải định nghĩa ở ngoài lớp. Tuy nhiên, C++17 cho phép ta định nghĩa nó trong định nghĩa lớp nếu ta đặt nó là `inline` hoặc `constexpr` (Best practice)

- **Static member function** là hàm thành viên có thể được gọi mà không cần object. Chúng không có con trỏ `*this`, và cũng không thể truy cập dữ liệu non-static 
- Cũng có thể hiểu nó chỉ là ở trong phạm vi của class đó, gọi với `Class::func()` hoặc `obj.func()` dù hàm không liên quan đến obj đó 

- Trong phần thân class, **friend declaration** dùng từ khóa `friend` để nói với compiler rằng class hoặc function khác (member hoặc non-member, dù member không có tác dụng gì khi thêm vào) là friend
- Trong C++, **friend** là hàm hoặc lớp đã được cho phép để truy cập đầy đủ đến các biến thành viên private hay protected của lớp khác 
```cpp
class Storage {
//...
	friend class Display;
};

class Display {
//...
};
```
- Class Display sẽ không truy cập được `this` của đối tượng của Storage
- Friend không có tính chất qua lại cũng như bắc cầu, như trên thì Storage không là bạn của Display 

- Best practice: Ưu tiên non-friend function khi có thể và hợp lý 

- **Ref-qualifier**: Dùng để overload cho trường hợp implicit object là lvalue hay rvalue







