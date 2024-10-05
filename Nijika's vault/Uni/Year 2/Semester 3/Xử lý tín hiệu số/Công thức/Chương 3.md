
# Biến đổi Fourier

- Định nghĩa

$\hspace{3cm}$$X(e^{j\omega})=\displaystyle{\sum_{n=-\infty}^\infty x(n).e^{-j\omega n}}$

- Điều kiện để tồn tại

$\hspace{3cm}$$\displaystyle{\sum_{n=-\infty}^\infty|x(n)|}<\infty$

- Các khái niệm 	

	- $X(e^{j\omega})$: Phổ của tín hiệu $x(n)$

	- $|X(e^{j\omega})|$: Phổ biên dộ của tín hiệu $x(n)$

	- $\arg[X(e^{j\omega})]=\varphi(\omega)$: Phổ pha của tín hiệu $x(n)$

	- $X(e^{j\omega]})=|X(e^{j\omega})|.e^{j\varphi(\omega)}$
	
	- $A(e^{j\omega})$: Độ lớn của tín hiệu $x(n)$, có thể dương hoặc âm hoặc bằng $0$
	
	- $\theta(\omega)$: Pha của tín hiệu $x(n)$

- Một số các quan hệ

$\hspace{3cm}$$X(e^{j\omega})=A(e^{j\omega}).e^{j\theta(\omega)}$

$\hspace{3cm}$$X(e^{j\omega})=|X(e^{j\omega})|.e^{j\varphi(\omega)}$

$\hspace{3cm}$$|X(e^{j\omega})|=|A(e^{j\omega})|$   khi $\omega\geq0$ 

$\hspace{3cm}$$\varphi(\omega)=\theta(\omega)$   khi $A(e^{j\omega})\geq 0$

$\hspace{3cm}$$\varphi(\omega)=\theta(\omega)+\pi$   khi $A(e^{j\omega})<0$

# Biến đổi Fourier ngược - IFT

- Định nghĩa

$\hspace{3cm}$$x(n)=\displaystyle{\frac{1}{2\pi}\int_{-\pi}^\pi X(e^{j\omega})e^{j\omega n} d\omega}$

# Một số tính chất cần chú ý

- Phép chập trong miền thời gian rời rạc $n$ sẽ thành phép nhân

$\hspace{3cm}$$x_1(n)*x_2(n)\Rightarrow X_1(e^{j\omega}).X_2(e^{j\omega})$

- Trễ tín hiệu

$\hspace{3cm}$$x(n-n_0)\Rightarrow e^{-j\omega n_0}.X(e^{j\omega})$

- Trễ tần số

$\hspace{3cm}$$e^{j\omega_0 n}x(n)\Rightarrow X[e^{j(\omega-\omega_0)}]$

- Quan hệ Parseval: thể hiện sự bảo toàn về mặt năng lượng khi chuyển từ  miền thời gian sang miền tần số

$\hspace{3cm}$$\displaystyle{\sum_{n=-\infty}^\infty|x(n)|^2 \Rightarrow \frac{1}{2}\int_{-\pi}^\pi |X(e^{j\omega})|^2 d\omega}$

# Đáp ứng tần số

- Quan hệ vào ra của hệ thống

$\hspace{3cm}$$Y(e^{j\omega})=X(e^{j\omega}).H(e^{j\omega})$

hay

$\hspace{3cm}$$H(e^{j\omega})=\frac{Y(e^{j\omega})}{X(e^{j\omega})}$ 

- $H(e^{j\omega})$ được gọi là **đáp ứng tần số** và nó chính là biến đổi Fourier của [[1.3 Các hệ thống tuyến tính bất biến#Đáp ứng xung của hệ thống tuyến tính|đáp ứng xung]] $h(n)$ 

- $H(e^{j\omega})$ đặc trưng hoàn toàn cho hệ thống trong miền tần số $\omega$

- Biểu diễn theo phần thực, ảo

$\hspace{3cm}$$H(e^{j\omega})=Re[H(e^{j\omega})]+j.Im[H(e^{j\omega})]$

- Biểu diễn theo Modul và Argument

$\hspace{3cm}$$H(e^{j\omega})=|H(e^{j\omega})|.e^{j.\arg[H(e^{j\omega})]}$ 

$\hspace{3cm}$$H(e^{j\omega})=|H(e^{j\omega})|.e^{j\varphi(\omega)}$

- Trong đó 
	- $|X(e^{j\omega})|:$ Đáp ứng tần số của biên độ (đáp ứng biên độ)
	- $\arg[H(e^{j\omega})]=\varphi(\omega):$ Đáp ứng tần số của pha (đáp ứng pha)

- Biểu diễn theo độ lớn và pha

$\hspace{3cm}$$H(e^{j\omega})=A(e^{j\omega}).e^{j\theta(\omega)}$
