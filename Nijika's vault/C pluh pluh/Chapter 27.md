
- Exceptions trong C++ cung cấp cơ chế để **tách rời** việc xử lý các lỗi hoặc các trường hợp ngoại lệ khỏi luồng điều khiển thông thường của code
- Cho phép tự do hơn trong việc xử lý lỗi khi nào và bằng cách nào hữu ích nhất trong một tình huống cụ thể,  giảm thiểu hầu hết (hoặc tất cả) sự phức tạp mà return gây ra 

- Exceptions trong C++ được thực hiện qua 3 từ khóa hoạt động kết hợp (conjunction) với nhau: `throw`, `try`, `catch`

- **Throw statement** được sử dụng để ra hiệu rằng một trường hợp ngoại lệ hoặc lỗi đã xảy ra (còn được gọi là **raising exception**)
- Sử dụng bằng cách sử dụng keyword `throw` + bất cứ giá trị nào ta muốn sử dụng (thường sẽ là error code, mô tả lỗi, hoặc là lớp custom)
```cpp
throw -1; // throw a literal integer value
throw ENUM_INVALID_INDEX; // throw an enum value
throw "Can not take square root of negative number"; // throw a literal C-style (const char*) string
throw dX; // throw a double variable that was previously defined
throw MyException("Fatal Error"); // Throw an object of class MyException
```

- Để kiểm tra lỗi của một đoạn code, ta sử dụng `try` (try block). Try block có tác dụng như là người quan sát, tìm kiếm các exceptions được throw bởi lệnh trong khối này
```cpp
try {
    // Statements that may throw exceptions you want to handle go here
    throw -1; // here's a trivial throw statement
}
```

- Cuối cùng, để bắt lỗi và thực hiện xử lý ngoại lệ cho một kiểu dữ liệu, ta sử dụng `catch`
```cpp
catch (int x) {
    // Handle an exception of type int here
    std::cerr << "We caught an int exception with value" << x << '\n';
}
```

- Nếu không sử dụng biến exceptions, có thể bỏ trống tên tham số. Tham số trong catch không thể được chuyển đổi kiểu
```cpp
try {
	// Statements that may throw exceptions you want to handle go here
	throw -1; // here's a trivial example
}
// no variable name since we don't use the exception itself in the block below
catch (double) {
	// Any exceptions of type double thrown within the above try block get sent here
	std::cerr << "We caught an exception of type double\n";
}
catch (int x) {
	// Any exceptions of type int thrown within the above try block get sent here
	std::cerr << "We caught an int exception with value: " << x << '\n';
}
catch (const std::string&) // catch classes by const reference
{
	// Any exceptions of type std::string thrown within the above try block get sent here
	std::cerr << "We caught an exception of type std::string\n";
}
```

- Catch block thường làm những điều sau
	- In lỗi (ra console hoặc log file) sau đó cho phép hàm tiếp tục
	- Có thể trả về giá trị hoặc error code cho caller
	- Có thể throw ngoại lệ khác. Vì catch block nằm ngoài try block, ngoại lệ mới được throw sẽ được xử lý trong khối try-catch tiếp theo
	- Catch block trong main có thể được dùng để kiểm tra lỗi nghiêm trọng và tạm dừng chương trình lập tức

- Exceptions  sẽ được xử lý ngay lập tức, nếu một exception được phát sinh, luồng thực thi sẽ nhảy đến khối try gần nhất có block catch mà có thể xử lý exception. Nếu một try/catch phù hợp được tìm thấy, stack sẽ được **unwound** (các đối tượng cục bộ bị hủy và các hàm lần lượt thoát ra) cho đến khi tìm được catch block phù hợp. Sau đó, chương trình sẽ  tiếp tục từ đầu của catch đó 
- Nếu không tìm thấy try hoặc match phù hợp thì chương trình gọi `std::terminate`, sẽ hủy chương trình với lỗi **unhandle exception**

