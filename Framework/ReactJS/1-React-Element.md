# React Element
React Element là phiên bản nâng cấp lên của DOM Element.


## React Element là gì?
Để có thể trả lời được câu hỏi này thì thì cách tốt nhất là sử dụng phép so sánh giữa **DOM Element** vào **React Element**

### 1. DOM Element
**Cú pháp tạo ra 1 DOM Element**
```javascript
const h1DOM = document.createElement('h1')
// Create Attribute Node
h1DOM.className =  'Heading'
h1DOM.id =  'Header-Top'

// Create Text Node
h1DOM.innerText =  'Tiêu để bài viết'
// đưa thẻ h1 vào body
document.body.appendChild(h1DOM)
```
**Cấu trúc của 1 DOM Element** bao gồm 3 thành phần:
1. Element Node: tên thẻ đóng/mở
2. Attribute Node: những cái thuộc tính của thẻ, vd như là class, id và tùy vào từng cập thẻ mà sẽ có những thuộc tính riêng.
3. Text Node: Nội dung nằm ở giữa cặp thẻ <Mở><Đóng>


### 2. React Element
**Cú pháp tạo ra 1 React Element**
```jsx
const title = React.createElement('h1', {}, 'My First React Code');
```

**Cấu trúc của 1 React Element**
```jsx
React.createElement(type, props, children, children_n);
```

method createElement nhận vào 3 tham số:
- param1: type (String/Class/Funtion)
- param2: props là một Object
- param3: childrent/childn là nội dung nằm ở giữ thẻ tag của react element (nó có thê là bất cứu kiểu dữ liệu gì trong JS (Object/Array/Funtion/Class)) 


## Khi nào cần sử dụng React Element ?
- cứ code React là phải dùng RE, thứ 2 là khi sử dụng JSX (chẳng qua bằng babel nó biên dịch sẳn cho chúng ta nên không để ý thôi)


# Level Up Knowledge
## 1. React Element Type
Như đã note ở trên type của RE hỗ trợ (String/Class/Funtion). Câu hỏi dặt ra ở đây là tại sao nó tạo ra thêm Class và Funtion để làm gì ?

- đơn giản là có thêm type Class và Funtion mục đích chính là tạo ra componennt.
- Tư tưởng của react là chia component (từ 1 ứng dụng lớn → bóc tách thành nhiều thành phần nhỏ → rap nó lại thành 1 ứng dụng hoàn chỉnh). Bóc tách nhỏ ra để code clean hơn, ngắn gọn hơn, logic nghiệp vụ cũng được chia rõ ràng hơn, tái sử dụng được component. 
```
Component chính là sức mạnh tối thượng của react → tái sử dụng lại
```
*kể từ khi đẻ ra component thì ai ai cũng xài react, từ người già trẻ em cho tới phụ nữ có thai đều dùng react.*

**Khi nào dùng funtion component, khi nào dùng class component ?**

trước khi có hook.

- function component : chứa UI, chứa chủ yếu là return ra JSX thôi
- class component : chứa đầy đủ tính năng.

khi mà có hook 
- function : hỗ trợ đầy đủ tính năng không khác gì class

**Cú pháp khai báo funtion component**

*Note: quy ước đặt tên component là viết hoa chữ cái đầu <Header />*

**Cú pháp tạo ra fn component**
```JSX
function Header() {
    return (
        <h1 className="Header" id="Title-Header">Tiêu đề bài viết</h1>
    )
}

class Content extends React.Component {
    render() {
        return (
            <div className="Content">Content Here</div>
        )
    }
} 

// Cách sử dụng JSX + Babel
const app = (
    <div className="wrapper">
        <Header />
        <Content />
        <div className="footer">Chân Trang</div>
    </div>
)

// Cách tự Code React Thuần
const appSecond =  React.createElement('div', {},
React.createElement(Header, null, ''),
React.createElement(Content, {}, ''),
React.createElement(div, {className:'footer'}, 'Chân Trang')
)

React.DOM.render(app, document.getElementById('root'))

```


## 2. Props
là 1 cái Object nó chứa những thuộc tính để mô tả cho thằng React Element mà chúng ta tạo ra.

