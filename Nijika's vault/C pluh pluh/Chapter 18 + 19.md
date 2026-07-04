# Chapter 18

- Bởi vì sắp xếp mảng rất hay dùng, C++ cung cấp hàm `std::sort` trong `<algorithm>`
```cpp
int array[] {30, 50, 20, 10};
std::sort(std::begin(array), std::end(array)); 

std::vector<int> ve {30, 50, 20, 10};
std::sort(ve.begin(), ve.end());
```

- **Iterator** là object được thiết kế để đi qua một container (e.g. giá trị trong mảng, ký tự trong xâu), cung cấp truy cập đến mỗi thành phần trên đường đi 
- Một dạng iterator cơ bản nhất là sử dụng pointer arithmetic
```cpp
std::array<int, 7> arr {0, 1, 2, 3, 4, 5, 6};

auto begin{&arr[0]};
auto end{begin + std::size(arr)};

for (auto ptr{begin}; ptr != end; ++ptr) {
	std::cout << *ptr << ' ';
}
```

- Nếu ta sử dụng
```cpp
auto end{&arr[std::size(arr)]};
```
- Thì có nghĩa là ta đang lấy địa chỉ của một phần tử phía sau mảng (0-based index)
- Thay vào đó dùng
```cpp
auto end{arr.data() + std::size(arr)}; 
// data() returns a pointer to the first element
```

- Một dạng iterator khác là dùng luôn của thư viện chuẩn C++
```cpp
auto begin{array.begin()};
auto end{array.end()};
```

- Header iterator cũng cung cấp 2 hàm generic `std::begin` và `std::end` (dùng cho C-style array)
```cpp
#include <array> // includes <iterator>

int main() {
	std::array array{1, 2, 3, 4};
	
	auto begin{std::begin(array)};
	auto end{std::end(array)};
}
```

- Đối với iterator, tiêu chuẩn sẽ là dùng `!=` thay cho `<` trong vòng lặp do một số kiểu iterator không so sánh tương đối với nhau được 

- Range-based for loop sử dụng iterator ở sau hậu trường, vì thế neen tránh làm lỗi iterator (dangling iterator)
```cpp
#include <vector>

int main() {
    std::vector v { 0, 1, 2, 3 };
    // implicitly iterates over v 
    for (auto num : v){
        if (num % 2 == 0)
			// when this invalidates the iterators of v, undefined behavior 
			// will result
            v.push_back(num + 1); 
    }
    
    return 0;
}
```

- Trường hợp khác:
```cpp
#include <iostream>
#include <vector>

int main() {
	std::vector v{ 1, 2, 3, 4, 5, 6, 7 };
	auto it{ v.begin() };
	
	++it; // move to second element
	std::cout << *it << '\n'; // ok: prints 2
	
	v.erase(it); // erase the element currently being iterated over
	
	// erase() invalidates iterators to the erased element (and subsequent
	// elements)
	// so iterator "it" is now invalidated
	
	++it; // undefined behavior
	std::cout << *it << '\n'; // undefined behavior
	
	return 0;
}
```
- Có thể fix bằng cách gán lại cho nó iterator hợp lý e.g. `begin()`, `end()` hay là giá trị trả về của hàm mà trả về iterator
- Hàm `erase()` ở trên trả về iterator cho thành phần ở tiếp theo thành phần bị xóa (`end()` nếu thành phần bị xóa là cuối cùng) -> có thể fix code trên như sau
```cpp
it = v.erase(it); // erase current element + set iterator to the next element 
```

- Thay vì phải dành thời gian để viết các hàm làm tác vụ cơ bản phổ biến, có thể sử dụng hàm đó của thư viện tiêu chuẩn C++
- Tính năng của các hàm được chia làm 3 loại:
	- **Inspectors**: Dùng để xem (không thay đổi) dữ liệu trong container e.g. search, count
	- **Mutators**: Dùng để thay đổi dữ liệu trong container e.g. sort, shuffle
	- **Facilitators**: Dùng để tạo kết quả dựa vào giá trị của biến thành viên e.g. object mà nhân giá trị, hoặc object quyết định thứ tự sắp xếp của cặp các elements 

- Các hàm này ở trong `<algorithm>`

