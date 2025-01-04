
# Đới cầu Fresnel

![[Pasted image 20240927161847.png]]

- Diện tích các đới cầu bằng nhau

$\hspace{3cm}$$\Delta S=\frac{\pi Rb}{R+b}\lambda$

- Trong đó
	- $R$: bán kính mặt cầu $\Sigma$ 
	- $b$: bán kính mặt cầu $\Sigma_0$

- Bán kính $r_k$ của đới cầu thứ $k$

$\hspace{3cm}$$r_k=\sqrt{\frac{\lambda Rb k}{R+b}}$ 

- Biên độ dao động do đới cầu thứ $k$ gây ra tại $M$

$\hspace{3cm}$$a_k=\frac{1}{2}(a_{k-1}+a_{k+1})$

- Biên độ dao động tại $M$

$\hspace{3cm}$$a=\frac{1}{2}(a_1\pm a_{n})$

($+$ nếu $n$ lẻ, $-$ nếu $n$ chẵn)

# Nhiễu xạ qua lỗ tròn

![[Pasted image 20240927162231.png]]

### Khi không có lỗ tròn $AB$ hoặc kích thước lỗ tròn rất lớn

- Lúc này $n\to\infty$, $a_n\approx 0$, nên [[2.1 Cơ sở của quang học sóng#Cường độ sáng|cường độ sáng]] tại $M$

$\hspace{3cm}$$I_0=a^2=\frac{a_1^2}{4}$

### Khi $AB$ chứa số lẻ đới cầu

- Biên độ sáng tổng hợp tại $M$

$\hspace{3cm}$$a=\frac{1}{2}(a_1+a_n)$

- Cường độ sáng tại $M$

$\hspace{3cm}$$I=(\frac{a_1}{2}+\frac{a_n}{2})^2$ 

- Ta có $I>I_0$ $\Rightarrow$ Tại $M$ là vân sáng, đặc biệt nếu lỗ chứa một đới cầu $a=\frac{1}{2}(a_1+a_1)=a_1$  

$\hspace{3cm}$$I=a_1^2=4I_0$ (sáng gấp 4 lần so với khi không có lỗ tròn $\to$ sáng nhất)

### Khi $AB$ chứa số chẵn đới cầu

- Biien độ sáng tổng hợp tại $M$

$\hspace{3cm}$$a=\frac{1}{2}(a_1-a_n)$

- Cường độ sáng tại $M$

$\hspace{3cm}$$I=(\frac{a_1}{2}-\frac{a_n}{2})^2$ 

- Ta có $I<I_0$ $\Rightarrow$ Tại $M$ là vân tối, đặc biệt nếu chứa 2 đới cầu $a=\frac{1}{2}(a_1-a_2)\approx 0$ 

$\hspace{3cm}$$I=0$ (tối nhất)

# Nhiễu xạ qua một đĩa tròn

![[Pasted image 20240927162325.png]]

- Giữa nguồn sáng $S$ và điểm $M$ có một đĩa tròn chắn sáng bán kính $r_0$ 
- Giả sử đĩa che khuất $m$ đới cầu Fresnel đầu tiên. Biên độ dao động tại $M$

$\hspace{3cm}$$a=\frac{a_{m+1}}{2}$ 

- Nếu đĩa che ít đới cầu thì $a_{m+1}$ không khác mấy $a_1$, tại $M$ có ánh sáng. Đặc biệt, nếu đĩa che 1 đới thì tại $M$ sáng nhất

# Nhiễu xạ gây bởi sóng phẳng qua một khe hẹp 

![[Pasted image 20240927163615.png]]

- Độ rộng một dải 

$\hspace{3cm}$$l=\frac{\lambda}{2\sin\varphi}$

- Số dải sáng trên khe

$\hspace{3cm}$$N=\frac{b}{l}=\frac{2b\sin\varphi}{\lambda}$

- Điều kiện tại $M$ là vân tối

$\hspace{3cm}$$N=2k \Rightarrow \sin\varphi=k\frac{\lambda}{b}$     với $k=\pm 1,\pm 2$ 

- Điều kiện tại $M$ là vân sáng

$\hspace{3cm}$$N=2k+1\Rightarrow \sin\varphi=(2k+1)\frac{\lambda}{2b}$     với $k\neq 0, k\neq -1$ 

- Cực đại giữa

$\hspace{3cm}$$\sin\varphi=0$

![[Pasted image 20240927163834.png]]

# Nhiễu xạ gây bởi sóng phẳng qua nhiều khe hẹp - cách tử nhiễu xạ

- Là một hệ nhiều khe hẹp giống nhau có độ rộng $b$, nằm song song cách đều trên cùng một mặt phẳng

![[Pasted image 20240927164919.png]]

- Khoảng cách $d$ giữa hai khe kế tiếp được gọi là *chu kì* của cách tử

- Số khe hẹp trên một đơn vị chiều dài được gọi là hằng số cách tử

$\hspace{3cm}$$N=\frac{l}{d}$

- Tất cả $N$ khe hẹp đều cho cực tiểu chính tại điểm thỏa mãn

$\hspace{3cm}$$\sin\varphi=k\frac{\lambda}{b}$

![[Pasted image 20240927165610.png]]

- Hiệu quang lộ hai tia sáng từ hai khe kế tiếp

$\hspace{3cm}$$\Delta L=d\sin\varphi$

- $d\sin\varphi=m\lambda$ $\Rightarrow$ Tại $M$ là cực đại chính

$\hspace{3cm}$$\sin\varphi=m\frac{\lambda}{d}$     với $m=0,\pm 1,\pm 2,...$

- Cực đại chính giữa $m=0$ nằm tại $F$

- Do $d>b$ $\Rightarrow$ Có thể có nhiều cực đại chính giữa hai cực tiểu chính 

# Nhiễu xạ của ánh sáng trắng qua cách tử

- Mỗi đơn sắc của ánh sáng trắng tạo nên một hệ thống các cực đại chính ứng với các giá trị $m$ khác nhau

$\hspace{3cm}$$\sin\varphi=m\frac{\lambda}{d}$     với $m=0,\pm1,\pm2,...$ 

- Tập hợp các cực đại chính có cùng giá trị $m$ tạo nên một quang phổ bậc $m$. Trong mỗi quang phổ, vạch tím $T$ nằm phía trong, vạch đỏ $Đ$ nằm phía ngoài

- Ra xa vân trắng giữa, các vạch quang phổ bậc khác nhau có thể chồng lên nhau

- Các quang phổ cho bởi cách tử được gọi là quang phổ nhiễu xạ

![[Pasted image 20240927182249.png]]

# Nhiễu xạ trên tinh thể

- Chiếu lên tinh thể một chùm tia Rơnghen, những tia nhiễu xạ trên các nút mạng tinh thể sẽ giao thoa với nhau và cho cực đại nhiễu xạ nếu hai tia nhiễu xạ kế tiếp có hiệu quang lộ bằng số nguyên lần bước sóng

$\hspace{3cm}$$\Delta L=2d\sin\varphi=k\lambda$

$\hspace{3cm}$$\sin\varphi=k\frac{\lambda}{2d}$

- $d$ là khoảng cách giữa hai mặt phẳng nguyên tử của vật rắn tinh thể (chu kì mạng tinh thể)

![[Pasted image 20240928000432.png]]