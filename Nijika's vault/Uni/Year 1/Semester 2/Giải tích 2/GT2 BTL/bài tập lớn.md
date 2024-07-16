
Trần Tiến Dũng - 26 
$h=26$
$m=6$
$k=7$
# 1)
### a)

- $f(x,y,z)=26z^3y^2ln(7x)$ 

$f_x= \frac{26z^3y^2}{x} \to f_{xx}=\frac{-26z^3y^2}{x^2}\to f_{xxy}=\frac{-52z^3y}{x^2} \to f_{xxyz}=\frac{-156yz^2}{x^2}\to f_{xxyzz}=\frac{-312yz}{x^2}$ 
### b)

- $f(x,y)=e^{7xy}$ 

$f_{x}=7ye^{7yx}\to f_{xx}=49y^2e^{7yx}\to f_{xxy}=98ye^{7xy}+343xy^2e^{7xy}$ 

# 2)

- $z=e^{2r}\sin(7\varphi)$, $r=st-t^2$, $\varphi=\sqrt{s^2+t^2}$  

- $\frac{\partial z}{\partial r}=2\sin(7\varphi)e^{2r}$ 
- $\frac{\partial z}{\partial \varphi}=7e^{2r}\cos(7\varphi)$
- $\frac{\partial r}{\partial s}=t$; $\frac{\partial r}{\partial t}=s-2t$
- $\frac{\partial \varphi}{\partial s}=\frac{s}{\sqrt{s^2+t^2}}$; $\frac{\partial \varphi}{\partial t}=\frac{t}{\sqrt{s^2+t^2}}$  


$\frac{\partial z}{\partial s}=\frac{\partial z}{\partial r}\frac{\partial r}{\partial s}+\frac{\partial z}{\partial \varphi}\frac{\partial \varphi}{\partial s}$ 
$\frac{\partial z}{\partial s}=2t\sin(7\varphi)e^{2r}+\frac{7s\cos(7\varphi)e^{2r}}{\sqrt{s^2+t^2}}=2t\sin(7\sqrt{s^2+t^2})e^{2(st-t^2)}+\frac{7s\cos(7\sqrt{s^2+t^2})e^{2(st-t^2)}}{\sqrt{s^2+t^2}}$   


$\frac{\partial z}{\partial t}=\frac{\partial z}{\partial r}\frac{\partial r}{\partial t}+\frac{\partial z}{\partial \varphi}\frac{\partial \varphi}{\partial t}$

$\frac{\partial z}{\partial t}=2\sin(7\varphi)e^{2r}(s-2t)+\frac{7e^{2r}\cos(7\varphi)t}{\sqrt{s^2+t^2}}=2\sin(7\sqrt{s^2+t^2})e^{2(st-t^2)}(s-2t)+\frac{7e^{2(st-t^2)}\cos(7\sqrt{s^2+t^2})t}{\sqrt{s^2+t^2}}$ 
# 3)

- $\frac{\partial f}{\partial r}$ , $\frac{\partial f}{\partial \theta}$ , $\frac{\partial f}{\partial \varphi}$  theo $\frac{\partial f}{\partial x}$ , $\frac{\partial f}{\partial y}$ , $\frac{\partial f}{\partial z}$ 

- Đặt $\begin{cases} x=r\sin\theta\cos\varphi \\ y=r\sin\theta\sin\varphi \\ z=r\cos\theta \end{cases}$ 

- Chọn $f(x,y,z)=x^2+y^2+z^2$ 

- Có $\begin{cases} \frac{\partial f}{\partial x}=2x; \frac{\partial f}{\partial y} = 2y; \frac{\partial f}{\partial z} = 2z \\ \\ \frac{\partial x}{\partial r}=\sin\theta\cos\varphi;\frac{\partial y}{\partial r}=\sin\theta\sin\varphi;\frac{\partial z}{\partial r}=\cos\theta \\ \\ \frac{\partial x}{\partial \theta}=r\cos\varphi\cos\theta;\frac{\partial y}{\partial \theta}=r\sin\varphi\cos\theta;\frac{\partial z}{\partial \theta}=-r\sin\theta \\ \\ \frac{\partial x}{\partial \varphi}=-r\sin\theta\sin\varphi;\frac{\partial y}{\partial \varphi}=r\sin\theta\cos\varphi;\frac{\partial z}{\partial \varphi}=0\end{cases}$ 

