[Phần 1] Tạo dự án ReactJS với Webpack và Babel
Sơn Đặng
Sơn Đặng

một năm trước · 12 phút đọc

Chào mọi người 🤗🤗

Hôm nay mình có quay một video trong khóa học ReactJS là “Tạo dự án ReactJS với Webpack và Babel”. Mình làm video này với mong muốn chia sẻ cho các bạn có thể hình dung ra dự án được tạo bởi “create-react-app” được xây dựng như thế nào. Các bạn có thể xem thêm video hướng dẫn ở đây nhé.

Click vào hình ảnh này để mở video nhé anh em!

image.png

👉👉 Đăng ký khóa ReactJS miễn phí của mình tại: https://fullstack.edu.vn/courses/reactjs

Bắt đầu
Nếu anh em chưa cài đặt NodeJS thì hãy xem video này trước nhé: https://www.youtube.com/watch?v=ysjJlvQ3FFc

1. Cấu trúc dự án
react-webpack # thư mục gốc
    | src # thư mục chứa source code chính
        | components # thư mục chứa components
        | index.js # File khởi tạo, render App vào #root
    | public
        | index.html # HTML page, nơi chứa #root element
2. Khởi tạo dự án
Trong hướng dẫn này mình sử dụng VSCode IDE. Các bạn chọn File --> Add Folder to Workspace.

image.png

Tiếp theo, bạn tự tạo một thư mục mới tên là react-webpack sau đó chọn thư mục đó và click vào Add.

image.png

3. Mở cửa sổ Terminal
image.png

Sau đó chạy dòng lệnh sau để khởi tạo dự án với Node:

npm init
Gõ npm init vào Terminal sau đó nhấn phím Enter để chạy dòng lệnh.

Kết quả trông như sau:

image.png

Khi đó trong Terminal của bạn sẽ yêu cầu nhập một số thông tin để mô tả cho dự án của bạn. Bạn có thể nhập thông tin vào nếu muốn, trong hướng dẫn này mình để mặc định nên Enter hết.

image.png

Sau khi khởi tạo dự án thành công bạn sẽ thấy file package.json được tạo trong thư mục dự án.

image.png

package.json là file chứa thông tin dự án như: tên dự án, phiên bản, mô tả, các thư viện được sử dụng trong dự án, v.v

4. Cài đặt webpack
Chạy lệnh sau để cài đặt 2 thư viện là webpack và webpack-cli:

npm install webpack webpack-cli --save-dev
--save-dev để đánh dấu 2 thư viện này chỉ dùng trong khi phát triển, khi dự án đẩy lên production sẽ không có các thư viện này.

Sau khi lệnh trên chạy xong, webpack và webpack-cli sẽ được thêm vào devDependencies:

image.png

devDependencies chứa các thư viện được cài đặt với flag --save-dev.

5. Cài đặt React và React-DOM
Chạy lệnh sau:

npm install react@17.0.2 react-dom@17.0.2 --save
--save để thêm các thư viện được cài vào phần dependencies trong package.json. Đây là các thư viện được sử dụng trong dự án, bao gồm cả development & production. Từ phiên bản NPM 5 trở đi thì --save được thêm vào mặc định, nếu bạn đang sử dụng NPM >= 5 thì có thể không cần --save.

Sau khi cài đặt thành công:

image.png

6. Cài đặt Babel
Chạy:

npm install @babel/core babel-loader @babel/preset-env @babel/preset-react --save-dev
babel-core: Chuyển đổi ES6 về ES5
babel-loader: Cho phép chuyển các files Javascript sử dụng Babel & Webpack
babel-preset-env: Cài đặt sẵn giúp bạn sử dụng Javascript mới nhất trên nhiều môi trường khác nhau (nhiều trình duyệt khác nhau). Gói này đơn giản là support truyển đổi ES6, ES7, ES8, ES… về ES5.
babel-preset-react: Hỗ trợ chuyển đổi JSX về Javascript
Sau khi cài đặt xong:

image.png

7. Tạo index.html
Tại thư mục gốc của dự án hãy tạo file public/index.html và thêm vào cấu trúc HTML mặc định như sau:

Screenshot at Sep 29 10-07-53.png

Thêm nhanh cấu trúc HTML mặc định với VSCode, gõ ! và nhấn Tab.

Tiếp theo, hãy tạo #root element:

image.png

