$\hspace{3cm}$$.$

# Định lý lấy mẫu Shannon

- Cho tín hiệu tương tự $x_\alpha(t)$ có tần số cao nhất là $F_{max}=B$. Tốc độ lấy mẫu Nyquist

$\hspace{3cm}$$F_S=F_{Nyquist}=2F_{max}=2B$

- Chuẩn hóa $T_s=1$

$\hspace{3cm}$$x(nT_s)\overset{T_s=1}{\to}x(n)$

- Các dãy tín hiệu cơ bản

	1. Dãy xung đơn vị

$\hspace{3cm}$$\delta(n)=\begin{cases} 1 \space\space n=0 \\ 0 \space\space n \neq\end{cases}$

	2. Dãy nhảy đơn vị

$\hspace{3cm}$$u(n)=\begin{cases}1\space\space n\geq 0 \\ 0 \space\space \text{n còn lại} \end{cases}$

	3. Dãy chữ nhật

$\hspace{3cm}$$rect_N(n)=\begin{cases} 1 \space\space 0\leq n\leq N-1 \\ 0 \space\space \text{n còn lại} \end{cases}$

	4. Dãy dốc đơn vị

$\hspace{3cm}$$r(n)=\begin{cases} n \space\space n\geq 0 \\ 0 \space\space \text{n còn lại} \end{cases}$

	5. Dãy hàm mũ

$\hspace{3cm}$$e(n)=\begin{cases} a^n \space\space n\geq 0 \\ 0 \space\space\space\space \text{n còn lại} \end{cases}$

# Dãy tuần hoàn

- Dãy $x(n)$ tuần hoàn với chu kỳ $N$ nếu

$\hspace{3cm}$$x(n)=x(n+N)=x(n+I.N)$

- Khi cần nhấn mạnh tính tuần hoàn, người ta ký hiệu dấu $\sim$ ở trên: $\overset{\sim}{x}(n)_N$ 

![[Pasted image 20240908112449.png]]

# Dãy có chiều dài hữu hạn

- Một dãy xác định với hữu hạn $N$ mẫu với $N$ là chiều dài của dãy

$\hspace{3cm}$$L[x(n)]=[0,3]=4$,   $L:$ toán tử chiều dài

![[Pasted image 20240908113844.png]]

# Năng lượng của dãy

