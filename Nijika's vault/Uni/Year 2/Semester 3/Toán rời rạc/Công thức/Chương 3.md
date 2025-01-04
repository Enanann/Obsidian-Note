# Phương pháp sinh

### Bài 1

- Liệt kê xâu nhị phân độ dài $n$

- Cấu hình đầu tiên là $n$ chữ số $0$
- Cấu hình cuối cùng là $n$ chữ số $1$

- Thuật toán sinh cấu hình tiếp theo

	1. Cấu hình hiện tại $X=x_1x_2 ...x_n$ 
	
	2. $x_k$ là số chữ số $0$ đầu tiên từ bên phải xâu hiện tại
	
	$\hspace{3cm}$$X=x_1 ...x_{k-1}011 . . . 1$  
	
	3. Cấu hình tiếp theo là $Y=y_1y_2 ... y_n$ 
	
	$\hspace{3cm}$$y_i=x_i$   với $1\leq i\leq k-1$ 
	
	$\hspace{3cm}$$y_i=1-x_i$   với $k\leq i\leq n$ 
	
	hay $Y=x_1,x_2...x_{k-1}1000 . . . 0$ 

### Bài 2

- Liệt kê các tổ hợp chập $k$ của $1,2,...n$ 

- Cấu hình đầu tiên là $(1,2,...,k)$
- Cấu hình cuối cùng là $(n-k+1,...,n)$

- Thuật toán sinh cấu hình tiếp theo

	1. Cấu hình hiện tại $X=(x_1,x_2,...x_k)$ 
	
	2. Nếu $x_i=n-k+i$ với mọi $i=1,2,...k$ thì $X$ là cấu hình cuối cùng
	
	3. $t$ là chỉ số lớn nhất thỏa mãn $x_t<n-k+t$ 
	
	4. Cấu hình tiếp theo
	
	$\hspace{3cm}$$y_i=x_i$   với $i<t$
	
	$\hspace{3cm}$$y_t=x_t+1$
	
	$\hspace{3cm}$$y_i=y_t+(i-t)$   với $i>t$ 

### Bài 3

- Liệt kê các hoán vị của $1,2,...n$ 

- Cấu hình đầu tiên là $(1,2,...,n)$ 
- Cấu hình cuối cùng là $(n,n-1, ..., 1)$ 

- Sinh cấu hình tiếp theo 
	
	1. Cấu hình hiện tại $X=(x_1,x_2,...x_n)$ 
	
	2. Tìm $j$ lớn nhất thỏa mãn $x_j < x_{j+1}$ 
	
	3. $x_k$ là số bé nhất còn lớn hơn $x_j$ trong $x_{j+1}...x_n$ 
	
	4. Đổi chỗ $x_k$ và $x_j$
	
	5. Lật ngược lại $x_{j+1}...x_n$ 

- Sinh cấu hình trước đó

	1. Cấu hình hiện tại $X=(x_1,x_2,...x_n)$ 
	
	2. Tìm $j$ lớn nhất để $x_j > x_{j+1}$ 
	
	3. $x_k$ là số lớn nhất còn bé hơn $x_j$ trong $x_{j+1}...x_n$
	
	4. Đổi chỗ $x_k$ và $x_j$
	
	5. Lật ngược lại $x_{j+1}...x_n$ 

### Bài 4

- Liệt kê xâu nhị phân độ dài $n$ bằng quay lui

![[Pasted image 20241005181538.png]]
![[Pasted image 20241005181545.png]]