$\Rightarrow$$\frac{\partial f}{\partial r} = \frac{\partial f}{\partial x} \cdot \frac{\partial x}{\partial r} + \frac{\partial f}{\partial y} \cdot \frac{\partial y}{\partial r} + \frac{\partial f}{\partial z} \cdot \frac{\partial z}{\partial r}=2r$ 

$\Rightarrow$$\frac{\partial f}{\partial \theta} = \frac{\partial f}{\partial x} \cdot \frac{\partial x}{\partial \theta} + \frac{\partial f}{\partial y} \cdot \frac{\partial y}{\partial \theta} + \frac{\partial f}{\partial z} \cdot \frac{\partial z}{\partial \theta}=0$

$\Rightarrow$$\frac{\partial f}{\partial \phi} = \frac{\partial f}{\partial x} \cdot \frac{\partial x}{\partial \phi} + \frac{\partial f}{\partial y} \cdot \frac{\partial y}{\partial \phi} + \frac{\partial f}{\partial z} \cdot \frac{\partial z}{\partial \phi}=0$ 

# 4)

### a)

- Đặt $r=f(x,y)$
- Áp dụng định lý $\cos$ 

$\Rightarrow$$f(x,y)=\sqrt{x^2+y^2-2xy\cos\theta}$

### b)

- Có $\theta=\frac{\pi}{3}, x=30, y=20, v_a=4, v_b=3$  
- Tốc độ thay đổi khoảng cách là $\frac{\partial f}{\partial t}$ 
- Chọn $P$ là gốc tọa độ $\Rightarrow$$\begin{cases} x=30-4t \\ y= 20-3t\end{cases}$

- Có $\frac{\partial f}{\partial x}=\frac{x-y\cos\theta}{\sqrt{x^2+y^2-2xy\cos\theta}};\frac{\partial f}{\partial y}=\frac{y-x\cos\theta}{\sqrt{x^2+y^2-2xy\cos\theta}};\frac{\partial x}{\partial t}=-4;\frac{\partial y}{\partial t}=-3$ 

- $\frac{\partial f}{\partial t}=\frac{\partial f}{\partial x}\frac{\partial x}{\partial t}+\frac{\partial f}{\partial y}\frac{\partial y}{\partial t}=-4\frac{x-y\cos\theta}{\sqrt{x^2+y^2-2xy\cos\theta}}-3\frac{y-x\cos\theta}{\sqrt{x^2+y^2-2xy\cos\theta}}$ 

$\Rightarrow$$\frac{\partial f}{\partial t}=-\frac{19\sqrt{7}}{14}$ 

# 5)

### a)

- $\frac{\partial f}{\partial \vec u}(2,0)$ , $f(x,y)=xe^{xy}+7y$ , $\theta=\frac{2\pi}{3}$ 

- Có $(\vec u, \vec {Ox})=\frac{2\pi}{3}$ $\Rightarrow$ $(\vec u, \vec {Oy})=\frac{\pi}{6}$
 $\frac{\partial f}{\partial \vec u}(2,0)=(f'_x \cos \frac{2\pi}{3}+f'_y\cos\frac{\pi}{6})(2,0)=[(e^{xy}+xy e^{xy})\cos\frac{2\pi}{3}+(x^2 e^{xy}+7)\cos\frac{\pi}{6}](2,0)=\frac{-1+11\sqrt {3}}{2}$   

### b)

- $\frac{\partial f}{\partial \vec v}(x,y, z)$ , $f(x,y,z)=x^2z+y^3z^2-7xyz$ , $\vec v =(-1,0,3)$ 

- $\vec v_0=\frac{\vec v}{||\vec v||}=(\frac{-1}{\sqrt {10}},0,\frac{3}{\sqrt{10}})$

- $f'_x=2zx-7yz$
- $f'_y=3z^2y^2-7xz$
- $f'_z=x^2+2y^3z-7xy$

$\frac{\partial f}{\partial \vec v}(x,y, z)=f'_x.\frac{-1}{\sqrt{10}} + f'_y.0 + f'_z.\frac{3}{\sqrt{10}}=\frac{-2zx+7yz}{\sqrt{10}}+\frac{3x^2+6y^3z-21xy}{\sqrt{10}}$

# 6)