- `std::find` để tìm element theo giá trị. Đầu vào gồm iterator khởi đầu, iterator kết thúc, giá trị muốn tìm -> trả về iterator của element (`end()` nếu không tìm thấy)
```cpp
int search{3};
auto found{std::find(arr.begin(), arr.end(), search)}; // find 3 in array 
// if not found -> found == arr.end()
```

- `std::find_if` để tìm element thỏa mãn điều kiện nào đó, hoạt động giống `std::find`, nhưng thay vì pass giá trị cần tìm, ta pass 1 **callable object** e.g. **function pointer** hay **lambda** 
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

- `std::count` và `std::count_if` dùng để đếm có bao nhiêu xuất hiện của một thành phần nào đó. Đầu vào tương tự `std::find` và `std::find_if`
```cpp
bool containsNut(std::string_view str) {
	return str.find("nut") != std::string_view::npos;
}

int main() {
	std::array<std::string_view, 4> arr{ banana", "walnut", "lemon", "peanut" };
	
	auto nuts{ std::count_if(arr.begin(), arr.end(), containsNut) };
	
	std::cout << "Counted " << nuts << " nut(s)\n";
	
	return 0;
}
```

- `std::sort` để sắp xếp mảng tùy chỉnh. Lấy thêm 1 fucntion so sánh là tham số thứ 3 
- Nếu ta muốn sắp xếp theo thứ tự tùy chỉnh, có thể thêm hàm lambda hoặc hàm riêng
```cpp
bool greater(int a, int b) {
	return a > b;
}

std::sort(ve.begin(), ve.end(), greater);

std::sort(ve.begin(), ve.end(), [](int a, int b) {
	return a > b; // descending
});
```
- Do sắp xếp giảm dần quá phổ biến, C++ cung cấp kiểu custom `std::greater` (trong `<functional>`)
```cpp
std::sort(ve.begin(), ve.end(), std::greater{});
// before C++17, need to specify the type e.g. std::greater<int>{}
```
- Lưu ý `std::greater` cần `{}` vì nó không phải là một hàm gọi được, nó là 1 kiểu (type)

- `std::for_each` để thực hiện một hành động gì đó đến tất cả các thành phần trong container 
- Đầu vào là iterator khởi đầu, iterator kết thúc, và một hàm custom
```cpp
void doubleNumber(int a) {
	a *= 2;
}

int main() {
	std::array arr{1, 2, 3};
	
	std::for_each(arr.begin(), arr.end(), doubleNumber); // 2, 4, 6
}
```
- Có thể bỏ qua thành phần ở đầu hoặc cuối containter e.g. bỏ qua thành phần đầu tiên dùng `std::next`
```cpp
std::for_each(std::next(arr.begin()), arr.end(), doubleNumber); // 1, 4, 6
```

- C++20 có thêm ranges, giúp tránh việc ghi đi ghi lại `begin()` và `end()` 
- Có cấu trúc như sau `std::ranges::thuật_toán(range, arguments..., projection);` 
	- **`range`**: Có thể là một container (`std::vector`, `std::array`) hoặc một `std::views`
	- **`arguments`**: Giá trị cần tìm hoặc hàm Lambda (tùy thuật toán).
	- **`projection` (tùy chọn)**: Tham số cuối cùng, cho phép bạn chỉ định "nhìn" vào một thuộc tính cụ thể của phần tử. 
```cpp
std::ranges::sort(v);                           // Range đơn giản
std::ranges::find(v, 5);                        // Range + giá trị
std::ranges::for_each(v, func);                 // Range + lambda
std::ranges::find(houses, 101, &House::id);     // Range + giá trị + projection
```

- Để xem hiệu năng của code, có thể dùng `<chrono>` 

# Chapter 19

- C++ hỗ trợ 3 kiểu cấp bộ nhớ cơ bản
	- **Static memory allocation** xảy ra cho biến global và static. Bộ nhớ của các kiểu này được cấp khi chương trình bắt đầu và tồn tại suốt quá trình chạy
	- **Automatic memory allocation** xảy ra cho các tham số của hàm và biến local. Bộ nhớ của các kiểu này được cấp khi block tương ứng được truy cập, và giải phóng khi ra khỏi block đó, nhiều lần nếu cần thiết
	- **Dynamic memory allocation**

- Static malloc và automatic malloc có điểm chung là
	- Kích cỡ của biến/mảng phải được biết tại thời điểm biên dịch
	- Cấp và giải phóng bộ nhớ được thực hiện tự động 