### Đối với React Element
- *Quy ước: 2 props class, for -> chuyển thành className, htmlFor trong React*
- Sử dụng props tương tự như Attribute Node của DOM Element
**VD**
```JSX
// Nhà phát triển React họ thiết để để cho dev dễ sử dụng thôi
const element = <h1 className="Heading">Hello World</h1>

// rồi nó cũng sẽ biên dịch thành
const element = React.createElement('h1',
    {
        // đây là props
        className:"Heading",
        style: {color: 'red'}
    },
    'Hello World'
)
```

### Đối với React Component
- sử dụng props giống như đối số cho Component(Funtion)

**VD**
```JSX
    function Heaader({color, id}){
        return (
            <h1 id={id} style={{color: color}}>Tiêu đề</h1>
        )
    }
```
đù function Heaader là hàm cho nên khi mình thực hiện lời gọi hàm truyền đối số cho nó dược luôn

```JSX
// thay vì hàm bình thường sẽ như vầy:
Header(param1)
// fn component trong react sẽ như này
<Header color='red', id='1' />
```
### Lưu Ý
- đối với cả React Element và React Component có Prop "key" là 1 prop đặc biệt
- Prop cơ bản là đối số của Component -> props có thể là bất cứ kiểu dữ liệu gì
- Sử dụng destructuring (vì khi sử dụng destruc có thể đặt được giá trị default cho khi khởi tạo componnent)

### Cách sử dụng Props
Component có sức mạnh sử dụng đi sử dụng lại còn prop là thứ giúp cho component có tính kế thừa.

-> Nội dung này sẽ nằm bên file JSX.md cho đỡ dài


## 3. Childrent Props
nội dung nằm giữa 1 cặp thẻ mở và đóng, cấu trúc bên trong DOM thì nó là Text Node, bên trong React thì nó là childrent prop


**Ôn tập lại 1 tí kiến thức cũ**

*Text Node Trong DOM*
```html
<h1>Thanh Long</h1>
```

*Childrent Prop Trong JSX*
Khai báo JSX:
```JSX
const h1React = <h1>ThanhLong<h1>
```
Babel sẽ biên dịch thành React:
```javascript
const h1React = React.createElement('h1', null, 'Thanh Long')
```

*Truyền Childrent Prop Trong Component*
Nó cũng tương tự như là truyền chilrent trong JSX thôi
```JSX
function Header(childrent){
    console.log(childrent) // -> Thanh Long
}
<Header>Thanh Long</Header>
```

Vì component được viết trong JSX. Mà JSX có 2 kiểu truyền, nên chilrent prop không chỉ nhận vào kiểu dữ liệu là String mà còn có thể nhận vào kiểu Expression

```jsx
    // UI Component
    function List({ data, children }) {
        return (
            <ul>
                {data.map(car => children(car))}
            </ul>
        )
    }

    // Container
    function App() {
        const cars = ['BMW', 'Honda', 'Mazda']

        return (
            <div id="wrapper">
                <List data={cars}>
                    {item => <li key={item}>{item}</li>}
                </List>
            </div>
        )
    }

```

```
Sau này trong thực tế, childrent Prop còn có thể bọc được cả Component luôn cơ ❤️
```








## Note
để có thể hiểu hết được được nội dung này thì nên đi từng bước sau

*Đầu tiên về mặt lý thuyết thì phải hiểu được:*
1. React Element là gì ?
2. JSX là gì ?
3. Component là gì ?


*Thứ 2 là phần thực hành*

sau khi đã nắm kiến thức rồi thì phải luyện tập cho thuần thục cách sử dụng React

**React Element**
1. Khởi tạo được React Element bằng JS thuần (đơn nhiên là phải thêm thư viện React vào)
2. Khởi tạo React Element trong JSX thì tạo như thế nào ?, nó nhờ thằng gì để khởi tạo nhanh như vậy ?
3. Khởi tạo component (trả về React Element thôi) trong JSX

**Prop**
1. truyền prop bằng phương thức createElement thì truyền theo kiểu nào
2. truyền prop bằng jsx thì truyền như thế nào nè.
3. truyền prop vào bên trong component thì truyền và nhận như thế nào nè.

**Childrent Prop**

Childrent thì cũng tương tự như thằng trên
1. truyền chilrent prop bằng phương thức createElement (Khởi tạo React Element bằng JS thuần)
2. truyền chilrent prop thông qua JSX (tương tự như html thôi không có gì khó)
3. truyền chilrent prop vào bên trong component thì truyền và nhận như thế nào.
