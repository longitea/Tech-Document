# React DOM
React-DOM là cầu nối giữa thằng react và DOM element

## Feature
1. method render
2. method làm pop-up



### 1. Method render
React dom sử dụng phương thức render và nhận vào 2 tham số:
- param1: React Element (là chuỗi html nhưng trong react)
- param2: Dom Element ( selector 1 element node cụ thể )

phương thức này xác định 1 element cụ thể trong dom và thực hiện thêm phần tử html trong param 1 vào vị trí đã được xác định trong param2

### 2. Method Create
**Công dụng**
dùng để render React element làm thằng con cuối cùng của thẻ Body


**Ứng dụng**
thường được sử dụng đẻ làm Pop-Up Login (vì nó có lớp phủ đè lên tất cả những cái thẻ cùng cấp)

**Cú pháp tạo ra fn component**
```jsx
ReactDOM.createPortal(child, container)
```