- Để có thể catch mọi ngoại lệ, sử dụng **catch-all handler**. Nó phải được để cuối trong chuỗi catch block
```cpp
int main() {
	try {
		throw 5; // throw an int exception
	}
	catch (double x) {
		std::cout << "We caught an exception of type double: " << x << '\n';
	}
	catch (...) // catch-all handler
	{
		std::cout << "We caught an exception of an undetermined type\n";
	}
}
```

- Do catch-all handler sẽ catch mọi loại ngoại lệ, trong bản debug nên tắt tạm thời nó đi để có thể phát hiện vấn đề ở đâu (có thể qua macro `ifndef NDEBUG...`)

- Try catch hoàn toàn có thể được sử dụng trong hàm thành viên và hàm khởi tạo của class 

- Để tránh độ mơ hồ của catch block, ta có thể tạo một hàm Exception riêng
- Best practice
	- Exceptions của kiểu cơ bản có thể được catch bằng value
	- Exceptions của kiểu lớp nên được catch bằng (const) tham chiếu để tránh việc copying và slicing 

- Đối với các lớp dẫn xuất, exception cũng có thể được match với lớp cơ sở, vì thế nên cần để thứ tự catch block từ trên xuống dưới là lớp dẫn xuất nhất đến lớp cơ sở nhất
```cpp
#include <iostream>

class Base {
public:
    Base() {}
};

class Derived: public Base {
public:
    Derived() {}
};

int main() {
    try {
        throw Derived();
    }
    catch (const Base& base) {
        std::cerr << "caught Base";
    }
    catch (const Derived& derived) {
        std::cerr << "caught Derived";
    }

    return 0;
}
```

```cpp 
caught Base // need to swap the two catch blocks
```

