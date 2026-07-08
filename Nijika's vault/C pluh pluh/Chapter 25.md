
### Virtual function

- Như ta đã biết, khi tạo một lớp kế thừa (derived), nó sẽ gồm 2 phần
	- Phần cơ sở (base)
	- Phần kế thừa (derived)

- Khá rõ ràng là ta có thể tạo một tham chiếu hay con trỏ đến lớp kế thừa
```cpp
class A {
public:
    void print() const {
        std::println("???");
    }
  
protected:
    A(int a) : m_a{a} {}
    
    int m_a{};
};

class B : public A {
public:
    B(int a) : A{a} {}

    void print() const {
        std::println("Derived");
    }
  
    void printInt() const {
        std::println("{}", m_a * 2);
    }
};

int main() {
    B b{2};
    b.print();      // Derived
    b.printInt();   // 4

    B& rB{b};     
    rB.print();     // Dervied
    rB.printInt();  // 4

    B* pB{&b};  
    pB->print();    // Derived
    pB->printInt(); // 4

    return 0;
}
```

- C++ cũng cho phép ta chuyển kiểu về lớp cơ sở, tuy nhiên do nó là lớp cơ sở nên ta chỉ có thể dùng các hàm trong lớp cơ sở 
```cpp
int main() {
	B b{2};
	
	A& rA{b};
    rA.print();     // ???
    rA.printInt();  // compile error

    A* pA{&b};
    pA->print();    // ???
    pA->printInt(); // compile error

	return 0
}
```

- Như trên có thể thấy mặc dù b là lớp thừa kế nhưng khi chuyển về lớp cơ sở thì hàm `print()` của nó đã bị thay bằng hàm gốc từ lớp cơ sở 

- Một lí do chính mà ta muốn chuyển về kiểu cơ sở là cho tính dễ đọc và giảm bớt rắc rối, xét trường hợp mà có nhiều lớp kế thừa từ lớp cơ sở và bạn muốn cho chúng vào một mảng, nếu không chuyển về lớp cơ sở thì mỗi lớp kế thừa sẽ cần một mảng riêng -> rối, khả năng mở rộng kém

- Để giải quyết vấn đề này, ta sử dụng **virtual function**. Virtual function là kiểu hàm thành viên đặc biệt mà, khi được gọi, sẽ được phân giải (resolve) thành phiên bản kế thừa nhất của hàm cho kiểu đối tượng đang được tham chiếu hoặc trỏ đến
- Hàm kế thừa được coi là phù hợp nếu nó có cùng tính nhận dạng (tên, kiểu tham số, là const hay không) và kiểu trả về như là hàm cơ sở, hàm này được gọi là **overrides**
- Để làm một hàm virtual, đặt `virtual` trước khai báo hàm
```cpp
class Base {
public:
    virtual std::string_view getName() const { return "Base"; } 
};

class Derived: public Base {
public:
    virtual std::string_view getName() const { return "Derived"; }
};

int main() {
    Derived derived {};
    Base& rBase{ derived };
    std::cout << "rBase is a " << rBase.getName() << '\n';
	// rBase is a Derived

    return 0;
}
```

- Ví dụ khác
```cpp
class A {
public:
    virtual std::string_view getName() const { return "A"; }
};

class B: public A {
public:
    virtual std::string_view getName() const { return "B"; }
};

class C: public B {
public:
    virtual std::string_view getName() const { return "C"; }
};

class D: public C {
public:
    virtual std::string_view getName() const { return "D"; }
};

int main() {
    C c {};
    A& rBase{ c };
    std::cout << "rBase is a " << rBase.getName() << '\n';
	// rBase is a C

    return 0;
}
```

### Polymorphism

- **Polymorphism** (tính đa hình) là khả năng cho một thực thể có thể mang nhiều hình thức khác nhau
	- Compile-time polymorphism là dạng đa hình được phân giải bởi compiler, bao gồm function overload cũng như template 
	- Runtime polymorphism là dạng đa hình được phân giải trong runtime, bao gồm virtual function 

- Best practice:
	- Không được gọi virtual function trong hàm khởi tạo hoặc hàm hủy

- Có 2 định danh liên quan đến kế thừa:
	- `override`
	- `final`

