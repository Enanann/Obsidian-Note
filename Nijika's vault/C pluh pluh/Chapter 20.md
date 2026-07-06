
- Đối số của hàm có thể được pass theo value, reference hoặc address
	- Pass by value cho các kiểu cơ bản 
	- Pass by reference cho struct, class, hoặc khi muốn thay đổi đối số
	- Pass by address khi muốn pass pointer hoặc built-in arrays
- Nên pass by const reference/address khi có thể

- Function có kiểu riêng của nó, tương tự như biến, function có địa chỉ trong bộ nhớ (khiến chúng là lvalue)
- **Function pointer** là pointer trỏ đến một function. Nó cho phép ta pass function vào một function khác
- Hữu ích khi muốn tùy chọn hành vi của một hàm e.g. cách sắp xếp một danh sách

- Để tạo một non-const function pointer
```cpp
// pointer to a function that takes no arguments and returns an integer
int (*fcnPtr)();
```

- `()` xung quanh `*fcnPtr` là cần thiết vì nếu không có `int *fcnPtr()` sẽ trở thành forward declaration cho một hàm không lấy vào đối số và trả về pointer to int 

- Để làm nó const -> để const sau `*`: `int (*const fcnPtr)();`. Nếu const trước int thì nó sẽ là hàm đang trỏ đến sẽ trả về const int 

- Để gán cho function pointer:
```cpp
int foo() {return 5;}
int goo() {return 6;}

int main() {
	int (*fcnPtr)(){&foo}; // fcnPtr points to foo
	fcnPtr = &goo;         // fcnPtr points to goo
	
	return 0;
}
```

- Kiểu của tham số và dữ liệu trả về của function pointer phải khớp với hàm
```cpp
// function prototype
int foo();
double goo();
int hoo(int x);

int (*fcnPtr1)(){&foo};
double (*fcnPtr2)(){&goo};
int (*fcnPtr3)(int){&hoo};
```

- Khác với kiểu dữ liệu cơ bản, C++ sẽ tự chuyển đổi ngầm hàm sang pointer khi cần (sẽ không cần ghi rõ `&` để lấy địa chỉ function). Tuy nhiên function pointer sẽ không chuyển qua void pointer và ngược lại 
```cpp
int foo();

int (*fcnPtr5)(){foo}; // ok, foo implicitly converts to function pointer to foo
void* vPtr{foo}; // not ok, some compiler may allow
```

- Có 2 cách để sử dụng function poiner
1. Explicit dereference
```cpp
int foo(int x) {
	return x;
}

int main() {
	int (*fcnPtr)(int){&foo};
	(*fcnPtr)(5); // call foo(5) through fcnPtr
	
	return 0;
}
```

2. Implicit dereference
```cpp
int foo(int x) {
	return x;
}

int main() {
	int (*fcnPtr)(int){&foo};
	fcnPtr(5); // call foo(5) through fcnPtr
	
	return 0;
}
```
- Cách thứ 2 trông y hệt như gọi hàm bình thường 

- Lưu ý là do function pointer có thể là `nullptr`, vì thế nên kiểm tra trước khi sử dụng 

- Điều hữu ích nhất của function pointer là ta có thể pass nó vào function khác, function được dùng làm đối số còn gọi là **callback functions**

- Nếu tham số của một hàm có kiểu là hàm, có thể viết như sau
```cpp
void selectionSort(int* array, int size, bool (*comparisonFcn)(int, int)) {
	//...
}
// to
void selectionSort(int* array, int size, bool comparisonFcn(int, int)) {
	//...
}
```
- Có thể thêm default function như bình thường 

- Có thể làm gọn code hơn với type alias
```cpp
using ValidateFunction = bool (*)(int, int);

void selectionSort(int* array, int size, ValidateFunction pfcn) {
	//...
}
```

