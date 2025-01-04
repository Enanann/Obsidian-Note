
# Các nguyên lí đếm cơ bản 
### Bài 1

- Tìm số nghiệm nguyên không âm của phương trình

$\hspace{3cm}$$x_1+x_2+...+x_n=k$

$\Rightarrow$ Số nghiệm nguyên không âm là $C^{n-1}_{n+k-1}$ 

### Bài 2

- Tìm số nghiệm nguyên không âm của phương trình

$\hspace{3cm}$$x_1+x_2+...+x_n=k$

thỏa mãn $x_1\geq m_1, ...x_n\geq m_n$ 

$\Rightarrow$ Số nghiệm thỏa mãn là $C^{n-1}_{n+k-1-(m_1+...+m_n)}$


### Bài 3

- Phương trình $x_1 + x_2 + x_3 + x_4 + x_5 + x_6 = 24$ có bao nhiêu nghiệm nguyên không âm thỏa mãn $1 \leq x_1 \leq 5, 3 \leq x_2 \leq 7$ 

- Đặt $y_1=x_1-1, y_2=x_2-3$ 
$\Rightarrow$ $y_1+y_2+x_3+x_4+x_5+x_6=20$ với điều kiện $y_1\leq 4, y_2\leq 4$ 

- Có thể tưởng tượng như sau
![[Pasted image 20240922115549.png]]

- Phần cần tìm là $X$, ta có thể chia thành từng trường hợp

TH1: Nghiệm không âm $\Rightarrow$ nghiệm sẽ là $X+1+2+3$

TH2: Nghiệm không âm thỏa mãn $y_1\geq 4$ $\Rightarrow$ $2+3$

TH3: Nghiệm không âm thỏa mãn $y_2\geq 4$ $\Rightarrow$ $1+2$

TH4: Nghiệm không âm thỏa mãn $y_1,y_2\geq 4$ $\Rightarrow$ $2$ 

$\Rightarrow$ Tìm $X$ bằng cách cộng trừ các tập nghiệm trên 

### Bài 4 

- Trong các số tự nhiên có 7 chữ số hãy đếm số các số thuận nghịch (số đối xứng) có tổng các chữ số là 18?

- Đặt số cần tìm là $a_1a_2a_3a_4a_3a_2a_1$ 
- Có
$\hspace{3cm}$$2(a_1+a_2+a_3)+a_4=18$ với $a_i$ là số nguyên không âm, $a_1\geq 1$ 

- Từ đó có các trường hợp

TH1: $a_4=0$ $\Rightarrow$ $a_1+a_2+a_3=9$ $\Rightarrow$ $C^{2}_{10}$ 

TH2: $a_4=2$ $...$ 

# Hệ thức truy hồi

### Bài 1

- Bài toán dân số

- Công thức 

$\hspace{3cm}$$P=P_0\times(1+r)^n$

- Trong đó 
	- $P$: dân số sau $n$ năm
	- $P_0$: dân số ban đầu
	- $r$: tỉ lệ tăng trưởng
	- $n$: số năm

### Bài 2

- Bài toán lãi kép

- Công thức

$\hspace{3cm}$$A=P\times(1+r)^{n}$

- Trong đó 
	- $P$: số tiền gốc gửi
	- $r$: lãi suất theo kì
	- $n$: số kì

### Bài 3

- Giải hệ thức truy hồi tuyến tính thuần nhất

$\hspace{3cm}$$a_n=c_1.a_{n-1}+c_2.a_{n-2}+...+c_k.a_{n-k}$ 

- Nghiệm sẽ có dạng $a_n=r^n$, $r$ là hằng số

- Ta có phương trình đặc trưng

$\hspace{3cm}$$r^k-c_1.r^{k-1}-c_2.r^{k-2}-...-c_k=0$ 

- Giả sử có $a_n=c_1.a_{n-1}+c_2.a_{n-2}$ 

- Phương trình đặc trưng $\Rightarrow$ $r^2-c_1.r-c_2=0$

- Nếu có 2 nghiệm phân biệt $r_1, r_2$ 

$\hspace{3cm}$$a_n=\alpha_1.r_1^n+\alpha_2.r_2^n$ 

tìm $\alpha_1, \alpha_2$ từ điều kiện ban đầu

- Nếu có nghiệm kép $r_0=r_1=r_2$ 

$\hspace{3cm}$$a_n=\alpha_1.r_0^n+\alpha_2.n.r_0^n$ 

tìm $\alpha_1, \alpha_2$ từ điều kiện ban đầu

- Nếu có nghiệm phức liên hợp $\begin{cases}r_1=r(\cos(\theta)+i.\sin(\theta))\\ r_2=r(\cos(\theta)-i.\sin(\theta))\end{cases}$ 

$\hspace{3cm}$$a_n=r^n(\alpha_1\cos(n\theta)+\alpha_2\sin(n\theta))$ 

tìm $\alpha_1, \alpha_2$ từ điều kiện ban đầu

- Tổng quát: Có $k$ nghiệm phân biệt

$\hspace{3cm}$$a_n=\alpha_1.r_1^n+\alpha_2.r_2^n+...+\alpha_k.r_k^n$ 

tìm $\alpha_i$ từ điều kiện ban đầu



