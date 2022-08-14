# Babel
Babel là 1 thư viện JS nó chuyên dùng để **phân tích cú pháp và chuyển đổi cú pháp**

## Feature
- Chuyển đổi cú pháp ES6 trở lên -> ES5 (mục đích: hỗ trợ cho những trình duyệt cũ chạy được JS có thể chạy được ES6)
- Hỗ trợ chuyển đổi JSX thành React Element (mục đích: để cho thằng React-DOM nó có thể đọc được, bởi vì React-DOM nó chỉ nhận vào tham số là 1 React Element)

## Example
1. Cú pháp trong JSX
```JSX
const element = <h1>Hello World</h1>
```

2. Thông qua Babel nó sẽ biên dịch JSX trên -> React Element:
```Javascript
"use strict";
var element = /*#__PURE__*/React.createElement("h1", null, "Hello World");
```
*const(ES6) nó được babel chuyển thành var(ES5)*

3. Cuối cùng, ta có thể truyền Element trên cho ReactDOM để nó render UI:
```JSX
ReactDOM.render(element, document.getElementById('root'))
```

## Nguyên tắc hoạt động của Babel
(Client truy cập) Khi trang web chúng ta được tải xong thư viện babel (khi đã nhúng cdn/cài đặt) sẽ đi tìm trong DOM xem có cái tag nào là script và có type="text/babel" hay không. Khi nó tìm thấy nó sẽ lấy nội dung trong cặp thẻ đó (để phân tích và chuyển đổi). Sau khi nó phân tích xong nó sẽ đẩy lên thẻ <head></head> 1 thẻ script và sẽ chạy JS ở đây.