- Một cách khác để định nghĩa và lưu trữ function pointer là sử dụng `std::function` trong `<functional>` 
```cpp
#include <functional>
bool validate(int x, int y, std::function<bool(int, int)> fcn);
// std::function method that returns a bool and take 2 int params
```

- Sử hàm `foo`:
```cpp
int foo() {return 5;}

int main() {
	int (*fcnPtr1)(){&foo};
	
	std::function<int()> fcnPtr2{&fpp};
}
```

- Ta cũng có thể dùng `auto` để suy luận kiểu của function pointer
```cpp
auto fcnPtr{&foo};
```
- Bất lợi là tất cả chi tiết về kiểu trả về, tham số bị ẩn 

- Bộ nhớ của chương trình thường được chia thành nhiều vùng khác nhau, gọi là **segment** (đoạn)
	- **Code segment** (text segment) là nơi chứa chương trình đã được biên dịch, thường là read-only
	- **Bss segment** (uninitialized data segment) là nơi chứa các biến static và global được zero-initialized
	- **Data segment** (initialized data segment) là nơi chứa các biến static và global được khởi tạo
	- **Heap** là nơi chứa các biến cấp phát động
	- **Stack** là nơi chứa tham số hàm, biến local, và các thông tin liên quan về hàm khác 

- Heap có một số lợi ích và bất lợi
	- Cấp phát bộ nhớ trên heap tương đối chậm
	- Bộ nhớ được cấp phát tồn tại cho đến khi được giải phóng cụ thể hoặc khi ứng dụng kết thúc (lúc này OS nên dọn dẹp)
	- Bộ nhớ được cấp phát động phải được truy cập qua pointer. Dereferencing pointer chậm hơn truy cập biến trực tiếp
	- Heap chứa nhiều bộ nhớ -> có thể cấp cho mảng lớn, struct, class 

- **Call stack** (còn được gọi là **stack**) theo dõi toàn bộ các hàm đang hoạt động (đã được gọi nhưng chưa kết thúc) từ bắt đầu chương trình đến thời điểm chạy hiện tại, và xử lý tất cả các tham số hàm và biến 
- Call stack được triển khai như là 1 stack (LIFO)

- Call stack segment chứa bộ nhớ được dùng cho call stack. Khi ứng dụng bắt đầu,  hàm `main()` được đưa vào call stack và chương trình bắt đầu chạy 
- Khi gặp một lời gọi hàm, hàm đó được đưa vào call stack. Khi hàm kết thúc, hàm đó được pop khỏi call stack (gọi là **unwinding the stack**)
- Các item mà ta đưa vào stack gọi là **stack frames**, gồm
	- Địa chỉ của lệnh nằm ngoài phạm vi gọi hàm (**return address**). Đây là cách CPU nhớ nơi trở về sau khi lời gọi hàm kết thúc
	- Tất cả đối số của hàm
	- Bộ nhớ cho biến cục bộ
	- Bản sao của thanh ghi được thay đổi bởi hàm khi hàm trả về 

- Stack sẽ chứa bộ nhớ có giới hạn, khi mà chương trình đặt quá nhiều thông tin vào stack thì sẽ gây ra hiện tượng **stack overflow**
- Thường là kết quả của việc cấp bộ nhớ stack cho quá nhiều biến, và/hoặc quá nhiều hàm lồng với nhau (A gọi B gọi C gọi D ....)

- Một số lợi ích và bất lợi của stack
	- Cấp bộ nhớ trên stack tương đối nhanh
	- Bộ nhớ được cấp phát trong stack ở trong scope miễn là nó ở trong stack. Bị hủy khi pop khỏi stack
	- Tất cả bộ nhớ trong stack là compile time. Kết quả là có thể trực tiếp truy cập chúng qua biến
	- Bởi vì stack nhỏ -> không phải là ý hay để làm việc gì đó tốn nhiều bộ nhớ stack 


