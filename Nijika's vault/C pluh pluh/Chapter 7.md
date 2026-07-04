
- **Compound statement** ha **block** là nhóm gồm 0 hoặc nhiều các lệnh khác nhau mà được compiler coi như là 1 lệnh. Nằm trong `{}`
- Best practice: Giữ cho khối lượng nested block không quá 3 

- **User-defined namespace** là namespace do người dùng tạo ra: 
```cpp
namespace NamespaceIdentifier {
	// content
}
```
- Truy cập với **scope resolution operator** `::`. Nếu không có toán hạng bên trái thì global scope sẽ được sử dụng 

- Tên được khai báo trong namespace có thể **shadow**/**name hide** tên giống nhau ở ngoài block 

- Có thể khai báo một namespace ở nhiều nơi khác nhau (file khác nhau hoặc cùng file). Tất cả sẽ ở cùng một namespace đó 
- Có thể lồng namespace với nhau e.g. `Foo::Goo::func()`

- Có thể tạo namespace aliases với `namespace Something = Foo::Goo` 

- **Storage duration** hay **duration** của một biến quyết định cách một biến được tạo và hủy -> trực tiếp quyết định lifetime của nó 
- Biến cục bộ sẽ có **automatic storage duration**, tức là chúng được tạo tại thời điểm định nghĩa và bị hủy khi đi ra ngoài block được định nghĩa 

- Biến global sẽ có **static duration**, tức là chúng được tạo ra khi chương trình chạy và hủy khi chương trình kết thúc
- Best practice: Nên để biến global ở trong một namespace 

- **Linkage** quyết định xem khai báo của cùng một identifier ở scope khác có phải là cùng một object (hoặc hàm) hay không 

- Biến cục bộ không có linkage 
- Best practice: Định nghĩa biến ở scope hạn chế nhất 

- **Internal linkage** chỉ rằng identifier đó có thể được thấy và dùng trong một translation unit (đơn vị dịch), nhưng không thể truy cập trong các đơn vị dịch khác 
- **Translation unit** là một đơn vị mã nguồn độc lập có thể biên dịch và tạo ra một đối tượng 
- Biến global non-const sẽ có **external linkage** theo mặc định, để làm nó có internal linkage, sử dụng `static` 
- Function sẽ có **external linkage** theo mặc định 

- Để làm biến global const/constexpr có external linkage, sử dụng `extern`
- Để thực sự sử dụng biến có external linkage, ta cần **forward declaration** chúng e.g. `extern const int g_x;`
- Best practice: Chỉ sử dụng `extern` cho forward declaration hoặc cho định nghĩa biến const global 

- **Inline expansion** là khi compiler thay thế lời gọi hàm bằng trực tiếp hàm đó. Hàm inline là hàm được khai báo với `inline`
- Cần 2 điều kiện:
	- Compiler cần thấy định nghĩa đầy đủ của hàm hoặc biến inline (chỉ forward declaration không đủ)
	- Mỗi định nghĩa cần giống hệt nhau

- Trong C++ hiện đại, `inline` được dùng để báo hiệu rằng nhiều định nghĩa có thể được (tránh ODR) -> Phù hợp cho các thư viện header-only 

- **Unnamed namespace** (Anonymous namespace) là namespace được định nghĩa mà không có định danh 
```cpp
namespace {
	// can only be accessed in this file 
    void doSomething() {
        std::cout << "v1\n";
    }
}
```
 - **Unnamed namespace** coi nội dung bên trong nó như là có internal linkage 