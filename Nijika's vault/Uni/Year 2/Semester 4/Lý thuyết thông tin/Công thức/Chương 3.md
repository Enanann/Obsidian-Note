
- Cho nguồn rời rạc $A$ gồm $s$ tin: $A=\{a_i; i={1,s}\}$ 
- Xét phép mã hóa $f:a_i\to a_i^{n_i}$ ;   $a_i^{n_i}\in V$
- Cơ số mã là $m$ $\Rightarrow$ Số các từ mã độ dài $n$: $N=m^n$
- Số từ mã được dùng: $s$ 

# Các định nghĩa cơ bản

### 1. Mã hóa

$\hspace{3cm}$$f: a_i \to a_i^{n_i}$

- Mã (bộ mã)

$\hspace{3cm}$$C=\{a_i^{n_i}\}$

$n_i$: Độ dài từ mã ($\text{const} \to$ mã đều, $\neq\to$ mã không đều)

$m$: Cơ số mã (số các giá trị khác nhau của một dấu trong từ mã: nhị phân $a_i=0/1$)

### 2. Độ thừa

$\hspace{3cm}$$D=1-\frac{H_0(A)}{H_0(V)}$

$H_0(A)=\log s$; $H_0(V)=\log N=n\log m$

- $s=N$: Mã đầy
- $s < N$: Mã vơi (sẽ có tổ hợp mã cấm không dùng)

### 3. Khoảng cách mã

- Là số các dấu mã khác nhau của 2 từ mã tính theo cùng một vị trí

$\hspace{3cm}$$d(a^n_i, a^n_j)$

- Tính chất 
	- $d(a_i^n,a_j^n)=d(a_j^n,a_i^n)$
	- $0\leq d(a_i^n, a_j^n)\leq n$
	- $d(a_i^n, a_j^n) + d(a_j^n, a_k^n) \geq d(a_i^n, a_k^n)$     (Tính chất tam giác)

### 4. Khoảng cách Hamming

$\hspace{3cm}$$d_0\overset{\Delta}{=}\displaystyle{\min_{\forall a_i^n, a_j^n}d(a_i^n, a_j^n)}$   

### 5. Trọng số của một từ mã

- Là số các dấu mã **khác 0** trong từ mã

$\hspace{3cm}$$W(a^n_i)$

- Tính chất 
	- $0\leq W(a_i^n) \leq n$
	- $d(a_i^n, a_j^n)=W(a_i^n+a_j^n)$ 

# Khả năng khống chế sai của mã đều nhị phân

### 1. Khả năng phát hiện sai

- Mã nhị phân có độ thừa $D>0$ và $d_0\geq 2$ có khả năng phát hiện được từ mã có $t$ lỗi sai thỏa mãn

$\hspace{3cm}$$t\leq d_0-1$ 

### 2. Khả năng sửa sai

- Mã nhị phân có độ thừa $D\geq 0$ và $d_0\geq 3$ có khả năng sửa được $e$ lỗi sai thỏa mãn 

$\hspace{3cm}$$e \leq [\frac{d_0-1}{2}]$ 

trong đó $[x]$ là phép lấy phần nguyên số $x$

### 3. Mã đều nhị phân không có độ thừa

- Còn gọi là mã đơn giản ($D=0$), $s=N=2^n$ $\Rightarrow$ Không **phát hiện** hoặc **sửa** lỗi sai 

- Điều kiện để sử dụng mã đơn giản trong kênh đối xứng nhị phân không nhớ là

$\hspace{3cm}$$p_s \leq p_{scp}$

hay

$\hspace{3cm}$$p_0 \leq \frac{p_{scp}}{n}$

# Mã tối ưu

### 1. Độ dài trung bình

- Là kỳ vọng của đại lượng ngẫu nhiên $n_i$ (độ dài từ mã sau khi mã hóa)

$\hspace{3cm}$$\bar n=M[n_i]=\displaystyle{\sum_{i=1}^s n_i p(a_i)}$ 

### 2. Định lý mã hóa nguồn của Shannon

- Luôn có thể xây dựng được một phép mã hóa các tin rời rạc mà $\bar n$ có thể nhỏ tùy ý nhưng không được nhỏ hơn entropy $H(A)$

$\hspace{3cm}$$\bar n \geq H(A)$

hay 

$\hspace{3cm}$$\bar n \geq \frac{H(A)}{\log m}$

### 3. Thuật toán Huffman

#### Mã hóa

- Đầu vào: Nguồn rời rạc $A=\begin{pmatrix} a_i \\ p(a_i)\end{pmatrix}, i=1,...S$
- Đầu ra: Từ mã $a_i^n$ tương ứng với $a_i$ 

- Các bước mã hóa
	- **Bước 1**: Khởi động 1 danh sách cây nhị phân một nút chứa các trọng lượng $p_1,p_2,...p_n$ cho $a_1,a_2,...a_n$ 

	- **Bước 2**: Thực hiện các bước sau $n-1$ lần:
		- Tìm hai cây $T, T'$ trong danh sách với các nút có trọng lượng tối thiểu $p', p''$ 
		- Thay thế hai cây bằng cây nhị phân với nút gốc có trọng lượng $p'+p''$, có các cây con là $T, T'$ 
		- Đánh dấu mũi tên chỉ đến các cây con 0 và 1 

	- **Bước 3**: Mã số tin của $a_i$ là dãy các bit được đánh dấu trên đường từ gốc của cây nhị phân cuối cùng tới nút $a_i$