- $I=\frac{W}{H^2}$ 

- Có $\Delta I=\frac{\partial I}{\partial W}+\frac{\partial I}{\partial H}=\frac{1}{H^2}\Delta W-2W\frac{1}{H^3}\Delta H$     

- Theo đề bài $(W,H)=(17,1.05)\to(18.5,1.07)$ 

$\Rightarrow$$\Delta W=1,5(kg)$; $\Delta H=0,02 (m)$

$\Rightarrow$ $\Delta I \approx 1,36-0,587 \approx 0,773$ 
# 7)

### a)

- $f(x,y)=3x^2y+y^3-3x^2-3y^2+26$ 

- Có $f'_x=6xy-6x$; $f'_y=3x^2+3y^2-6y$ 

- $\begin{cases} f'_x=0 \\ f'_y=0 \end{cases}$ $\Rightarrow$ Các điểm dừng là $(0,0);(0,2);(1,1);(-1,1)$ 

- Có $A=\frac{\partial ^2f}{\partial x^2}=6y-6$; $B=\frac{\partial ^2 f}{\partial x \partial y}=6x$, $C = \frac{\partial ^2 f}{\partial y^2}=6y-6$ 

- Xét $(0,0)$: $\Delta=B^2-AC=-36<0$ ; $A=-6<0$ $\Rightarrow$ Cực đại 

- Xét $(0,2)$ $\Delta=B^2-AC=-36<0$ ; $A=6>0$ $\Rightarrow$ Cực tiểu

- Xét $(1,1)$ $\Delta=B^2-AC=36>0$ $\Rightarrow$ Không đạt cực trị

- Xét $(-1,1)$ $\Delta=B^2-AC=36>0$ $\Rightarrow$ Không đạt cực trị 

### b)

- $f(x,y)=x^3+y^4-6x-2y^2+7$ 

- Có $f'_x=3x^2-6$; $f'_y=4y^3-4y$

- $\begin{cases} f'_x=0 \\ f'_y=0 \end{cases}$ $\Rightarrow$ Các điểm dừng là $(\sqrt {2},1);(\sqrt {2},-1);(\sqrt {2},0);(-\sqrt {2},1),(-\sqrt {2},-1),(-\sqrt {2},0)$ 

- Có $A=6x$; $B=0$; $C=12y^2-4$ 

- Xét $(\sqrt {2},1)$: $\Delta=-48\sqrt{2} < 0$; $A=6\sqrt{2}>0$  $\Rightarrow$ Cực tiểu

- Xét $(\sqrt {2},-1)$: $\Delta=-48\sqrt{2} < 0$; $A=6\sqrt{2}>0$  $\Rightarrow$ Cực tiểu

- Xét $(\sqrt {2},0)$: $\Delta=24\sqrt{2}>0$ $\Rightarrow$ Không đạt cực trị

- Xét $(-\sqrt {2},1)$: $\Delta=48\sqrt{2}>0$ $\Rightarrow$ Không đạt cực trị

- Xét $(-\sqrt {2},-1)$: $\Delta=48\sqrt{2}>0$ $\Rightarrow$ Không đạt cực trị

- Xét $(-\sqrt {2},0)$: $\Delta=-24\sqrt{2} < 0$; $A=-6\sqrt {2} < 0$  $\Rightarrow$ Cực đại






# 8)

### a)

- $f(x,y)=x^3+x^2y+2y^2+26$ ; $x,y \geq 0, x+y \leq 1$ 

- $f'_x=3x^2+2yx$; $f'_y=x^2+4y$ 

- $\begin{cases} f'_x=0 \\ f'_y=0 \end{cases}$ $\Rightarrow$ Các điểm dừng là $(0,0)$ 

- Có $f(0,0)=26$

- Có miền $D$ là tam giác $OAB$ với $O(0,0);A(1,0); B(0,1)$

- Xét trên $OA:y=0$ $\Rightarrow$ $f=x^3+26$ $\Rightarrow$ $Min f_{[0,1]}=26, Max f_{[0,1]}=27$ 

- Xét trên $OB:x=0$ $\Rightarrow$ $f=2y^2+26$ $\Rightarrow$ không xác định trên $[0,1]$ 

