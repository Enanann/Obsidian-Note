
### Bài 1

- Bài toán cái túi bằng duyệt toàn bộ

$\hspace{3cm}$$f(X)=10x_1+5x_2+3x_3+6x_4 \to \max$
$\hspace{3cm}$$5x_1+3x_2+2x_3+4x_4\leq 8$ 

- Cho giá trị tối ưu là $FOPT=-\infty$ 

- Tính tất cả các phương phương án $f(x_1,x_2,x_3,x_4)$ thỏa mãn. Ví dụ như $f(0,0,0,0), f(0,0,0,1),..., f(1,1,1,1)$ 

- Trả về kết quả

### Bài 2

- Bài toán cái túi bằng nhánh cận 

$\hspace{3cm}$$f(X)=10x_1+5x_2+3x_3+6x_4 \to \max$
$\hspace{3cm}$$5x_1+3x_2+2x_3+4x_4\leq 8$ 

- Gọi $c_i$ là giá trị sử dụng và $a_i$ là khối lượng 

- **Bước 1:** Sắp xếp lại theo $\frac{c_1}{a_1}\geq \frac{c_2}{a_2}\geq...\geq\frac{c_n}{a_n}$

- **Bước 2 (Lặp):** Lập trên các bộ phận cấp $k=1,...,n$ 

	Giá trị sử dụng của $k$ đồ vật trong túi: $\delta_k=\displaystyle{\sum_{i=1}^k c_ix_i}$

	Trọng lượng còn lại của túi: $b_k=b-\displaystyle{\sum_{i=1}^k a_ix_i}$

	Cận trên của phương án bộ phận cấp $k$: $g(x_1,...x_k)=\delta_k+b_k\frac{c_{k+1}}{a_{k+1}}$ (nếu thỏa mãn)

- **Bước 3 (Trả lại kết quả):** Phương án tối ưu và giá trị tối ưu tìm được 

![[Pasted image 20241019152656.png]]

### Bài 3

- Bài toán người đi du lịch bằng phương pháp nhánh cận

- Ví dụ về ma trận chi phí

| **0**  | **3**  | **14** | **18** | **15** |
| :----: | :----: | :----: | :----: | ------ |
| **3**  | **0**  | **4**  | **22** | **20** |
| **17** | **9**  | **0**  | **16** | **4**  |
| **6**  | **3**  | **7**  | **0**  | **12** |
| **9**  | **15** | **11** | **5**  | **0**  |
$c_{ij}$: Chi phí đi từ thành phố $i\to j$  

- Gọi $c_{min}=\min\{c[i,j],i,j=1,2,...,n\}$ là giá trị nhỏ nhất của ma trận chi phí

- Giả sử đang có hành trình qua $k$ thành phố

$\hspace{3cm}$$T_1\to T_{u_2}\to...\to T_{u_k}$  $(T_1=1)$ 

- Khi đó chi phí là

$\hspace{3cm}$$\delta=c[1,u_2]+c[u_2,u_3]+...+c[u_{k-1},u_k]$ 

- Để hoàn thành chuyến đi, cần qua $n-k$ thành phố nữa rồi quay lại thành phố $1$ $\Rightarrow$ Qua $n-k+1$ đoạn đường nữa

- Vì mỗi đoạn đường đều có chi phí không nhỏ hơn $c_{min}$ $\Rightarrow$ Cận dưới

$\hspace{3cm}$$g(u_1,...u_k)=\delta + (n-k+1)c_{min}$ 

![[Pasted image 20241019164453.png]]