#### Giải mã

- Đầu vào: Xâu bit
- Đầu ra: Xâu tin (ký tự)

- Các bước giải mã
	- **Bước 1**: Khởi động con trỏ P chỉ đến gốc cây Huffman
	- **Bước 2**: While (chưa đạt tới kết thúc thông báo) do:
		- Đặt $x$ là bit tiếp theo trong xâu bit
		- If x = 0 then
			- P = con trỏ chỉ đến cây con trái của nó
		- Else
			- P = con trỏ chỉ đến cây phải của nó
		- If (P chỉ đến nút lá) then
			- Hiển thị ký tự tương ứng với nút lá
			- Đặt lại P để nó lại chỉ đến gốc cây Huffman  

# Mã sửa lỗi

### 1. Mã khối 

- **Mã hóa khối**: Từ thông tin dài $k$ $\to$ từ mã dài $n$ 

$\hspace{3cm}$$x=(x_0, x_1,...,x_{k-1})\overset{Encoder}{\rightarrow} c=(c_0,c_1,...c_{n-1})$ 

trong đó $x_i\in GF(q); c_j\in GF(q)$ với $q$ là cơ số mã (mặc định là 2)

- **Mã khối (n, k)**: Là tập $2^k$ từ mã độ dài $n$ chọn từ $2^n$ tổ hợp có thể có độ dài $n$ 

- **Code rate**: Tỷ lệ hiệu quả, cao $\to$ ít dư nhưng giảm khả năng sửa lỗi

$\hspace{3cm}$$R_c=\frac{k}{n}$

### 2. Phát hiện và sửa lỗi

- Giả sử kênh có nhiều cộng![[Pasted image 20250403162444.png]]

$c = (c_0, c_1,...c_{n-1})$: Từ mã phát (n-tuples), thuộc bộ mã C(n, k)
$u = (u_0,u_1,...u_{n-1})$: Vector thu
$e = (e_0,e_1,...e_{n-1})$: Mẫu lỗi, có $2^n$ cấu trúc lỗi 

- Error pattern (cấu trúc lỗi): 

$\hspace{1cm}$$e=u\oplus c=(u_0+ c_0, u_1+c_1,...u_{n-1}+c_{n-1})=(e_0,e_1,...e_{n-1})$

trong đó $e_i=1$ với $u_i\neq c_i$ và $e_i=0$ với $u_i=c_i$ 

- Máy thu không phát hiện ra có lỗi nếu vector thu $u$ là **một từ mã hợp lệ**