- **Command line arguments** là đối số xâu không bắt buộc được pass bởi hệ điều hành đến chương trình khi nó chạy. Chương trình có thể dùng nó cho input (hoặc bỏ qua nó)
- Có thể hiểu tương tự như tham số của hàm cung cấp input cho hàm khác, command line argument cung cấp một cách để ta hoặc các chương trình cung cấp input cho một chương trình 

- Để pass command line arguments, ta chỉ cần liệt kê các CLAs sau tên executable
```bash
./app MyFile.txt

./app MyFile1.txt Myfile2.txt
```

- Để hàm `main` nhận đối số, ta sẽ dùng dạng khác của main
```cpp
int main(int argc, char* argv[])
```
- Có thể ghi dưới dạng pointer to pointer
```cpp
int main(int argc, char** argv)
```

- **argc** là một số nguyên bao gồm số lượng đối số sẽ được pass vào chương trình. Sẽ luôn ít nhất là 1 vì đối số đầu tiên luôn là tên của chương trình. Mỗi CLAs người dùng cung cấp sẽ làm argc tăng thêm 1
- **argv** là nơi mà đối số thực sự được lưu trữ. Nó chỉ là một C-style array chứa char pointers (C-style string) 
```cpp
#include <iostream>

int main(int argc, char* argv[]) {
	std::cout << "There are " << argc << " arguments\n";
	
	for (int count{0}; count < argc; count++) {
		std::cout << count << ' ' << argv[count] << '\n';
	}
	 
	return 0;
}
```

- Do argv luôn là C-string, nếu muốn làm việc với dạng số thì cần chuyển qua int (có thể dùng `std::stringstream`)

- **Lambda expression** (còn được gọi là **lambda** hay **closure**) cho phép chúng ta định nghĩa một hàm ẩn danh (anonymous function) ở trong một hàm khác
- Việc lồng nhau này quan trọng vì nó cho phép ta tránh namespace và naming pollution, cũng như định nghĩa hàm ở nơi nó được dùng gần nhất (thêm ngữ cảnh)
- Có cấu trúc như sau
```cpp
[ captureClause ] ( parameter ) -> returnType {
	statement;
}
```
- **captureClause** có thể để trống nếu không cần captures
- **parameter** có thể để trống nếu không cần tham số. Nó cũng có thể được bỏ hoàn toàn trừ khi kiểu trả về được chỉ rõ 
- **returnType** là tùy chọn, nếu bỏ trống thì `auto` sẽ được sử dụng 

- Viết lại hàm sau
```cpp
// Our function will return true if the element matches
bool containsNut(std::string_view str) {
    // std::string_view::find returns std::string_view::npos if it doesn't find
    // the substring. Otherwise it returns the index where the substring occurs
    // in str.
    return str.find("nut") != std::string_view::npos;
}

int main() {
    std::array<std::string_view, 4> arr{ "apple", "banana", "walnut", "lemon" };
    
    // Scan our array to see if any elements contain the "nut" substring
    auto found{ std::find_if(arr.begin(), arr.end(), containsNut) };
    
    if (found == arr.end()) {
        std::cout << "No nuts\n";
    } else {
        std::cout << "Found " << *found << '\n';
    }
    
    return 0;
}
```

```cpp
auto found{ std::find_if(arr.begin(), arr.end(), [](std::string_view str) {
	return str.find("nut") != std::string_view::npos;
})};
```

- Cách sử dụng lambda ở trên đôi khi được gọi là **function literal**. Có thể hiểu là ta chèn luôn code vào đó -> có thể khiến code khó đọc
- Ta có thể tạo một biến lambda và pass nó vào
```cpp
auto containsNut{[](std::string_view str) {
	return str.find("nut") != std::string_view::npos;
}};
```
- Thực chất thì lambda "không có kiểu", compiler tự sinh một kiểu độc lập dành riêng cho nó 
- Best practice:
	- Khi lưu lambda trong biến, sử dụng `auto` là kiểu của biến
	- Khi pass lambda vào hàm:
		- C++20: sử dụng `auto` là kiểu của tham số
		- Nếu không, dùng hàm với tham số là type template, hoặc dùng tham số là `std::function`  function pointer nếu lambda không có captures)

