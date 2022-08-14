# JSX là gì?
Javascript XML (cú pháp của 1 cặp thẻ mở và đóng)
hiểu đơn giản JSX giúp tạo ra React Element nhanh hơn và ngắn gọn hơn.


## Feature
- được dùng để viết code Javascript và XML(HTML) trong cùng một file

## Khi nào cần sử dụng JSX ?
- Khi 1 file cần tạo ra nhiều React Element, JSX sẽ giúp viết code ngắn gọn hơn, và dễ nhìn hơn.

- Đơn nhiên ưng dụng web không thể đọc được file JSX, vì thế nó cần thêm 1 thư viện Babel để biên dịch mã file này thành JS thuần và React Element, JS thuần thì đã có chrome v8 hiểu còn RE thì đã có React-DOM đưa nó vào DOM.

## Sự khác nhau khi có và không có JSX !
**Không có JSX**
```JS
const element = React.createElement('h1',
    {
        className:"Heading",
        style: {color: 'red'}
    },
    'Hello World'
)
```


**JSX**
```JSX
const element = <h1
    className="Heading"
    style={{ color: 'red' }}
>Hello World</h1>
```

*Trong JSX cú pháp { ... } đầu tiên dùng để viết Javacript*

## Làm việc với JSX

### 1. Tạo ra 1 Component bằng JSX
-> define 1 funtion và trả về UI

### truyền Props trong JSX

```jsx
<YourComponent
    propName1="String literals"
    propName2={expression}
/>
```
Có 2 cách truyền props vào trong Compnent:
- Cách 1: truyền dưới dạng chuỗi (String literals)
- Cách 2: truyền dưới dạng expression