- Xét trên $AB:x+y=1$ $\Rightarrow$ $f=3x^2-4x+28$ 
  $\Rightarrow$ $Min f_{[0,1]}=\frac{80}{3}, Max f_{[0,1]}=28$ 

$\Rightarrow$ $Min f =26, Max f=28$ 

### b)

- $f(x,y)=(4y^2-x^2)e^{-x^2-y^2}+7$; $x^2+y^2\leq 2$ 

- $f'_x=2xe^{-x^2-y^2}(x^2-4y^2-1)$;$f'_y=2ye^{-x^2-y^2}(x^2-4y+4)$ 

- $\begin{cases} f'_x=0 \\ f'_y=0 \end{cases}$ $\Rightarrow$ Các điểm dừng là $(0,0);(0,1);(0,-1)$ 

- Có $f(0,0)=7;f(0,1)=4e^{-1}+7;f(0,-1)=4e^{-1}+7$

- Có miền $D$ là $x\in[-\sqrt{2},\sqrt{2}], y\in[-\sqrt{2},\sqrt{2}]$ 

- Từ $x^2+y^2=2$ $\Rightarrow$ $f=e^2(8-5x^2)$ $\Rightarrow$ $f'=0 \Leftrightarrow x=0$ 

- Có $f(0)=8e^2, f(\sqrt{2})=-2e^2, f(-\sqrt{2})=-2e^2$ 

$\Rightarrow$ $Min f=-2e^2, Maxf=8e^2$


# 9)

- $f(x,y,z)=4y-2z$  với điều kiện: $2x-y-z=2$, $x^2+y^2=1$ 

- Xét hàm Lagrange

$L(x,y,z,\lambda_1,\lambda_2)=4y-2z+\lambda_1(2x-y-z-2)+\lambda_2(x^2+y^2-1)$ 

- Có
	- $L'_x=2\lambda_1+2\lambda_2 x$ 

	- $L'_y=4-\lambda_1+2\lambda_2 y$

	- $L'_z=-2-\lambda_1$

	- $L'_{\lambda_1}=2x-y-z-2$

	- $L'_{\lambda_2}=x^2+y^2-1$

- Từ trên cho các đạo hàm riêng $=0$ tìm được điểm dừng $(\frac{2}{\sqrt{5}},\frac{-1}{\sqrt{5}},-2+\sqrt{5}),(\frac{-2}{\sqrt{5}},\frac{1}{\sqrt{5}},-2-\sqrt{5})$  

- $f(\frac{2}{\sqrt{5}},\frac{-1}{\sqrt{5}},-2+\sqrt{5})=\frac{20-14\sqrt{5}}{5}$  
- $f(\frac{-2}{\sqrt{5}},\frac{1}{\sqrt{5}},-2-\sqrt{5})=\frac{20+14\sqrt{5}}{5}$ 

$\Rightarrow$ $Min f=\frac{20-14\sqrt{5}}{5}, Max f=\frac{20+14\sqrt{5}}{5}$ 
# 10)

### a)

- $\displaystyle{\int_0^3\int_{x^2}^9 26x^3e^{y^3}}dydx$ 

- Có $0\leq x \leq 3$, $x^2 \leq y\leq 9$ 

- Đổi cận ta có $0\leq y\leq 9$, $0\leq x\leq \sqrt y$ 

$\Rightarrow$ $I=\displaystyle{\int_0^9\int_0^{\sqrt{y}} 26x^3e^{y^3}dxdy=\int_0^9 \frac{26e^{y^3}y^2}{4}dy}=\frac{13}{6}(e^{729}-1)$     

### b)

- $\displaystyle{\int_0^8\int_{\sqrt[3]{y}}^2 \sqrt{x^4+1}dxdy}$ 

- Có $0\leq y\leq 8$, $\sqrt[3]{y}\leq x\leq 2$ 

- Đổi cận ta có $0\leq x\leq 2$, $0\leq y\leq x^3$ 

$\Rightarrow$ $I=\displaystyle{\int_0^2\int_0^{x^3} \sqrt{x^4+1}dydx=\int_0^2 \sqrt{x^4+1}.x^3dx}=\frac{17\sqrt{17}-1}{6}$


# 11)

- $\displaystyle{\iiint_S}dxdydz$ ; $S=\{x^2+y^2+z^2=9, z\geq 0, x^2+y^2\leq 5\}$ 

