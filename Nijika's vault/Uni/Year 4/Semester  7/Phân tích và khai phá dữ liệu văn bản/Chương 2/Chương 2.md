# Tách từ (Tokenization)

- **Khái niệm**: Tách từ là quá trình chia một chuỗi văn bản thành các đơn vị nhỏ hơn có ý nghĩa, gọi là "token"
- Token thường là từ, nhưng cũng có thể là số, dấu câu, hoặc các đơn vị có ý nghĩa khác tùy thuộc vào mục đích 

- **Tầm quan trọng**: Là bước đầu tiên và cơ bản nhất trong hầu hết các tác vụ xử lý ngôn ngữ tự nhiên. Nếu tách từ không chính xác thì các bước xử lý sau bị ảnh hưởng 

### Các phương pháp tách từ 

- **Tách theo khoảng trắng**: Đơn giản nhất, chia chuỗi theo dấu cách 
	- Ưu điểm: Dễ thực hiện
	- Nhược điểm: Không sử lý được dấu câu dính liên từ, từ ghép, hoặc các ngôn ngữ không có khoảng trắng rõ ràng (e.g. Tiếng Trung, Tiếng Nhật)

- **Tách theo dấu câu**: Chia chuỗi theo các dấu câu (, . ? !...)

- **Tách dựa trên từ điển**: Sử dụng một từ điển các từ đã biết để nhận diện và tách các từ

- **Tách dựa trên quy tắc**: Áp dụng các quy tắc ngữ pháp hoặc hình thái học để tách từ (e.g. tách tiền tố, hậu tố)

- **Tách dựa trên học máy**: SỬ dụng các mô hình học máy để dự đoán ranh giới từ 

### Cách tiếp cận dựa trên từ điển

#### Longest matching

- Duyệt câu đầu vào tuần tự và chọn từ **dài nhất** nếu từ đó **có trong từ điển**
- Đây là kỹ thuật phổ biến trong xử lý chuỗi, đặc biệt trong bài tón tách từ trong các ngôn ngữ không có dấu cách giữa các từ như tiếng Trung, Nhật, Việt  

- Ví dụ
>Input: Học sinh học sinh học
>
>Duyệt tuần tự từ trái qua phải
>Output: Học_sinh học_sinh học

#### Maximum matching

- Sử dụng từ điển, **tạo ra tất cả các cách tách từ** có thể cho một câu bất kỳ, sau đó câu được tách từ đúng được chọn là câu chứa **ít từ nhất**

- Ví dụ:
>Input: Đó là cách để tuyên truyền thông tin
>Output: Đó là cách để tuyên_truyền thông_tin 

# Chuẩn hóa văn bản 

- **Khái niệm**: Là tập hợp các kỹ thuật nhằm đưa văn bản về một dạng thống nhất, dễ dàng xử lý hơn cho các tác vụ NLP 
- **Mục tiêu**:
	- Giảm thiểu sự đa dạng của dữ liệu ("Apple", "apple" -> "apple")
	- Loại bỏ nhiễu và thông tin không cần thiết 
	- Cải thiện hiệu suất của các mô hình học máy 
- **Các bước chính**: Làm sạch, tách từ, loại bỏ từ dừng, chỉnh sửa lỗi chính tả, lấy từ gốc 

## Làm sạch văn bản (Text Cleaning)

- **Mục tiêu**: Loại bỏ các yếu tố không mong muốn hoặc không mang ý nghĩa ngữ nghĩa từ văn bản
- Các loại nhiễu thường gặp:
	- HTML tags, XML tags
	- URLs (Địa chỉ web)
	- Ký tự đặc biệt, biểu tượng cảm xúc (emojis)
	- Số (tùy ngữ cảnh)
	- Khoảng trắng thừa
	- Ký tự không phải ASCII (nếu cần)

## Tách từ tiếng Việt

- **Mục tiêu**: Chia văn bản thành các đơn vị nhỏ hơn (token)

## Loại bỏ ký tự đặc biệt và từ dừng