- `override` là từ định danh để cho compiler biết rằng hàm này chính là một override, để sau cùng ở hàm (sau const)
- `final` là từ định danh để ngăn chặn việc override một hàm hay là ngăn cho lớp khác kế thừa từ lớp này 
```cpp
class A {};

class B final : public class A {};
```

- **Covariant return types** là một ngoại lệ cho phép hàm virtual được override trả về một con trỏ hoặc tham chiếu đến lớp dẫn xuất nếu hàm trong lớp cơ sở trả về con trỏ hoặc tham chiếu đến lớp cơ sở
```cpp
class A {
public:
	virtual A* get() {
		return this;
	}
	
	void print() const {}
	virtual vprint() const {}
};

class B : public A {
public:
	B* get() override {
		return this;
	}
	
	void print() const {}
	virtual vprint() const {}
};
```

- Một lưu ý là đối với hàm non-virtual, nó vẫn sẽ được gọi dựa trên kiểu tĩnh của đối tượng gọi hàm 
```cpp
B b{};
A* a{&b};

b.get()->print();  // call B::get(), non-virtual => call B::print()
a->get()->print(); // call B::get(), non-virtual => call A::print()

b.get()->vprint();  // call B::get(), virtual => call B::vprint()
a->get()->vprint(); // call B::get(), virtual => call B::vprint()
```

- Trong C++ có:
	- **Kiểu tĩnh (static type)**: compiler biết lúc biên dịch
	- **Kiểu động (dynamic type)**: object thật lúc chạy
```cpp
class Base { 
}; 

class Derived : public Base { 
}; 

int main() { 
	// wb is a pointer to Base 
	Base* wb = new Derived(); 
	// STATIC TYPE of 'wb' is: Base* 
	// DYNAMIC TYPE of 'wb' is: Derived*

}
```

### Virtual destructors, virtual assignment, overriding virtualization 

- Khi làm việc với thừa kế, luôn nên để hàm hủy là virtual
```cpp
class A {
public:
    A(int a) : m_a{a} {}
    ~A() {
        std::println("Calling ~A");
    }
    
private:
	int m_a{};
};

class B : public A {
public:
    B(int a) : A{a} {}

    ~B() {
        std::println("Calling ~B");
    }
};

int main() {
    B* b{new B(5)};
    A* a{b};

    delete a;

    return 0;
}
```
- Nếu không để hàm hủy là virtual thì `delete a` sẽ chỉ sử dụng hàm hủy của lớp A, nếu hàm hủy là virtual thì compiler mới tìm đến hàm hủy "kế thừa nhất", tức là hàm hủy của lớp B

- Cũng có thể làm cho toán tử gán virtual -> **không nên**

- Trong trường hợp ta muốn bỏ qua virtualization (hiếm), có thể gọi
```cpp
/*
class...
	virtual print()...
*/

int main() {
	Derived d{};
	Base& b{d};
	
	b.print();       // virtualization -> call Derive::print
	b.Base::print(); // call Base::print
	
	return 0;
}
```

- Rule:
	- Nếu class được thiết kế làm lớp cơ sở, đảm bảo rằng hàm hủy là virtual và public
	- Nếu class không được thiết kế làm lớp bị kế thừa, thì để nó là final

### Binding sớm, muộn (optional)

- Trong lập trình nói chung, **binding** là quá trình gắn tên với những thuộc tính (e.g. x với int)
- **Function binding** (method binding) là quá trình quyết định định nghĩa hàm nào được gắn với lời gọi hàm. Quá trình thực hiện hàm đó gọi là **dispatching**

- Trong C++, thì binding dùng một cách đơn giản hơn (dispatching thường được coi là một phần của binding)

- **Early binding** (static binding) là khi lời gọi trực tiếp được thực hiện đến một hàm không phải là thành viên hoặc hàm thành viên không phải là virtual (compiler có thể quyết định luôn hàm nào) 
```cpp
#include <iostream>

struct Foo {
    void printValue(int value) {
        std::cout << value;
    }
};

void printValue(int value) {
    std::cout << value;
}

int main() {
    printValue(5);   // direct function call to printValue(int)

    Foo f{};
    f.printValue(5); // direct function call to Foo::printValue(int)
    return 0;
}
```

