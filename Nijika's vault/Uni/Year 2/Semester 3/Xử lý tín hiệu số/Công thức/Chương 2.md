
# Biến đổi $Z$

- Biến đổi $Z$ của một dãy $x(n)$ được định nghĩa như sau

$\hspace{3cm}$$X(z)=\displaystyle{\sum_{n=-\infty}^\infty x(n)z^{-n}}$

- Ký hiệu bởi toán tử

$\hspace{3cm}$$ZT[x(n)]=X(z)$

$\hspace{3cm}$$x(n) \overset{ZT}{\to}X(z)$ 

- Trong định nghĩa trên, nếu đổi cận $n=0$ ta có biến đổi $Z$ một phía

$\hspace{3cm}$$X(z)=\displaystyle{\sum_{n=0}^\infty x(n)z^{-n}}$

- $z$ là số phức 

- Biểu diễn theo phần thực, phần ảo

$\hspace{3cm}$$z=Re[z]+Im[z]$

![[Pasted image 20240925153656.png]]

- Biểu diễn theo tọa độ cực

$\hspace{3cm}$$z=re^{j\omega}=r(\cos\omega+j\sin\omega)=r\cos\omega+j.r.\sin\omega$ 

$\hspace{3cm}$$z=Re[z]+j.Im[z]$

- $|z|=r=1$ ta có vòng tròn đơn vị

# Miền hội tụ biến đổi $Z$

- $RC$ (Region of Convergence) là tập hợp các giá trị $z$ để $X(z)=\displaystyle{\sum_{n=-\infty}^\infty x(n)z^{-n}}$ hội tụ

>![[Pasted image 20240925155538.png]]

# Điểm cực, điểm không (Pole and Zero)

- Điểm không là $z_{0r}$ để tại đó $X(z)=0$, $z_{0r}$ là nghiệm của $N(z)$

$\hspace{3cm}$$X(z)|_{z=z_{0r}}=0$

- Điểm cực là $z_{pk}$ để tại đó $X(z)$ không xác định, $z_{pk}$ là nghiệm của $D(z)$

$\hspace{3cm}$$X(z)|_{z=z_{pk}}\to \infty$

- Biểu diễn $X(z)$ theo $N(z), D(z)$

$\hspace{3cm}$$X(Z)=\frac{N(z)}{D(z)}=\frac{b_M}{a_N}.\displaystyle{\frac{\prod_{r=1}^M(z-z_{0r})}{\prod_{k=1}^N(z-z_{pk})}}$

# Biến đổi $Z$ ngược

- Biến đổi $Z$ ngược được định nghĩa như sau

$\hspace{3cm}$$x(n)=\frac{1}{2\pi.j}\oint_c X(z).z^{n-1}dz$ 

- Ký hiệu 

$\hspace{3cm}$$IZT[X(z)]=x(n)$

$\hspace{3cm}$$X(z)\overset{IZT}{\to}x(n)$ 

### Phương pháp khai triển thành chuỗi lũy thừa

- Ta khai triển biến đổi $Z$ thành một chuỗi lũy thừa có dạng

$\hspace{3cm}$$X(z)=\displaystyle{\sum_{n=-\infty}^\infty \alpha_n z^{-n}}$

- So sánh với định nghĩa

$\hspace{3cm}$$X(z)=\displaystyle{\sum_{n=-\infty}^\infty x(n)z^{-n}} \Rightarrow x(n)\equiv \alpha_n$ 

- Hệ số của chuỗi chính là các mẫu của tín hiệu $x(n)$

### Phương pháp khai triển thành phân thức tối giản

- Xét

$\hspace{3cm}$$X(z)=\frac{N(z)}{D(z)}$

- Trong đó bậc của $N(z)$ là $M$; bậc của $D(z)$ là $N$

#### Trường hợp $M\geq N$ 

- Để phân thức tối giản thì

$\hspace{3cm}$$X(z)=\frac{N(z)}{D(z)}=S(z)+\frac{P(z)}{Q(z)}$

với $S(z)$ là phần nguyên, $D(z)\equiv Q(z)$ 
Bậc của $S(z)=M-N$ 

- Lúc này ta có

