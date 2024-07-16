
# Khái niệm

>[!text]
>Phương trình vi phân là phương trình liên hệ giữa các biến, hàm phải tìm và các đạo hàm của hàm phải tìm
>
>$\hspace{3cm}$$F(x,y,y',y'',...y^{(n)})=0$ (PTVT cấp $n$)

- Ví dụ:
>$y'''-x.y'+y=0$     (PTVT cấp 3)

>$y''=x^2$     (PTVP cấp 2)
>$y'=\frac{x^3}{3}+c_1$
>$y=\frac{x^4}{12}+c_1x+c_2$ 

- Để giải PTVP, dùng tích phân
- Nghiệm có dạng

$\hspace{3cm}$$y=f(x,c_1,c_2,...c_n)$   (dạng tường minh)

$\hspace{3cm}$$f(x,y,c_1,...c_n)=0$   (dạng không tường minh)

- Cho $c_1,...c_n$ bởi các hằng số ta được nghiệm riêng

$\hspace{3cm}$$y=f(x,c^0_1,...c^0_n$

$\hspace{3cm}$$f(x,y,c^0_1,...c^0_n)=0$

# Phương trình vi phân cấp 1

- $F(x,y,y')=0$ 

### Phương trình phân li

- Dạng 1: $M(x)d(x)+N(y)d(y)=0$     ($y'=\frac{dy}{dx}$)

- Cách giải

>$\int M(x)dx+ \int N(y)dy = C$

- Dạng 2: $M_1(x)N_1(y)dx+M_2(x)N_2(y)dy=0$ 

- Cách giải:

>Chia cả 2 vế cho $N_1(y)M_2(x)$ 
>
>$\frac{M_1(x)}{M_2(x)}dx+\frac{N_2(y)}{N_1(y)}dy=0$ 

### Phương trình đẳng cấp

- Dạng 1: $y'=f(\frac{y}{x})$ 

- Cách giải
>Đặt $u=\frac{y}{x}$ $\Rightarrow$ $y=ux$ $\Rightarrow$ $y'=u'x+u$ 

- Dạng 2: Các số hạng có cùng bậc $n$

- Cách giải
>Chia cho $x^n$ $\Rightarrow$ Đưa về dạng 1

### Phương trình tuyến tính

- $y'+P(x)y=Q(x)$

- Cách giải
>$y=Ce^{-\int P(x)dx}+e^{-\int P(x)dx}\int Q(x)e^{\int P(x)dx}dx$ 



### Xem thêm [[8.1 Các quy tắc tính đạo hàm]]

![[Pasted image 20240701115854.png]]
