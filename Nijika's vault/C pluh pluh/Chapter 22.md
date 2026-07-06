
- Khi làm việc với tài nguyên cấp phát động, dễ xảy ra tình huống ta quên xóa, early return, throw, gây ra memory leak
- **Smart pointer** là một composition class (lớp bao gộp) được thiết kế để quản lý bộ nhớ cấp phát động và đảm bảo bộ nhớ đó được xóa khi smart pointer object đi ra khỏi scope

- **Move semantic** có nghĩa là một object sẽ chuyển quyền ownership cho object khác hơn là tạo bản sao. Việc này thường được thực hiện qua **move constructor** và **move assignment operator**

- Recap lvalue reference 

| L-value reference       | Can be initialized with | Can modify |
| ----------------------- | ----------------------- | ---------- |
| Modifiable l-values     | Yes                     | Yes        |
| Non-modifiable l-values | No                      | No         |
| R-values                | No                      | No         |

| L-value reference to const | Can be initialized with | Can modify |
| -------------------------- | ----------------------- | ---------- |
| Modifiable l-values        | Yes                     | No         |
| Non-modifiable l-values    | Yes                     | No         |
| R-values                   | Yes                     | No         |

- C++11 thêm một kiểu reference nữa là **r-value reference**
- **R-value reference** là tham chiếu được thiết kế để (chỉ) có thể được khởi tạo với r-value 
- Rvalue reference được tạo với 2 dấu `&&` (thay vì 1 như lvalue reference)
```cpp
int x{5};
int& lref{x};   // lvalue ref initialized with lvalue x
int&& rref{5};  // rvalue ref initialized with rvalue 5
```

- Rvalue reference không thể được khởi tạo với lvalue 

| R-value reference       | Can be initialized with | Can modify |
| ----------------------- | ----------------------- | ---------- |
| Modifiable l-values     | No                      | No         |
| Non-modifiable l-values | No                      | No         |
| R-values                | Yes                     | Yes        |

| R-value reference to const | Can be initialized with | Can modify |
| -------------------------- | ----------------------- | ---------- |
| Modifiable l-values        | No                      | No         |
| Non-modifiable l-values    | No                      | No         |
| R-values                   | Yes                     | No         |

- Rvalue reference có 2 tính chất hữu ích
	- Nó sẽ kéo dài thời gian sống của object nó được khởi tạo với (lvalue ref to const cũng có thể làm điều này)
	- Nó cho phép thay đổi giá trị rvalue 
```cpp
int&& rref{5};
rref = 10;

std::cout << rref << '\n'; // 10
```
- Rvalue ref không hay được dùng với mục đích ở trên

- Rvalue ref thường đưuọc dùng như là tham số của hàm. Có ích nhất trong overload khi ta muốn có 2 hành động khác nhau cho trường hợp là lvalue và rvalue
```cpp
#include <iostream>
void fun(const int& lref) {
	std::cout << "l-value reference to const: " << lref << '\n';
}

void fun(int&& rref) {
	std::cout << "r-value reference: " << rref << '\n';
}

int main() {
	int x{ 5 };
	fun(x); // l-value argument calls l-value version of function
	fun(5); // r-value argument calls r-value version of function
	
	return 0;
}
```

- Biến rvalue ref là lvalue (dù nó có kiểu `int&&` nhưng khi dùng trong biểu thức thì nó là 1 lvalue, giống như mọi biến có tên). Giá trị và kiểu của object là độc lập 
```cpp
int&& ref{5};
fun(ref); // will call fun(const int&)
```
- Có nghĩa `int&& ref` là lvalue của kiểu `int&&`, cũng như `int x` là lvalue của `int`, `5` là rvalue của `int`

- Không nên trả về rvalue ref vì nguyên nhân giống như trả về lvalue ref, hầu hết sẽ gây hanging reference 

- Recap copy constructor và copy assignment
	- Copy constructor e.g. `ClassName(const Classname& a)` được dùng để khởi tạo một object bằng cách tạo bản sao của object khác cùng class
	- Copy assignment (qua overload operator `=` của class) được dùng để sao chép một object sang một object khác đã tồn tại cùng class