- Đặt $\begin{cases} x=r\sin\theta\cos\varphi \\ y=r\sin\theta\sin\varphi \\ z=r\cos\theta \end{cases}$ 

- Có $J=r^2\sin\theta$ 

- Theo miền $S$, có $0\leq r\leq 3, 0\leq \varphi\leq 2\pi, 0\leq \theta \leq \frac{\pi}{2}$ 

$\Rightarrow$ $V_{\text{mặt cầu}}=\displaystyle{\int_0^{2\pi} \int_0^{\frac{\pi}{2}}  \int_0^3 r^2\sin\theta}drd\theta d\varphi=\displaystyle{\int_0^{2\pi} \int_0^{\frac{\pi}{2}}}\frac{\sin\theta}{9}d\theta d\varphi=\frac{2\pi}{9}$    

![[btl.png]]

- Có $V_2=\displaystyle{\int_0^{2\pi} \int_0^{\frac{\pi}{2}}  \int_0^{\sqrt {5}}r^2\sin\theta}drd\theta d\varphi=\frac{10\sqrt{5}\pi}{3}$ 

- Có $V_1=h_1.S_{\text{đáy trụ}}=2.\pi.5=10\pi$
- Trong đó $h_1=|z|$, trong hệ phương trình $\begin{cases} x=\pm\sqrt{5} \\ x^2+z^2=9 \end{cases}$    (Chiếu lên $Oxz$) $\Rightarrow$ $h_1=2$ 

- Có $V_{\text{trụ}}=h.S_{\text{đáy trụ}}=3.\pi.5=15\pi$ 

$\Rightarrow$ $V_{\text{cần tìm}}=\frac{2\pi}{9}-15\pi+10\pi+\frac{10\sqrt{5}\pi}{3}=\frac{-43+30\sqrt{5}}{9}\pi$  

# 12)

- $\displaystyle{\iiint_V}\sqrt{x^2+y^2+z^2}dxdydz$ . $V=\{z=\sqrt{x^2+y^2}, z=7\}$ 

- Đặt $\begin{cases} x=r\sin\theta\cos\varphi \\ y=r\sin\theta\sin\varphi \\ z=r\cos\theta \end{cases}$ 

- $J=r^2\sin\theta$ 

- Theo $V$ có $0\leq r\leq 7, 0\leq \theta\leq \frac{\pi}{4}, 0\leq \varphi \leq 2\pi$ 

$\Rightarrow$ $I=\displaystyle{\int_0^{2\pi} \int_0^{\frac{\pi}{4}}  \int_0^7 r^3\sin\theta}drd\theta d\varphi=2\pi.(1-\frac{\sqrt{2}}{2}).\frac{2401}{4}$  


# 13)

- $\displaystyle{\iiint_W 26ydxdydz}$ 

- $W=\{\frac{x^2}{4}+\frac{y^2}{9}=1;x^2+y^2+z^2=16;x,y,z\geq 0\}$

![[btl2.png]]


- Có $0\leq x \leq 2, 0\leq y\leq 3, 0\leq z\leq \sqrt{16-x^2-y^2}$ 

$W=\displaystyle{\int_0^2 \int_0^3  \int_0^{\sqrt{16-x^2-y^2}}26ydzdydx=26\int_0^2 \int_0^3 y\sqrt{16-x^2-y^2}dydx=26\int_0^2 \frac{-1}{2}[\frac{(7-x^2)^2}{2}-\frac{(16-x^2)^2}{2}]dx}$ 
$\Rightarrow$ $W=2379$

# 14)

### a)

- $\displaystyle{\int_0^{2\pi} \int_0^{\frac{\pi}{2}} \int_4^9 r^2\sin\varphi drd\varphi d\theta=\int_0^{2\pi} \int_0^{\frac{\pi}{2}}\frac{665}{3}\sin\varphi d\varphi d\theta =\int_0^{2\pi}\frac{665}{3} d\theta=\frac{1330\pi}{3}}$ 

$\Rightarrow$ Miền $D=\{4\leq r\leq 9, 0\leq \varphi\leq \frac{\pi}{2},0\leq \theta \leq 2\pi\}$

![[Pasted image 20240518082436.png]]

### b)

