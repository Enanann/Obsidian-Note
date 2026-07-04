
- Bình thường thì điều kiện trong if sẽ được tính toán tại runtime
- Tuy nhiên, xét trường hợp điều kiện là constexpr -> Nếu false thì block sẽ không bao giờ chạy -> tốn tài nguyên 
- C++17 thêm **constexpr if statement**, nó yêu cầu điều kiện phải là constant expression, và sẽ được chạy trong compile-time
```cpp
constexpr double gravity{9.8};
if constexpr (gravity == 9.8) {
	//...
} else {
	//...
}
```
- Best practice: Ưu tiên constexpr if khi điều kiện là constant expression  

- Best practice: Ưu tiên không lùi dòng cho các labels trong switch 
- Switch sẽ thực hiện lần lượt các case khi tìm được match, điều này chỉ kết thúc khi:
	- Kết thúc block switch
	- `break` hoặc `return`
	- Thứ gì đó làm gián đoạn flow của chương trình (OS sập, crash,...)
=> **fallthrough**
- Nếu muốn tự ý để fallthrough, nên thêm `[[fallthrough]];` vào cuối. `;` được gọi là **null statement** 

- Các biến khai báo trong case đều nằm trong scope của switch 
- Best practice: Nếu muốn khai báo biến cho case, làm thế trong một block của case 

- **Halt** cho phép chúng ta kết thúc chương trình 
- **Normal termination** đồng nghĩa với chương trình kết thúc thuận lợi 
- `std::exit()` sẽ tự động được gọi ở cuối chương trình. Ta cũng có thể gọi nó ở bất kì đâu (trong `cstdlib`), lưu ý là nó sẽ không cleanup biến cục bộ, hay unwind call stack 

- Có thể sử dụng `std::atexit(func)` để tự động chạy một hàm cleanup khi `std::exit()` được gọi 

- `std::abort()` được gọi khi chương trình của bạn kết thúc không bình thường (**abnormal termination**). Nghĩa là khi chương trình gặp lỗi runtime mà không xử lý được e.g. chia cho 0 
- `std::abort()` không chạy clean up 
- `std::terminate()` thường được dùng kết hợp với exception, mặc định nó sẽ gọi `std::abort()` 