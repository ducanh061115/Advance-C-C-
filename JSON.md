# Định nghĩa:
- JSON là 1 chuỗi: char *json_str=".."; có thể có nhiều kiểu dữ liệu như mảng, chuỗi khác
- Key và value: "name" : "John" ngăn cách nhau bằng dấu phẩy giữa các cặp key : value
```
char *json = "
{
"name" : "John" ,
"age" : 30
}
"
```
- Key là chuỗi
- value có thể là chuỗi hoặc số thậm chí là NULL
- JSON dùng để xử lý một mảng gồm nhiều phần tử phức tạp
