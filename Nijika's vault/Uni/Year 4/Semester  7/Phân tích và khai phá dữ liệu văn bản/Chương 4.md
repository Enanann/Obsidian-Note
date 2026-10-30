
# Giới thiệu tóm tắt văn bản tự động

- **Khái niệm**: Là quá tình tạo ra một phiên bản ngắn gọn hơn của một hoặc nhiều tài liệu văn bản, trong khi vẫn giữ lại các thông tin quan trọng nhất và ý nghĩa cốt lõi
- **Mục tiêu**: Giúp người dùng nhanh chóng nắm bắt nội dung chính của tài liệu mà không cần đọc toàn bộ 

- Ví dụ
	- Tóm tắt bài báo tin tức
	- Tóm tắt cuộc họp 
	- ...

- Tại sao cần tóm tắt văn bản
	- Giảm quá tải thông tin
	- Giúp tiết kiệm thời gian
	- Cải thiện khả năng truy cập
	- Hỗ trợ ra quyết định
	- Ứng dụng đa dạng e.g. công cụ tìm kiếm, hệ thống đề xuất,...


# Các kỹ thuật tóm tắt văn bản

- Các kỹ thuật phổ biến
	- Trích xuất từ khóa (Keyphrase extraction)
	- Mô hình hóa chủ đề (Topic modeling)
	- Tóm tắt tự động (Automated Summarization) 

### Keyphrase extraction

- Đơn giản nhất
- Trích xuất từ khóa hoặc cụm từ chính phản ánh nội dung văn bản
- Ứng dụng
	- Từ khóa trong nghiên cứu, sản phẩm online
	- Có thể xem như dạng đơn giản của topic modeling

- **Khái niệm**: Là quá trình tự động xác định các từ hoặc cụm từ quan trọng nhất, đại diện cho nội dung chính tài liệu 
- **Mục tiêu**: Cung cấp cái nhìn nhanh về chủ đề của văn bản, hỗ trợ tìm kiếm, phân loại hoặc làm tiền đề cho tóm tắt 
- Khác biệt với tóm tắt: Tóm tắt tạo ra một văn bản thu gọn của văn bản trong khi trích xuất từ khóa chỉ tập trung vào các thuật ngữ quan trọng

- Ý tưởng: Các từ hoặc cụm từ xuất hiện với tần số cao xuất hiện trong một tài liệu thì nó mang ý nghĩa quan trọng trong tài liệu đó
- Cách tiếp cận đơn giản
	- Đếm tần xuất xuất hiện (hoặc n-gram) của từng từ
	- Sắp xếp các từ/n-gram theo giảm dần
	- Chọn N từ/n-gram có tần suất cao nhất làm từ khóa 

- Lưu ý: Cần loại bỏ từ dừng và chuẩn hóa văn bản trước khi đếm 

- Ưu điểm
	- Đơn giản, dễ triển khai
	- HIệu quả tốt cho các tài liệu ngắn hoặc khi cần từ khóa nhanh
- Nhược điểm
	- Không xem xét ngữ cảnh

### Topic modeling

- Sử dụng kỹ thuật thống kê & toán học để rút ra chủ đề/khái niệm
- Thường áp dụng cho tập hợp tài liệu (corpus), không chỉ một văn bản
- Các mô hình tiêu biểu
	- SVD (Singular Value Decomposition)
	- LDA (Latent Dirichlet Allocation)
- Ứng dụng
	- Text analytics
	- Bioinformatics

### Automated Summarization

- Tạo tóm tắt ngắn gọn từ 1 hoặc nhiều tài liệu
- Dựa trên thuật toán thống kê và ML
- Hai hướng tiếp cận
	- Extraction-based (chọn câu/đoạn đại diện)
	- Abstraction-based (tái viết, khái quát)
- **Extraction-based**
	- Trích chọn văn bản/cụm từ trong văn bản gốc để tạo bản tóm tắt
	- Bản tóm tắt là tập hợp con của văn bản gốc
	- Ưu điểm: Đơn giản, dễ thực hiện, đảm bảo tính chính xác ngữ pháp
	- Nhược điểm: Có thể thiếu tính mạch lạc, không tạo ra câu mới

- **Abstraction-based**
	- Tạo ra câu mới, diễn giải lại nội dung gốc bằng từ ngữ riêng của mô hình
	- Yêu cầu hiểu sâu về ngữ nghĩa và khả năng sinh ngôn ngữ tự nhiên
	- Ưu điểm: Mạch lạc, tự nhiên, ngắn gọn hơn
	- Nhược điểm: Phức tạp hơn, dễ mắc lỗi ngữ pháp hoặc sai lệch thông tin

