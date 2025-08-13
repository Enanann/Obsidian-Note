
# Cơ sở toán học

- Xét trên $GF(2)$ 

### 1. Cộng đa thức

$\hspace{3cm}$$a(x)+b(x)=c(x)=\displaystyle{\sum_{i=0}^{n-1}(a_i+b_i)x^i}$    

với $a_i + b_i$ trên $GF(2)$

### 2. Nhân đa thức 

- Được thực hiện theo phép nhân modulo $X^n + 1$ 

$\hspace{3cm}$$c(x)=a(x).b(x)=\displaystyle{(\sum_{i=0}^{n-1}a_i x^i).(\sum_{i=0}^{n-1}b_i x^i)\mod X^n + 1}$ 

- Chú ý: Tích của hai đa thức được thực hiện trên cơ sở tích hai đơn thức $a_ix^i,b_jx^j$ theo quy tắc

$\hspace{3cm}$$x^i.x^j=x^{(i+j)\mod n}$  

### 3. Phép dịch vòng

- Xét đa thức $a(X)$

$\hspace{3cm}$$a(X)=\displaystyle{\sum_{i=0}^{n-1}a_i x^i}\leftrightarrow a=(a_0,\space a_1,\space a_2,\space ...\space a_{n-1})$  

- Phép dịch vòng

$\hspace{1.5cm}$$c(X)=x^j.a(X)=x^j.\displaystyle{\sum_{i=0}^{n-1}a_i x^i}\leftrightarrow c= (a_{n-j}, \space a_{n-j+1},\space...\space a_{n-j-1})$ 

### 4. Đa thức bất khả quy 

- Là đa thức chỉ chia hết cho 1 và chính nó, ngoại trừ $1+x$ thì đa thức bất khả quy có **trọng số lẻ** và **số hạng tự do là 1**

>Bậc 1: $1+x$
>
>Bậc 2: $1+x+x^2$
>
>Bậc 3: $1+x+x^3$;   $1+x^2+x^3$
>
>Bậc 4: $1+x+x^4$;   $1+x^3+x^4$;   $1+x+x^2+x^3+x^4$

- **Định lý**: Nếu $2^m-1=n$, đa thức $X^n + 1$ được phân tích thành tích của tất cả các đa thức bất khả quy có bậc $m$ và ước của $m$ 

### 5. Ideal của vành đa thức

- **Định nghĩa**: Ideal $I$ của vành đa thức $Z_2[x]/x^n+1$ gồm tập các đa thức là bội của một đa thức $g(X)=\displaystyle{\sum_{i=0}^rg_ix^i}$ thỏa mãn
	1. $g(X)|X^n+1$     (Tức $g(X)$ là ước của $X^n+1$)

	2. Với mọi $a(X)\in I, a(X)\neq 0$ ta có $\deg g(X)=r=\min\deg a(X)$

- Ký hiệu: $I=\langle g(X)\rangle$  

- Để tìm tất cả các Ideal
	- Phân tích $X^n+1$ thành tích các đa thức bất khả quy (ví dụ $a(x).b(x).c(x)$)
	- Ideal là tất cả các tổ hợp tích các nhân tử trên
		- $1$: Toàn bộ vành
		- $a(x)$
		- $b(x)$
		- $c(x)$
		- $a(x)b(x)$
		- $a(x)c(x)$
		- $b(x)c(x)$
		- $a(x)b(x)c(x)$: Chính nó (**không lấy**)

$\Rightarrow$ Nếu phân tích thành $a$ đa thức bất khả quy thì $|I|=2^a-1$ 

### 6. Đa thức đối ngẫu

- $g^*(X)$ là đa thức đối ngẫu của $g(X)$

$\hspace{3cm}$$g^*(X)=X^{\deg g(X)}.g(X^{-1})$ 

# Mã Cyclic

### 1. Đa thức sinh

- Mã cyclic (n, k) là Ideal $I=\langle g(x)\rangle$ của vành đa thức $Z_2[x]/X^n + 1$ 

