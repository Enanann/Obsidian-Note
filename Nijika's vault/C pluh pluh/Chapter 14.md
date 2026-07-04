>[!note]
>Thứ tự khai báo của Google C++ style guide
>1. Types và type aliases (typedef, using, enum, nested structs/classes, và friend types)
>2. Static constants
>3. Factory functions
>4. Constructors và assignment operators 
>5. Destructor
>6. Tất cả các hàm khác (static và non-static, và friend functions)
>7. Biến thành viên (static và non-static)

- **Procedural programming** là lập trình tạo ra các "thủ tục" (hàm) cho logic chương trình
- **Object-oriented programming** là kiểu lập trình mà ta tập trung vào tạo các program-defined data types bao gồm cả các tính chất và một tập các hành động 

- **Class invariant** là điều kiện phải đúng trong suốt thời gian tồn tại của đối tượng, nếu không thì đối tượng sẽ ở **invalid state** -> lỗi, undefined 

- Giống như `struct`, `class` là kiểu dữ liệu phức program-defined gồm nhiều biến thành phần
	- Theo lý thuyết thì class và struct gần như y hệt nhau, class có thể tạo mọi thứ mà struct có thể
	- Thực tế thì sử dụng class và struct vào trường hợp khác nhau

- Để khai báo class
```cpp
class Employee {
	int m_id{};
	int m_age{};
	double m_wage{};
}
```
- Tên biến thường bắt đầu với `m_` để cho dễ phân biệt với tên của các biến cục bộ, tham số hàm, và hàm thành viên

- Các hàm nằm trong định nghĩa của class type là **member function**. Các hàm khác là **non-member function**
- Object mà member function được gọi trên là **implicit object**
- Nếu class của bạn không có biến thành viên -> ưu tiên dùng namespace 

- Có thể khai báo biến và hàm thành viên theo bất kỳ thứ tự nào, nhưng nếu là khởi tạo từ biến thành viên khác, thì phải đảm bảo rằng biến được dùng để làm giá trị khởi tạo phải được khởi tạo trước. Thứ tự khởi tạo là theo thứ tự khai báo 
```cpp
struct Foo {
	int m_bad1{m_bad2};
	int m_bad2{5};
	int m_bad3{bad()};
	
	int y() {return 5;}
	int m_ok{y()};
	
	int bad() {return m_ok;}
};
```

- Best practice: Nên tránh tạo hàm thành viên, vì làm thế sẽ khiến bị mất tính **aggregate** 

- Giống như const bình thường, **const class object** sẽ không cho phép thay đổi giá trị biến thành viên, và phải được khởi tạo tại thời điểm khai báo 
- Một điểm nữa, const class object sẽ không thể gọi hàm thành viên non-const 
- Để tạo hàm thành viên const, thêm `const` vào sau danh sách parameter nhưng sau phần thân hàm
- Hàm const nghĩa là hàm đảm bảo không làm thay đổi biến thành viên hoặc gọi hàm non-const khác (do hàm non-const có thể thay đổi biến thành viên)
```cpp
struct Date {
	int year{};
	
	void print() const {
		//...
	}
};
```
- Hàm const có thể được gọi bởi các non-const class object 

- Có thể overload để một hàm có cả 2 phiên bản là const và non-const 

- Mỗi thành viên trong class đều có một cấp độ truy cập, là **access level**, chỉ ra xem ai có quyền truy cập nó. Có 3 cấp độ:
	- `public`: Có thể được truy cập ở cả ngoài hàm (mặc định của struct)
	- `private`: Chỉ có thể truy cập được với class đó (mặc định của class)
	- `protected`

- Best practice: Thứ tự khai báo
	- `public` -> `protected` -> `private` 

- Best practice:
	- Struct nên tránh dùng access specifier (để mặc định) -> Để là aggregate
	- Class thì để các biến thành viên là private mặc định, còn các hàm thành viên là public (tùy hàm)

- **Access function** là các hàm cơ bản có chức năng lấy, hoặc thay đổi giá trị của một biến thành viên private, được gọi là **setter** (**mutator**) và **getter** (**accessor**)
- Getters nên cung cấp dữ liệu chỉ đọc -> nên trả về by value (nếu rẻ để copy), hoặc const lvalue reference (nếu đắt để copy) 
- Việc trả về (const) lvalue reference trong hàm thành viên thường sẽ là an toàn vì thành viên được trả về sẽ có cùng thời gian sống với caller (object gọi)