- C++ cung cấp mặc định cho 2 cái trên nếu không tự định nghĩa. Các hàm C++ cung cấp sẽ thực hiện **shallow copies** -> gây vấn đề đối với các class dùng cấp phát động
- Tuy nhiên nếu ta viết lại các hàm này để thực hiện **deep copies** -> sẽ gây thừa thãi rất nhiều 
```cpp
#include <iostream>

template<typename T>
class Auto_ptr3 {
	T* m_ptr {};
public:
	Auto_ptr3(T* ptr = nullptr) : m_ptr { ptr } {}
	
	~Auto_ptr3() {
		delete m_ptr;
	}
	
	// Copy constructor
	// Do deep copy of a.m_ptr to m_ptr
	Auto_ptr3(const Auto_ptr3& a) {
		m_ptr = new T;
		*m_ptr = *a.m_ptr;
	}
	// Copy assignment
	// Do deep copy of a.m_ptr to m_ptr
	Auto_ptr3& operator=(const Auto_ptr3& a) {
		// Self-assignment detection
		if (&a == this)
			return *this;
		// Release any resource we're holding
		delete m_ptr;
		
		// Copy the resource
		m_ptr = new T;
		*m_ptr = *a.m_ptr;
		
		return *this;
	}
	
	T& operator*() const { return *m_ptr; }
	T* operator->() const { return m_ptr; }
	bool isNull() const { return m_ptr == nullptr; }
};

class Resource {
public:
	Resource() { std::cout << "Resource acquired\n"; }
	~Resource() { std::cout << "Resource destroyed\n"; }
};

Auto_ptr3<Resource> generateResource() {
	Auto_ptr3<Resource> res{new Resource};
	return res; // this return value will invoke the copy constructor
}

int main() {
	Auto_ptr3<Resource> mainres;
	mainres = generateResource(); // this will invoke the copy assignment
	
	return 0;
}
```
- Giả sử như trên thì output sẽ là 
```
Resource acquired     của res trong hàm
Resource acquired     hàm return by value -> res được copy sang temp obj
Resource destroyed    res trong hàm ra khỏi scope
Resource acquired     mainres được cấp bộ nhớ từ copy assignment
Resource destroyed    hủy temp obj sau khi gán 
Resource destroyed    mainres đi ra khỏi scope main()
```

- Để giải quyết vấn đề trên, C++11 định nghĩa 2 hàm phục vụ cho move semantic: **move constructor** và **move assignment operator** 
- Mục tiêu của nó là chuyển ownership của tài nguyên từ object này sang object khác (rẻ hơn nhiều so với copy)

- Định nghĩa move constructor và move assignment hoạt động giống như phiên bản copy. Tuy nhiên, chúng sẽ lấy đầu vào là non-const rvalue reference (chỉ gán với rvalue) thay vì const lvalue reference (có thể được gán với mọi thứ)
```cpp
// Move constructor
Auto_ptr3(Auto_ptr3&& a) noexcept : m_ptr {a.m_ptr} {
	a.m_ptr = nullptr;
}

// Move assignment 
Auto_ptr3& operator=(Auto_ptr3&& a) noexcept {
	// self-assignment detection
	if (&a == this) return *this;
	
	// release any resource we're holding
	delete m_ptr;
	
	m_ptr = a.m_ptr;
	a.m_ptr = nullptr;
	
	return *this;
}
```
- Move constructor và Copy assignment operator nên được đánh dấu là `noexcept`
- Ta đặt `a.m_ptr` ở trên thành nullptr để khi `a` ra khỏi scope, destructor của nó sẽ được gọi và xóa hợp lý, nếu không thì `a` cũng sẽ đang chỉ đến cùng một object với cái mà ta đã move qua -> gây dangling pointer 

- `res` trong hàm `generateResource()` được move mặc dù nó là lvalue, vì trong đặc tả C++, automatic object được trả về từ hàm có thể được move mặc dù chúng là lvalues (vì đằng nào cũng sẽ ra khỏi scope hàm)

- Để tắt copying -> đặt copy constructor và copy assignment operator `= delete` 
- Tương ứng với tắt move 

- **Rule of five**: Nếu copy constructor, copy assignment, move constructor, move assignment hay destructor được định nghĩa hoặc xóa, thì mỗi hàm còn lại cũng nên được định nghĩa hoặc xóa (tức là cứ có 1 cái thì nên làm với tất cả các cái còn lại)