- $\displaystyle{\int_{-2}^1 \int_{\frac{\pi}{3}}^{\frac{\pi}{4}} \int_0^2 r drd\varphi dz=\int_{-2}^1 \int_{\frac{\pi}{3}}^{\frac{\pi}{4}}2 d\varphi dz =\int_{-2}^1 \frac{-\pi}{6}dz=\frac{-\pi}{2}}$

$\Rightarrow$$D=\{0\leq r\leq 2, \frac{\pi}{4}\leq \varphi \leq \frac{\pi}{3}, -2\leq z\leq 1\}$ 

![[Pasted image 20240518083244.png]]

### c)

- $\displaystyle{\int_0^{2\pi} \int_0^3 \int_{-\sqrt{9-r^2}}^0 r d\varphi dz dr=\int_0^{2\pi} \int_0^3 r\sqrt{9-r^2} dz dr =\int_0^{2\pi}3r\sqrt{9-r^2} dr=-(9-4\pi^2)^{\frac{3}{2}}+27}$

- Có $D=\{-\sqrt{9-r^2}\leq \varphi\leq 0, 0\leq z\leq 3, 0\leq r\leq 2\pi\}$

- Có $\varphi^2+r^2=9, 0\leq r\leq 2\pi$ $\Rightarrow$ $-3\leq \varphi \leq 0$ 

![[Pasted image 20240518084807.png]]


# 15)

- $\displaystyle{\int_{-2}^2 \int_{-\sqrt{4-x^2}}^{\sqrt{4-x^2}} \int_0^{\sqrt{4-x^2-y^2}} e^{-7(x^2+y^2+z^2)^{\frac{3}{2}}}dxdydz}$  

- Có $-2\leq x\leq 2, -\sqrt{4-x^2}\leq y \leq \sqrt{4-x^2}, 0\leq z\leq \sqrt{4-x^2-y^2}$ 

- Đặt $\begin{cases} x=r\sin\theta\cos\varphi \\ y=r\sin\theta\sin\varphi \\ z=r\cos\theta \end{cases}$ 

- $J=r^2\sin\theta$

![[Pasted image 20240518092032.png]]

$\Rightarrow$ Đổi sang hệ tọa độ cầu ta có $0\leq \varphi\leq 2\pi, 0\leq \theta\leq \frac{\pi}{2}, 0\leq r\leq 2$ 

$\Rightarrow$ $\displaystyle{\int_0^2 \int_0^{2\pi} \int_0^{\frac{\pi}{2}} e^{-7(r^2)^{\frac{3}{2}}}.r^2\sin\theta drd\varphi d\theta=\int_0^2 e^{-7r^3}.r^2 dr \int_0^{2\pi} d\varphi \int_0^{\frac{\pi}{2}}\sin\theta d\theta}=\frac{-1}{21}(e^{-56}-1).2\pi$    

# 16)

- $\displaystyle{\int_{C}(x+y+26z)ds}$ 

- $C:c(t)=(\cos(t),\sin(t),t)$, $0\leq t\leq \pi$ 

$\Rightarrow$ $C:\begin{cases} x=\cos t \\ y=\sin t\\ z= t\end{cases}$ 

$\Rightarrow$ $\displaystyle{\int_{C}(x+y+26z)ds=\int_0^{\pi}(\cos t+\sin t+26t)\sqrt{(-\sin t)^2+(\cos t)^2+1^2}dt}=\sqrt{2}(2+13\pi^2)$ 
# 17)

- $\vec F=(\frac{2xy}{z},z+\frac{x^2}{z},y-\frac{x^2y}{z^2})$ 

- Có $rot \vec F=(\frac{\partial R}{\partial y}-\frac{\partial Q}{\partial z}, \frac{\partial P}{\partial z}-\frac{\partial R}{\partial x}, \frac{\partial Q}{\partial x}-\frac{\partial P}{\partial y})$

- Có
	- $P=\frac{2xy}{z}$ $\Rightarrow$ $P'_y=\frac{2x}{z}$, $P'_z=-\frac{2xy}{z^2}$
	- $Q=z+\frac{x^2}{z}$ $\Rightarrow$ $Q'_x=\frac{2x}{z}$, $Q'_z=1-\frac{x^2}{z^2}$ 
	- $R=y-\frac{x^2y}{z^2}$ $\Rightarrow$ $R'_x=-\frac{2xy}{z^2}$, $R'_y=1-\frac{x^2}{z^2}$  

