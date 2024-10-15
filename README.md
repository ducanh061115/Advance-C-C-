# Pointer
## Định nghĩa:
Con trỏ là 1 biến đặc biệt vì nó không lưu trữ giá trị thông thường mà lưu trữ địa chỉ của 1 biến khác
## Cách dùng thông thường:
Khi khai báo biến con trỏ ta thêm dấu * vào trước tên biến
>  - int a = 50
>  - *ptr = &a 
- Khi này biến ptr sẽ lưu trữ địa chỉ của biến a(ví dụ 0x01) còn biến a sẽ có giá trị là 50
## Kích thước:
Kích thước của con trỏ phụ thuộc vào kiến trúc của máy tính:
- Nếu là windowX64 thì biến int có giá trị là 8 byte
- Nếu là trên vi xủ lý có cấu trúc ARM (32 bit) thì biến int có giá trị 4 byte
- **Ta dùng hàm sizeof() để biết được kích thước của biến**
> - int *a =  NULL
> - printf("kich thuoc: %d\n", sizeoff(a))
# Void Pointer
## Định nghĩa:
Void pointer thường dùng để trỏ để tới bất kỳ địa chỉ nào mà không cần biết tới kiểu dữ liệu của giá trị tại địa chỉ đó.
Cú pháp: 
> void *ptr_void. 
```gcc
#include <stdio.h>.
#include <stdlib.h>.

int main() {

    int value = 5;
    double test = 15.7;
    char letter = 'A';

    void *ptr = &value;
    printf("value is: %d\n", *(int*)(ptr));

    ptr = &test;
    printf("value is: %f\n", *(double*)(ptr));

    ptr = &letter;
    printf("value is: %c\n", *(char*)(ptr));
   
    return 0;
}
```
- *(kiểu dữ liệu*)(ptr) là cách ta gán kiểu dữ liệu cho biến ptr do biến ptr chưa được khai báo kiểu dữ liệu
- phải có dấu & để con trỏ trỏ được tới biến ta cần.
# Function Pointer
## Định nghĩa
- Con trỏ hàm là 1 biến mà giữ địa chỉ của 1 hàm. Nó cho phép bạn truyền một hàm như là một đối số cho một hàm khác. lưu trữ địa chỉ của hàm hoặc thậm chí truyền hàm như 1 giá trị trả về của hàm khác.
- Cú pháp: 
> return_type (*pointer_name)(input parameter)
- Ví dụ:
```
void print(){
  printf("hello world");
}
int main(){
  void (*ptr)(); //ta phải gọi lại 1 hàm void
  ptr = print; //gán địa chỉ hàm print cho con trỏ ptr
  ptr(); //gọi hàm thông qua con trỏ hàm hoặc dùng cú pháp (*ptr)()
}
```
- Ta có thể sử dụng con trỏ hàm như 1 đối số truyền vào:
```
#include<stdio.h>
void Tong(int a, int b){
    printf("%d + %d = %d\n",a,b, a + b);
}
void Hieu(int a, int b){
    printf("%d - %d = %d\n",a,b,a - b);
}
void congthuc(void(*ptr)(int,int), int a, int b){
ptr(a,b);
}
int main() 
{   
congthuc(Tong,5,7);
congthuc(Hieu,5,7);
return 0;
} 
```
Kết quả:
```
5 + 7 = 12.

5 - 7 = -2
```
# Pointer to Constant( Con trỏ hằng)
## Định nghĩa:
Con trỏ chỉ có khả năng đọc giá trị mà không thay đổi được giá trị của vùng nhớ mà nó trỏ tới nhưng vẫn trỏ được tới vùng nhớ khác.
- Cú pháp:
> const int *ptr_const;
- ví dụ:
```
const int value1 = 10;
const int value2 = 20;
const int *ptr = &value1; // con tỏ ptr nhận giá trị tại địa chỉ của biến value1
*ptr = 15 // hệ thống sẽ báo lỗi do value1 có giá trị cố định là 10
```
# Constant Pointer
## Định nghĩa: 
Con trỏ hằng là con trỏ mà sau khi được khởi tạo và trỏ đến 1 địa chỉ cụ thể, nó không thể thay đổi để trỏ tới một địa chỉ khác.
- Ví dụ:
```
const int value1 = 10;
const int value2 = 20;
int *const *ptr = &value1;
*ptr = 5
// *ptr = &value2 sẽ xảy ra lỗi
```
# Pointer to Pointer
## Định nghĩa:
Con trỏ đến con trỏ là một kiểu dữ liệu cho phép lưu trữ địa chỉ của một con trỏ. Cho phép bạn thay đổi giá trị của con trỏ bằng địa chỉ của một con trỏ khác.
# NULL Pointer
## Định nghĩa:
Con trỏ NULL không trỏ đến bất kì đối tượng hoặc vùng nhớ cụ thể nào