- Khi bạn muốn thực hiện move semantic với lvalue, có thể dùng `std::move` trong `<utility>`. **`std::move`** sử dụng `static_cast` để chuyển đối số của nó thành rvalue, cho phép ta đối xử với lvalue như rvalue
- Thay vì copy 3 lần
```cpp
template <typename T>
void swap(T& a, T& b) {
	T tmp{a};  // copy constructor
	a = b;     // copy constructor
	b = tmp;   // copy constructor
}
```
- Ta có thể dùng move constructor
```cpp
#include <utility>

template <typename T>
void swap(T& a, T& b) {
	T tmp{std::move(a)}; // move constructor
	a = std::move(b);    // move constructor
	b = std::move(tmp);  // move constructor
}
```

- Ta cũng có thể dùng `std::move` khi thêm phần tử lvalue vào container e.g. `std::vector`
```cpp
#include <iostream>
#include <string>
#include <utility> // for std::move
#include <vector>

int main() {
	std::vector<std::string> v;
	
	// We use std::string because it is movable (std::string_view is not)
	std::string str { "Knock" };
	
	std::cout << "Copying str\n";
	v.push_back(str); // calls l-value version of push_back, which copies str into the array element
	
	std::cout << "str: " << str << '\n';
	std::cout << "vector: " << v[0] << '\n';
	
	std::cout << "\nMoving str\n";
	
	v.push_back(std::move(str)); // calls r-value version of push_back, which moves str into the array element
	
	std::cout << "str: " << str << '\n'; // The result of this is indeterminate
	std::cout << "vector:" << v[0] << ' ' << v[1] << '\n';
	
	return 0;
}
```
- Đầu ra:
```
Copying str
str: Knock
vector: Knock

Moving str
str:
vector: Knock Knock
```

- Object được move sẽ ở dạng valid, nhưng mà unspecified. Tức là ở trên, str có thể trống, là string gốc, hoặc có thể là bất cứ string hợp lý nào 
=> Tránh sử dụng giá trị của lvalue object được move 


- Smart pointer dùng để tự động quản lý bộ nhớ cho các object cấp phát động -> không bao giờ nên cấp phát động cho bản thân nó (có thể quên xóa), nên cấp phát trên stack thì stack đảm bảo nó sẽ đi ra khỏi scope
- Thư viện tiêu chuẩn C++ cung cấp 4 lớp smart pointer
	- `std::auto_ptr`: Xóa ở C++17
	- `std::unique_ptr`
	- `std::shared_ptr`
	- `std::weak_ptr`

- `std::unique_ptr` được sử dụng nhiều nhất, thay thế trực tiếp cho `std::auto_ptr`. Nó nên được dùng để quản lý bất kỳ object nào được cấp phát động mà **không được chia sẻ bởi nhiều object khác**
- Nằm trong `<memory>`
```cpp
#include <iostream>
#include <memory> // for std::unique_ptr

class Resource {
public:
	Resource() { std::cout << "Resource acquired\n"; }
	~Resource() { std::cout << "Resource destroyed\n"; }
};

int main() {
	// allocate a Resource object and have it owned by std::unique_ptr
	std::unique_ptr<Resource> res{ new Resource() };
	
	return 0;
} // res goes out of scope here, and the allocated Resource is destroyed
```
- Khác với `std::auto_ptr`, `std::unique_ptr` có triển khai move semantic -> copy initialization và copy assignment bị tắt 

- Để truy cập object đang được quản lý (`*` và `->` được overload)
	- `*` trả về tham chiếu đến tài nguyên được quản lý
	- `->` trả về pointer 
- Do `std::unique_ptr` có thể là nullptr hoặc không quản lý tài nguyên nào, nên kiểm tra trước khi truy cập. `std::unique_ptr` tự chuyển đổi ngầm về bool, trả về `true` nếu nó đang quản lý 
```cpp
std::unique_ptr<Resource> res{ new Resource{} };

if (res) // use implicit cast to bool to ensure res contains a Resource
	std::cout << *res << '\n'; // print the Resource that res is owning
```

- Best practice: Ưu tiên `std::array`, `std::vector` hơn smart pointer quản lý mảng tĩnh/động/C-style string