- C++14, lambda có thể dùng `auto` cho tham số, tức là nó là viết tắt của template parameter (C++20 mới mở rộng qua hàm bình thường - abbreviated function template) => có thể làm việc với nhiều kiểu dữ liệu => **generic lambdas**

- Lambda được ngầm định là constexpr kể từ C++17 nếu nó thỏa mãn điều kiện
	- Không có captures, hoặc tất cả captures phải là constexpr
	- Hàm gọi bởi lambda phải là constexpr (nhiều hàm trong thư viện chuẩn algorithm và math không là constexpr cho đến C++20 hay C++23)

- Giống như function template với biến static local, generic lambda sẽ tạo một phiên bản khác cho mỗi kiểu khác nhau mà `auto` trở thành 
```cpp
#include <algorithm>
#include <array>
#include <iostream>
#include <string_view>

int main() {
	// Print a value and count how many times @print has been called.
	auto print{[](auto value) {
		static int callCount{ 0 };
		std::cout << callCount++ << ": " << value << '\n';
	}};
	
	print("hello"); // 0: hello
	print("world"); // 1: world
	
	print(1); // 0: 1
	print(2); // 1: 2
	
	print("ding dong"); // 2: ding dong
	
	return 0;
}
```

- Quay lại với code tìm "nut", nếu ta muốn tìm một từ chứa substring bất kỳ
```cpp
int main() {
    std::array<std::string_view, 4> arr{ "apple", "banana", "walnut", "lemon" };
    
    std::string search{};
    std::cin >> search;
    // Scan our array to see if any elements contain the "nut" substring
    auto found{ std::find_if(arr.begin(), arr.end(), [](std::string_view str) {
		return str.find(search) != std::string_view::npos;
		// Error: search not accessible in this scope
	})};
    
    if (found == arr.end()) {
        std::cout << "No nuts\n";
    } else {
        std::cout << "Found " << *found << '\n';
    }
    
    return 0;
}
```
- Thì sẽ bị lỗi do lambda không truy cập được search. Khác với khối lồng nhau, lambdas chỉ có thể truy cập một số loại object được định nghĩa ngoài lambda:
	- Object với static (hoặc thread local) storage duration (bao gồm biến global và static local)
	- Constexpr object 
- Vì ở trên `search` không thỏa mãn cái nào nên lambda không truy cập được -> cần sử dụng capture clause

- **Capture clause** được sử dụng để (gián tiếp) cho lambda truy cập đến với một biến ở scope xung quanh mà bình thường không thể truy cập được 
- Ta chỉ cần liệt kê các biến ta muốn lambda truy cập trong capture clause 
```cpp
//                                                vvvvvv
auto found{ std::find_if(arr.begin(), arr.end(), [search](std::string_view str) {
	return str.find(search) != std::string_view::npos;
})};
```
- Biến được capture thực chất là **bản sao** của biến ở scope ngoài, không thực chất là biến đó 

- Capture được coi như là const theo mặc định, tức là lambda không thể thay đổi capture 
- Để cho phép lambda có quyền thay đổi capture, ta phải đặt nó là `mutable`, tuy nhiên thì biến được capture ở ngoài không bị thay đổi do capture chỉ là bản sao 
```cpp
int ammo{10};

auto shoot{[ammo]() mutable {
	--ammo;
	std::cout << ammo << " shot(s) left.\n";
}};
shoot(); // 9 shot(s) left.

std::cout << ammo << " shot(s) left.\n"; // 10 shot(s) left.
```
- Best practice: Tránh mutable lambda. Non-mutable lambdas dễ hiểu hơn cũng như không gây ra một số vấn đề liên quan đến bản sao, hay là vấn đề nguy hiểm hơn khi thêm thực thi song song 