- **Từ dừng** (stop words): Là các từ rất phổ biến trong ngôn ngữ nhưng thường không mang nhiều ý nghĩa phân biệt hoặc ngữ nghĩa quan trọng cho các tác vụ NLP (e.g. và, là, của, một, những)
- **Mục tiêu**:
	- Giảm kích thước dữ liệu
	- Giảm thời gian xử lý
	- Cải thiện hiệu suất của mô hình bằng cách loại bỏ nhiễu 

- **Danh sách từ dừng**: Thường có sẵn cho từng ngôn ngữ

- **Ký tự đặc biệt**: Ký tự không phải chữ cái hoặc số (!, @, #, $, %, ^, &, *, (, ), -, _, +, =, {, }, [, ], |, \, ;, :, ', ", <, >, ?, /, ., ,, ~)
- Lưu ý: Cần cân nhắc ngữ cảnh e.g. ! có thể thay đổi nghĩa tích cực mạnh, $, _ có nghĩa trong phân tích mã 

## Chỉnh sửa từ 

- **Mục tiêu**: Sửa lỗi chính tả, lỗi gõ phím, hoặc các biến thể không chuẩn của từ để đảm bảo tính nhất quán của dữ liệu
- **Tầm quan trọng**: Giảm hiệu quả của các mô hình do nhiều từ khác nhau cho 1 khái niệm, gây nhiễu
- Các loại lỗi
	- Lỗi gõ phím: "hte" thay vì "the"
	- Lỗi chính tả: "chính tar" thay vì "chính tả"
	- Lỗi

- Phương pháp
	- Sử dụng từ điển: So sánh từ với một từ điển chuẩn, tìm từ gần nhất (e.g. khoảng cách Levenshtein)
	- Sử dụng mô hình ngôn ngữ: Sử dụng các mô hình thống kê hoặc học sâu để dự đoán từ đúng dựa trên ngữ cảnh 
	- Rule-based: Áp dụng các quy tắc để sửa lỗi phổ biến 

## Lấy gốc từ (Stemming & Lemmatization)

- **Mục tiêu**: Giảm các từ có cùng gốc về một dạng cơ bản duy nhất để được coi là 1 thực thể duy nhất
- **Tầm quan trọng**: Giảm kích thước từ điển, tăng cường khả năng tổng quát hóa
- Ví dụ
	- "chơi", "chơi đùa", "vui chơi" -> "chơi"

### Stemming

- **Khái niệm**: Là quá trình cắt bỏ các hậu tố (đôi khi tiền tố) để đưa nó về dạng gốc (stem)
- **Cách hoạt động**: Dựa trên các quy tắc heuristic (quy tắc kinh nghiệm), và không đảm bảo từ gốc tạo ra là một từ có nghĩa trong từ điển 

- Ưu điểm: Nhanh chóng, đơn giản
- Nhược điểm: Có thể tạo ra các từ không có nghĩa, cắt quá mức/cắt không đủ 

### Lemmatization 

- **Khái niệm**: Là quá trình đưa một từ về dạng gốc có nghĩa trong từ điểm (lemma)
- **Cách hoạt động**: Yêu cầu kiến thức về ngữ pháp và từ loại của từ. Sử dụng từ điển và các quy tắc hình thái học phức tạp hơn 

- Ưu điểm: Tạo ra các từ gốc có nghĩa, chính xác hơn Stemming
- Nhược điểm: Chậm, phức tạp hơn Stemming

# Hiểu cấu trúc ngữ pháp

- **Khái niệm**: Phân tích cấu trúc ngữ pháp (Syntactic Analysis) là quá trình phân tích câu để hiểu cấu trúc ngữ pháp của nó, mối quan hệ giữa các từ và cashc chúng tạo thành các cụm từ, mệnh đề 
- **Mục tiêu**:
	- Hiểu được ý nghĩa chính xác của câu
	- Phát hiện lỗi ngữ pháp
	- Hỗ trợ các tác vụ NLP phức tạp hơn như dịch máy, tóm tắt văn bản, trả lời câu hỏi  
- **Cấp độ phân tích**: Từ từ loại, cụm từ đến cấu trúc câu hoàn chỉnh 

## Gán nhãn từ loại

- **Khái niệm**: Là quá trình gán nhãn từ loại (e.g. danh từ, động từ, tính từ, trạng từ) cho mỗi từ trong câu
- **Tầm quan trọng**:
	- Là bước nền tảng cho nhiều tác vụ NLP khác
	- Giúp phân biệt các từ có cùng cách viết nhưng khác từ loại (e.g. "book" vừa là danh từ vừa là động từ)
	- Hỗ trợ Lemmatization, phân tích cú pháp 
- **Nhãn từ loại**: Thường theo một bộ nhãn chuẩn 

- Ví dụ
	- Văn bản: "Tôi thích ăn phở Hà Nội."
	- Kết quả POS Tagging
		- Tôi: Đại từ (PR - Pronoun)
		- thích: Động từ (V - Verb)
		- ăn: Động từ (V - Verb)
		- phở: Danh từ (N - Noun)
		- Hà Nội: Danh từ riêng (Np - Proper Noun)
		- ".": Dấu câu (PUNC - Punctuation)

## Phân tích cú pháp nông

- Chunking (shallow parsing) là bước nhóm các từ đơn lẻ thành cụm từ có ý nghĩa ngữ pháp (phrase), dựa trên kết quả gán nhãn từ loại (POS tagging)

- "Cô gái trẻ đang đọc một cuốn sách thú vị."
- Kết quả Chunking:
	- \[NP Cô gái trẻ\] \[VP đang đọc\] \[NP một cuốn sách thú vị\].
- Giải thích:
- \[NP Cô gái trẻ\] là một cụm danh từ.
- \[VP đang đọc\] là một cụm động từ.
- \[NP một cuốn sách thú vị\] là một cụm danh từ khác.
- Ứng dụng: Trích xuất thông tin (ví dụ: tìm tất cả các cụm danh từ
trong văn bản)

## Phân tích cú pháp phụ thuộc

- **Khái niệm**: Phân tích cú pháp phụ thuộc (Dependency Parsing) là quá trình phân tích mối quan hệ phụ thuộc ngữ pháp giữa các từ trong một câu, xác định từ nào là "đầu" (head) và từ nào là "phụ thuộc" (dependent) của nó
- **Mục tiêu**: Biểu diễn các cấu trúc ngữ pháp dưới dạng một đồ thị có hướng, nơi các nút là từ và các cạnh là mối quan hệ phụ thuộc 

- Ưu điểm:
	- Tập trung vào mối quan hệ ngữ nghĩa giữa các từ
	- Hiệu quả hơn cho các ngôn ngữ có cấu trúc câu linh hoạt (e.g. tiếng Việt)

- Ví dụ
	- Văn bản: "Hà Nội là thủ đô của Việt Nam."
	- Mối quan hệ phụ thuộc (ví dụ):
		- Hà Nội -> gốc (root) của câu.
		- là -> phụ thuộc vào Hà Nội (quan hệ pred – vị ngữ).
		- thủ đô -> phụ thuộc vào là (quan hệ obj – bổ ngữ).
		- của -> phụ thuộc vào thủ đô (quan hệ case/mark – giới từ).
		- Việt Nam -> phụ thuộc vào của (quan hệ obl – bổ ngữ của giới từ).
		- Dấu chấm “.” -> phụ thuộc vào root (quan hệ punct).

- Ứng dụng: Trích xuất quan hệ (ví dụ: "thủ đô của Việt Nam"), dịch máy, trả lời câu hỏi.

- NLP hiện đại tập trung vào gốc từ (root) là từ chi phối toàn bộ câu
	- Trong bất kỳ câu nào, tất cả các từ, trừ một từ, đều có một mối quan hệ hoặc sự phục thuộc vào các từ khác trong câu
	- Từ không có sự phụ thuộc được gọi là gốc (root)
	- Hầu hết các trường hợp, động từ được coi là gốc của câu 

## Phân tích cú pháp thành phần