- C++14 thêm vào `std::make_unique()`, có tác dụng tại object của kiểu template và khởi tạo nó với đối số được truyền vào hàm
```cpp
// we have a Fraction class

int main() {
	// Create a single dynamically allocated Fraction 3/4
	// Can also use automatica type deduction
	auto f1{std::make_unique<Fraction>(3, 5)};
	
	// Create a dynamically allocated array of Fractions of length 4
	auto f2{std::make_unique<Fraction[]>(4)};
	
	return 0;
}
```
- Best practice: Ưu tiên dùng `std::make_unique()` thay vì tạo thủ công với `new` (vì thủ công có thể có lỗi leak)

- Có thể trả về `std::unique_ptr` theo value an toàn 

- Khi truyền `std::unique_ptr` cho hàm
	- Nếu bạn muốn hàm lấy quyền sở hữu con trỏ, pass theo value (vì copy bị disable, cần dùng `std::move`)
	- Tuy nhiên, hầu hết trường hợp thì bạn không muốn hàm lấy quyền sở hữu, có thể pass theo const ref, tốt hơn là nên pass tài nguyên đó trực tiếp (theo pointer hoặc ref tùy vào nếu null là giá trị hợp lệ)

| Hàm muốn làm gì?                            | Tham số nên là                  |
| ------------------------------------------- | ------------------------------- |
| Lấy ownership                               | `std::unique_ptr<T>` (by value) |
| Có thể sửa object nhưng không lấy ownership | `T&`                            |
| Chỉ đọc object                              | `const T&`                      |
| Có thể không có object (`nullptr` hợp lệ)   | `T*` hoặc `const T*`            |

```cpp
// This function takes ownership of the Resource, which isn't what we want
void takeOwnership(std::unique_ptr<Resource> res) {
     if (res)
          std::cout << *res << '\n';
} // the Resource is destroyed here

int main() {
    auto ptr{ std::make_unique<Resource>() };
    
	// takeOwnership(ptr); // This doesn't work, need to use move semantics
    takeOwnership(std::move(ptr)); // ok: use move semantics
    
    std::cout << "Ending program\n";
    
    return 0;
}
```

- Để lấy raw pointer từ `std::unique_ptr`, có thể dùng hàm thành viên `get()`
```cpp
// The function only uses the resource, so we'll accept a pointer to the resource, not a reference to the whole std::unique_ptr<Resource>
void useResource(const Resource* res) {
	if (res)
		std::cout << *res << '\n';
	else
		std::cout << "No resource\n";
}

int main() {
	auto ptr{ std::make_unique<Resource>() };
	
	useResource(ptr.get()); // note: get() used here to get a pointer to the Resource
	std::cout << "Ending program\n";
	
	return 0;
} // The Resource is destroyed here
```

- Có 2 cách để dùng sai `std::unique_ptr`
	- Không nên để nhiều object cùng quản lý tài nguyên giống nhau
	- Không thủ công xóa tài nguyên nằm trong `std::unique_ptr` thủ công 

- Khác với `std::unique_ptr` dùng để quản lý và chỉ sở hữu một tài nguyên, **`std::shared_ptr`** được thiết kế để quản lý khi bạn có nhiều smart pointer cùng sở hữu một tài nguyên
- Tức là có thể có nhiều `std::shared_ptr` cùng trỏ đến tài nguyên giống nhau
- `std::shared_ptr` sẽ theo dõi xem có bao nhiêu `std::shared_ptr` khác đang chia sẻ tài nguyên. Chỉ cần có một `std::shared_ptr` trỏ đến tài nguyên, thì nó sẽ không bị giải phóng, kể cả khi các `std::shared_ptr` riêng bị bị xóa 

- `std::shared_ptr` cũng nằm trong `<memory>`
```cpp
#include <iostream>
#include <memory> // for std::shared_ptr

class Resource {
public:
	Resource() { std::cout << "Resource acquired\n"; }
	~Resource() { std::cout << "Resource destroyed\n"; }
};

int main() {
	// allocate a Resource object and have it owned by std::shared_ptr
	Resource* res { new Resource };
	std::shared_ptr<Resource> ptr1{ res };
	{
		std::shared_ptr<Resource> ptr2 { ptr1 }; 
		// make another std::shared_ptr pointing to the same thing
		
		std::cout << "Killing one shared pointer\n";
	} // ptr2 goes out of scope here, but nothing happens
	
	std::cout << "Killing another shared pointer\n";
	
	return 0;
} // ptr1 goes out of scope here, and the allocated Resource is destroyed
```

