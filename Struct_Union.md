# Struct
struct là một cấu trúc dữ liệu cho phép lập trình viên tự định nghĩa một kiểu dữ liệu mới bằng cách nhóm các biến có các kiểu dữ liệu khác nhau lại với nhau. struct cho phép tạo ra một thực thể dữ liệu lớn hơn và có tổ chức hơn từ các thành viên (members) của nó
- Ví dụ:
```
struct Data{
int a;
double b;
};
struct Data data1, *data2;
data1.a =10; // biến a có giá trị bằng 10
data2->b=5; // biến data 2 trỏ tới địa chỉ của b và gán giá trị cho b =5 
```
- Ta tạo ra 1 kiểu dữ liệu mới tên là Data và khi tạo ra 1 biến dựa trên kiểu dữ liệu mới này ta phải dùng cú pháp struct tenbien
- Ta có thể dùng câu lệnh typedef struct {...} tenbien; để tạo ra 1 kiểu dữ liệu mới
- Từng kiểu dữ liệu chỉ có thể ghi vào các địa chỉ phù hợp (chẳng hạn double 8 byte chỉ ghi vào được 0x00, 0x08, 0x16,...)
## Kích thước
- Padding là các ô địa chỉ trống không sử dụng
- Kích thước phụ thuộc vào số byte của kiểu dữ liệu lớn nhất trong các biến cho mỗi lần cấp phát ô nhớ cho các biến( chẳng hạn 4 byte thì mỗi lần cấp pháp sẽ được 4 ô địa chỉ)
- Nếu là mảng thì mỗi phần tử sẽ được lưu trữ trong 1 ô và quy tắc cấp phát ô nhớ như một biến bình thường.
```typedef struct 
 {
    uint8_t a;  // 1 byte  
    uint16_t b; // 2 byte
    uint32_t c; // 4 byte
} frame;
```
- Kích thước của struct frame trên là 8
# Union
union là một cấu trúc dữ liệu giúp lập trình viên kết hợp nhiều kiểu dữ liệu khác nhau vào cùng một vùng nhớ. Mục đích chính của union là tiết kiệm bộ nhớ bằng cách chia sẻ cùng một vùng nhớ cho các thành viên của nó. Điều này có nghĩa là, trong một thời điểm, chỉ một thành viên của union có thể được sử dụng. Điều này được ứng dụng nhằm tiết kiệm bộ nhớ
- Ví dụ:
```
Union Data{
int a;
double b;
};
Union Data data1, *data2;
data1.a =10; // biến a có giá trị bằng 10
data2->b=5; // biến data 2 trỏ tới địa chỉ của b và gán giá trị cho b =5 
```
- Khá tương tự Struct
## Kích thước
- Kích thước của union là kiểu giá trị lớn nhất trong union + padding
- Các biến cùng sử dụng địa chỉ giống nhau
```
typedef union 
 {
    uint8_t a; // 1 byte  
    uint32_t b; // 4 byte 
    uint16_t c; // 2 byte 
} frame;

int main(int argc, char const *argv[]){
	printf("kich thuoc: %d\n", sizeof(frame));
```
- Kích thước sẽ là 4 byte bằng kiểu giá trị lớn nhất.
