
# Nguyên tắc đo lường thông tin

Xét nguồn tin $A=\{a_1, a_2,...a_s\}$ với $p(a_i), i=1,...,s$; $\sum p(a_i)=1$

### 1. Độ bất định của một dấu của nguồn (lượng tin riêng)

$\hspace{3cm}$$I(a_i)=\log\frac{1}{p(a_i)}=-\log [p(a_i)]$

đơn vị: nat ($\ln$), bit ($\log_2$), hart ($\log_10$) 

$1 \text{ nat} = 1,443 \text{ bit}$
$1 \text{ hart} = 3,322 \text{ bit}$

### 2. Entropy (lượng tin trung bình)

$\hspace{3cm}$$H(A)=\displaystyle{-\sum_{i=1}^s p(a_i)\log[p(a_i)]}$    $(\text{bit/symbol})$

$H(A)\equiv H_1(A)$: Entropy tiên nghiệm; Entropy không điều kiện

- **Tính chất 1**:

$\hspace{3cm}$$H_1(A)\geq 0$

Dấu "$=$" xảy ra $\Leftrightarrow$ tồn tại một $\text{symbol}$ ($a_i$) có xác suất $p(a_i)=1$   

- **Tính chất 2**: Một nguồn $A$ rời rạc gồm $s$ dấu thì

$\hspace{3cm}$$H_1(A)\leq \log s \equiv H_0(A)$

Dấu "$=$" xảy ra $\Leftrightarrow$ các $\text{symbol}$ của nguồn đồng xác suất. Tức entropy đạt **max**, ký hiệu $H_0(A)$ 

### 3. Entropy nguồn nhị phân

$\hspace{3cm}$$H_1(A)=\displaystyle{-p\log p-(1-p)\log(1-p)}$

### 4. Thông tin tương hỗ 

$\hspace{3cm}$$I(x_k; y_l)=\log\frac{p(x_k|y_l)}{p(x_k)}$

- Tính chất

$\hspace{3cm}$$I(x_k;y_l)=I(x_k)-I(x_k|y_l)$

$\hspace{3cm}$$-\infty\leq I(x_k;y_l)\leq I(x_k), I(y_l)$

$\hspace{3cm}$$I(x_k;y_l)=I(y_l;x_k)=\log\frac{p(y_l|x_k)}{p(y_l)}$

- $X, Y$ là kênh độc lập 

$\hspace{3cm}$$p(x_k|y_l)=p(x_k) \forall k$ 

$\Rightarrow$$\hspace{3cm}$$I(x_k;y_l)=0$

- $X, Y$ là kênh lý tưởng 

$\hspace{3cm}$$p(x_k|y_l)=1$

$\Rightarrow$$\hspace{3cm}$$I(x_k;y_l)=I(x_k)$

### 5. Entropy đồng thời

$\hspace{3cm}$$H(A,B)\overset{\Delta}{=}E[\log\frac{1}{p(a_i, b_j)}]=\displaystyle{\sum_{i=1}^s\sum_{j=1}^t p(a_i, b_j).\log[p(a_i, b_j)]}$   

- Tính chất
	- $H(A,B)\leq H(A)+H(B)$

	- Nếu $A$ độc lập với $B$
$\hspace{3cm}$$p(a_i, b_j)=p(a_i)p(b_j)$ $\Rightarrow$ $H(A,B)=H(A)+H(B)$

### 6. Entropy có điều kiện

- Entropy của $A$ khi đã rõ một dấu $b_j$ của $B$

$\hspace{3cm}$$H(A|b_j)\overset{\Delta}{=}E[I(a_i|b_j)]=-\sum_{i=1}^sp(a_i|b_j)\log[p(a_i|b_j)]$   

- Entropy của $A$ khi đã rõ $B$

$\hspace{3cm}$$H(A|B)\overset{\Delta}{=}E[H(A|b_j)]=\sum_{j=1}^t p(b_j)H(A|b_j)$
$\hspace{3cm}$$=-\sum_{j=1}^t\sum_{i=1}^s p(a_i, b_j)\log[p(a_i|b_j)]$

- **Tính chất 1**: Chain rule (luật xâu chuỗi)

$\hspace{3cm}$$H(B,A)=H(A,B)=H(A) + H(B|A) = H(B) + H(A|B)$

- **Tính chất 2**:

$\hspace{3cm}$$0\leq H(A|B) \leq H(A)$

$\hspace{3cm}$$0\leq H(B|A)\leq H(B)$
	
	- $H(A|B)=H(B|A)=0$ khi $A$ và $B$ đồng nhất (kênh hoàn hảo, không nhiễu)
	- $H(A|B)=H(A), H(B|A)=H(B)$ khi $A$ và $B$ độc lập (kênh bị đứt)

- **Tính chất 3**: Cho DMS $X=\{x_k\}, k=1,...N$. Một hàm toán học $f(X)$ mô tả mối quan hệ xác định của $f$ và $X$. Khi đó

$\hspace{3cm}$$H(f(X)|X)=0$

$\hspace{3cm}$$H(X|f(X))\geq 0;H(X)\geq H(f(X))$

	- Dấu "$=$" xảy ra khi và chỉ khi $f(X)$ là quan hệ ánh xạ $1-1$ 