8. Tạo file index.js
Tại thư mục gốc của dự án hãy tạo file src/index.js và thêm vào nội dung sau:

import React from 'react' // nạp thư viện react
import ReactDOM from 'react-dom' // nạp thư viện react-dom

// Tạo component App
function App() {
    return (
        <div>
            <h1>Xin chào anh em F8!</h1>
        </div>
    )
}

// Render component App vào #root element
ReactDOM.render(<App />, document.getElementById('root'))

Cấu hình webpack
1. Cài đặt CSS-Loader và Style-Loader
2 thư viện này giúp webpack có thể tải file .css dưới dạng module.

Chạy:

npm install css-loader style-loader --save-dev
2. Tạo webpack.config.js
Tạo file webpack.config.js tại thư mục gốc của dự án với nội dung sau:

const path = require("path");

module.exports = {
  entry: "./src/index.js", // Dẫn tới file index.js ta đã tạo
  output: {
    path: path.join(__dirname, "/build"), // Thư mục chứa file được build ra
    filename: "bundle.js" // Tên file được build ra
  },
  module: {
    rules: [
      {
        test: /\.js$/, // Sẽ sử dụng babel-loader cho những file .js
        exclude: /node_modules/, // Loại trừ thư mục node_modules
        use: ["babel-loader"]
      },
      {
        test: /\.css$/, // Sử dụng style-loader, css-loader cho file .css
        use: ["style-loader", "css-loader"]
      }
    ]
  },
  // Chứa các plugins sẽ cài đặt trong tương lai
  plugins: [
  ]
};
Anh em lưu ý đặt file webpack.config.js ở thư mục gốc, ngang hàng với package.json nhé:

image.png

3. Tạo file .babelrc
File .babelrc dùng để cấu hình cho thư viện Babel.

Lưu ý tên file bắt đầu bằng dấu .

Tại thư mục gốc dự án tạo file .babelrc và thêm nội dung sau:

{
    "presets": [
        "@babel/preset-env",
        "@babel/preset-react"
    ]
}
Cài đặt này để cho Babel biết sử dụng preset-env và preset-react trong việc hỗ trợ chuyển đổi mã.

Đây là ảnh chụp file mình tạo, các bạn so sánh xem giống chưa nhé.

image.png

4. Thêm scripts cho dự án
Tại package.json thêm nội dung sau:

"scripts": {
    ...
    "start": "webpack --mode development --watch",
    "build": "webpack --mode production"
}
Bạn làm đúng trông nó sẽ như thế này:

image.png

Cấu hình scripts này để bạn có thể chạy lệnh tương ứng qua Terminal. Ví dụ: npm start sẽ chạy lệnh ở phần start, npm run build sẽ chạy lệnh ở phần build. Trừ start ra thì bạn cần thêm từ run nữa nhé.

Chạy dự án
Qua những bước trên ta đã hoàn thành các cấu hình cơ bản rồi nhé, giờ ta có thể chạy dự án lên.

1. Biên dịch code với Webpack
Tại Ternimal hãy chạy:

npm start
Lệnh này sẽ chạy webpack --mode development --watch mà ta đã cấu hình trong package.json, --watch để webpack sẽ luôn lắng nghe thay đổi, khi file thay đổi webpack sẽ thực hiện biên dịch nhé.

Kết quả trông như sau anh em nhé:

image.png

Có file mới được tạo ra trong build/bundle.js (vì ta đã cấu hình như vậy trong webpack.config.js)
Nội dung trong build/bundle.js chính là code của file src/index.js đã được Babel chuyển đổi, bạn có thể mở ra để quan sát.
Bạn sẽ thấy có rất nhiều code trong này vì nó bao gồm cả code của những thư viện chúng ta đã import như: react và react-dom.

image.png

2. Chạy dự án với Live Server (VSCode)
Phần này chúng ta làm 2 việc:

Thêm thẻ script link tới file build/bundle.js
Chạy dự án với Live Server
image.png

Thêm nội dung sau vào vị trí như ảnh mô tả ở trên:

<script src="../build/bundle.js"></script>
Sau đó chạy Live Server và đạt được kết quả như sau là bạn đã làm đúng nhé:

image.png

Tiếp theo chúng ta sẽ test xem webpack có đang lắng nghe thay đổi file không nhé (vì trong lệnh start chúng ta có sử dụng cờ --watch mà).