- Best practice: Ưu tiên dùng giá trị trả về của hàm thành viên trả về reference ngay lập tức để tránh dangling reference khi mà implicit object là rvalue 

- **Interface** của một kiểu class định nghĩa cách người dùng tương tác với đối tượng của class đó (e.g. qua các hàm thành viên public -> public interface)
- **Implementation** của một kiểu class bao gồm các dòng lệnh làm cho class hành động như mong muốn -> Gồm các biến thành viên, và phần thân gồm logic chương trình và biến đổi biến thành viên

- **Data hiding** (data abstraction) là khi ta **tách** interface với implementation qua việc ẩn cách triển khai các kiểu dữ liệu do người dùng tạo ra

- **Encapsulation** (đóng gói, thi thoảng cũng được nhắc là data hiding) thường nói đến 1 trong 2 việc sau:
	- Đóng gói 1 hoặc nhiều vật trong một container 
	- Gộp các dữ liệu và hàm cho việc thực hiện các hành động lên dữ liệu đó 

- Khi nào dùng non-member hoặc member function
	- Sử dụng member funciton khi phải dùng e.g. hàm khởi tạo, hàm hủy, hàm ảo, một số hàm khác.
	- Ưu tiên member function khi cần truy cập biến thành viên private hay protected
	- Ưu tiên non-member function trong các trường hợp khác 
-> 2 trường hợp sau sẽ có ngoại lệ 

- **Constructor** (hàm khởi tạo) là hàm thành viên đặc biệt cho được dùng để khởi tạo object class type. Một hàm khởi tạo phù hợp phải được có cho các object class type non-aggregate 
- Một cách để tạo hàm khởi tạo là dùng member initilizer list (3 kiểu format, ưu tiên cách 3 hoặc 2 nếu có ít biến thành viên)
```c++
class Foo {
public:
	Foo (int x, int y) : m_x(x), m_y(y) {}

	Foo(int x, int y) :
	    m_x { x },
	    m_y { y }
	{
	}

	Foo(int x, int y)
	    : m_x { x }
	    , m_y { y }
	{
	}

private:
	int m_x {};
	int m_y {};
};
```

- **Default constructor** là hàm khởi tạo mà không có tham số đầu vào
- Có thể tạo hàm khởi tạo mặc định rõ ràng bằng `Foo() = default`, nếu không thì C++ sẽ tự có 1 hàm mặc định ngầm. So sánh giữa hàm khởi tạo mặc định explicit và hàm khởi tạo rỗng tự định nghĩa (`Foo() {}`)
	1. Với `= default` và hàm khởi tạo ngầm định: zero initialized -> default initialized
	2. Với hàm khởi tạo người dùng tự định nghĩa: default initialized
```cpp
class User {
private:
    int m_a; // note: no default initialization value
    int m_b {};
public:
    User() {} // user-defined empty constructor
    int a() const { return m_a; }
    int b() const { return m_b; }
};

class Default {
private:
    int m_a; // note: no default initialization value
    int m_b {};
public:
    Default() = default; // explicitly defaulted default constructor
    int a() const { return m_a; }
    int b() const { return m_b; }
};

class Implicit {
private:
    int m_a; // note: no default initialization value
    int m_b {};
public:
    // implicit default constructor
    int a() const { return m_a; }
    int b() const { return m_b; }
};

int main()
{
    User user{}; // default initialized
    std::cout << user.a() << ' ' << user.b() << '\n'; // undefined 0

    Default def{}; // zero initialized, then default initialized
    std::cout << def.a() << ' ' << def.b() << '\n';   // 0 0

    Implicit imp{}; // zero initialized, then default initialized
    std::cout << imp.a() << ' ' << imp.b() << '\n';   // 0 0

    return 0;
}
```
- Best practice: Ưu tiên `= default`

- Không nên gọi hàm constructor trực tiếp trong thân của một function khác, điều này có thể dẫn đến lỗi hoặc tạo trực tiếp một temporary object
- **Temporary object** (**anonymous object** hay **unnamed object**) là object không có tên và chỉ tồn tại trong khoảng thời gian diễn ra một biểu thức duy nhất 
```cpp
class Employee {
private:
    std::string m_name { "???" };
    int m_id { 0 };
    bool m_isManager { false };

public:
	// this constructor initializes name and id
    Employee(std::string_view name, int id) : m_name{ name }, m_id { id } {}

	// this constructor initializes m_isManager
    Employee(std::string_view name, int id, bool isManager)
        : m_isManager { isManager } 
    {
        // Call Employee(std::string_view, int) to initialize m_name and m_id
        Employee(name, id); // this doesn't work as expected!
        // Create a temporary object here that does nothing
    }

    const std::string& getName() const { return m_name; }
};

int main()
{
    Employee e2{ "Dave", 42, true };
    
    // print e2.m_name, got "???"
    std::cout << "e2 has name: " << e2.getName() << "\n"; 
}
```