$\Rightarrow$ $rot \vec F=(0,0,0)$ $\Rightarrow$ $\vec F$ là trường thế 

$\Rightarrow$ Tồn tại $\varphi(x,y,z)$ thỏa mãn $\begin{cases} \frac{\partial \varphi}{\partial x}= \frac{2xy}{z}\\ \frac{\partial \varphi}{\partial y}= z+\frac{x^2}{z}\\ \frac{\partial \varphi}{\partial z}= y-\frac{x^2y}{z^2} \end{cases}$ 

- $\frac{\partial \varphi}{\partial x}=\varphi'_x= \frac{2xy}{z}$ $\Rightarrow$ $\varphi=\frac{y}{z} x^2 + f(y,z)$    $(*)$

$\Rightarrow$ $\varphi'_y=\frac{x^2}{z}+f'_y(y,z)=z+\frac{x^2}{z}$ $\Rightarrow$ $f'_y(y,z)=z$ $\Rightarrow$ $f(y,z)=zy+g(z)$ 

- $(*)\Rightarrow$ $\varphi'_z=-\frac{x^2y}{z^2}+f'_z(y,z)=y-\frac{x^2y}{z^2}$ 
  
  $\Rightarrow$ $y+g'(z)=y$ $\Rightarrow$ $g'(z)=0$ $\Rightarrow$ $g(z)=C$  

$\Rightarrow$ $f(y,z)=zy+C$ 

$\Rightarrow$ $\varphi=\frac{y}{z}x^2+zy+C$ 

# 18)

### a)

- $\vec F=(xy^2,x^2y)$, $\varphi(x,y)=\frac{1}{2}x^2y^2$
- $\displaystyle{\int_c \vec F}$, $c$: upper half of the unit circle centered at the origin oriented counterclockwise  

- $\nabla \varphi=(\varphi'_x, \varphi'_y)=(xy^2,x^2y)=\vec F$ 

- Có đường đi là $AB$
![[Pasted image 20240518161117.png]]

- $\displaystyle{\int_{AB} \vec F=\int_{AB}xy^2dx+x^2ydy}$ 

- Đặt $\begin{cases} x=\cos t \\ y=\sin t \end{cases}$, $t\in [0,\pi]$ $\Rightarrow$ $\begin{cases} dx=-\sin t dt\\ dy=\cos t dt\end{cases}$

$\Rightarrow$ $\displaystyle{\int_{AB} \vec F=\int_0^{\pi} [\cos t\sin^2(-\sin t) + \cos^2t \sin t \cos t ]dt}=0$  




### b)

- $\vec F=(\frac{z}{x-y},\frac{z}{y-x},\ln(x-y))$, $\varphi(x,y,z)=z\ln(x-y)$ 

- Ellipse $C: 2x^2+3(y-4)^2=12$ in the clockwise direction