$\Rightarrow$ $g(x)=g_0+g_1x+\dots + g_rx^r$ được gọi là đa thức sinh của mã cyclic, $r=n-k$ 

### 2. Ma trận sinh

- Ma trận sinh của mã cyclic (n, k)

$\hspace{3cm}$$G=\begin{pmatrix} g(X) \\ x.g(X) \\ ... \\ x^{k - 1}.g(X) \end{pmatrix}$ 

### 3. Ma trận kiểm tra 

- Đa thức kiểm tra

$\hspace{3cm}$$h(X)=\frac{x^n + 1}{g(X)}$

- Ma trận kiểm tra của mã cyclic (n, k)

$\hspace{3cm}$$H=\begin{pmatrix} h^*(X) \\ x.h^*(X) \\ ... \\ x^{r-1}.h^*(X) \end{pmatrix}$

với $h^*(X)$ là đa thức đối ngẫu của $h(X)$ 

- Các liên hệ

$\hspace{3cm}$$G.H^T=0$

$\hspace{3cm}$$a(X).H^T=0$    víu $a(X)$ là một từ mã

### 4. Mã cyclic hệ thống

- Mã cyclic (n, k) là **mã cyclic hệ thống** nếu chỉ được rõ vị trí các **dấu thông tin** và các **dấu kiểm tra**

$\hspace{3cm}$$f=[\underbrace{f_0,f_1,...f_{r-1}}_{\text{r dấu kiểm tra}}\space,\underbrace{f_r,f_{r+1},...p_{n-1}}_{\text{k dấu thông tin}}]$ 

$\hspace{3cm}$$f(X)=\displaystyle{\sum_{i=0}^{n-1} f_i x^i=r(X)+x^{n-k}a(X)}$ 

### 5. Mã hóa hệ thống theo phương pháp chia

VÀO: Tin rời rạc $a_i\in A$ 

RA: Từ mã $f_i(X)$ tương ứng với $a_i$ 

**Bước 1**: Mô tả tin $a_i$ trong tập tin cần mã hóa (gồm $2^k$ tin) bằng một đa thức $a_i(X)$ với $\deg a_i(X)\leq k - 1$ 

**Bước 2**: Nâng bậc $a_i(X)$ bằng cách nhân nó với $x^{n-k}$

**Bước 3**: Chia $a_i(X).x^{n-k}$ cho đa thức sinh $g(X)$ để tìm phần dư $r_i(X)$ 

**Bước 4**: Xây dựng từ mã cyclic: $f_i(X)=r_i(X) + x^{n-k}.a(X)$ 


- Bộ tạo mã hệ thống 

![[Pasted image 20250514231606.png]]

### 6. Mã hóa hệ thống theo phương pháp nhân

VÀO: Mã cyclic (n, k), $g(X)$, tin $a_i\in A$ 

RA: Từ mã hệ thống của mã (n, k) cyclic

**Bước 1**: Mã hóa tin $a_i$ bằng đa thức thông tin $a(X)$ với $\deg a(X)\leq k-1$, $a(X)=\displaystyle{\sum_{j=0}^{k-1}a_jx^j}$ 

**Bước 2**: Nâng bậc $x^{n-k}.a(X)$ $\Rightarrow$ Tính vùng dấu mã vùng bit cao. Tính $h(X)=\frac{x^n+1}{g(X)}$ 

**Bước 3**: Lập công thức các dấu mã vùng bit thấp: ```for i = 1 to n - k do``` 

$\hspace{3cm}$$f_{n-k-i}=\displaystyle{\sum_{j=0}^{k-1}h_j.f_{n-j-i}}$  

**Bước 4**: Thiết lập từ mã hệ thống

$\hspace{3cm}$$(f_0, f_1,\dots, f_{n-1})\leftrightarrow f(X)=\displaystyle{\sum_{i=r}^{n-1}f_i x^i}$  

- Bộ tạo mã hệ thống

![[Pasted image 20250514232815.png]]
