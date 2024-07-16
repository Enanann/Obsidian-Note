# Chương 1

- Tần suất

$\hspace{3cm}$$f_n(A)=\frac{n_A}{n}$ 

- Xác suất

$\hspace{3cm} P(A) = \frac{\text{số kết quả thuận lợi cho biến cố A}}{\text{số kết quả có thể xảy ra}} = \frac{|A|}{|\Omega|}$

$\hspace{3cm}$$P(A)=\displaystyle{\lim_{n\to \infty}f_n(A)}$ 

- Tính chất cơ bản

$\hspace{3cm}$$0\leq P(A)\leq 1$

$\hspace{3cm}$$P(\varnothing)=0$ 

$\hspace{3cm}$$P(\Omega)=1$ 

- Quy tắc cộng xác suất

$\hspace{3cm}$$P(A\cup B)=P(A)+P(B)-P(A\cap B)$ 

$\hspace{3cm}$$P(A\cup B\cup C)=P(A)+P(B)+P(C)$
$\hspace{6cm}$$-P(AB)-P(AC)-P(BC)+P(ABC)$ 

- Nhận xét

$\hspace{3cm}$$P(A\cup B)=P(A)+P(B)$ nếu $A, B$ là [[1.1 Phép thử và biến cố#Hai biến cố xung khắc|biến cố xung khắc]]

$\hspace{3cm}$$P(A)+P(\bar A)=1$ 

- Xác suất có điều kiện

$\hspace{3cm}$$P(A|B)=\frac{P(AB)}{P(B)}$ 

- Quy tắc nhân xác suất

$\hspace{3cm}$$P(AB)=P(A)P(B|A)=P(B)P(A|B)$  

$\hspace{3cm}$$P(A_1A_2...A_n)=P(A_1)P(A_2|A_1)...P(A_n|A_1A_2...A_{n-1})$

- $A, B$ là hai biến cố độc lập

$\hspace{3cm}$$P(A|B)=P(A)$  hoặc  $P(B|A)=P(B)$

$\hspace{3cm}$$(A, \bar B); (\bar A, \bar B); (\bar A, B)$ độc lập

$\hspace{3cm}$$P(AB)=P(A)P(B)$

- Công thức xác suất đầy đủ: $A_1,...A_n$ là hệ đầy đủ các biến cố, $A$ là biến cố bất kì

$\hspace{3cm}$$P(A)=P(A_1)P(A|A_1)+P(A_2)P(A|A_2)+...P(A_n)P(A|A_n)$ 

- Công thức Bayes: $A_1,...A_n$ là hệ đầy đủ các biến cố, $A$ là biến cố bất kì ($P(A)\neq 0$), $\forall j = 1,...n$ 

$\hspace{3cm}$$P(A_j|A)=\frac{P(A_jA)}{P(A)}=\frac{P(A_j)P(A|A_j)}{P(A)}=\frac{P(A_j)P(A|A_j)}{\displaystyle{\sum_{i=1}^n P(A_i)P(A|A_i)}}$  

- Phép thử Bernoulli: Tiến hành $n$ phép thử độc lập, để biến cố $A$ xuất hiện $k$ lần, $P(A)=p$

$\hspace{3cm}$$P_n(k)=C^k_n p^k (1-p)^{n-k}$; $k=0,1,...,n$ 

- Tìm số lần xuất hiện chắc chắn nhất $m$ 

$\hspace{3cm}$$P_n(m) \geq P_n(k) \forall k=0,1,...,n$

$\hspace{3cm}$$(n+1)p - 1 \leq m\leq (n+1)p$

# Chương 2

- Hàm khối lượng xác suất

$\hspace{3cm}$$p_X(x)=P(X=x), x\in \mathbb R$ 

$\hspace{3cm}$$p_X(x)>0, \forall x\in R_X$ 

$\hspace{3cm}$$\displaystyle{\sum_{x\in R_X}p_X(x)=1}$ 

$\hspace{3cm}$$p_X(x)=0, \forall x\notin \mathbb R$ 

- Bảng phân bố xác suất

| $X$ | $x_1$      | $x_2$      | ... |
| --- | ---------- | ---------- | --- |
| $P$ | $p_X(x_1)$ | $p_X(x_2)$ | ... |

- Hàm phân bố xác suất

$\hspace{3cm}$$F_X(x)=P(X < x); -\infty < x< +\infty$ 

$\hspace{3cm}$$0 \leq F(x) \leq 1 \forall x\in \mathbb R$

$\hspace{3cm}$$F(-\infty) = \displaystyle{\lim_{x\to -\infty} F(x)} = 0$

$\hspace{3cm}$$F(+\infty) = \displaystyle{\lim_{x\to +\infty} F(x)} = 1$

$\hspace{3cm}$$P(a<X\leq b) = F_X(b)-F_X(a)$

$\hspace{3cm}$$F_X(x)$ là hàm không giảm

$\hspace{3cm}$$F_X(x)$ là hàm liên tục phải

- Hàm mật độ xác suất

$\hspace{3cm}$$F_X(x)=\displaystyle{\int_{-\infty}^x f_X(t)dt}, \forall x\in \mathbb R$

$\hspace{3cm}$$f_X(x)\geq 0 \forall x\in \mathbb R$

$\hspace{3cm}$$f_X(x)=F'_X(x)$ tại các điểm $x$ mà $f_X(x)$ liên tục

$\hspace{3cm}$$P(a \leq X \leq b) = P(a\leq X < b)$
$\hspace{3cm}$$=P(a<X\leq b)=P(a<X<b)=\int_a^bf_X(x)dx$ 

$\hspace{3cm}$$\int_{-\infty}^{+\infty}f_X(x)dx = 1$ 

- Kỳ vọng

$\hspace{3cm}$$E(X)=\displaystyle{\sum_{i=1}^n x_ip_X(x_i)}$     (Bnn rời rạc) 

$\hspace{3cm}$$E(X)=\displaystyle{\int_{-\infty}^{+\infty}xf_X(x)dx}$     (Bnn liên tục)

$\hspace{3cm}$$E(C)=C$

$\hspace{3cm}$$E(kX+Y)=kE(X)+E(Y)$

$\hspace{3cm}$$E[g(x)]=\begin{cases} \displaystyle{\sum_{x\in R_X}g(x)p_X(x)} \\ \displaystyle{\int_{-\infty}^{+\infty}g(x)f_X(x)} \end{cases}$ 

$\hspace{3cm}$$E(XY)=E(X)E(Y)$, $X,Y$ là Bnn độc lập

- Phương sai

$\hspace{3cm}$$D(X)=E(X^2)-[E(X)]^2=E[(X-E(X))^2]$

$\hspace{3cm}$$E(X^2)=\displaystyle{\sum_{i=1}^n}x_i^2p_X(x_i)$ 

$\hspace{3cm}$$D(C)=0$

$\hspace{3cm}$$D(kX)=k^2D(X)$

$\hspace{3cm}$$D(X+Y)=D(X)+D(Y)$ với $X,Y$ là Bnn độc lập

- Độ lệch chuẩn

$\hspace{3cm}$$\sigma(X)=\sqrt{D(X)}$

- Mode

$\hspace{3cm}$Xác suất lớn nhất nếu $X$ là Bnn rời rạc

$\hspace{3cm}$Cực đại của hàm mật độ nếu $X$ là Bnn liên tục

- Phân bố nhị thức: $X\sim B(n;p)$ 

$\hspace{3cm}$$P(X=k)=C^k_n p^k(1-p)^{n-k}; k=0,1,...,n; n\in \mathbb N^*;0<p<1$  

$\hspace{3cm}$$E(X)=np$

$\hspace{3cm}$$D(X)=np(1-p)$

- Phân bố Poisson: $X\sim P(\lambda)$

$\hspace{3cm}$$P(X=k)=\frac{\lambda^k}{k!}e^{-\lambda},k=0,1,2,...$

$\hspace{3cm}$$E(X)=D(X)=\lambda$

$\hspace{3cm}$$ModX=m_0:\lambda-1 \leq m_0\leq \lambda$

- Phân bố đều $X\sim U[a;b]$ 

$\hspace{3cm}$$f_X(x)=\begin{cases} \frac{1}{b-a}, x\in[a;b] \\ 0, x\notin[a;b] \end{cases}$

$\hspace{3cm}$$E(X)=\frac{a+b}{2}$

$\hspace{3cm}$$D(X)=\frac{(b-a)^2}{12}$

$\hspace{3cm}$$F_X(x)=\begin{cases} 0 \hspace{1cm} \text{nếu } x < a \\ \frac{x-a}{b-a} \space \space \space \text{nếu } a\leq x \leq b \\ 1  \hspace{1cm}\text{nếu } x > b \end{cases}$ 

- Phân bố chuẩn: $X\sim N(\mu,\sigma^2)$ 

$\hspace{3cm}$$f_X(x)=\frac{1}{\sigma\sqrt{2\pi}}e^{-\frac{(x-\mu)^2}{2\sigma^2}}, x\in \mathbb R$ 

$\hspace{3cm}$$E(X)=\mu$

$\hspace{3cm}$$D(X)=\sigma^2$

- Phân bố chuẩn tắc: $X\sim N(0,1)$ 

$\hspace{3cm}$$\varphi(x)=\frac{1}{\sqrt{2\pi}}e^{-\frac{x^2}{2}}$     (hàm mật độ xs)

$\hspace{3cm}$$\phi(x)=\frac{1}{\sqrt{2\pi}}\displaystyle\int_{-\infty}^{x}e^{-\frac{t^2}{2}}dt$     (hàm phân bố xs)

- Cho biến ngẫu nhiên $X\sim N(0,1)$. Giá trị tới hạn mức $\alpha$ của $X$, ký hiệu $U_\alpha$, là giá trị thỏa mãn

$\hspace{3cm}$$P(X>U_\alpha)=\alpha$

- Các tìm $U_\alpha$: Tính $\phi(U_\alpha)=1-\alpha$ , sau đó tra bảng để tìm $U_\alpha$ 
- Một số giá trị thường dùng:

$\hspace{3cm}$$U_{0,025}=1,96; U_{0,05}=1,645; U_{0,01}=2,33; U_{0,005}=2,575$ 

- Các công thức tính xác suất, nếu $X\sim N(\mu, \sigma^2)$ 

	+ $P(X<a)=\phi(\frac{a-\mu}{\sigma})$

	+ $P(a<X<b)=\phi(\frac{b-\mu}{\sigma})-\phi(\frac{a-\mu}{\sigma})$ 

- Phân bố mũ với tham số $\lambda>0$ 

$\hspace{3cm}$$f_X(x)=\begin{cases} \lambda e^{-\lambda x} \hspace{1cm} \text{nếu } x > 0 \\ 0 \hspace{1.95cm} \text{nếu } x \leq 0 \end{cases}$

$\hspace{3cm}$$F_X(x)=\begin{cases} 1-e^{-\lambda x} \hspace{1cm} \text{nếu } x > 0 \\ 0 \hspace{2.5cm} \text{nếu } x \leq 0   \end{cases}$

$\hspace{3cm}$$E(X)=\frac{1}{\lambda}$

$\hspace{3cm}$$D(X)=\frac{1}{\lambda^2}$

# Chương 3

# Chương 4

# Chương 5
