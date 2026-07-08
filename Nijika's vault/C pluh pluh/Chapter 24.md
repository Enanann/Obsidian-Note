
- **Inhertance** (Thừa kế) trong C++ xảy ra ở giữa các lớp (is-a). Lớp được thừa kế từ gọi là **parent class, base class** hay **superclass**. Và lớp thừa kế được gọi là **child class, derived class** hay **subclass** 

- Lớp con thừa kế cả biến thành viên và hàm thành viên từ lớp cha (trừ một số trường hợp ngoại lệ)
- Syntax cho lớp B kế thừa public lớp A (**public inheritance**)
```cpp
class A {
public:
	int m_a{};
	
	A(int a = 0) : m_a{a} {}
};

class B : public A {
public:
	double m_b{};
	
	B(double b = 0.0) : m_b{b} {}
};
```

- Lúc này, thay vì các thành viên của lớp A được sao chép vào lớp B, lớp B sẽ được chia thành 2 phần: một phần A và một phần B
- Khi khởi tạo sẽ theo thứ tư sau: Đi từ lớp cha nhất xuống lớp con nhất  
```cpp
A a; 
// initializing A

B b; 
// initializing A
// initializing B
```

- Khi khởi tạo lớp B `B b{3.6}`
	1. Bộ nhớ đủ cho cả A và B được cấp phát
	2. Hàm khởi tạo phù hợp cho B được gọi 
	3. Lớp A được khởi tạo trước sử dụng hàm khởi tạo phù hợp, nếu không có thì dùng hàm mặc định 
	4. Member initializer list khởi tạo biến thành viên
	5. Phần thân hàm khởi tạo thực hiện
	6. Quyền điều khiển được chả về cho caller

- C++ không cho phép khởi tạo biến thành viên thừa kế trong member initializer list (đề phòng trường hợp là const hoặc tham chiếu), nên không thể
```cpp
class B : public A {
public:
	double m_b{};
	
	B(double b = 0.0, int id = 0) 
		: m_b{b}
		, m_a{id}
	{}
}
```
- Ta sẽ cần gọi hàm khởi tạo của A trong member initializer list
```cpp
class B : public A {
public:
	double m_b{};
	
	B(double b = 0.0, int id = 0) 
		: A{id}
		, m_b{b}
	{}
}
```
- Giờ các biến thành viên có thể được cho là private 

- Khi lớp thừa kế bị hủy, các hàm hủy sẽ được gọi theo thứ tự ngược lại với thứ tự khởi tạo, cụ thể
```cpp
// initialize A
// initialize B
// destroy B
// destroy A
```

- Lưu ý, nếu lớp cha có virtual functions, hàm hủy cũng nên là virtual, nếu không có thể xảy ra ub (undefined behaviour) trong một số trường hợp nhất định

- **Access specifier** (Chỉ định truy cập)
	- `public`: Có thể được truy cập bởi mọi đối tượng
	- `protected`: Có thể được truy cập bởi lớp chính, friends, và các lớp con
	- `private`: Chỉ có thể được truy cập bởi lớp chính và friends 

- Các loại inheritance
```cpp
// Inherit from Base publicly
class Pub: public Base {
};

// Inherit from Base protectedly
class Pro: protected Base {
};

// Inherit from Base privately
class Pri: private Base {
};

// Defaults to private inheritance
class Def: Base {
};
```
- Chỉ định truy cập của lớp gốc có thể thay đổi tùy thuộc vào các loại kế thừa (chỉ phiên bản trong lớp con, chứ lớp gốc không thay đổi)

| Access specifier in base class | Access specifier when inherited publicly |
| ------------------------------ | ---------------------------------------- |
| Public                         | Public                                   |
| Protected                      | Protected                                |
| Private                        | Inaccessible                             |

|Access specifier in base class|Access specifier when inherited protectedly|
|---|---|
|Public|Protected|
|Protected|Protected|
|Private|Inaccessible|

|Access specifier in base class|Access specifier when inherited privately|
|---|---|
|Public|Private|
|Protected|Private|
|Private|Inaccessible|
- Best practice
	- Ưu tiên `private` hơn `protected`
	- Sử dụng public inheritance trừ khi bạn có lí do cụ thể khác

