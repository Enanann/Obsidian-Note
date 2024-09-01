
# Khái niệm thuật toán

- Thuật toán hoặc giải thuật (algorithm)
	- Là một thủ tục giải quyết một vấn đề nào đó trong một số hữu hạn bước
	- Là một tập hợp hữu hạn các chỉ thị được định nghĩa rõ ràng để giải quyết một vấn đề nào đó
	- Là một tập các quy tắc định nghĩa chính xác một dãy các hành động

- Cách mô tả thuật toán
	- Sử dụng ngôn ngữ tự nhiên $\Rightarrow$ Dài dòng, ít sử dụng
	- Sử dụng giả mã (Pseudo-code) $\Rightarrow$ Ngắn gọn, dễ hiểu, hay được sử dụng
	- Sử dụng ngôn ngữ lập trình

# Độ phức tạp tính toán của thuật toán

- Độ phức tạp thời gian (time complexity): Là **số phép toán cơ bản** thực hiện giải thuật (quyết định lượng thời gian thực hiện giải thuật)

- Độ phức tạp không gian (space complexity): Là lượng bộ nhớ lớn nhất cần thiết để lưu các đối tượng của thuật toán tại một thời điểm thực hiện thuật toán

$\Rightarrow$ Độ phức tạp của thuật toán thường được biểu diễn như một hàm của kích thước dữ liệu đầu vào

# Khái niệm O-lớn

- Định nghĩa
>[!text]
>$f(n)=O(g(n))$, với $n$ đủ lớn, $f(n)$ không vượt quá một hằng số cố định nhân với $g(n)$, hay
>
>$\hspace{3cm}$$f(n)=O(g(n)) \Leftrightarrow \exists c, k, \forall n \geq k, f(n) \leq c*g(n)$

- Định lý: Nếu $\displaystyle{\lim_{n\to \infty}\frac{f(n)}{g(n)}}$ tồn tại và hữu hạn thì $f(n)=O(g(n))$   

![[Pasted image 20240901155651.png]]

- Bảng các thuật ngữ O-lớn thường dùng

| Độ phức tạp   | Thuật ngữ               |
| ------------- | ----------------------- |
| $O(1)$        | Constant complexity     |
| $O(\log n)$   | Logarithmic complexity  |
| $O(n)$        | Linear complexity       |
| $O(n\log n)$  | Linearithmic complexity |
| $O(n^b)$      | Polynomial complexity   |
| $O(b^n), b>1$ | Exponential complexity  |
| $O(n!)$       | Factorial complexity    |