- Nhiều lớp và toán tử trong thư viện chuẩn sẽ throw một exception class khi thất bại. Tính đến C++20 có 28 class exceptions khác nhau có thể bị throw. Tất cả chúng đều được dẫn xuất từ một lớp là `std::exception` (trong `<exception>)
- Ta có thể catch nó trong hầu hết mọi trường hợp mà không quan tâm cụ thể nó là gì 
```cpp
try {
	// Your code using standard library goes here
	// We'll trigger one of these exceptions intentionally for the sake of the example
	std::string s;

	// will trigger a std::length_error or allocation exception
	s.resize(std::numeric_limits<std::size_t>::max()); 
}
// This handler will catch std::exception and all the derived exceptions too
catch (const std::exception& exception) {
	std::cerr << "Standard exception: " << exception.what() << '\n';
}
```

- `.what()` ở đây là một virtual function của từng lớp dẫn xuất cụ thể,  ta hoàn toàn có thể tạo lớp exception của riêng ta và kế thừa từ `std::exception`
```cpp
class ArrayException : public std::exception {
public:
	ArrayException(std::string_view error)
		: m_error{error}
	{
	}

	// std::exception::what() returns a const char*, so we must as well
	const char* what() const noexcept override { return m_error.c_str(); }
	
private:
	std::string m_error{}; // handle our own string
};
```
- Do `what()` là `noexcept`, nên hàm `what` của ta cũng để là `noexcept`

- Ta cũng có tạo lớp ngoại lệ của ta kế thừa từ  `std::runtime_error`, do `std::runtime_error` có khả năng xử lý string. Ta sẽ không cần override `what()` nữa. Tham số khởi tạo sẽ có thể là C-style string, hoặc `const std::string&`
```cpp
class ArrayException : public std::runtime_error {
public:
	// std::runtime_error takes either a null-terminated const char* or a const std::string&.
	// We will follow their lead and take a const std::string&
	ArrayException(const std::string& error)
		: std::runtime_error{ error } // std::runtime_error will handle the string
	{
	}


	// no need to override what() since we can just use std::runtime_error::what()
};
```


- Trong trường hợp mà ta muốn catch một ngoại lệ, nhưng lại không muốn (hoặc không có khả năng) xử lý nó hoàn toàn tại nơi mà ta catch (thường khi ta muốn log một lỗi, nhưng truyền vấn đề này cùng với caller để thực hiện xử lý)
- Ta hoàn toàn có thể throw một exception mới để sau khi unwind stack, khối try block caller sẽ thực hiện xử lý tiếp
- Còn nếu ta muốn rethrow lại chính exception này, ta sẽ sử dụng `throw;` và **không thêm gì cả**. 
- Do `throw expression;` sẽ thực hiện copy initialized đối tượng exception, nên có thể xảy ra hiện tượng slicing. Nếu dùng pointer, chỉ có giá trị địa chỉ được copy chứ không copy object mà pointer trỏ tới, do đó có thể dẫn đến dangling pointer nếu object gốc bị hủy trong quá trình stack unwinding (hoặc phải tự quản lý bộ nhớ nếu cấp phát động)  
- `throw;` là ngoại lệ, nó chỉ rethrow exception hiện tại 
```cpp
#include <iostream>
class Base {
public:
    Base() {}
    virtual void print() { std::cout << "Base"; }
};

class Derived: public Base {
public:
    Derived() {}
    void print() override { std::cout << "Derived"; }
};

int main() {
    try {
        try {
            throw Derived{};
        }
        catch (Base& b) {
            std::cout << "Caught Base b, which is actually a ";
            b.print();
            std::cout << '\n';
            throw; // note: We're now rethrowing the object here
        }
    }
    catch (Base& b) {
        std::cout << "Caught Base b, which is actually a ";
        b.print();
        std::cout << '\n';
    }

    return 0;
}
```
```
Caught Base b, which is actually a Derived
Caught Base b, which is actually a Derived
```

**function try block** (...)

- Một vấn đề cần chú ý đến khi sử dụng exception là dọn dẹp tài nguyên. Một số ví dụ
```cpp
#include <iostream>

try {
    openFile(filename);
    writeFile(filename, data);
    closeFile(filename);
}
catch (const FileException& exception) {
    std::cerr << "Failed to write to file: " << exception.what() << '\n';
}
```
- Nếu `writeFile()` thất bại và throw exception thì `closeFile()` sẽ không bao giờ được gọi. Ta cầ gọi `closeFile()` ở ngoài try/catch 
```cpp
#include <iostream>

try {
    openFile(filename);
    writeFile(filename, data);
}
catch (const FileException& exception) {
    std::cerr << "Failed to write to file: " << exception.what() << '\n';
}

// Make sure file is closed
closeFile(filename);
```

```cpp
#include <iostream>

try {
    auto* john { new Person{ "John", 18, PERSON_MALE } };
    processPerson(john);
    delete john;
}
catch (const PersonException& exception) {
    std::cerr << "Failed to process person: " << exception.what() << '\n';
}
```
- Nếu `processPerson()` thất bại và throw exception thì `john` sẽ bị hủy khi đi ra khỏi try block, gây memory leak. Sẽ có 2 cách để fix
	- Khai báo `john` ở ngoài block để tránh memory leak 
	- Sử dụng biến thành viên có khả năng tự dọn dẹp e.g. `std::unique_ptr`
```cpp
#include <iostream>

Person* john{ nullptr };

try {
    john = new Person("John", 18, PERSON_MALE);
    processPerson(john);
}
catch (const PersonException& exception) {
    std::cerr << "Failed to process person: " << exception.what() << '\n';
}

delete john;
```

```cpp
#include <iostream>
#include <memory> // for std::unique_ptr

try {
    auto john = std::make_unique<Person>("John", 18, PERSON_MALE);

    ProcessPerson(*john); // ProcessPerson() require a raw pointer

    // when john goes out of scope, it will delete itself
}
catch (const PersonException& exception) {
    std::cerr << "Failed to process person: " << exception.what() << '\n';
}
```

- Khác với hàm khởi tạo, hàm hủy **không bao giờ nên có** exception. Vấn đề xảy ra khi exception được throw khỏi hàm hủy (*thoát ra ngoài*) trong quá trình stack unwinding, lúc này compiler sẽ không bbiếtphari tiếp tục stack unwinding hay xử lý exception, kết quả là chương trình sẽ bị terminated (Thay vào đó ta có thể ghi ra log)

- Trong C++, mọi hàm được phân làm 2 loại: **non-throwing** và **potentially throwing**
	- **Non-throwing**: Là hàm hứa không throw exception, được đánh dấu với `noexcept`
	- **Potentially throwing**: Là hàm có thể throw exception 

- Lưu ý là hàm non-throwing không ngăn chặn hoàn toàn hàm throw exception hoặc gọi các hàm potentially throwing. Điều này cho phép miễn là hàm noexcept catch và xử lý các exceptions đó trong hàm nó, và exceptions **không thoát ra** khỏi hàm noexcept 
```cpp
// h/t to reader yellowEmu for the first draft of this program
#include <iostream>

class Doomed {
public:
    ~Doomed() {
        std::cout << "Doomed destructed\n";
    }
};

void thrower() {
    std::cout << "Throwing exception\n";
    throw 1;
}

void pt() {
    std::cout << "pt (potentally throwing) called\n";
    //This object will be destroyed during stack unwinding (if it occurs)
    Doomed doomed{};
    thrower();
    std::cout << "This never prints\n";
}

void nt() noexcept {
    std::cout << "nt (noexcept) called\n";
    //This object will be destroyed during stack unwinding (if it occurs)
    Doomed doomed{};
    thrower();
    std::cout << "this never prints\n";
}

void tester(int c) noexcept {
    std::cout << "tester (noexcept) case " << c << " called\n";
    try
    {
        (c == 1) ? pt() : nt();
    }
    catch (...)
    {
        std::cout << "tester caught exception\n";
    }
}

int main()
{
    std::cout << std::unitbuf; // flush buffer after each insertion
    std::cout << std::boolalpha; // print boolean as true/false
    tester(1);
    std::cout << "Test successful\n\n";
    tester(2);
    std::cout << "Test successful\n";

    return 0;
}
```

```
tester (noexcept) case 1 called
pt (potentially throwing) called
Throwing exception
Doomed destructed
tester caught exception
Test successful

tester (noexcept) case 2 called
nt (noexcept) called
throwing exception
terminate called after throwing an instance of 'int'
```

- Note: `noexcept` có thể có tham số bool tùy chọn (`true` -> non-throwing; `false`-> potentially throwing). Đây thường được dùng trong template

- Dù code của bạn không throw lỗi không có nghĩa là luôn nên đánh dấu nó là `noexcept`. Các lí nên do đánh dấu hàm là non-throwing
	- Hàm non-throwing có thể được gọi từ các hàm không **exception-safe**, như là hàm hủy
	- Có thể cho phép compiler thực hiện tối ưu hóa
	- Có một số trường hợp mà việc biết một hàm có non-throwing hay không cho phép ta tạo code hiệu quả hơn 

- Luôn đánh dấu các hàm sau là `noexcept`
	- Move constructors
	- Move assignment operators
	- Swap functions

- Xem xét đánh dấu là `noexcept`
	- Hàm mà ta muốn diễn tả nó là no-throw hoặc no-fail (e.g. để document)
	- Copy constructors và copy assignment operators mà là no-throw (để tối ưu hóa)
	- Hàm hủy. Nó được ngầm định là `noexcept` miễn là tất cả các thành viên có hàm hủy `noexcept` 

**`std::move_if_noexcept`**

- Ôn lại bản chất của `std::move`, nó chỉ có việc là cast object đầu vào thành một rvalue reference (T&&), cho phép ta đối xử với lvalue như rvalue. `std::move` **không thực hiện việc move**, các hàm của ta tạo sẽ phải thực hiện điều này
```cpp
// Example move constructor definition for std::pair
// Take in an 'old' pair, and then move construct the new pair's 'first' and 'second' subobjects from the 'old' ones
template <typename T1, typename T2>
pair<T1,T2>::pair(pair&& old)
  : first(std::move(old.first)),
    second(std::move(old.second))
{}
```

- Giả sử ta có một `std::pair`, trong đó `first` có move constructor, còn `second` không có move constructor nên khi "move" sẽ phải sử dụng copy constructor. 
```cpp
#include <iostream>
#include <utility> // For std::pair, std::make_pair, std::move, std::move_if_noexcept
#include <stdexcept> // std::runtime_error

class MoveClass
{
private:
  int* m_resource{};

public:
  MoveClass() = default;

  MoveClass(int resource)
    : m_resource{ new int{ resource } }
  {}

  // Copy constructor
  MoveClass(const MoveClass& that)
  {
    // deep copy
    if (that.m_resource != nullptr)
    {
      m_resource = new int{ *that.m_resource };
    }
  }

  // Move constructor
  MoveClass(MoveClass&& that) noexcept
    : m_resource{ that.m_resource }
  {
    that.m_resource = nullptr;
  }

  ~MoveClass()
  {
    std::cout << "destroying " << *this << '\n';

    delete m_resource;
  }

  friend std::ostream& operator<<(std::ostream& out, const MoveClass& moveClass)
  {
    out << "MoveClass(";

    if (moveClass.m_resource == nullptr)
    {
      out << "empty";
    }
    else
    {
      out << *moveClass.m_resource;
    }

    out << ')';

    return out;
  }
};


class CopyClass
{
public:
  bool m_throw{};

  CopyClass() = default;

  // Copy constructor throws an exception when copying from
  // a CopyClass object where its m_throw is 'true'
  CopyClass(const CopyClass& that)
    : m_throw{ that.m_throw }
  {
    if (m_throw)
    {
      throw std::runtime_error{ "abort!" };
    }
  }
};

int main()
{
  // We can make a std::pair without any problems:
  std::pair my_pair{ MoveClass{ 13 }, CopyClass{} };

  std::cout << "my_pair.first: " << my_pair.first << '\n';

  // But the problem arises when we try to move that pair into another pair.
  try
  {
    my_pair.second.m_throw = true; // To trigger copy constructor exception

    // The following line will throw an exception
    std::pair moved_pair{ std::move(my_pair) }; // We'll comment out this line later
    // std::pair moved_pair{ std::move_if_noexcept(my_pair) }; // We'll uncomment this later

    std::cout << "moved pair exists\n"; // Never prints
  }
  catch (const std::exception& ex)
  {
      std::cerr << "Error found: " << ex.what() << '\n';
  }

  std::cout << "my_pair.first: " << my_pair.first << '\n';

  return 0;
}
```

- Đầu ra
```
destroying MoveClass(empty)
my_pair.first: MoveClass(13)
destroying MoveClass(13)
Error found: abort!
my_pair.first: MoveClass(empty)
destroying MoveClass(empty)
```

- Có thể thấy do bị throw giữa chừng, nên việc move cũng sẽ bị dừng giữa chừng. `moved_pair` không được tạo thành công, nhưng `my_pair.first` đã bị move khỏi đối tượng nguồn, khiến `my_pair` rơi vào trạng thái **partially moved-from**.

- Để tránh trường hợp một phép move thất bại giữa chừng và làm đối tượng nguồn bị **partially moved-from**, ta có thể sử dụng `std::move_if_noexcept()`
- `std::move_if_noexcept()` sẽ quyết định nên **move** hay **copy** đối tượng:
	- Nếu kiểu dữ liệu có **move constructor được đánh dấu `noexcept`** (hoặc kiểu đó là **move-only**, tức không có copy constructor), nó sẽ hoạt động như `std::move()` và trả về một **rvalue reference (`T&&`)**
	- Ngược lại, nó sẽ trả về một **const lvalue reference (`const T&`)**, để compiler ưu tiên gọi copy constructor thay vì move constructor

- Cập nhật code trên
```cpp
//std::pair moved_pair{std::move(my_pair)}; // comment out this line now
std::pair moved_pair{std::move_if_noexcept(my_pair)}; // and uncomment this line
```

- Đầu ra
```
destroying MoveClass(empty)
my_pair.first: MoveClass(13)
destroying MoveClass(13)
Error found: abort!
my_pair.first: MoveClass(13)
destroying MoveClass(13)
```

- Lưu ý: `std::move_if_noexcept()` **không ngăn exception xảy ra**. Nếu copy constructor cũng có thể throw (như ví dụ trên), exception vẫn sẽ được phát sinh. Mục đích của `std::move_if_noexcept()` là tránh làm đối tượng nguồn bị **partially moved-from** khi move constructor có khả năng throw