- $\nabla \varphi=(\varphi'_x,\varphi'_y,\varphi'_z)=(\frac{z}{x-y}, \frac{z}{y-x},\ln(x-y))=\vec F$ 

- $C:2x^2+3(y-4)^2=12$ $\Rightarrow$ $\frac{x^2}{6}+\frac{(y-4)^2}{4}=1$ 

- Đặt $\begin{cases} x=\sqrt 6 \cos t \\ y=4+2\sin t \end{cases}$ , $0\leq t \leq 2\pi$  $\Rightarrow$ $\begin{cases} dx=-\sqrt{6}\sin t \\ dy=2\cos t \end{cases}$

- $\displaystyle{\int_C \vec F=\int_C \frac{z}{x-y}dx+\frac{z}{y-x}dy+\ln(x-y)dz}$  

# 19)

- $\displaystyle{\iint_S (z-x)dS}$

- $S: z=x+y^2; 0\leq x\leq y\leq 1$ 

$\Rightarrow$ $dS=\sqrt{1+z'^2_x+z'^2_y}dxdy=\sqrt{2+4y^2}dxdy$

![[Pasted image 20240518214402.png]]

$\Rightarrow$ $\displaystyle{\iint_S (z-x)dS=\iint_D (x+y^2-x)\sqrt{2+4y^2}dxdy}$ 

- Trong đó $D$ là tam giác $OAB$, $O(0,0,0)$, $A(1,1,0)$, $B(0,1,0)$ 

$\Rightarrow$ $0\leq y\leq 1, 0\leq x\leq y$  

$\Rightarrow$ $\displaystyle{\int_0^1 \int_0^y (x+y^2-x)\sqrt{2+4y^2}dxdy=\int_0^1 \sqrt{2+4y^2}.y^3dy}=\frac{6\sqrt {6}+\sqrt{2}}{30}$ 
# 20)

### a)

- $\vec F(x,y,z)=(y,x^2y,e^{xz})$, $x^2+y^2=9, -3\leq z\leq 3$, outward-pointing normal

- $\vec n=(2x,2y,0)$ $\Rightarrow$ $\vec n_0 =\frac{\vec n}{||\vec n||}=(\frac{x}{2x^2+2y^2},\frac{y}{2x^2+2y^2},0)$ 

$\Rightarrow$ $I = \displaystyle{\iint_S (P\cos\alpha+Q\cos\beta+R\cos\gamma})ds=\iint_S \frac{x^2y^2+xy}{2x^2+2y^2}ds$

- Có $y=\sqrt{9-x^2}$, $-3\leq z\leq 3$ $\Rightarrow$ $I=\displaystyle{\iint_D \frac{x^2y^2+xy}{2x^2+2y^2}ds}$   Với $D$ là hình chiếu của $S$ trên $Oxz$ $\Rightarrow$ $-3\leq z\leq 3, -3\leq x\leq 3$

- $ds=\sqrt{1+y'^2_x+y'^2_z}dxdz=\sqrt{1+\frac{x^2}{9-x^2}}$  

- $I=\displaystyle{\int_{-3}^3 \int_{-3}^3} \frac{-x^4+9x^2+x\sqrt{9-x^2}}{18}dxdz=\frac{108}{5}$  


### b)

- $\vec F(x,y,z)=(0,0,xze^{xy})$, $z=xy, 0\leq x,y\leq 1$, upward-pointing normal

- $xy-z=0$ $\Rightarrow$ $\vec n=\pm(y,x,-1)$ $\Rightarrow$ $\vec n_0=\pm(\frac{y}{\sqrt{x^2+y^2+1}},\frac{x}{\sqrt{x^2+y^2+1}},\frac{-1}{\sqrt{x^2+y^2+1}})$

- $I=\displaystyle{\iint_S xze^{xy}dxdy}$  

- Véc tơ mặt trên $\Rightarrow$ $I=\displaystyle{\iint_{D_{xy}} xze^{xy}dxdy}$ 

- $D_{xy}=\{0\leq x\leq 1, 0\leq y\leq 1\}$ 

- $\Rightarrow$ $I=\displaystyle{\int_0^1 \int_0^1 xxye^{xy}dxdy=\int_0^1 [y^2e^y-2e^y(y-1)-2]dy=3e-8}$ 

### c)

- $\vec F(x,y,z)=(x^2-z^2,e^{z^2}-\cos x, y^3)$, $x+2y+4z=12$, and the coordinate planes in the first octant, outward-pointing normal

- the coordinate planes in the first octant $\Rightarrow$ $x\geq 0, y\geq 0, z\geq 0$ 

- $x+2y+4z-12=0$ $\Rightarrow$  $\vec n=(1,2,4)$ $\Rightarrow$ $\vec n_0=(\frac{1}{\sqrt{21}},\frac{2}{\sqrt{21}},\frac{4}{\sqrt{21}})$ 

- $\Rightarrow$ $I=\displaystyle{\iint_D (x^2-z^2)dydz+(e^{z^2}-\cos x)dzdx+(y^3)dxdy}$ 

$I=\displaystyle{\iint_{D_{yz}}(x^2-z^2)dydz+\iint_{D_{xz}}(e^{z^2}-\cos x)dzdx+\iint_{D_{xy}}y^3dxdy}$ 

$I=\displaystyle{\int_0^3 \int_0^6 ((12-2y-4z)^2-z^2) dydz +\int_0^{12} \int_0^3 (e^{z^2}-\cos x)dzdx + \int_0^6 \int_0^{12} y^3 dxdy}$ 
$I=432+\displaystyle{\int_0^{12} \int_0^3 e^{z^2}dzdx}-3\sin 12+3888$

$I=\displaystyle{\int_0^{12} \int_0^3 e^{z^2}dzdx}-3\sin 12+4320$   
