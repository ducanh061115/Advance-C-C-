# Extern
## Định nghĩa:
Khái niệm Extern trong ngôn ngữ lập trình C được sử dụng để thông báo rằng một biến hoặc hàm đã được khai báo ở một nơi khác trong chương trình hoặc trong một file nguồn khác giúp quản lý sự liên kết giữa các phần khác nhau của chương trình hoặc giữa các file nguồn.
- ví dụ: File test.c
```
#include<stido.h>
int a = 5;
void display(){
printf("this is file test\n");
return 0;
}
```
- File main.c:
```
#include<stdio.h>
extern int a;
extern void display;
int main(int argc, char const *argv[]) {
a = 20;
printf("a = %d\n", a);
display();
return 0;
}
```
- Ta phải liên kết file main.c và file test.c thông qua câu lệnh: gcc main.c test.c -o main
- Mục đích việc sử dụng extern là khi ta chỉ muốn sử dụng 1 số biến nhất định trong 1 file khác mà không cần đến toàn bộ nội dung, tránh việc phải include toàn bộ file đó vào.
# Static
## Static local variables (biến cục bộ)
Giữ giá trị của biến qua các lần gọi hàm và giữ phạm vị của biến chỉ trong hàm đó
```
#include <stdio.h>

void exampleFunction() {
     static int count = 0;  // Biến static giữ giá trị qua các lần gọi hàm
    count++;
    printf("Count: %d\n", count);
}

int main() {
    exampleFunction();  // In ra "Count: 1"
    exampleFunction();  // In ra "Count: 2"
    exampleFunction();  // In ra "Count: 3"
    return 0;
}
```
- Ta phải dùng biến static vì nếu không mỗi 1 lần hàm Function được gọi ra biến cout tăng giá trị lên 1 thì sau khi hàm kết thúc giá trị tăng lên đó sẽ bị xóa đi trở lại giá trị ban đầu. Còn nếu có static thì giá trị tăng lên đó sẽ được giữ nguyên khi lần gọi hàm tiếp theo đên.
## Static global variables (biến toàn cục)
Hạn chế phạm vi của biến đó chỉ trong file nguồn hiện tại.
- file other.c
```
#include <stdio.h>

int g_value = 30;
static int s_g_value = 20; //Biến chỉ có thể gọi và thay đổi giá trị trong file other.c


void display()
{
	printf("static global value: %d\n", s_g_value);
	printf("global value: %d\n", g_value);
}
```
- File main.c
```
#include <stdio.h>

extern void display();
//extern int s_g_value; //không thể gọi biến s_g_value do nó bị giới hạn trong file other.c
extern int g_value;

int main()
{
	printf("hello\n");
	g_value = 40;
	
	display();

	return 0;
}
```
## Static trong class
Khi một thành viên của lớp được khai báo là static, nó thuộc về lớp chứ không thuộc về các đối tượng cụ thể của lớp đó. Các đối tượng của lớp sẽ chia sẻ cùng một bản sao của thành viên static, và nó có thể được truy cập mà không cần tạo đối tượng. Nó thường được sử dụng để lưu trữ dữ liệu chung của tất cả đối tượng.
- Ví dụ:
```
#include <iostream>

typedef enum
{
    red = 0,
    blue,
    green,
    purple,
    black,
    yellow
} Pen_Color;

void print_color_pen(Pen_Color color)
{
    switch (color)
    {
    case red:
        std::cout << "Red\n";
        break;
    case blue:
        std::cout << "Blue\n";
        break;
    case green:
        std::cout << "Green\n";
        break;
    
    default:
        break;
    }
}


class PEN
{
public:
    Pen_Color pen_color;
    static int pen_length;

    PEN(Pen_Color color);
    Pen_Color get_color()
    {
        return pen_color;
    }
    void set_length(int length)
    {
        pen_length = length;
    }
};

int PEN::pen_length;

PEN::PEN(Pen_Color color)
{
    pen_color = color;
    pen_length = 10;
}


int main(int argc, char const *argv[])
{
    PEN blue_pen(blue);
    PEN red_pen(red);
    PEN green_pen(green);

    blue_pen.set_length(9);

    std::cout << "Color: ";
    print_color_pen(blue_pen.get_color());
    std::cout << "Length: " << blue_pen.pen_length << '\n';

    std::cout << "Color: ";
    print_color_pen(red_pen.get_color());
    std::cout << "Length: " << red_pen.pen_length << '\n';

    std::cout << "Color: ";
    print_color_pen(green_pen.get_color());
    std::cout << "Length: " << green_pen.pen_length << '\n';

    return 0;
}
```
- Trong ví dụ trên ta có thể thấy biến pen_length dùng để lưu trữ cố định giá trị cho tất cả các đối tượng thuộc lớp PEN. Đầu tiên ta gán giá trị của pen_length = 10 thì tất cả các đối tượng thuộc lớp PEN đều có output là 10 sau đó ta gọi hàm set_length từ biến blue_pen và set_length = 9 vì vậy oen_length ở tất cả các đối tượng thuộc lớp PEN đều có giá trị output là 9.
# Register