Các bạn lưu ý không tắt Terminal đi nhé. Chạy dự án theo cách này bạn phải luôn dữ cho Ternimal chạy.

Thử đi sửa nội dung file src/index.js:

image.png

Nội dung website trên trình duyệt cũng thay đổi theo:

image.png

Nhờ Live Server mà ta không cần F5 trang web.

Okie, tới đây các bạn hình dung flow chạy nó như này:
Webpack khi được chạy sẽ lắng nghe thay đổi của file
Khi file thay đổi Webpack sẽ biên dịch và update vào build/bundle.js
Website được chạy sẽ link file script từ build/bundle.js
Live Server chạy web và lắng nghe thay đổi của build/bundle.js để F5 lại trang
Cài đặt html-webpack-plugin
Tại sao phải cài thằng này làm gì? Ở phần trước các bạn có nhớ ta phải tự đi thêm thằng này vào index.html không?

image.png

Làm như này khá thủ công, chúng ta có thể tự động hóa nó vì rõ ràng ta đã mất công cấu hình trong Webpack rồi mà.

Chỗ này này:

image.png

Chính vì vậy html-webpack-plugin ra đời để giúp chúng ta “nhờ” Webpack sau khi build ra build/bundle.js thì thêm hộ chúng ta vào public/index.html luôn.

Cài đặt:

npm install html-webpack-plugin --save-dev
Nếu thấy Ternimal đang được dùng để chạy npm start rồi thì bạn có 2 cách sau:

Mở Teminal mới để chạy (không thoát Terminal cũ)
Đóng Terminal hiện tại (Click vào Terminal rồi nhấn Ctrl + C), chạy lệnh cài đặt, chạy lại npm start
Cài thành công sẽ trông như này:

image.png

Tiếp theo ta đi update cấu hình Webpack để thêm html-webpack-plugin vào dự án.

Tại webpack.config.js hãy thêm:

...
const HtmlWebpackPlugin = require("html-webpack-plugin");

module.exports = {
  ...
  // Chứa các plugins sẽ cài đặt trong tương lai
  plugins: [
    new HtmlWebpackPlugin({
      template: "./public/index.html"
    })
  ]
};
Làm đúng trông sẽ như sau:

image.png

Đi xóa bỏ phần khoanh đỏ khỏi file public/index.html:

image.png

Nhấn Ctrl + C tại Terminal và chạy lại lệnh npm start để thấy kết quả!

image.png

Thuộc tính defer trong thẻ script để báo với trình duyệt rằng hãy thực thi code Javascript sau khi HTML đã được parse xong. Điều này giúp đặt được thẻ script trên thẻ head mà code Javascript vẫn có thể truy cập được HTML DOM viết dưới body.

Cài đặt webpack-dev-server
Đây là bước cuối cùng của hướng dẫn này.

Ở phần trước chúng ta vẫn sử dụng VSCode Live Server để chạy web, trong thực tế khi ta đã cài đặt Node và sử dụng Webpack thì ta sẽ không cần dùng tới Live Server. Bản thân Node có thể start được web server (máy chủ web) rồi, giờ ta sẽ đi cài thêm webpack-dev-server để có được một web server kết hợp được Webpack và Node nhé.

Chạy:

npm install webpack-dev-server --save-dev
Sau khi cài đặt thành công:

image.png

Sửa lại cấu hình scripts trong package.json:

"scripts": {
    ...
    "start": "webpack-dev-server --mode development --open --hot",
    ...
}
Làm đúng trông sẽ như sau:

image.png

Tắt bỏ Live Server, nhấn Ctrl + C tại Terminal và chạy lại lệnh npm start để thấy kết quả!

Thành quả
Sau khi chạy npm start:

image.png

Trang web tự động được mở trên trình duyệt:

image.png

Thử đi sửa nội dung file src/index.js xem sao?

image.png

Hết phần 1
Đợi mình ra phần 2 nữa nhé, phần 2 sẽ hướng dẫn anh em cài thêm SASS, chia component và xây dựng một ứng dụng nhỏ xinh gì đó nhé 😍😍😍

Tham khảo:
https://webpack.js.org/
https://webpack.js.org/plugins/html-webpack-plugin/
https://webpack.js.org/configuration/dev-server/
https://github.com/sondnpt00343/react-webpack (Source code trên Github nhé 😍)
