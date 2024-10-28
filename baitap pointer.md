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
- Các hàm so sánh tên điểm và id đều sử dụng chung 1 kiểu dữ liệu. Các hàm so sánh đều nhận 2 tham số là con trỏ kiểu void a và b. Do khi so sánh hàm sẽ truyền từng phần tử của con trỏ vào hàm để so sánh thứ tự nên ta cần 2 con trỏ a và b để trỏ đến các phần tử của mảng được so sánh.
- Ta sẽ phải sử dụng ép kiểu 2 con trỏ kiểu void a và b thành con trỏ kiểu SinhVien để 2 con trỏ a và b có thể trỏ tới các kiểu dữ liệu trong struct SinhVien qua đó con trỏ có thể thao tác với các thành viên trong cấu trúc SinhVIen.
- Sau đó ta có hàm sắp xếp chung:
```
void sort(SinhVien array[], size_t size, int (*compareFunc)(const void *, const void *)) {
   int i, j;
   SinhVien temp;
   for (i = 0; i < size-1; i++)    
       for (j = i+1; j < size; j++)
           if (compareFunc(array+i, array+j)>0) {
               temp = array[i];
               array[i] = array[j];
               array[j] = temp;
           }
}

void display(SinhVien *array, size_t size) {
   for (size_t i = 0; i < size; i++) {
       printf("ID: %d, Ten: %s, Diem Trung Binh: %.2f\n", array[i].id, array[i].ten, array[i].diemTrungBinh);
   }
   printf("\n");
}
```
- Hàm sort dùng để sắp xếp sinh viên theo các tiêu chí mà con trỏ hàm compareFunc chỉ định thông qua các hàm so sánh ở trên còn hàm display để hiện thị các mảng đã được sắp xếp
- Với hàm sort ta tạo ra một con trỏ hàm kiểu int và truyền vào đó 2 con trỏ kiểu void. 2 con trỏ void được định nghĩa con trỏ hằng vì mục đích của 2 con trỏ void này chỉ để hứng giá trị của các mảng được so sánh vì vậy dùng const để giữ nguyên giá trị của 2 con trỏ void không bị thay đổi trong quá trình chạy chương trình
- Để so sánh ta dùng 2 vòng lặp for lồng nhau. Ta có thể thấy i < size -1 vì j bắt đầu từ phần tử i+1, để không bị tràn bộ nhớ nếu khi thực hiện vòng lặp j thì phần tử cuối của mảng i sẽ là size - 2 và phần tử bắt đầu vòng lặp j là i+1 và kết thúc là phần tử cuối size -1 . Và với điều kiện i < size -1 thì array[i] và array[j] sẽ so sánh được tất cả phần tử mà phần tử cuối sẽ không phải so sánh khi không còn phần tử nào. Nguyên nhân gây tràn bộ nhớ là do bộ đếm máy tính bắt đầu từ phần tử 0 do đó phần tử cuối của 1 mảng là size - 1.
- Khi hàm compareFunc trả giá trị so sánh của array[i] với array[j] trả giá trị dương thì sẽ thực hiện hoán đổi.
- Cuối cùng hàm int main() thực hiện chương trình:
```
int main() {
   SinhVien danhSachSV[] = {
       {  
           .ten = "Hoang",
           .diemTrungBinh = 7.5,
           .id = 100
       },
       {
           .ten = "Tuan",
           .diemTrungBinh = 4.5,
           .id = 101
       },
       {
           .ten = "Vy",
           .diemTrungBinh = 6.8,
           .id = 102},
       {  
           .ten = "Ngan",
           .diemTrungBinh = 5.6,
           .id = 10
       },
   };
   size_t size = sizeof(danhSachSV) / sizeof(danhSachSV[0]);

   // Sắp xếp theo tên
   sort(danhSachSV, size, compareByName);

   display(danhSachSV, size);

   // Sắp xếp theo điểm trung bình
   sort(danhSachSV, size, compareByDiemTrungBinh);

   display(danhSachSV, size);

   // Sắp xếp theo ID
   sort(danhSachSV, size, compareByID);

   display(danhSachSV, size);

   return 0;
}
```
- Đơn giản ta nhập thông tin học sinh, điểm, ID vào sau đó tính kích thước của mảng cần thiết size. Khi sắp xếp ta chỉ cần trỏ đến con trỏ mà ta cần lấy dữ liệu và thực hiện xuất ra màn hình qua hàm display.
