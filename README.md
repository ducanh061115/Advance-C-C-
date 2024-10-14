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
- 
