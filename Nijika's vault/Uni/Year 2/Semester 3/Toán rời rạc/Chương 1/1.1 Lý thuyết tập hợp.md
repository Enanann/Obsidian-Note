
# Một số kí hiệu

- Tập hợp

$\hspace{3cm}$$A, B, ..., X, Y,...$

- Phần tử của tập hợp

$\hspace{3cm}$$a, b,..., x, y,...$

- Phần tử $x$ thuộc (không thuộc) $A$

$\hspace{3cm}$$x \in A \space (x\notin A)$

- Số phần tử của tập hợp $A$

$\hspace{3cm}$$|A|$

- Tập hợp con

$\hspace{3cm}$$A \subseteq B$:   $x\in A \Rightarrow x\in B$ 

- Tập hợp bằng nhau

$\hspace{3cm}$$A \subseteq B \space \text{và} \space B \subseteq A \Rightarrow A=B$

- Tập rỗng

$\hspace{3cm}$$\emptyset$ 

	- Không có phần tử nào
	- Là con của mọi tập

# Các phép toán trên tập hợp

- Phần bù của $A$ trong $X$

$\hspace{3cm}$$\bar A=\{x\in X | x\notin A\}$ 

- Hợp hai tập hợp

$\hspace{3cm}$$A\cup B = \{x|x\in A \space \text{hoặc} \space x\in B\}$

- Giao hai tập hợp

$\hspace{3cm}$$A\cap B = \{x| x\in A \space \text{và} \text x\in B\}$

- Hiệu hai tập hợp

$\hspace{3cm}$$A\setminus B=\{x|x\in A \space \text{và} \space x\notin B\}$    

- Luật kết hợp

$\hspace{3cm}$$(A\cup B) \cup C =A\cup (B\cup C)$ 

$\hspace{3cm}$$(A\cap B) \cap C=A\cap (B\cap C)$

- Luật giao hoán

$\hspace{3cm}$$A\cup B = B\cup A$
$\hspace{3cm}$$A\cap B=B\cap A$

- Luật phân phối

$\hspace{3cm}$$A\cup(B\cap C)=(A\cup B)\cap (A\cup C)$
$\hspace{3cm}$$A\cap(B\cup C)=(A\cap B)\cup(A\cap C)$

- Luật đối ngẫu

$\hspace{3cm}$$\overline{A\cup B}=\bar A \cap \bar B$
$\hspace{3cm}$$\overline{A\cap B}=\bar A \cup \bar B$

- Tích đề các 

$\hspace{3cm}$$A \times B = {(a, b)| a\in A, b\in B}$

# Quan hệ tương đương và phân hạch

>[!text]
>Một quan hệ hai ngôi $R$ trên tập $X$, ký hiệu $R(X)$, là một tập con của tích Đề các $X\times X$
>
>Kí hiệu: Nếu $(a,b) \in X\times X$ và $a,b$ có quan hệ hai ngôi $R$ với nhau trên $X$ thì được kí hiệu là $aRb$ 

- Tính chất

	- $R$ được gọi là có tính chất phản xạ nếu $\forall a\in X, aRa$ 

	- $R$ được gọi là có tính chất đối xứng nếu $aRb$ thì $bRa$

	- $R$ được gọi là có tính chất phản đối xứng nếu $aRb$ và $bRa$ thì $a=b$

	- $R$ được gọi là có tính chất kéo theo (bắc cầu) nếu $aRb$ và $bRc$ thì $aRc$ 
 
- Ví dụ
>Cho $X = \{1, 2, 3, 4\}$
>$a, b ∈ X$, $a$ có quan hệ $R$ với $b$ nếu $a$ chia hết cho $b$
>
>$\Rightarrow$ $R(X) = \{(1, 1),(2, 1),(2, 2),(3, 1),(3, 3),(4, 1),(4, 2),(4, 4)\}$ 
>
>$\Rightarrow$ Phản xạ, kéo theo, phản đối xứng nhưng không đối xứng.

- Quan hệ tương đương và phân hoạch

	- **Quan hệ tương đương**: là quan hệ có đủ ba tính chất phản xạ, đối xứng và kéo theo

	- **Lớp tương đương**: một quan hệ tương đương trên tập hợp sẽ chia tập hợp thành các lớp tương đương
		- Hai phần tử thuộc cùng một lớp có quan hệ với nhau
		- Hai phần tử khác lớp không có quan hệ với nhau
		- Các lớp tương đương phủ kín tập hợp ban đầu

	- **Phân hoạch**: là một họ các lớp tương đương (tập con khác rỗng) của một tập hợp

>[!text]
>Một quan hệ tương đương trên tập hợp sẽ xác định một phân hoạch trên tập hợp, ngược lại một phân hoạch bất kỳ trên tập hợp sẽ tương ứng với một quan hệ tương đương trên nó

