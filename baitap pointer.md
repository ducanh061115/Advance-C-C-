# Chương trình quản lý học sinh 
- Đầu tiên ta khởi tạo biến struct có tên SinhVien với các kiểu dữ liệu con bên trong
```
#include <stdio.h>
#include <string.h>

typedef struct {
   char ten[50];
   float diemTrungBinh;
   int id;
} SinhVien;
```
- Sau đó ta tạo một hàm so sánh chuỗi StringCompare
```
int stringCompare(const char *str1, const char *str2) {
   while (*str1 && (*str1 == *str2)) {
       str1++;
       str2++;
   }
   return *(const unsigned char*)str1 - *(const unsigned char*)str2;
```
- 
