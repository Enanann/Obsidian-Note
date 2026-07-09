
- Ta có thể sử dụng template để tạo class, cấu trúc tương tự như function templates
- Ví dụ cho lớp Array
```cpp
#pragma once

#include <cassert>

template <typename T> // added
class Array {
public:
    Array(int length) {
        assert(length > 0);
        m_data = new T[length]{}; // allocated an array of objects of type T
        m_length = length;
    }

    Array(const Array&) = delete;
    Array& operator=(const Array&) = delete;

    ~Array() {
        delete[] m_data;
    }

    void erase() {
        delete[] m_data;
        // We need to make sure we set m_data to 0 here, otherwise it will
        // be left pointing at deallocated memory!
        m_data = nullptr;
        m_length = 0;
    }

    // templated operator[] function defined below
    T& operator[](int index); // now returns a T&

    int getLength() const { return m_length; }
    
private:
    int m_length{};
    T* m_data{}; // changed type to T
};

// member functions defined outside the class need their own template declaration
template <typename T>
T& Array<T>::operator[](int index) // now returns a T&
{
    assert(index >= 0 && index < m_length);
    return m_data[index];
}
```

- Có 2 cách chính để tách file chứa class template
	- Để tất cả định nghĩa lớp và định nghĩa hàm trong một header file (như trên)
	- Sử dụng file header để chứa định nghĩa lớp, tạo một file ".inl" (inline; là convention) (hoặc `.tpp`, `.ipp`...) chứa định nghĩa các hàm đó và `#include` vào cuối file header 

```cpp 
#### array.h 
#pragma once

#include <cassert>

template <typename T> // added
class Array {
	// ...
};

#include "array.inl"

#### array.inl
// member functions defined outside the class need their own template declaration
template <typename T>
T& Array<T>::operator[](int index) // now returns a T&
{
    assert(index >= 0 && index < m_length);
    return m_data[index];
}
```

- Nguyên nhân không làm được theo kiểu tách 1 file header, 1 file cpp
	- Giống với function template, compiler sẽ không tạo instance của kiểu dữ liệu đó nếu như không bao giờ sử dụng 
	- Khi compiler gặp một specialization như `Array<int>`, nó sẽ cần biết mọi định nghĩa của lớp và hàm thành viên để có thể tạo thể hiện
	- Mà định nghĩa hàm thành viên của lớp này đang ở trong file source riêng, nên compiler sẽ không thấy nó (do C++ compile từng file source riêng biệt), dẫn đến linker error

- **Non-type parameters** là tham số template mà kiểu của nó đã được định nghĩa trước và thay thế cho một giá trị constexpr truyền vào lớp/hàm như là một tham số
	- Kiểu số nguyên
	- Kiểu enum
	- Con trỏ hoặc tham chiếu đến một lớp
	- Con trỏ hoặc tham chiếu đến một hàm
	- Con trỏ hoặc tham chiếu đến một hàm thành viên 
	- `std::nullptr_t`
	- Kiểu dấu phẩy động (floating point) (C++20)

```cpp
template <typename T, int size> // size is an integral non-type parameter
class StaticArray {
public:
    T* getArray();

    T& operator[](int index) {
        return m_array[index];
    }
    
private:
    // The non-type parameter controls the size of the array
    T m_array[size] {};
};

// Showing how a function for a class with a non-type parameter is defined outside of the class
template <typename T, int size>
T* StaticArray<T, size>::getArray() {
    return m_array;
}

int main() {
    // declare an integer array with room for 12 integers
    StaticArray<int, 12> intArray;

    // Fill it up in order, then print it backwards
    for (int count { 0 }; count < 12; ++count)
        intArray[count] = count;

    for (int count { 11 }; count >= 0; --count)
        std::cout << intArray[count] << ' ';
    std::cout << '\n';

    // declare a double buffer with room for 4 doubles
    StaticArray<double, 4> doubleArray;

    for (int count { 0 }; count < 4; ++count)
        doubleArray[count] = 4.4 + 0.1 * count;

    for (int count { 0 }; count < 4; ++count)
        std::cout << doubleArray[count] << ' ';

    return 0;
}
```

- Có thể thấy là ta không cần phải cấp phát động cho `m_array`, do như đã nói ở trên, non-type template parameter là một constant expression, đồng nghĩa với việc ta không thể
```cpp
constexpr int x{5}; 
StaticArray<int, x> arr; // OK 

int y{5}; 
StaticArray<int, y> arr; // Error
```

- Nếu class là template và hàm thành viên cũng là template, để định nghĩa hàm ở ngoài 
```cpp
template<typename T>
struct Foo {
	template<typename U>
	void foo();
};

template <typename T>
template <typename U>
void Foo<T>::foo() {
}
```

**Function template specialization**

- Trong trường hợp mà ta muốn một hàm template có cách xử lý khác nhau tùy thuộc vào kiểu dữ liệu, ta có thể
	- Tạo một hàm cụ thể non-template
	- Sử dụng template specialization

- **Template specialization** là tính năng cho phép ta định nghĩa cách triển khai khác nhau của một template cho một kiểu dữ liệu cụ thể. 
	- **Full specialization** là khi mà tất cả tham số template được specialized 
	- **Partial specialization** là khi mà một số tham số template được specialized 

- Lưu ý function template specialization không hỗ trợ partial specialization
```cpp
template <typename T>
void print(const T& t) {
    std::cout << t << '\n';
}

// non-template
void print(double d) {
    std::cout << std::scientific << d << '\n';
}

// template specialization 
// A full specialization of primary template print<T> for type double
// Full specializations are not implicitly inline, so make this inline if put in header file
template<>     // template parameter declaration containing no template parameters
void print<double>(const double& d) // specialized for type double
{
    std::cout << std::scientific << d << '\n';
}
```

- Full specialization không được ngầm định là inline, vì thế cần để nó là inline nếu để trong header file để tránh vi phạm ODR

**Class template specialization**

- **Class template specialization** là tính năng cho phép ta định nghĩa cách triển khai khác nhau của một class template cho một kiểu dữ liệu cụ thể e.g. (`Storage8<T>` - lưu trữ 8 giá trị, sẽ phí bộ nhớ nếu T là bool)

- Tuy nhiên, khi sử dụng tính năng này, ta cần định nghĩa lại toàn bộ class
```cpp
template <typename T>
class Storage8 {
public:
    void set(int index, const T& value) {
        m_array[index] = value;
    }

    const T& get(int index) const {
        return m_array[index];
    }

private:
    T m_array[8];
}

template<>
class Storage8<bool> {
public:
    void set(int index, bool value) {
        auto mask{ 1 << index };

        if (value)  // If we're setting a bit
            m_data |= mask;   
        else  // if we're turning a bit off
            m_data &= ~mask;  
	}

    bool get(int index) {
        // Figure out which bit we're getting
        auto mask{ 1 << index };
        // bitwise-and to get the value of the bit we're interested in
        // Then implicit cast to boolean
        return (m_data & mask);
    }

private:
    std::uint8_t m_data{};
}
```

- Trong trường hợp mà ta chỉ muốn specialize một hàm thành viên, ta hoàn toàn có thể làm tương tự với funtion template specialization
```cpp
template <typename T>
class Storage {
public:
    Storage(T value)
      : m_value { value }
    {
    }

    void print() {
        std::cout << m_value << '\n';
    }

private:
    T m_value {};
};

// This is a specialized member function definition
// Explicit function specializations are not implicitly inline, so make this inline if put in header file
template<>
void Storage<double>::print() {
    std::cout << std::scientific << m_value << '\n';
}
```