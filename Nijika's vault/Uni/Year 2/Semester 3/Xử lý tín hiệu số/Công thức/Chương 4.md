
- Biến đổi Fourier rời rạc với dãy tuần hoàn chu kì $N$ (DFT)

$\hspace{3cm}$$\overset{\sim}{X}(k)=\displaystyle{\sum_{n=0}^{N-1}\overset{\sim}{x}(n).e^{-j\frac{2\pi}{N}kn}}$ 

$\hspace{3cm}$$\omega_k=\frac{2\pi}{N}k$

- Biến đổi ngược IDFT với dãy tuần hoàn chu kì $N$

$\hspace{3cm}$$\overset{\sim}{x}(n)=\frac{1}{N}\displaystyle{\sum_{n=0}^{N-1}\overset{\sim}{X}(k).e^{j\frac{2\pi}{N}kn}}$ 

- Lưu ý $\overset{\sim}{X}(k)$ cũng tuần hoàn với chu kì $N$

- Đặt $W^{kn}_N=e^{-j\omega_kn}=e^{-j\frac{2\pi}{N}kn}$ 

- Biến đổi DFT với dãy có chiều dài hữu hạn $N$ 

$\hspace{3cm}$$X(k)=\begin{cases} \displaystyle{\sum_{n=0}^{N-1}x(n)W^{kn}_n} \space\space 0\leq k\leq N-1 \\ 0 \space\space k\neq\end{cases}$

- Biến đổi IDFT với dãy có chiều dài hữu hạn $N$

$\hspace{3cm}$$x(n)=\begin{cases} \frac{1}{N}\displaystyle{\sum_{n=0}^{N-1}X(k)W^{-kn}_n} \space\space 0\leq n\leq N-1 \\ 0 \space\space n\neq\end{cases}$

- Một số ký hiệu, khái niệm

	- $x(n)_N:$ tín hiệu $x(n)$ có chiều dài hữu hạn $N$

	- $\overset{\sim}{x}(n)_N:$ tín hiệu tuần hoàn có chu kì $N$

	- $x(n)_N\neq x(n)$ 

	- $x_1(n)*x_2(n):$ Phép chập tuyến tính

	- $x_1(n)_N (*)_N x_2(n)_N:$ Phép chập vòng


