# Goto
goto là một từ khóa trong ngôn ngữ lập trình C, cho phép chương trình nhảy đến một nhãn (label) đã được đặt trước đó trong cùng một hàm.
```
#include <stdio.h>

int main() {
    int i = 0;

    // Đặt nhãn
    start:
        if (i >= 5) {
            goto end;  // Chuyển control đến nhãn "end"
        }

        printf("%d ", i);
        i++;

        goto start;  // Chuyển control đến nhãn "start"

    // Nhãn "end"
    end:
        printf("\n");

    return 0;
}
```
- Trong ví dụ trên ta có thể thấy 2 label được đặt là end và start. Nếu giá trị của i lớn hơn hoặc bằng 5 thì nó sẽ nhảy ra khỏi vòng lặp đi đến nhãn end để thực hiện câu lệnh printf. CÒn nếu giá trị của i nhỏ hơn 5 thì sẽ thực hiện vòng lặp vô hạn nhờ goto start nhưng do có điều kiện thoát khỏi vòng lặp là goto end nên ta không bị lặp vô hạn.
- Ngoài ra khi có 1 đoạn code có nhiều vòng lặp thì dùng goto sẽ thoát được vòng lặp nhanh hơn là dùng nhiều lệnh break
```
for(i=0; j<5; i++) {
printf(" vong lap trong: %d\n ", j);
if (j == 3){
printf(" thoat vong lap ", j);
break; }
}
```
# Thư viện setjmp.h 
- setjmp.h là một thư viện trong ngôn ngữ lập trình C, cung cấp hai hàm chính là setjmp và longjmp. Cả hai hàm này thường được sử dụng để thực hiện xử lý ngoại lệ trong C, mặc dù nó không phải là một cách tiêu biểu để xử lý ngoại lệ trong ngôn ngữ này.

