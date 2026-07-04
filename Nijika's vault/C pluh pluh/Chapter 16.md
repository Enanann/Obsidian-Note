
- **Container** là kiểu dữ liệu cung cấp kho lưu trữ cho các unnamed objects (**elements**)
- Số các elements trong container gọi là **length** (**count** hay **size**)
- Trong hầu hết các ngôn ngữ lập trình (bao gồm C++), container là **homogenous**, tức là kiểu dữ liệu của các elements phải giống nhau 

- C++ có 3 kiểu array chính: 
	- C-style array `int arr[]`
	- Vector `std::vector`
	- Array `std::array`

- Vector không phải là một aggregate do nó có hàm user-defined 
- Khởi tạo vector với một số các giá trị: `std::vector<int> arr {2, 3, 5, 7};`
- Kia là **list constructor** cho phép ta khởi tạo container 
	- Đảm bảo container có đủ không gian nhớ (nếu cần)
	- Đặt độ dài container (nếu cần)
	- Khởi tạo thành viên trong initializer list (theo thứ tự)

- Để khởi tạo vector trống với độ dài cụ thể: `std::vector<int> arr(10);`
- Sử dụng explicit constructor `explicit std::vector<T>(std::size_t)` 
- Direct initialization như trên không dùng được nếu vector là biến thành viên, có thể khắc phục với `std::vector<int> arr{std::vector<int>(10)}`

- Khi ta cần pass vector vào hàm, ta sẽ pass theo (const) reference để tránh tạo bản sao
- Tuy nhiên, ta lại có thể trả về vector theo value bởi vì **move semantics** 
- **Move semantics** là luật quyết định cách dữ liệu từ một object được chuyển sang một object khác 
- Tương tự, **copy semantic** là luật quyết định dữ liệu được sao chép từ một object này sang object khác
- Việc vector sử dụng move semantic giúp nó hiệu năng cao hơn là copy semantic 
=> Có thể return by value các type có move semantic

- Best practice: Đối với range-based
	- `auto` khi muốn thay đổi sao chép của element
	- `auto&` khi muốn thay đổi element gốc
	- `const auto&` trường hợp còn lại 

- Để resize vector, dùng `resize(std::size_t)`. Các thành phần trước được bảo toàn 
- **Length** là số thành phần đang được sử dụng
- **Capacity** là số thành phần vector có thể chứa 
- Khi ta thay đổi size vector, đồng nghĩa với vector có thể sẽ di chuyển bộ nhớ nếu cần - **reallocation**. Ta phân biệt length và capacity để giúp vector có thể quyết định thông minh hơn khi nào cần reallocate 
```cpp
std::vector<int> ve{1, 2, 3, 4, 5};
// len: 5, cap: 5
// 1 2 3 4 5

ve.resize(3);
// len: 3, cap: 5
// 1 2 3

ve.resize(7);
// len: 7, cap: 7
// 1 2 3 0 0 0 0 
```

- Khi ta muốn thu nhỏ vector mà không muốn để thừa capacity (trong trường hợp object lớn + thừa nhiều sẽ rất tốn bộ nhớ), sử dụng `shrink_to_fit()`

| Function Name  | Stack Operation | Behavior                                                             | Notes                                          |
| -------------- | --------------- | -------------------------------------------------------------------- | ---------------------------------------------- |
| push_back()    | Push            | Put new element on top of stack                                      | Adds the element to end of vector              |
| pop_back()     | Pop             | Remove the top element from the stack                                | Returns void, removes element at end of vector |
| back()         | Top or Peek     | Get the top element on the stack                                     | Does not remove item                           |
| emplace_back() | Push            | Alternate form of push_back() that can be more efficient (see below) | Adds element to end of vector                  |
- Best practice:
	- Ưu tiên `emplace_back()` khi muốn construct object trực tiếp trong container (object chưa tồn tại, cần gọi constructor với tham số e.g. `ve.emplace_back(arg1, arg2)`)
	- Ưu tiên `push_back()` khi đã có object và muốn thêm nó vào container


- C++20 có thêm `<ranges>` -> Cho phép range-based for loop theo thứ tự ngược 
```cpp
for (const auto& word : std::views::reverse(words)) 
```

- Ưu tiên `constexpr std::bitset`, `std::vector<char>`, hoặc các bitsets động từ thư viện thứ 3 thay cho `std::vector<bool>` 