- Khả năng khống chế lỗi của mã khối 
	- Một bộ mã $(n,k,d_0)$ có khả năng phát hiện được lỗi nếu cấu trúc lỗi có [[3.2 Các định nghĩa và khái niệm cơ bản#Trọng số của một từ mã|trọng số]] thỏa mãn
$\hspace{3cm}$$w(e)\leq (d_0-1)$

	- Một bộ mã $(n,k,d_0)$ có khả năng tự sửa được lỗi nếu cấu trúc lỗi có trọng số thỏa mã
$\hspace{3cm}$$w(e)\leq [\frac{d_0-1}{2}]$

### 3. Mã khối tuyến tính

- Mã khối tuyến tính **C(n, k)** là mã có chiều dài từ mã $n$, mỗi dấu mã là một dạng tuyến tính của $k$ dấu thông tin

$\hspace{3cm}$$c=(c_0c_1.....c_{n-1})$ 

$\hspace{3cm}$$c_j=\displaystyle{\sum_{i=1}^k a_i x_i}$ 

trong đó: 
	$k$ là số bit thông tin (số bit dữ liệu gốc) 
	$n$ là độ dài từ mã sau khi mã hóa (gồm bit thông tin và bit dư)
	$n-k$ là số bit kiểm tra dư  

### 4. Ma trận sinh của mã khối tuyến tính

- Là ma trận $G_{k\times n}$ 

$\hspace{3cm}$$G=\begin{pmatrix} g_{0,0} & g_{0,1} & ... & g_{0, n-1} \\ g_{1,0} & g_{1,1} & ... & g_{1, n - 1} \\ ... & ... & ... & ... \\ g_{k-1, 0} & g_{k-1, 1} & ... & g_{k-1, n-1} \end{pmatrix}$    

- Mô hình tạo mã khối tuyến tính
>
>Vector tin vào (k dấu): $u=(x_0,x_1,\dots, x_{k-1})$
>
>Từ mã ra (n dấu): $c=(c_0,c_1,\dots c_{k-1},c_k,\dots,c_{n-1})$  
>
>Với $c=u.G$ 

- Ma trận kiểm tra $H$

$\hspace{3cm}$$G.H^T=0$  

với $H^T$ là ma trận chuyển vị của $H$ 

### 5. Ma trận sinh hệ thống

#### Dạng thức 1: $G_{sys}=[P|I_k]$  

- Từ mã có dạng $c=[\underbrace{p_1,p_2,...p_{n-k}}_{\text{Redundant checking part}}|\space \underbrace{x_1,x_2,...x_k}_{\text{message part}}]$     
- Ma trận sinh

$\hspace{3cm}$$G_{sys}=\left[ \begin{array}{ccc|ccc} p_{0,0} & ... & p_{0, n-k-1} & I_{0, n-k} & ... & I_{0, n-1} \\ p_{1,0} & ... & p_{1, n - k - 1} & I_{1, n-k} & ... & I_{1, n - 1} \\ ... & ... & ... & ... &...&...\\ p_{k-1, 0} & ... & p_{k-1, n-k-1} & I_{k-1, n-k} & ... & I_{k - 1, n- 1} \end{array}\right]$

- Tương ứng các dấu mã kiểm tra và các dấu mã mang thông tin:

$c_j=x_0p_{0,j}+x_1p_{1,j}+...+x_{k-1}p_{k-1, j}$   với $0\leq j\leq n -k- 1$ 

$c_{n-k+i}=x_i$   với $n-k\leq i\leq n-1$ 

- Ma trận kiểm tra chẵn lẻ 

$\hspace{3cm}$$H_{sys}=[I_{n-k}P^T]$ 

#### Dạng thức 2: $G_{sys}=[I_k|P]$

- Từ mã có dạng $c=[\underbrace{x_1,x_2,...x_k}_{\text{message part}}\space|\underbrace{p_1,p_2,...p_{n-k}}_{\text{Redundant checking part}}]$ 

- Ma trận sinh

$G_{sys}=\left[ \begin{array}{ccc|ccc} I_{0, 0} & ... & I_{0, k-1} & p_{0,k} & ... & p_{0, n-1}  \\ I_{1, 0} & ... & I_{1, k - 1} & p_{1,k} & ... & p_{1, n - 1}  \\ ... & ... & ... & ... & ... & ... \\  I_{k-1, 0} & ... & I_{k - 1, k - 1} & p_{k-1, k} & ... & p_{k-1, n-1}  \end{array}\right]$ 

- Tương ứng các dấu mã mang thông tin và các dấu kiểm tra trong từ mã

$c_i=x_i$   với $0\leq i\leq k-1$

$c_j=x_0p_{0,j}+x_1p_{1,j}+...+x_{k-1}p_{k-1,j}$   với $k\leq j\leq n-1$ 

- Ma trận kiểm tra chẵn lẻ

$\hspace{3cm}$$H_{sys}=[P^TI_{n-k}]$  

### 6. Các quy trình với ma trận sinh, ma trận kiểm tra

#### Ma trận sinh

- Dùng để mã hóa thông điệp $u$ $\to$ từ mã $c$

$\hspace{3cm}$$c=u.G$

#### Ma trận kiểm tra

- Dùng để kiểm tra xem từ mã có hợp lệ không (kiểm tra lỗi)

- Tính **hội chứng** (syndrome) $s$ từ từ mã $c$ nhận được

$\hspace{3cm}$$s=H.c^T$

nếu $s=0$ thì từ mã hợp lệ

nếu $s\neq 0$ thì từ mã không hợp lệ (có lỗi trong từ mã $c$)

- Tìm vị trí lỗi sử dụng **hội chứng** $s$ 
	- So sánh $s$ với các cột trong ma trận kiểm tra $H$
	- Vị trí cột $H$ giống với hội chứng $s$ chính là vị trí sai của từ mã $c$ nhận được

- Cách lấy $d_0$ từ ma trận $H$ 
	- Ta có $d_0=\displaystyle{\min_{c\in C}} W(c)$  (do trong mã tuyến tính **tổng/hiệu hai từ mã bất kì cũng là một từ mã**) 
	- Tìm số số 1 ít nhất trong $c$ để $H.c^T=0$ 

### 7. Các bài toán tối ưu mã tuyến tính nhị phân

- Khi xây dựng một mã tuyến tính $(n, k, d_0)$, mong muốn mã có độ thừa nhỏ (số bit thừa $r=n-k$) nhưng khả năng khống chế sai lớn. Để đơn giản hóa, có thể chia thành các bài toán  tối ưu sau

#### $k, d_0$, tìm $n_{\min}$ 

- Giới hạn Griesmer

$\hspace{3cm}$$n\geq \displaystyle{\sum_{i=0}^{k-1}\lceil \frac{d_0}{2^i} \rceil}$ 

#### $n, k$, tìm ${d_0}_{\max}$ 

- Giới hạn Plotkin

$\hspace{3cm}$$d_0\leq \frac{n.2^{k-1}}{2^k-1}$ 

#### $n, t/d_0$, tìm $k_\max$ ($r=(n-k)_\min$)

- Giới hạn Hamming

$\hspace{3cm}$$2^{n-k}\geq \displaystyle{\sum_{i=0}^t C^i_n}$

với $d_0=2t+1$ 

