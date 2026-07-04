
- **Function parameter** là biến được sử dụng trong function mà giá trị được cấp bởi caller
- Function parameter và các biến định nghĩa trong function body là **local variables**
- **Lifetime** là thời gian sống (tồn tại) của biến. Biến được tạo và hủy trong **runtime**
- **Scope** của biến quyết định nơi nó có thể được nhìn thấy và sử dụng. Scope là **compile-time**
- Trong định nghĩa hàm, tên của function parameter là optional, parameter không có tên là **unnamed parameter** -> có thể để tên nó trong comment
```c++
void doSomething(int /*count*/) {
	//...
}
```
- Có thể là do bản cũ dùng đến nhưng bản mới không dùng đến -> xóa đi thì gây hỏng (tốn nhiều công sức để fix)


- **Argument** là giá trị cụ thể được đưa từ caller đến function
- Khi argument được sao chép vào parameter -> **pass by value**
- **Return by value** sẽ trả về một object tạm thời (chứa bản sao của giá trị trả về) cho caller 

- Best practice: hàm `main` nên trả về `0` khi chương trình chạy bình thường 
- Best practice: DRY 
- Best practice: Định nghĩa các biến gần nơi sử dụng lần đầu nhất có thể 

- **Forward declaration** cho phép ta nói với compiler về sự tồn tại của **indentifier** trước khi định nghĩa nó 
- Trường hợp là function, cho phép ta nói về sự tồn tại của hàm đó trước khi định nghĩa thân hàm -> **function declaration** (function prototype). Bao gồm return type, name, parameter types, kết thúc với `;`  (có thể để tên của parameter trống)
- Best practice: Giữ tên parameter trong function declaration

- **Declaration** bảo compiler về sự tồn tại của identifier
- **Definition** là declaration mà thực sự triển khai (hàm, kiểu) hoặc khởi tạo (biến) cho identifier 

- **ODR - One definition rule**
	1. Trong một file, mỗi hàm, biến, kiểu, hoặc template trong một scope nào đó chỉ có thể có 1 definition. Các definitions trong các scope khác không vi phạm luật này
	2. Trong một chương trình, mỗi hàm hoặc biến trong một scope nào đó chỉ có thể có một definition. Các hàm và biến không được thấy bởi linker thì không ảnh hưởng
	3. Các kiểu, template, hàm inline, và biến inline được phép có definition trùng trong các file khác nhau, khi và chỉ khi chúng giống hệt nhau
- Các ngoại lệ của ODR
	- Các kiểu dữ liệu như class, struct, enum với điều kiện định nghĩa phải y hệ nhau 
	- Function template
	- Biến và hàm inline 


- **Namespace** cho phép ta tạo một vùng scope khác (namespace scope) để tránh **naming collision**

- **Preprocessor** được chạy trước khi compile
- **Directives** là các hướng dẫn đặc biệt cho preprocessor. Bắt đầu với `#` và kết thúc với newline 
- **Macro** định nghĩa cách input text được chuyển thành một output text thay thế 
- Best practice: Tên của macro nên được viết in hoa, với các từ tách bởi `_` 

- **Header files** được thiết kế để truyền các khai báo đến code
- **Header guards** ngăn chặn việc nội dung của header file được include nhiều hơn một lần vào một code file nào đấy. Chúng không ngăn chặn việc nội dung được include vào nhiều code file khác nhau 
- Header guards có dạng:
```c++
#ifndef SOME_UNIQUE_NAME
#define SOME_UNIQUE_NAME

// declarations (and certain types of definition)

#endif
```
- Hoặc có thể dùng `#pragma once`

- Best practice: Source file nên `#include` header file tương ứng của nó (nếu có). Không `#include` .cpp file 

- **Transitive include** là khi một header file được include lại include thêm nhiều header file khác
- Best practice: Nên include các header rõ ràng, tránh transitive include 

- Best practice: Thứ tự include
	- Header cặp tương ứng 
	- Các header trong cùng project
	- Header của thư viện bên thứ 3
	- Header của thư viện standard C++ 