- Để thêm hàm mới vào lớp con thì như là thêm hàm mới vào một lớp 
- Để sửa một hàm trong lớp cha thì lớp con có thể override nó, hàm mới sẽ sử dụng chỉ định truy cập của nơi nó được định nghĩa, tức là hàm private trong lớp cha có thể định nghĩa lại là hàm public trong lớp con và ngược lại 

- Nếu ta muốn thêm tính năng vào hàm gốc trong lớp con (thay vì tái định nghĩa hoàn toàn), ta có thể
```cpp
class A {
public:
	int m_a{};
	
	A(int a = 0) : m_a{a} {}
	
	void hello() const {
		std::println("Hello");
	};
};

class B : public A {
public:
	double m_b{};
	
	B(double b = 0.0) : m_b{b} {}
	
	void hello() const {
		A::hello();
		std::println("I'm a child class");
	} 
};
```

- Trường hợp ta muốn gọi friend function của lớp cha trong một override friend function của lớp con, vì hàm friend nó không phải là một phần của lớp cha, ta không sử dụng được scope qualifier `::`. Ta sẽ phải tạm thời làm lớp con giống lớp cha qua `static_cast`
```cpp
class Fruit {
public:
    Fruit(std::string_view name = "", std::string_view color = "")
        : m_name{name}
        , m_color{color}
    {
    }
  
    friend void say(const Fruit& f) {
        std::println("I'm {}", f.m_name);
    }
   
protected:
    std::string m_name{};
    std::string m_color{};
};

  

class Apple : public Fruit {
public:
    Apple(std::string_view name="", std::string_view color="", double fiber=0)
        : Fruit{name, color}
        , m_fiber{fiber}
    {
    }

    friend void say(const Apple& a) {
	    // if say(a) -> infinite recursion 
        say(static_cast<const Fruit&>(a));
        std::println("Apple({}, {}, {})", a.m_name, a.m_color, a.m_fiber);
    }

private:
    double m_fiber{};
};
```

- Ta có thể thay đổi cấp truy cập của thành viên lớp con qua việc sử dụng `using`
```cpp
class A {
public:	
	A(int a = 0) : m_a{a} {}
	
protected:
	void p_print() const {
		std::println("Hello");
	}
	
private:
	int m_a{};
};

class B : public A {
public:
	B(double b = 0.0) : m_b{b} {}
	
	using A::p_print;
	
private:
	double m_b{};
};

int main() {
	B b{3.6};
	b.p_print(); // inaccessible if not using 'using A::p_print;'
}
```
- Ở trên là ta đổi cấp truy cập của lớp cha từ protected sang public trong lớp con. Ta có thể đổi public, protected sang bất cứ cấp truy cập nào, nhưng không thể đổi cấp truy cập của thành viên private (do lớp con không truy cập được private từ đầu)

- Ta cũng có thể xóa hẳn một hàm với `= delete`

- Một lớp cũng có thể thừa kế từ nhiều lớp, các lớp con nhỏ kế thừa để lấy thuộc tính được gọi là **mixin** (mix-in)
```cpp
// h/t to reader Waldo for this example
#include <string>

struct Point2D
{
	int x{};
	int y{};
};

class Box // mixin Box class
{
public:
	void setTopLeft(Point2D point) { m_topLeft = point; }
	void setBottomRight(Point2D point) { m_bottomRight = point; }
private:
	Point2D m_topLeft{};
	Point2D m_bottomRight{};
};

class Label // mixin Label class
{
public:
	void setText(const std::string_view str) { m_text = str; }
	void setFontSize(int fontSize) { m_fontSize = fontSize; }
private:
	std::string m_text{};
	int m_fontSize{};
};

class Tooltip // mixin Tooltip class
{
public:
	void setText(const std::string_view str) { m_text = str; }
private:
	std::string m_text{};
};

class Button : public Box, public Label, public Tooltip {}; // Button using three mixins

int main()
{
	Button button{};
	button.Box::setTopLeft({ 1, 1 });
	button.Box::setBottomRight({ 10, 10 });
	button.Label::setText("Submit");
	button.Label::setFontSize(6);
	button.Tooltip::setText("Submit the form to the server");
}
```
- Ta cần gọi cụ thể `button.Label::setText()` để tránh tính mơ hồ (ambiguity) 

- Best practice: Tránh thừa kế nhiều trừ khi lựa chọn còn lại phức tạp hơn