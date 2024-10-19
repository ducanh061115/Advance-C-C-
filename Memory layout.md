# Memory layout
## Phân vùng text:
- Chứa mã máy (tập hợp các lệnh thực thi)
- Thường chỉ có quyền đọc và thực thi, không có quyền ghi do chứa các mã máy
- Tất cả các biến lưu ở phân vùng text không thể thay đổi giá trị mà chỉ được đọc
- const cục bộ lưu ở stack còn const toàn cục lưu ở text (data với window: WinGM)
```
#include<stdio.h>
const int a = 5;
char *ptr = "hello world";
int main(){
printf("%d\n", a);
printf("%s\n", *ptr) 
// int a =20; sẽ báo lỗi do chỉ có quyền đọc chứ không có quyền ghi
return 0;
}
```
## Phân vùng Data (dữ liệu đã khởi tạo)
- chứa các biến toàn cục được khởi tạo với giá trị khác 0
- Chứa các biến static // gcc -S -o main.s main.c
- Có quyền truy cập đọc và ghi
- Tất cả các biến sẽ được thu hồi sau khi chương trình kết thúc
```
#include<stdio.h>
int a = 5;
const int b= 10;
void *ptr = &a; // địa chỉ biến a và con trỏ ptr nằm ở phân vùng data
static double c = 6;
void test(){
static int d = 5;
}
int main(){
 a = 7;
 d = 10; 
printf("%d\n", a);
return 0;
}
```
## Phân vùng Bss (dữ liệu chưa khởi tạo)
- Chứa các biến toàn cục khởi tạo với giá trị bằng 0 hoặc không gán giá trị
- Chứa các biến static với giá trị khởi tạo bằng 0 hoặc không gián giá trị
- Quyền truy cập là đọc và ghi
- Tất cả các biến sẽ bị thu hồi khi chương trình kết thúc
```
#include<stdio.h>
int a = 5;
const int b= 0;// biến b sẽ lưu ở bss
void *ptr = &a; // địa chỉ biến a và con trỏ ptr nằm ở phân vùng data
static double c = 0;
void test(){
static int d = 5;
int e;
}
int main(){
 c = 7;
 d = 10; 
printf("%d\n", c); 
return 0;
}
```
- Biến static chưa được khởi tạo ko ghi ra bss mà nó có biến ghi .lcomm c,8,8 cấp phát và căn chỉnh
## Stack
- Chứa các biến cục bộ, tham số truyền vào
- Quyền truy cập: Đọc và ghi
- Sau khi ra khỏi hàm, sẽ thu hồi vùng nhớ
- LIFO (
```
#include<stdio.h>
void swap(int a, int b){
int temp =a;
a = b;  //địa chỉ cả 3 biến sẽ được lưu ở stack
b = temp;
}
int main(){
int a = 10;
int b = 5;
swap(a,b); // thực hiện ct không làm thay đổi giá trị a và b do địa chỉ của a và b sẽ bị thu hồi sau khi hàm void chạy xong muốn chạy ta phải dùng con trỏ
return 0;
}
```
## Heap
- Cấp phát động trong quá trình thực thi của chương trình
- Cho phép chương trình tạo ra và giải phóng bộ nhớ theo nhu cầu
- Dùng các hàm malloc(), calloc(), realloc(), free() được sử dụng để cấp phát và giải phóng bộ nhớ trên heap
- Không tự động thu hồi địa chỉ
```
#include<stdio.h>
#include<stdlib.h>
#include<stdint.h>
int main()
{
malloc(5); // cấp phát 5 ô địa chỉ ở phân vùng heap
return 0;
}
```

