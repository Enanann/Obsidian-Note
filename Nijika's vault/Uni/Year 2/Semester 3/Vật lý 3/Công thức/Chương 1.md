
# Dao động điện từ điều hòa

- Phương trình dao động điện từ điều hòa

$\hspace{3cm}$$i=I_0\cos(\omega_0 t+\varphi)$

- Tần số góc riêng của dao động

$\hspace{3cm}$$\omega_0=\frac{1}{\sqrt{LC}}$

- Chu kỳ

$\hspace{3cm}$$T=\frac{2\pi}{\omega_0}=2\pi\sqrt{LC}$

- Có thể thấy $i$ sớm pha $\frac{\pi}{2}$ so với $q$

$\hspace{3cm}$$q=Q_0\sin(\omega_0 t)$

$\hspace{3cm}$$i=\frac{dq}{dt}$

$\hspace{3cm}$$i=I_0\cos(\omega_0 t)$

# Dao động điện từ tắt dần

- Phương trình dao động

$\hspace{3cm}$$i=I_0.e^{-\beta t}\cos(\omega t +\varphi)$

- Điều kiện $(\omega_0>\beta)$, đặt $2\beta=\frac{R}{L}$

- Tần số góc của dao động điện từ tắt dần

$\hspace{3cm}$$\omega=\sqrt{\frac{1}{LC}-(\frac{R}{2L})^2} < \omega_0$

- Chu kỳ

$\hspace{3cm}$$T=\frac{2\pi}{\omega}=\frac{2\pi}{\sqrt{\omega_0^2-\beta^2}}$ 

- Giảm lượng lôga

$\hspace{3cm}$$\delta=\ln\frac{I_0.e^{-\beta t}}{I_0.e^{-\beta(t+T)}}=\beta T$  

# Dao động điện từ cưỡng bức

- Mắc thêm vào mạch một nguồn điện xoay chiều có suất điện động biến thiên tuần hoàn 

$\hspace{3cm}$$\varepsilon = \varepsilon_0\sin(\Omega t)$ 

- Phương trình dao động điện từ cưỡng bức

$\hspace{3cm}$$i=I_0\cos(\Omega t + \phi)$ 

- Trong đó $\begin{cases}\Omega:\text{Tần số góc của nguồn điện kích thích} \\ I_0:\text{biên độ}, I_0=\frac{\varepsilon_0}{\sqrt{R^2+(\Omega L - \frac{1}{\Omega C})^2}} \\ \phi:\text{Pha ban đầu của dao động}, \cot \phi=-\frac{\Omega L - \frac{1}{\Omega C}}{R} \end{cases}$ 

- Đặt $Z=\sqrt{R^2+(\Omega L - \frac{1}{\Omega C})^2}$: Tổng trở của mạch dao động

- $Z_L=\Omega L$ và $Z_C=\frac{1}{\Omega C}$ lần lượt là cảm kháng và dung kháng của mạch dao động

- Cộng hưởng

$\hspace{3cm}$$Z_L=Z_C$ 

$\hspace{3cm}$$\Omega_{ch}=\omega_0$

- Công thức liên hệ $T, v, f, \lambda$

$\hspace{3cm}$$T=\frac{1}{f}=\frac{\lambda}{v}$

# Tổng hợp hai dao động

- Giả sử có chất điểm thao gia đồng thời hai dao động điều hòa cùng phương, cùng tần số

$\hspace{3cm}$$x_1=A_1\cos(\omega_0 t + \varphi_1)$

$\hspace{3cm}$$x_2=A_2\cos(\omega_0 t + \varphi_2)$

- Dao động tổng hợp của chất điểm bằng tổng hai dao động thành phần

$\hspace{3cm}$$x=x_1+x_2=A\cos(\omega t + \varphi)$

- Xác định bởi

$\hspace{3cm}$$A=\sqrt{A_1^2+A_2^2+2A_1A_2\cos(\varphi_2-\varphi_1)}$

$\hspace{3cm}$$\tan \varphi=\frac{A_1\sin \varphi_1+A_2\sin \varphi_2}{A_1\cos\varphi 1 + A_2\cos\varphi_2}$ 

- $A_{max}$ khi $(\varphi_2-\varphi_1)=2k\pi$

$\hspace{3cm}$$A_{max}=A_1+A_2$

- $A_{min}$ khi $(\varphi_2-\varphi_1)=(2k+1)\pi$ 

$\hspace{3cm}$$A_{min}=|A_1-A_2|$

- Phương trình biên độ dao động tổng hợp 2 dao động  phương vuông góc, cùng tần số (elip)

$\hspace{3cm}$$\frac{x^2}{A_1^2}+\frac{y^2}{A_2^2}-\frac{2xy}{A_1A_2}\cos(\varphi_2-\varphi_1)=\sin^2(\varphi_2-\varphi_1)$ 

# Sóng điện từ

- Vận tốc truyền sóng điện từ trong môi trường đồng chất, đẳng hướng 

$\hspace{3cm}$$v=\frac{c}{\sqrt{\varepsilon.\mu}}$ 

-  Sóng điện từ phẳng đơn sắc 

	- Mật độ năng lượng sóng điện từ

$\hspace{3cm}$$\omega=\frac{1}{2}\varepsilon_0\varepsilon E^2+\frac{1}{2}\mu_0\mu H^2$ 

	- Đối với sóng điện từ phẳng đơn sắc

$\hspace{3cm}$$\sqrt{\varepsilon_0\varepsilon}|\vec E|=\sqrt{\mu_0\mu}|\vec H|$

$\hspace{3cm}$$\to \omega=\varepsilon_0\varepsilon E^2=\mu_0\mu H^2$ 

- Hiệu ứng Doppler là hiện tượng tần số của sóng thay đổi khi nguồn phát chuyển động tương đối với người quan sát

$\hspace{3cm}$$f'=f\frac{v+u'}{v-u}$ 

- Trong đó
	- $f$: tần số nguồn phát

	- $f'$: tần số nguồn thu

	- $v$: vận tốc truyền âm trong môi trường

	- $u$: vận tốc chuyển động của nguồn phát $\begin{cases} u>0: \text{nguồn phát chuyển động gần nguồn thu} \\ u < 0:\text{nguồn phát chuyển động xa nguồn thu} \end{cases}$ 
	
	- $u'$: vận tốc chuyển động của nguồn thu $\begin{cases} u' > 0: \text{nguồn thu chuyển động gần nguồn phát} \\ u' < 0:\text{nguồn thu chuyển động xa nguồn phát} \end{cases}$ 

- Hiệu ứng Doppler trong ánh sáng

$\hspace{3cm}$$f'=f\sqrt{\frac{c-v}{c+v}}$

- Trong đó
	- $f$: tần số nguồn phát
	- $f'$: tần số nguồn thu
	- $v$: vận tốc chuyển động nguồn phát, trong trường hợp này nguồn thu coi như đứng yên $\begin{cases} v>0: \text{nguồn phát chuyển động gần nguồn thu} \\ v < 0:\text{nguồn phát chuyển động xa nguồn thu} \end{cases}$
	- $c$: vận tốc ánh sáng



