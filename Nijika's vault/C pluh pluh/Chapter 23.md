
# Composition & Aggregation

- **Object composition** là quá trình xây dựng một đối tượng phức tạp từ các đối tượng đơn giản hơn. Có 2 loại
	- Composition
	- Aggregation 

- **Composition** tồn tại khi biến thành viên có quan hệ "part-of" với lớp chứa nó, cụ thể cần đủ điều kiện sau
	- Thành viên là một phần của lớp
	- Thành viên chỉ có thể thuộc về một lớp trong cùng một thời điểm
	- Thành viên được quản lý bởi lớp đó (vòng đời)
	- Thành viên không biết về sự tồn tại của lớp 

-> Thường được triển khai qua biến thành viên bình thường, hoặc con trỏ khi lớp quản lý các phép cấp và giải phóng bộ nhớ. Nếu có thể dùng composition, thì nên dùng composition 


- **Aggregation** tồn tại khi lớp có quan hệ "has-a" với biến thành viên, cụ thể cần đủ điều kiện sau
	- Thành viên là một phần của lớp
	- Thành viên có thể thuộc về nhiều lớp trong cùng một thời điểm
	- Thành viên không được quản lý bởi lớp đó
	- Thành viên không biết về sự tồn tại của lớp 

-> Thường được triển khai qua con trỏ hoặc tham chiếu 

# Association 

- **Association** là kiểu quan hệ lỏng hơn, khi mà lớp "uses-an" một lớp khác vốn không có quan hệ gì với nó, cụ thể cần thỏa mãn các điều kiện
	- Đối tượng liên kết không có mối liên hệ nào khác đối với đối tượng chính 
	- Đối tượng liên kết có thể thuộc về nhiều đối tượng trong cùng một thời điểm
	- Đối tượng liên kết không được quản lý bởi đối tượng chính 
	- Đối tượng liên kết có thể biết hoặc không biết về sự tồn tại của đối tượng chính 

-> Có thể được triển khai qua con trỏ hoặc tham chiếu, hoặc bằng cách gián tiếp hơn như là giữ index hoặc key của đối tượng liên quan 

- Thường nên tránh liên kết bidirectional nếu có thể, vì chúng có xu hướng viết khó hơn và dễ gây lỗi hơn

# Dependency

- Là kiểu quan hệ mà một lớp sử dụng một lớp khác để thực hiện một nhiệm vụ. Lớp phụ thuộc thường không phải là biến thành viên mà sẽ là một đối tượng tạm thời hoặc được truyền vào qua bên ngoài 

|Property\Type|Composition|Aggregation|Association|Dependency|
|---|---|---|---|---|
|Relationship type|Whole/part|Whole/part|Otherwise unrelated|Otherwise unrelated|
|Members can belong to multiple classes|No|Yes|Yes|Yes|
|Members existence managed by class|Yes|No|No|No|
|Directionality|Unidirectional|Unidirectional|Unidirectional or bidirectional|Unidirectional|
|Relationship verb|Part-of|Has-a|Uses-a|Depends-on|

# Container class

- Cung cấp một nơi để chứa nhiều đối tượng của kiểu khác
- **Value container** là composition chứ bản sao của đối tượng nó đang giữ
- **Reference container** là aggregation chứa con trỏ hoặc tham chiếu đến đối tượng nằm ở ngoài container 

- `std::initializer_list` có thể được dùng để triển khai hàm khởi tạo, phép gán, và các hàm mà chấp nhận tham số là list initializer (nằm trong `<initializer_list>`)