$\hspace{3cm}$$S(z)=B_{M-N}z^{M-N}+B_{M-N-1}z^{M-N-1}+...+B_1z^1+B_0$ 
$s(n)=B_{M-N}\delta[n+(M-N)]+B_{M-N-1}\delta[n+(M-N-1)]+...+B_1\delta[n+1]+B_0\delta(n)$  
#### Trường hợp $M<N$ 

- Có

$\hspace{3cm}$$X(z)=\frac{N(z)}{D(z)}\equiv\frac{P(z)}{Q(z)}$ 

- Xét 

$\hspace{3cm}$$X(z)=\frac{P(z)}{Q(z)}$

##### Trường hợp 1: $X(z)$ chỉ có các cực đơn

- $\frac{1}{z-1}$ $\Rightarrow$ $z=1$ là cực đơn

- $z_{pk}$ là điểm cực của $X(z)$ có $N$ cực 

$\hspace{3cm}$$X(z)=\displaystyle{\sum_{k=1}^N\frac{A_k}{z-z_{pk}}}$

- Trong đó $A_k=(z-z_{pk})\frac{P(z)}{Q(z)}|_{z=z_{pk}}$ 

##### Trường hợp 2: $X(z)$ có một cực bội $z_{pl}$ bậc $s$, còn lại các nghiệm $z_{pk}$ đơn 

- $\frac{1}{(z-1)^2}$ $\Rightarrow$ $z=1$ là cực bội bậc 2

- Xét

$\hspace{3cm}$$X(z)=\displaystyle{\sum_{k=1}^{N-s} \frac{A_k}{z-z_{pk}}+\sum_{j=1}^s\frac{C_j}{(z-z_{pl})^j}}$ 

- Trong đó

$\hspace{3cm}$$A_k=(z-z_{pk})\frac{P(z)}{Q(z)}|_{z=z_{pk}}$

$\hspace{3cm}$$C_j=\frac{1}{(s-j)!}\frac{d^{s-j}}{dz^{s-j}}[(z-z_{pl})^s\frac{P(z)}{Q(z)}]|_{z=z_{pl}}$  

- Lưu ý

$\hspace{3cm}$$IZT[\frac{z}{(z-z_{pk})^{m+1}}]=\frac{n(n-1)...(n-m+1)}{m!}z_{pk}^{n-m}u(n)$

# Độ ổn định

### Tìm bình thường

- Cho hàm truyền đạt $H(z)$, htttbb nhân quả là ổn định nếu **tất cả điểm cực** của nó nằm bên trong vòng tròn đơn vị (nằm trên hoặc ngoài $\Rightarrow$ Không ổn định)

### Tiêu chuẩn ổn định Jury 

- Từ [[2.4 Biểu diễn hệ thống rời rạc trong miền Z#Liên hệ với phương trình sai phân|liên hệ với phương trình sai phân]], ta có hàm truyền đạt của hệ thống

$\hspace{3cm}$$H(z)={\frac{\displaystyle{\sum_{r=0}^M b_rz^{-r}}}{\displaystyle{1+\sum_{k=1}^Na_kz^{-k}}}}$ 

- Từ công thức trên, gọi $D(z)=1+\displaystyle{\sum_{k=1}^N a_kz^{-k}}$ 

- Từ các hệ số $a_k$, ta lập bảng Jury có $2N-3$ hàng bằng cách sau

![[Pasted image 20240925214458.png]]

- Công thức tính $c_i, d_i$

$\hspace{3cm}$$c_i=\det\begin{bmatrix} 1 & a_{N-1} \\ a_N & a_i\end{bmatrix}=a_i-a_N.a_{N-1};\space\space i:0 \to N-1$     

$\hspace{1cm}$$d_i=\det\begin{bmatrix} c_0 & c_{N-1-i} \\ c_{N-1} & c_i\end{bmatrix}=c_0.c_i-c_{N-1}.c_{N-1-i};\space\space i:0 \to N-2$

- Sau khi lập xong $2N-3$ hàng ta có tiêu chuẩn

- Một hệ thống là ổn định nếu và chỉ nếu các điều kiện sau đây thỏa mãn

	1. $D(z)|_{z=1} > 0$

	2. $D(z)|_{z=-1}>0$  với $N$ chẵn
	        $D(z)|_{z=-1}<0$  với $N$ lẻ

	3. $1>|a_N|, |c_0|>|c_{N-1}|, |d_0|>|d_{N-2}|,...,|r_0|>|r_2|$ 