- Cần có thể cung cấp bộ nhớ động do:
	- Có thể gây tốn bộ nhớ thừa không được dùng
	- Không biết phần nào đang được dùng 
	- Hầu hết các biến/fixed-array đều được cung cấp bộ nhớ trên **stack** -> ít 
	- Có thể dẫn đến tràn bộ nhớ e.g. có 400 bản nhưng mà mảng chỉ có 300 thành phần 

- Để cấp bộ nhớ động cho một biến đơn, dùng `new`
```cpp
new int; // dynamically allocate an integer (and discard the result)
```
- Ta yêu cầu hệ thống cấp bộ nhớ ứng với 1 integer, `new` sẽ tạo object dùng bộ nhớ đó, và trả về pointer chứa địa chỉ bộ nhớ đó
- Thông thường, ta sẽ gán nó với một pointer
```cpp
int* ptr{new int};

*ptr = 7;
```

- Bộ nhớ tạo bằng `new` sẽ được đặt ở **heap**. Truy cập **heap-allocated object** thường sẽ chậm hơn stack-allocated object do compiler biết địa chỉ của stack-allocated object -> có thể trực tiếp đi đến đó 

- Khác với static và automatic memory allocation, dynamically allocated memory phải được cấp và giải phóng bởi chương trình 

- Để khởi tạo một biến dynamically allocated
```cpp
int* ptr1{new int(5)};  // direct initialization
int* ptr2{new int{6}};  // uniform initialization
```

- Để xóa một biến đơn, sử dụng `delete`
```cpp
// assume ptr has previously been allocated with new
delete ptr;     // return the memory pointed to by ptr to the OS
ptr = nullptr;  // set ptr to nullptr
```

- `delete` thực chất không xóa pointer, mà nó chỉ là trả lại bộ nhớ được trỏ đến về lại cho hệ điều hành. Pointer đó vẫn tồn tại trong scope, và có thể được gán với các địa chỉ khác e.g. `nullptr` 

- Pointer trỏ đến bộ nhớ đã được giải phóng là dangling -> undefined 
- Best practice: Đặt pointer đã xóa thành nullptr 

- Khi mà hệ điều hành không thể cấp được bộ nhớ yêu cầu -> ngoại lệ *bad_alloc*. Nếu không được xử lý -> crash 
- Có thể để tự động thành nullptr nếu không cấp được bộ nhớ với `std::nothrow`
```cpp
int* ptr{new (std::nothrow) int};
if (!ptr) {
	// do error handling 
	std::cerr << "Could not allocate memory\n";
}
```

- Delete nullptr không có hiệu ứng gì cả -> không cần kiểm tra điều kiện 

- Dynamically allocated memory sẽ tồn tại cho đến khi ta (chương trình) giải phóng nó, hoặc đến khi chương trình kết thúc (và hệ điều hành dọn dẹp, nếu có)
- Tuy nhiên, pointer dùng để chứa địa chỉ bộ nhớ cấp động hoạt động theo luật scope của biến cục bộ
```cpp
void doSomething() {
	int* ptr{new int{}};
}
```
- Code trên cấp bộ nhớ động cho biến int, nhưng mà không bao giờ xóa nó. `ptr` sẽ bị xóa khi đi ra khỏi scope hàm => Khi `ptr` đi ra khỏi scope, bộ nhớ cấp đó bị "mất" => **memory leak** 

- Memory leak cũng có thể xảy ra khi pointer đang chứa bộ nhớ được cấp động chuyển qua bộ nhớ khác mà chưa xóa
```cpp
int value = 5;
int* ptr{new int{}};
ptr = &value;          // old address lost, memory leak 
```

- Ta cũng có thể cấp bộ nhớ động cho mảng -> Độ dài mảng không cần là constexpr. Kiểu mảng thường được cấp bộ nhớ động nhất là C-style array
- Có thể cấp bộ nhớ động cho `std::array` -> dùng `std::vector` không cấp bộ nhớ động tốt hơn
- Để cấp bộ nhớ động cho C-style array, dùng kiểu mảng của `new`, `delete`, thường gọi là `new[]` và `delete[]`
```cpp
#include <cstddef>
#include <iostream>

int main() {
    std::cout << "Enter a positive integer: ";
    std::size_t length{};
    std::cin >> length;
    int* array{ new int[length]{} }; 
    // use array new.  Note that length does not need to be constant!
    std::cout << "Allocated an array of integers of length " << length << '\n';
    array[0] = 5; // set element 0 to value 5
    
    delete[] array; // use array delete to deallocate array
    // we don't need to set array to nullptr/0 here because it's going out of scope immediately after this anyway
    
    return 0;
}
```