- Nếu muốn lambda thực sự thay đổi biến ở ngoài -> sử dụng reference (không cần mutable nữa) => **capture by reference**
```cpp
auto shoot{[&ammo]() {
	--ammo;
	std::cout << ammo << " shot(s) left.\n";
}};
shoot(); // 9 shot(s) left.

std::cout << ammo << " shot(s) left.\n"; // 9 shot(s) left.
```

- Để capture nhiều biến, liệt kê + phân cách bằng `,`
```cpp
int a{1};
int b{2};
double c{3};

// capture a and b by value, c by reference
[a, b, &c]() {};
```

- **Default capture** (**capture-default**) sẽ capture tất cả các biến được nhắc đến trong lambda. Các biến không nhắc trong lambda sẽ không được capture nếu sử dụng default capture
	- Để capture tất cả biến được sử dụng theo value, dùng `=`
	- Để capture tất cả biến được sử dụng theo reference, dùng `&`
```cpp
int x{ 10 }; int y{ 20 }; 

// Dùng [=] để copy x và y 
auto add{[=]() {
	return x + y;
}};

// Dùng [&] để tham chiếu tới x và y 
auto multiply{[&]() {
	// Có thể thay đổi giá trị gốc bên ngoài
	x = 5;
	return x * y;
}}; 
```

- Có thể mix với normal capture, ta có thể capture biến này theo value, biến kia theo reference, nhưng mỗi biến chỉ được capture một lần
```cpp
int health{ 33 };
int armor{ 100 };
std::vector<CEnemy> enemies{};

// Capture health and armor by value, and enemies by reference.
[health, armor, &enemies](){};

// Capture enemies by reference and everything else by value.
[=, &enemies](){};

// Capture armor by value and everything else by reference.
[&, armor](){};

// Illegal, we already said we want to capture everything by reference.
[&, &armor](){};

// Illegal, we already said we want to capture everything by value.
[=, armor](){};

// Illegal, armor appears twice.
[armor, &health, &armor](){};

// Illegal, the default capture has to be the first element in the capture group.
[armor, &](){};
```

- Ta có thể định nghĩa biến mới trong capture. Biến này chỉ có thể được thấy trong scope của lambda 
```cpp
std::array areas{ 100, 25, 121, 40, 56 };

int width{};
int height{};

std::cin >> width >> height;

// We store areas, but the user entered width and height.
// We need to calculate the area before we can search for it.
auto found{ std::find_if(areas.begin(), areas.end(), 
						// Declare a new variable only visible to the lambda.
						// The type of userArea is automatically deduced to int.
						[userArea{ width * height }](int knownArea) {
							return userArea == knownArea;
						})};

if (found == areas.end()) {
	std::cout << "I don't know this area :(\n";
} else {
	std::cout << "Area found :)\n";
}
```
- Best practice: Chỉ khởi tạo biến trong capture nếu giá trị của chúng ngắn và kiểu của chúng là hiển nhiên (**init capture**), còn không thì nên tạo ở ngoài sau đó capture 

- Còn nếu định nghĩa trong hàm lambda thì nó sẽ mang scope của lambda như hàm bình thường. Nếu trùng tên biến ở ngoài capture thì sẽ bị shadowing (kể cả reference)
```cpp
int ammo{10};

auto shoot{[&ammo]() {
	int ammo{1};
	--ammo;
	std::cout << ammo << " left\n";
}};

shoot();               // 0 left
std::cout << ammo;     // 10
```


### optional (ellipsis)

- Từ trước đến nay, số tham số của hàm luôn được biết trước. Sẽ có vài trường hợp mà ta muốn pass một số tham số không biết trước vào hàm. C++ cung cấp một định danh đặc biệt là **ellipsis** (hay ...) để làm điều này 