- Lời gọi các hàm được nạp chồng hoặc template cũng có thể được phân giải tại thời điểm biên dịch

- Trong các trường hợp mà lời gọi hàm không thể phân giải được cho đến khi runtime thì gọi là **late binding** (trường hợp phân giải hàm ảo thì gọi là **dynamic dispatch**). Ngoài hàm ảo thì function pointer cũng là một cách để thực hiện late binding (indirect function call)

### Virtual table (optional)

- Virtual table là một bảng tìm kiếm gồm các hàm sử dụng cho phân giải các lời gọi hàm trong một dynamic/late binding. Còn được gọi là vtable, virtual function table, virtual method table, dispatch table 

- Hiểu đơn giản là mỗi lớp có sử dụng virtual function sẽ tự động có thêm một biến thành viên là con trỏ `*__vptr`, trỏ đến một bảng vtable của riêng nó
- Tức là sử dụng virtual function sẽ khiến các hàm gọi lâu hơn và do cần con trỏ đến vtable, mỗi lớp sẽ tăng thêm bộ nhớ bằng 1 con trỏ

### Pure virtual function, abstract base class, interface class

- Một hàm ảo có thể được làm thành pure/abstract bằng cách thêm `= 0` vào sau prototype của hàm ảo
- Một lớp chứa pure virtual function được gọi là **abstract class** và không thể được khởi tạo
- Lớp kế thừa abstract class bắt buộc phải định nghĩa chúng hoặc không thì cũng sẽ được coi là abstract
- Pure virtual function có thể có phần thân nhưng chúng vẫn được coi là abstract 

- **Interface class** là lớp mà không có biến thành viên, và tất cả các hàm đều là pure virtual
- Hữu ích khi ta muốn định nghĩa các tính năng mà lớp kế thừa phải triển khai

### Object slicing

- Object slicing là khi mà lớp dẫn xuất được gán (assign) cho lớp cơ sở thay vì theo tham chiếu hoặc con trỏ. Lúc này lớp cơ sở sẽ chỉ nhận được sao chép của phần cơ sở của lớp dẫn xuất  

### Dynamic casting

- Dynamic cast được sử dụng để chuyển đổi kiểu từ con trỏ lớp cơ sở thành con trỏ lớp dẫn xuất, còn được gọi là **downcasting**
- **Upcasting** là khi mà C++ cho phép ta ngầm định chuyển từ con trỏ lớp dẫn xuất lên con trỏ lớp cơ sở

- Dynamic casting dùng trong trường hợp mà ta chỉ có con trỏ lớp cơ sở, mà ta muốn truy cập thông tin chỉ có trong lớp dẫn xuất. Điều kiện là lớp cơ sở phải có ít nhất một hàm virtual
- Trong trường hợp mà dynamic cast lỗi (trường hợp mà b thật sự là con trỏ lớp cơ sở), nó sẽ trả về `nullptr`
```cpp
Base* getObject(bool returnDerived) {
	if (returnDerived)
		return new Derived{1, "Apple"};
	else
		return new Base{2};
}

int main() {
	Base* b{ getObject(true) };

	// use dynamic cast to convert Base pointer into Derived pointer
	Derived* d{ dynamic_cast<Derived*>(b) }; 

	if (d) {
		std::cout << "The name of the Derived is: " << d->getName() << '\n';
	}

	delete b;

	return 0;
}
```

- Một số trường hợp mà downcasting với `dynamic_cast` không hoạt động
	- Với kế thừa private hoặc protected
	- Lớp mà không khai báo hoặc kế thừa bất cứ hàm ảo nào  
	- Một số trường hợp liên quan virtual base classes

- Ta cũng có thể thực hiện downcasting với `static_cast`, điểm khác biệt chính là `static_cast` không thực hiện kiểm tra kiểu runtime như `dynamic_cast`, tức là nó sẽ nhanh hơn nhưng nguy hiểm hơn. 
- Nó sẽ luôn thành công mặc dù `Base*` có thể không phải là một `Derived*` 

- `dynamic_cast` cũng có thể được dùng với tham chiếu, cách sử dụng tương tự, điểm khác biệt là do tham chiếu không thể là `nullptr` nên khi thất bại sẽ trả về một exception kiểu `std::bad_cast`