- Mảng cấp bộ nhớ động gần như y hệt mảng tĩnh, với điểm khác biệt là người lập trình phải thủ công giải phóng bộ nhớ qua `delete[]`

- Để khởi tạo mảng cấp phát động
```cpp
int* array{new int[5]{1, 2, 3, 4, 5}};

auto* array1{new int[6]{0, 1, 2, 3, 4, 5}};
```

- C++ không cung cấp hàm built-in để thay đổi kích cỡ của array. Có thể tạo array mới xong copy qua -> không nên, dùng `std::vector` tốt hơn

- **Destructor** là một hàm thành viên đặc biệt khác mà sẽ được chạy khi một object bị hủy, được dùng để thực hiện các clean-up
- Với các kiểu dữ liệu cơ bản thì C++ có thể tự dọn dẹp bộ nhớ. Tuy nhiên, đối với các class phức tạp mà cần thực hiện bảo trì trước khi object bị xóa, thì cần phải dùng destructor 
- Cách tạo destructor
	- Có tên giống class, bắt đầu với `~`
	- Không được nhận tham số
	- Không có kiểu trả về 
- Một class chỉ có thể có duy nhất 1 destructor 
```cpp
class IntArray {
public:
	IntArray(int length) {
		assert(length > 0);
		m_length = length;
		m_array = new int[static_cast<std::size_t>(m_length)]{};
	}
	
	~IntArray() {
		delete[] m_array;
	}
	
	void setValue(int index, int value) {m_array[index] = value;}
	int getValue(int index) {return m_array[index];}
	
private:
	int m_length{};
	int* m_array{};
};
```

- **RAII** (**Resource Acquisition Is Initialization**) là kỹ thuật lập trình mà tài nguyên được gắn liền với thời gian sống của object với automatic duration (e.g. non-dynamically allocated object)
- Trong C++, RAII được thực hiện qua class với constructor và destructor
	- Tài nguyên (bộ nhớ, file, database handle,...) sẽ được lấy được trong constructor của object 
	- Tài nguyên sẽ được giải phóng trong destructor 
=> Giúp tránh resource leak vì được giải phóng tự động 

- **Void pointer**, hay còn gọi là generic pointer, là pointer đặc biệt có thể được dùng để chỉ đến object của mọi kiểu
- Khai báo như pointer bình thường với kiểu là `void`
```cpp
void* ptr{};
```

- Có thể dùng để chứa địa chỉ của bất kì kiểu dữ liệu nào
```cpp
int nValue{};
float fValue{};

struct Something {
	int n{};
	float f{};
};

Something sValue{};

void* ptr{};

ptr = &nValue; // valid
ptr = &fValue; // valid
ptr = &sValue; // valid
```
- Tuy nhiên, void pointer không biết kiểu dữ liệu nó đang trỏ đến là gì => cấm không được dereferencing void pointer
- Ta cần phải cast nó qua kiểu pointer khác trước khi thực hiện dereference
```cpp
int value{5};
void* voidPtr{&value};
// std::cout << *voidPtr; // illegal

int* intPtr{static_cast<int*>(voidPtr)};
std::cout << *intPtr; // ok
```

- Thường thì nên tránh dùng void pointer trừ khi cần thiết 

### optional

- Pointer to pointer là pointer chứa địa chỉ của một pointer khác
```cpp
int x{5};
int* ptr{&x};
int** ptrptr{&ptr};

std::cout << **ptrptr; //5
```
- Không đặt trực tiếp pointer to pointer đến một giá trị được, do `&` yêu cầu lvalue, nhưng `&value` là rvalue
```cpp
int x{5};
int** ptrptr{&&x}; // not valid
```

- Pointer to pointer thường được dùng nhất là để cấp phát động cho mảng các pointer
```cpp
int** array{new int*[10]};
```

- Có thể dùng để cấp phát động cho mảng nhiều chiều -> rất phức tạp
- Best practice: Không ưu tiên dùng pointer to pointer nếu không cần thiết optional