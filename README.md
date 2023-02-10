# Lời mở đầu
Các cú pháp sắp được liệt kê dưới đây chỉ dành cho những người đã thành thạo cú pháp C++ cơ bản, nếu bạn chưa đạt đến trình độ theo yêu cầu thì tốt nhất hãy học chúng trước trước khi đọc trang này. Ngoài ra, đa số các cú pháp dưới đây chỉ có mặt ở các phiên bản `C++ >= 11`, hãy xem kĩ phiên bản C++ của mình bởi vì đa số các bạn có thể đang dùng phiên bản `C++98` (nếu bạn sử dụng DevC++).

<br>
Các thông tin trong tài liệu này đã được lấy từ nhiều nguồn khác nhau, và sẽ tôi sẽ để lại link đến trang tương ứng với từng nội dung trong bài viết này.

# Vòng lập tà đạo
Nguồn: https://www.learncpp.com/cpp-tutorial/for-each-loops/
### Vòng lập for
Trong khi vòng lập `for` cho phép ta truy cập các phần tử trong mảng một cách dễ dàng, cách viết của chúng khá dài và đôi khi khiến ta dễ viết sai.
```cpp
...
// code để in ra các phần tử của mảng arr
const int n = 5;
int arr[n] = {1, 2, 3, 4, 5};
for (int i = 0; i < n; i++) {
    cout << arr[i] << ' ';
}
...
```
### Vòng lập for-each
Trong `C++11`, người ta đã giới thiệu một cú pháp mới cho vòng lập `for` chính là cú pháp vòng lập `for-each`. Ta có thể dùng vòng lập `for-each` để viết đoạn code trên một cách gọn gàng và dễ đọc hơn.
```cpp
/*
* Cú pháp của vòng lập for-each
* for (<tên kiểu của phần tử> <tên của phần tử> : <mảng>)
*     <mệnh đề>
*/
...
const int n = 5;
int arr[n] = {1, 2, 3, 4, 5};
for (int i : arr) {
    cout << i << ' ';
}
...
```
### Vòng lập for-each với từ khóa auto
Vì mọi phần tử trong một mảng đều có cùng một kiểu nên ta có thể dùng từ khóa `auto` để C++ tự quyết định tên kiểu cho phần tử đang xét hiện tại.
```cpp
...
const int n = 5;
int arr[n] = {1, 2, 3, 4, 5};
for (auto i : arr) {
    cout << i << ' ';
}
...
```
### Vòng lập for-each với các cấu trúc dữ liệu khác
Tất nhiên, ta cũng có thể dùng vòng lập `for-each` trên các cấu trúc dữ liệu có phần tử truy cập được bằng chỉ số.
```cpp
...
// trên mảng tiêu chuẩn std::array
const int n = 5;
array<int, n> arr({ 1, 2, 3, 4, 5 });
for (auto i : arr) {
    cout << i << ' ';
} 
...

...
// trên vector
vector<int> arr({ 1, 2, 3, 4, 5 });
for (auto i : arr) {
    cout << i << ' ';
}
...

...
// trên map
map<string, int> mp {
    {"a", 1},
    {"b", 2},
    {"c", 3}
};

for (auto i : mp) {
    cout << i.first << ' ' << i.second << endl;
}
...
```
### Vòng lập for-each và truy cập bằng tham chiếu
Ở đoạn code dưới đây, các phần tử được truy cập bằng tham trị. Tức có nghĩa là chúng ta đang truy cập một bản sao của phần tử đó.
```cpp
...
const int n = 5;
int arr[n] = {1, 2, 3, 4, 5};
for (auto i : arr) {
    cout << i << ' ';
}
...
```
Việc tạo ra một bản sao cho một phần tử khá tốn thời gian và trong đa số các trường hợp, chúng ta chỉ muốn truy cập tham chiếu của nó. May thay, tính năng truy cập bằng tham chiếu trong vòng lập `for-each` là có tồn tại.
```cpp
...
const int n = 5;
int arr[n] = {1, 2, 3, 4, 5};

// dấu & cho biết phần tử i đang được truy cập bằng tham chiếu
for (auto &i : arr) {
    cout << i << ' ';
    // tất nhiên, vì đây là truy cập bằng tham chiếu, bạn cũng có thể trực tiếp thay đổi giá trị của phần tử đó
    i = 1;
}
...
```
Nếu bạn chỉ muốn truy cập phần tử trong mảng mà không làm thay đổi giá trị của nó thì ta nên thêm từ khóa `const` trước tên kiểu.
```cpp
...
const int n = 5;
int arr[n] = {1, 2, 3, 4, 5};

for (const auto &i : arr) {
    cout << i << ' ';
}
...
```
### Một số nhược điểm của vòng lập for-each
Vòng lập `for-each` **không** cho phép ta truy cập chỉ số của phần tử hiện tại. Tuy nhiên, ở phiên bản `C++20` thì đã cú pháp cho phép ta làm điều đó!
```cpp
...
/* Cú pháp 
* for (<mệnh đề khởi tạo>; <tên kiểu> <tên của phần tử> : <mảng>)
*     <mệnh đề>
*/

const int n = 5;
int arr[n] = {1, 2, 3, 4, 5};

// i là chỉ số hiện tại của phần tử el
// khác với vòng lập thông thường, nếu muốn tăng biến đếm thì ta phải tăng nó bên trong vòng lập
for (int i = 0; const auto &el : arr) {
    cout << i << ' ' << el << endl;
    i++;
}
```
Vòng lập `for-each` **không** cho phép ta lặp qua các phần tử của mảng theo chiều ngược lại. Tuy nhiên, đối với các cấu trúc dữ liệu tiêu chuẩn STL, ta có thể dùng con trỏ ngược `reverse_iterator` và một vòng lập `for` thông thường để làm giải pháp thay thế. Còn đối với mảng thông thường thì có thể lập từ chỉ số cuối đến đầu.
```cpp
...
// Đối với mảng thường
const int n = 5;
int arr[n] = {1, 2, 3, 4, 5};

for (int i = n - 1; i >= 0; i--) {
    cout << arr[i] << ' ';
}

...
// Đối với các cấu trúc dữ liệu tiêu chuẩn STL, ví dụ như vector
vector<int> arr({ 1, 2, 3, 4, 5 });
for (auto i = arr.rbegin(); i != arr.rend(); i++) {
    cout << *i << ' ';
}
...
```

