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
- Sau đó ta tạo các hàm so sánh để có thể sắp xếp:
```
int stringCompare( const char *str1, const char *str2) {
   while (*str1 && (*str1 == *str2)) {
       str1++;
       str2++;
   }
   return *(const unsigned char*)str1 - *(const unsigned char*)str2;
}


// Hàm so sánh theo tên
int compareByName(const void *a, const void *b) {
   SinhVien *sv1 = (SinhVien *)a;
   SinhVien *sv2 = (SinhVien *)b;
   return stringCompare(sv1->ten, sv2->ten);
}

// Hàm so sánh theo điểm trung bình
int compareByDiemTrungBinh(const void *a, const void *b) {
   SinhVien *sv1 = (SinhVien *)a;
   SinhVien *sv2 = (SinhVien *)b;
   if (sv1->diemTrungBinh > sv2->diemTrungBinh)
   {
       return 1;
   }
  
   return 0;
}

// Hàm so sánh theo ID
int compareByID(const void *a, const void *b) {
   SinhVien *sv1 = (SinhVien *)a;
   SinhVien *sv2 = (SinhVien *)b;
   return sv1->id - sv2->id;
}
```
- Ta có thể thấy tất cả các hàm so sánh đều dùng hàm con trỏ hằng. Lí do là trong quá trình chạy chương trình các hàm void chỉ có tác dụng lưu trữ địa chỉ của các con trỏ sv1 sv2. Do vậy để đảm bảo giá trị lưu trữ không bị thay đổi trong quá trình chạy chương trình ta dùng hàm con trỏ hằng.
- Hàm stringCompare được tạo là do tên là 1 chuỗi kí tự do vậy để sắp xếp ta phải so sánh từng biến của chuỗi đó. Trong vòng lặp while có phép toán logic (*str1 && *str1 == *str2) vì nếu không có điều kiện *str1 # \0 thì khi so sánh từng biến của chuỗi str1 và str2 khi hết kí tự đến \0 sẽ tạo ra vòng lặp vô hạn vì vậy điều kiên *str1 # \0 vào để làm điều kiện kết thúc vòng lặp.
- Các hàm so sánh tên điểm và id đều sử dụng chung 1 kiểu dữ liệu. Các hàm so sánh đều nhận 2 tham số là con trỏ kiểu void a và b. Do khi so sánh hàm sẽ truyền từng phần tử của con trỏ vào hàm để so sánh thứ tự nên ta cần 2 con trỏ a và b để trỏ đến địa chỉ của 