- Năng lượng của dãy $x(n$

$\hspace{3cm}$$E_x=\displaystyle{\sum_{n=-\infty}^\infty}|x(n)|^2$

# Công suất trung bình một tín hiệu 

- Công suất trung bình của một tín hiệu được định nghĩa

$\hspace{3cm}$$P=\displaystyle{\lim_{N\to \infty}\frac{1}{2N + 1}\sum_{n=-N}^{N}|x(n)|^2 \Leftrightarrow P = \lim_{N\to \infty}\frac{1}{2N + 1}E_N}$ 

# Tổng của 2 dãy

- Tổng hai dãy nhận được bằng cách cộng từng đôi một các giá trị mẫu đối với cùng một trị số của biến độc lập

- Ví dụ:
>$x_3(n)=x_1(n)+x_2(n)$ 
>![[Pasted image 20240909220258.png]]

# Tích của hai dãy

- Tích hai dãy nhận được bằng cách nhân từng đôi một các giá trị mẫu đối với cùng một trị số của biến độc lập

- Ví dụ
>$x_3(n)=x_1(n).x_2(n)$
>![[Pasted image 20240909220350.png]]

# Tích với hằng số 

- Tích của một dãy với hằng số nhận được bằng cách nhân các giá trị mẫu của dãy với hằng số đó

# Trễ 

- Dãy $x_2(n)$ là dãy lặp lại trễ của $x_1(n)$ nếu

$\hspace{3cm}$$x_2(n)=x_1(n-n_0)$     $n_0$: nguyên

- Một dãy tín hiệu bất kỳ $x(n)$ có thể được biểu diễn dưới dạng

$\hspace{3cm}$$x(n)=\displaystyle{\sum_{k=-\infty}^\infty x(k).\delta(n-k)}$

# Hệ thống tuyến tính

- Toán tử $T$ phải tuân theo nguyên lí xếp chồng

$\hspace{1.5cm}$$T[a.x_1(n)+b.x_2(n)]=a.T[x_1(n)]+b.T[x_2(n)]=a.y_1(n)+b.y_2(n)$ 

- Cho kích thích (đầu vào) $x(n)$ $\Rightarrow$ Đáp ứng (dãy ra)

$\hspace{3cm}$$y(n)=\displaystyle{\sum_{k=-\infty}^\infty}x(k).h_k(n)$

- Đáp ứng xung hệ thống tuyến tính

$\hspace{3cm}$$h_k(n)=T[\delta(n-k)]$

# Phép chập

- Để dễ dàng hơn trong việc tính toán, ta có thể tính bằng phương pháp đồ thị

![[Pasted image 20240924103536.png]]

- Ví dụ
>Cho một htttbb có $x(n)=rect_5(n); h(n)=\begin{cases} 1-\frac{n}{4} \space\space 0\leq n \leq 4\\ 0 \space\space \text{n còn lại}\end{cases}$ 
>Tìm đáp ứng ra của hệ thống $y(n)$
>
>![[Pasted image 20240924104836.png]]

### Các tính chất của phép chập

- Tính giao hoán
$\hspace{3cm}$$y(n)=x(n)*h(n)=h(n)*x(n)=\displaystyle{\sum_{k=-\infty}^\infty h(k)x(n-k)}$ 
![[Pasted image 20240924105303.png]]

- Tính kết hợp

$\hspace{3cm}$$y(n)=x(n)*[h_1(n)*h_2(n)]=[x(n)*h_1(n)]*h_2(n)$ 

![[Pasted image 20240924105316.png]]

- Tính phân phối (chập và cộng)

$\hspace{3cm}$$y(n)=x(n)*[h_1(n)+h_2(n)]=[x(n)*h_1(n)]+[x(n)*h_2(n)]$

![[Pasted image 20240924105325.png]]

- Hệ thống tuyến tính bất biến được gọi là nhân quả nếu  

$\hspace{3cm}$$h(n)=0 \space\space\forall n<0$

- Hệ thống tuyến tính bất biến được gọi là ổn định nếu

$\hspace{3cm}$$S=\displaystyle{\sum_{n=-\infty}^\infty |h(n)| < \infty}$

# Phương trình sai phân tuyến tính hệ số hằng

- Phương trình sai phân tổng quát

$\hspace{3cm}$$\displaystyle{\sum_{k=0}^N a_ky(n-k)=\sum_{r=0}^M b_rx(n-r)}$ 

- Một HTTT bất biến về mặt toán học được mô tả bời một ptsp tuyến tính hệ số hằng dạng tổng quát sau $(a_0=1)$

$\hspace{3cm}$$y(n)=\displaystyle{\sum_{r=0}^M b_rx(n-r)-\sum_{k=1}^N a_ky(n-k)}$  

- Trong đó $a_k, b_r$ là hệ số hằng, $N$ là bậc của phương trình

- $a_k,b_r$ đặc trưng cho hệ thống, tương đương với đáp ứng xung $h(n)$

- Có hai phương pháp giải phương trình sai phân
	- Phương pháp thế
	- Phương pháp tìm nghiệm tổng quát: giải phương trình tìm nghiệm thuần nhất, nghiệm riêng rồi xác định nghiệm tổng quát

# Hệ thống không đệ quy

- Từ phương trình sai phân tổng quát trên, nếu $N=0, a_0=1$

$\hspace{3cm}$$y(n)=\displaystyle{\sum_{r=0}^Mb_rx(n-r)}$

$\Rightarrow$ htttbb được mô tả bởi phương trình sai phân tuyến tính hệ số hằng bậc $0$ là hệ thống không đệ quy

- Nhận xét: $y(n)$ phụ thuộc vào đầu vào ở thời điểm hiện tại và các thời điểm quá khứ

$\hspace{3cm}$$y(n)=F[x(n), x(n-1),...x(n-M)]$

# Hệ thống đệ quy

- Trong trường hợp $N>0, a_0=1$ 

$\hspace{3cm}$$y(n)=\displaystyle{\sum_{r=0}^Mb_rx(n-r)-\sum_{k=1}^N a_ky(n-k)}$

$\Rightarrow$ htttbb được mô tả bởi phương trình sai phân bậc $N>0$ được gọi là hệ thống đệ quy

- Nhận xét: $y(n)$ phụ thuộc cả vào đầu vào ở hiện tại và quá khứ và đầu ra ở quá khứ

$\hspace{3cm}$$y(n)=F[x(n),x(n-1),...,x(n-M),y(n-1),...,y(n-N)]$

- $N>0, M=0$ ta có hệ thống đề quy thuần túy

# [[1.6 Thực hiện hệ thống]]