### 7. Lượng thông tin tương hỗ trung bình

$\hspace{3cm}$$I(A;B)\overset{\Delta}{=}E[I(a_i;b_j)]=\displaystyle{\sum_{i=1}^s\sum_{j=1}^t p(a_i, b_j)\log\frac{p(a_i|b_j)}{p(a_i)}}$ 

- **Tính chất 1**

$\hspace{3cm}$$I(A;B)\geq 0$

	- Dấu "$=$" xảy ra khi và chỉ khi $A$ độc lập với $B$ $\to$ Kênh đứt

- **Tính chất 2**

$\hspace{3cm}$$I(A;A)=H(A)$

- **Tính chất 3**

$\hspace{3cm}$$I(A;B)=I(B;A)$

- **Tính chất 4**

$\hspace{3cm}$$I(A;B)\leq H(A)$

	- $I(A;B)=H(A)=H(B)$ khi kênh không nhiễu

- **Tính chất 5**

$\hspace{3cm}$$I(A;B)=H(A)-H(A|B)=H(B)-H(B|A)$
$\hspace{3cm}$$=H(A)+H(B)-H(A,B)$

# Các tham số đặc trưng cho nguồn và kênh rời rạc

### 1. Tốc độ baud của nguồn

$\hspace{3cm}$$v_n\overset{\Delta}{=}\frac{1}{T_n}$   ($Baud$)

$T_n$: Thời hạn **trung bình của mỗi dấu nguồn phát**

### 2. Tốc độ bit của nguồn

$\hspace{3cm}$$R_n\overset{\Delta}{=}v_n H(A)=\frac{H(A)}{T_n}$   ($bps$)

$R_n \max$ khi $H(A) \max=H_0(A)=\log S$

### 3. Độ thừa và hệ số nén tin

$\hspace{3cm}$$D=1-\mu$ 

$\hspace{3cm}$$\mu=\frac{H(A)}{H_0(A)}$   (hệ số nén tin)

### 4. Tốc độ baud của kênh

$\hspace{3cm}$$v_k\overset{\Delta}{=}\frac{1}{T_k}$   ($Baud$)

$T_k$: Thời gian trung bình để truyền một dấu qua kênh $\begin{cases}\text{Kênh giãn tin:}\space\space T_k>T_n \\ \text{Kênh nén tin:}\space\space T_k<T_n \\ \text{Thông thường:}\space\space T_k=T_n\end{cases}$ 

### 5. Tốc độ bit của kênh

$\hspace{3cm}$$R_k=v_kI(A;B)$   ($bps$)

### 6. Dung lượng kênh

$\hspace{3cm}$$C=\underset{A}{\max}I(A;B)$   ($bit/symbol$)

- Tính chất
	- $0\leq C\leq \log S$
	- $C=0$ khi $A,B$ độc lập (kênh đứt)

### 7. Khả năng thông qua của kênh

$\hspace{3cm}$$C'=\underset{A}{\max} R_k=v_k\underset{A}{\max}I(A;B)=v_kC$   ($bit/s$)

### 8. Độ thừa của kênh 

$\hspace{3cm}$$D_k=1-\eta_k$

$\eta_k=\frac{R_k}{C'}$ (Hiệu suất sử dụng kênh)

# Nguồn và kênh liên tục không nhớ

### 1. Entropy vi phân

$\hspace{3cm}$$h(S)\overset{\Delta}{=}\displaystyle{\int_{-\infty}^{+\infty} W_1(s)\log\frac{1}{W_1(s)}ds}$ 

$W_1$: Hàm mật độ phân bố xác suất

### 2. Công thức entropy theo phân bố

- Phân bố chuẩn

$\hspace{3cm}$$h(X)=\frac{1}{2}\log(2\pi e\sigma^2)=\log\sqrt{2\pi e\sigma^2}$

- Phân bố đều

$\hspace{3cm}$$h(X)=\displaystyle{-\int_a^b\frac{1}{b-a}\log\frac{1}{b-a}dx=\log(b-a)}$ 

- Phân bố mũ

$\hspace{3cm}$$h(X)=\log\frac{e}{\lambda}$

### 3. Entropy đồng thời, entropy có điều kiện

### 4. Lượng tin tương hỗ

### 5. Kênh AWGN không nhớ

- Dung lượng kênh

$\hspace{3cm}$$C'=F\log(1+\frac{\mu^2 P_s}{N_0F})=F.\log(1+SNR)$  $[bps]$ 

	- $F$: BW của kênh (band width)
	- $P_n$: Công suất trung bình của nhiễu trong giải $F$
	- $P_n=N_0.F$: Với trường hợp nhiễu tạp âm trắng
	- $N_0$: Mật độ phổ công suất của nhiễu cộng

- Nếu $F\to\infty$, tức là khi giải thông kênh là vô hạn

$\hspace{3cm}$$C'_{\infty}=\lim_{F\to\infty}C'=(\log_2e) (\frac{\mu^2 P_s}{N_0})=1,443.\frac{P_{\mu s}}{N_0}$   $[bps]$