- Để khắc phục lỗi trên, constructor được phép ủy quyền (**delegate**) các khởi tạo cho constructor khác trong cùng một kiểu class. Quá trình này được gọi là **constructor chaining** và các constructors đó gọi là **delegating constructor**
- Chỉ định một **core constructor** khởi tạo đầy đủ member, và để mọi constructor khác **delegate về core**. Lưu ý là nếu sử dụng delegation thì không được dùng member initializer list nữa
```cpp
class Foo {
    // Core constructor – khởi tạo tất cả member
    Foo(int x, int y, int z) : m_x{x}, m_y{y}, m_z{z} {}

    // Overload tiện lợi – delegate về core
    Foo(int x, int y) : Foo{x, y, 0} {}

private:
	int m_x{};
	int m_y{};
	int m_z{};
};
```

- **Copy constructor** là constructor dùng để khởi tạo object với một object khác cùng loại 
- Best practice: Copy constructor không nên có side effect khác ngoài sao chép
- Có thể tự tạo copy constructor bằng cách overload tham số là kiểu của class đó hoặc dùng `= default` để C++ tự sinh ra hàm khởi tạo mặc định 
-> Ưu tiên sử dụng hàm ngầm định nếu không có yêu cầu đặc biệt
- Trong trường hợp bạn muốn ngăn không cho các đối tượng của lớp đó bị sao chép, bạn có thể xóa copy constructor bằng cách khai báo như sau: `Foo(const Foo& f) = delete;`. Điều này sẽ khiến việc sao chép đối tượng của lớp bị cấm

- As-if rule nói rằng compiler có thể thay đổi chương trình tùy ý để tối ưu hóa, miễn là không làm ảnh hưởng đến "hành vi có thể quan sát được" của chương trình. Một ngoại lệ của cái này là **copy elision**
- **Copy elision** là cách mà compiler tối ưu hóa khởi tạo object, nhằm tránh việc tạo sao chép object thừa thãi. Khi mà compiler tối ưu hóa một call đến copy constructor, ta gọi constructor này đã bị **elided**
- Ngoại lệ là do copy constructor có thể có side effect như là in ra màn hình, nhưng vẫn có thể bị compiler loại bỏ

- **User-defined conversion** là hàm ta đã viết để chuyển đổi một giá trị -> program-defined type
- Hàm khởi tạo có thể được dùng để chuyển đổi ngầm gọi là **converting constructor**. Mặc định thì tất cả các hàm khởi tạo đều là converting constructor 
```cpp
class Foo {
public:
	Foo(int x) : m_x{x} {}
	
	int getX() const {return m_x;}

private:
	int m_x{};
};

void printFoo(Foo f) {std::cout << f.getX() << '\n'}
//...
printFoo(5)
```
- Compiler sẽ chuyển 5 thành Foo
- Lưu ý chỉ được áp dụng user-defined conversion **1 lần**. Giả sử `m_x` là kiểu string và hàm khởi tạo dùng string_view để tối ưu hóa, mà ta dùng `printFoo("test")` thì `"test"` là C-Style -> `string_view` -> `string` => 2 lần chuyển, ta cần dùng `printFoo("test"sv)` để chuyển sẵn C-style qua string_view (cần `using namespace std::literals;`)

- Ta có thể dùng `explicit` để bảo compiler rằng constructor không được dùng làm converting constructor
```cpp
class Foo {
public:
	explicit Foo(int d) : m_foo{d} {}

private:
	int m_foo{};
};
```

- Vẫn có thể dùng được với direct và direct list initialization (do là explicit conversion)
```cpp
// Foo(int) is explicit
int main() {
	Foo d1(1); //ok
	Foo d2{2}; // ok
}
```
- Tương tự với trả về  
- Điều này có ích khi ta muốn một hàm nào đó chỉ nhận đầu vào là class type đó 
- Best practice:
	- Biến mọi constructor nhận 1 đối số là `explicit`. Nếu chuyển đổi ngầm giữa 2 kiểu có cấu trúc ngữ nghĩa và hiệu năng y hệt nhau, có thể để `non-explicit`
	- Không làm cho copy hay move constructor explicit, do chúng không thực hiện đổi kiểu 