- Để ý là `ptr2` được tạo ra từ `ptr1` chứ không phải từ `res`. Nếu tạo ra từ `res` thì nó sẽ tạo **2 `std::shared_ptr` riêng biệt** cùng quản lý `res`, tức là nếu 1 cái bị xóa thì `res` được giải phóng (2 control block khác nhau)

- Giống với `std::make_unique()` để tạo `std::unique_ptr`, `std::make_shared()` có thể (và nên dùng) để tạo `std::shared_ptr` -> an toàn hơn, giúp **tránh raw pointer bị lộ ra ngoài**
```cpp
// not exposing Resource* res {new Resource};
auto ptr1{std::make_shared<Resource>()};

auto ptr2{ptr1};
```

- Khác với `std::unique_ptr` mà bản thân chỉ sử dụng 1 pointer, `std::shared_ptr` sử dụng 2 pointer ở bên trong
	- Một để trỏ đến tài nguyên đang được quản lý
	- Một để trỏ đến "control block", là object cấp phát động để theo dõi nhiều thứ như có bao nhiêu `std::shared_ptr` đang quản lý tài nguyên
- Khi tạo qua constructor của `std::shared_ptr`, bộ nhớ cho quản lý object và control block được cấp riêng biệt. Còn khi dùng `std::make_shared()`, có thể tối ưu lại thành 1 lần cấp bộ nhớ -> hiệu năng tốt hơn

- `std::shared_ptr` có thể được tạo từ `std::unique_ptr` qua hàm khởi tạo đặc biệt. Nội dung của `std::unique_ptr` sẽ được moved qua `std::shared_ptr`
- Trái lại `std::unique_ptr` không thể được chuyển an toàn từ `std::shared_ptr` sang

- Cũng giống như `std::unique_ptr`, `std::shared_ptr` cũng có một số điểm nguy hiểm
	- Nếu cấp phát bộ nhớ nó trên heap, cần phải thủ công xóa nếu không sẽ gây memory leak
- Cần phải quản lý toàn bộ các `std::shared_ptr`, đảm bảo phải giai phóng hết 

- C++20, `std::shared_ptr` có hỗ trợ cho arrays (C++17 không hỗ trợ)

- `std::shared_ptr` có một khuyết điểm là **circular references** (**cyclical reference** hay **cycle**), là chuỗi các tham chiếu mà mỗi object lại tham chiếu đến object tiếp theo, và object cuối tham chiếu đến object đầu
- Tham chiếu không nhất thiết phải là C++ reference, có thể là pointer, unique IDs, hay bất kỳ cách nào khác để phân biệt object 
```cpp
#include <iostream>
#include <memory> // for std::shared_ptr
#include <string>

class Person {
public:
	std::string m_name;
	std::shared_ptr<Person> m_partner; // initially created empty
	
	Person(const std::string &name): m_name(name) {
		std::cout << m_name << " created\n";
	}
	~Person() {
		std::cout << m_name << " destroyed\n";
	}
};

int main() {
	auto lucy{std::make_shared<Person>("Lucy")}; // create a Person named "Lucy"
	auto rick{std::make_shared<Person>("Rick")}; // create a Person named "Ricky"
	
	// should put in a function to check for validity and stuff
	lucy->m_partner = rick;
	rick->m_partner = lucy;
	
	return 0;
}
```
- Như hàm ở trên thì lucy trỏ đến rick và rick lại trỏ đến lucy, khi main kết thúc:
	- rick ra khỏi scope -> xóa rick, nhưng lucy đang chứa pointer đến rick -> không xóa tài nguyên, chỉ xóa pointer
	- lucy ra khỏi scope -> xóa lucy, nhưng rick đang chứa pointer đến lucy -> không xóa tài nguyên, chỉ xóa pointer
=> Phụ thuộc vòng, tài nguyên không bao giờ được giải phóng -> memory leak

