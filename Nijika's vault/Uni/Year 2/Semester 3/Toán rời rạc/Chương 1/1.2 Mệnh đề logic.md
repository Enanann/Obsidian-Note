
# Định nghĩa

>[!text]
>**Mệnh đề** là một câu khẳng định, có thể xác định được giá trị hoặc đúng hoặc sai

- Ví dụ
>"Hà Nội là thủ đô của Việt Nam" là mệnh đề đúng
>
>"5<3" là mệnh đề sai
>
>"a<7" không phải là mệnh đề vì nó không biết khi nào đúng khi nào sai

- Giá trị chân lý của mệnh đề
	- Giá trị đúng: ký hiệu $T$
	- Giá trị sai: ký hiệu $F$
	
	- Tập $\{T, F\}$ được gọi là giá trị chân lý của mệnh đề

- Ký hiệu

	- Mỗi mệnh đề được ký hiệu bằng các chữ cái in thường $(a,b,q,r,t,...)$ 
	- Mỗi mệnh đề còn được gọi là công thức
	- Từ các khái niệm, xây dựng được các mệnh đề phức hợp (công thức) thông qua các phép toán trên mệnh đề

# Các phép toán của mệnh đề logic

- [[1.2 Các phép liên kết logic mệnh đề|Phép phủ định, phép hội, phép tuyển, phép tương đương, phép kéo theo]] 

- Phép tuyển loại: đúng khi hoặc $p$ hoặc $q$ có giá trị đúng và sai trong các trường hợp khác còn lại

$\hspace{3cm}$$p\oplus q$: đọc là "hoặc $p$ hoặc $q$"

- **Thỏa được**: một mệnh đề là **thỏa được** nếu nó *đúng với một bộ giá trị chân lý* nào đó của các mệnh đề thành phần

- **Không thỏa được**: một mệnh đề là **không thỏa được** nếu nó *sai với mọi bộ giá trị chân lý* của các mệnh đề thành phần

- **Vững chắc**: Một mệnh đề là vững chắc nếu nó *đúng với mọi bộ giá trị chân lý* của các mệnh đề thành phần

# Mệnh đề logic cơ bản

- Hai mệnh đề $a,b$ được gọi là **tương đương** nếu chúng có cùng giá trị chân lý với mọi bộ giá trị chân lý của các mệnh đề thành phần 
	- Ký hiệu: $a\equiv b$ 

- Một số mệnh đề tương đương cơ bản
>[!text]
>1. $a\vee F \equiv a$
>$\space$   
>2. $a\wedge F \equiv F$
>$\space$
>3. $a\vee T \equiv T$
>$\space$
>4. $a\wedge T \equiv a$
>$\space$
>5. $a\Rightarrow b \equiv \neg a \vee b$ 
$\space$
>6. $a\Leftrightarrow b \equiv (a\Rightarrow b)\wedge (b\Rightarrow a)$
$\space$
>7. $\neg(\neg a) \equiv a$

- Luật giao hoán

$\hspace{3cm}$$a\vee b \equiv b\vee a$

$\hspace{3cm}$$a\wedge b \equiv b \wedge a$

- Luật kết hợp

$\hspace{3cm}$$(a\vee b)\vee c \equiv a\vee (b\vee c)$

$\hspace{3cm}$$(a\wedge b)\wedge c \equiv a\wedge (b\wedge c)$

- Luật phân phối

$\hspace{3cm}$$a\wedge (b\vee c) \equiv (a\wedge b)\vee (a\wedge c)$

$\hspace{3cm}$$a\vee (b\wedge c) \equiv (a\vee b)\wedge (a\vee c)$

- Luật De Morgan

$\hspace{3cm}$$\neg(a\wedge b) \equiv \neg a \vee \neg b$

$\hspace{3cm}$$\neg(a\vee b) \equiv \neg a \wedge \neg b$

# Dạng chuẩn tắc hội

- Mệnh đều (câu) tuyển
>[!text]
>Là tuyển của các mệnh đề nguyên thủy
>
>$\Rightarrow$ $p_1\vee p_2\vee...\vee p_n$
>
>Trong đó $p_i$ là các mệnh đề nguyên thủy

- Dạng chuẩn tắc hội là hội của các câu tuyển

$\hspace{3cm}$$(a\vee e \vee f \vee g)\wedge (x\vee y\vee z)$

- Có thể biến đổi một công thức bất kì về dạng chuẩn tắc hội bằng cách sau đây

>Khử các phép tương đương
>
>Khử các phép kéo theo
>
>Chuyển các phép phủ định vào sát các ký hiệu mệnh đề bằng De Morgan
>
>Khử phủ định kép
>
>Áp dụng luật phân phối