- Cũng có thể xảy ra với 1 `std::shared_ptr`, khi mà nó tham chiếu đến object chứa nó 
```cpp
#include <iostream>
#include <memory> // for std::shared_ptr

class Resource {
public:
	std::shared_ptr<Resource> m_ptr {}; // initially created empty
	
	Resource() { std::cout << "Resource acquired\n"; }
	~Resource() { std::cout << "Resource destroyed\n"; }
};

int main() {
	auto ptr1 { std::make_shared<Resource>() };
	
	ptr1->m_ptr = ptr1; // m_ptr is now sharing the Resource that contains it
	
	return 0;
}
```
- Khi kết thúc, xóa `ptr1` nhưng do `m_ptr` đang chứa `ptr1` nên chỉ xóa con trỏ, không giải phóng bộ nhớ. Cách duy nhất là đặt `m_ptr` sang cái khác, nhưng không truy cập được do `ptr1` đã bị xóa -> memory leak 

- **`std::weak_ptr`** được thiết kế để giải quyết vấn đề trên, `std::weak_ptr` là một người quan sát - nó có thể quan sát và truy cập cùng object với `std::shared_ptr` (hoặc `std::weak_ptr` khác) nhưng mà nó không được coi là một owner 
- Giải quyết `Person` ở trên:
```cpp
#include <iostream>
#include <memory> // for std::shared_ptr
#include <string>

class Person {
public:
	std::string m_name;
	std::weak_ptr<Person> m_partner; // Note: This is now a std::weak_ptr
	
	Person(const std::string &name): m_name(name) {
		std::cout << m_name << " created\n";
	}
	~Person() {
		std::cout << m_name << " destroyed\n";
	}
};

int main() {
	auto lucy{std::make_shared<Person>("Lucy")}; // create a Person named "Lucy"
	auto rick{std::make_shared<Person>("Rick")}; // create a Person named "Ricky"
	
	// should put in a function to check for validity and stuff
	lucy->m_partner = rick;
	rick->m_partner = lucy;
	
	return 0;
}
```
- Lúc này, khi `rick` đi ra khỏi scope, `std::weak_ptr` của `lucy` không được tính và `Rick` sẽ được giải phóng, điều tương tự xảy ra với `lucy`

- Một điều bất lợi của `std::weak_ptr` là nó không thể được dùng trực tiếp (không có `->`). Muốn dùng thì phải chuyển về `std::shared_ptr` qua hàm thành viên `lock()`
```cpp
auto partner = lucy->m_partner.lock(); // std::shared_ptr
std::cout << partner->m_name;
```
- Không lo `partner` vì nó là biến cục bộ và sẽ đi ra khỏi scope và số tham chiếu sẽ giảm đi 1 

- Bởi vì `std::weak_ptr` chỉ là người quan sát, nó có thể quan sát đến object đã được giải phóng -> dangling. Tuy nhiên, nó có truy cập đến số tham chiếu của một object, nó có thể quyết định xem object đó có hợp lệ hay không -> sử dụng hàm thành viên `expired()`
- Trả về `true` nếu đang trỏ đến object không hợp lệ, `false` nếu ngược lại => Thích hợp để tránh dangling pointer 
```cpp
#include <iostream>
#include <memory>

class Resource {
public:
	Resource() { std::cerr << "Resource acquired\n"; }
	~Resource() { std::cerr << "Resource destroyed\n"; }
};

// Returns a std::weak_ptr to an invalid object
std::weak_ptr<Resource> getWeakPtr() {
	auto ptr{ std::make_shared<Resource>() };
	return std::weak_ptr<Resource>{ ptr };
} // ptr goes out of scope, Resource destroyed

// Returns a dumb pointer to an invalid object
Resource* getDumbPtr() {
	auto ptr{ std::make_unique<Resource>() };
	return ptr.get();
} // ptr goes out of scope, Resource destroyed

int main() {
	auto dumb{ getDumbPtr() };
	std::cout << "dumb ptr is: " << ((dumb == nullptr) ? "nullptr\n" : "non-null\n");
	
	auto weak{ getWeakPtr() };
	std::cout << "weak ptr is: " << ((weak.expired()) ? "expired\n" : "valid\n");
	
	return 0;
}
```

- Đều cấp bộ nhớ với smart pointer để đảm bảo chúng bị xóa sau khi ra khỏi hàm
- Khi chạy thì sẽ thấy `dumb` là `non-null` (đang giữ địa chỉ bộ nhớ đã bị xóa -> undefined)
- Còn `weak` sẽ là expired -> tránh undefined
