# Dự án Shopee Clone Typescript

## Chức năng trong dự án

- Authentication module: Quản lý bằng JWT

  - Đăng ký
  - Đăng nhập
  - Đăng xuất

- Trang danh sách sản phẩm:

  - Có phân trang
  - Sort (sắp xếp) theo từng thuộc tính sản phẩm
  - filter nâng cao theo từng thuộc tính sản phẩm
  - Tìm kiếm sản phẩm

- Trang chi tiết sản phẩm:

  - Hiển thị thông tin chi tiết
  - Ảnh hiển thị theo slider + hover zoom effect
  - Mô tả thì hiển thị rich text dạng WYSIWYG HTML
  - Có chức năng mua hàng

- Giỏ hàng

  - Quản lý đơn hàng: Thêm, sửa, xóa sản phẩm
  - Mua hàng

- Quản lý Profile khách hàng

  - Update thông tin cá nhân
  - Upload Avatar
  - Đổi mật khẩu
  - Xem tình trạng đơn hàng

## Công nghệ sử dụng

- UI / CSS Library: Tailwindcss + HeadlessUI
- State Management: React Query cho async state và React Context cho state thường
- Form Management: React Hook Form
- Router: React Router
- Build tool: Vite
- API: Rest API dựa trên server mình cung cấp sẵn
- Hỗ trợ đa ngôn ngữ với react.i18next
- Hỗ trợ SEO với React Helmet
- Mô hình hóa các component với story book
- Unit Test
- Và còn nhiều thứ nữa khi làm chúng ta sẽ áp dụng...

## Cài đặt package cho dự án Vite React TS

### Cài các depedency

### Bộ ESLint và Prettier trước

> Chúng ta sẽ cài hơi nhiều package 1 tí vì chúng ta setup từ đầu, còn Create React App setup sẵn 1 số thứ về ESLint rồi.

Dưới đây là những depedency mà chúng ta cần cài

- ESLint: linter (bộ kiểm tra lỗi) chính

- Prettier: code formatter chính

- @typescript-eslint/eslint-plugin: ESLint plugin cung cấp các rule cho Typescript

- @typescript-eslint/parser: Parser cho phép ESLint kiểm tra lỗi Typescript.

- eslint-config-prettier: Bộ config ESLint để vô hiệu hóa các rule của ESLint mà xung đột với Prettier.

- eslint-plugin-import: Để ESLint hiểu về cú pháp `import...` trong source code.

- eslint-plugin-jsx-a11y: Kiểm tra các vấn đề liên quan đến accessiblity (Tính thân thiện website, ví dụ cho thiết bị máy đọc sách).

- eslint-plugin-react: Các rule ESLint cho React

- eslint-plugin-prettier: Dùng thêm 1 số rule Prettier cho ESLint

- prettier-plugin-tailwindcss: Sắp xếp class tailwindcss

- eslint-plugin-react-hooks: ESLint cho React hook

Chạy câu lệnh dưới đây

```bash
yarn add eslint prettier @typescript-eslint/eslint-plugin @typescript-eslint/parser eslint-config-prettier eslint-plugin-import eslint-plugin-jsx-a11y eslint-plugin-react eslint-plugin-prettier prettier-plugin-tailwindcss eslint-plugin-react-hooks -D
```

Cấu hình ESLint

Tạo file `.eslintrc.cjs` tại thư mục root

```js
/* eslint-disable @typescript-eslint/no-var-requires */
const path = require('path')

module.exports = {
  extends: [
    // Chúng ta sẽ dùng các rule mặc định từ các plugin mà chúng ta đã cài.
    'eslint:recommended',
    'plugin:react/recommended',
    'plugin:react-hooks/recommended',
    'plugin:import/recommended',
    'plugin:import/typescript',
    'plugin:jsx-a11y/recommended',
    'plugin:@typescript-eslint/recommended',
    // Disable các rule mà eslint xung đột với prettier.
    // Để cái này ở dưới để nó override các rule phía trên!.
    'eslint-config-prettier',
    'prettier'
  ],
  plugins: ['prettier'],
  settings: {
    react: {
      // Nói eslint-plugin-react tự động biết version của React.
      version: 'detect'
    },
    // Nói ESLint cách xử lý các import
    'import/resolver': {
      node: {
        paths: [path.resolve(__dirname, '')],
        extensions: ['.js', '.jsx', '.ts', '.tsx']
      }
    }
  },
  env: {
    node: true
  },
  rules: {
    // Tắt rule yêu cầu import React trong file jsx
    'react/react-in-jsx-scope': 'off',
    // Cảnh báo khi thẻ <a target='_blank'> mà không có rel="noreferrer"
    'react/jsx-no-target-blank': 'warn',
    // Tăng cường một số rule prettier (copy từ file .prettierrc qua)
    'prettier/prettier': [
      'warn',
      {
        arrowParens: 'always',
        semi: false,
        trailingComma: 'none',
        tabWidth: 2,
        endOfLine: 'auto',
        useTabs: false,
        singleQuote: true,
        printWidth: 120,
        jsxSingleQuote: true
      }
    ]
  }
}
```

Tạo file `.eslintignore`

```json
node_modules/
dist/
```

Tạo file `.prettierrc`

```json
{
  "arrowParens": "always",
  "semi": false,
  "trailingComma": "none",
  "tabWidth": 2,
  "endOfLine": "auto",
  "useTabs": false,
  "singleQuote": true,
  "printWidth": 120,
  "jsxSingleQuote": true
}
```

Tạo file `.prettierignore`

```json
node_modules/
dist/
```

Thêm script mới vào `package.json`

```json
  "scripts": {
    ...
    "lint": "eslint --ext ts,tsx src/",
    "lint:fix": "eslint --fix --ext ts,tsx src/",
    "prettier": "prettier --check \"src/**/(*.tsx|*.ts|*.css|*.scss)\"",
    "prettier:fix": "prettier --write \"src/**/(*.tsx|*.ts|*.css|*.scss)\""
  },
```

### Cài editorconfig

Tạo file `.editorconfig` ở thư mục root

```EditorConfig
[*]
indent_size = 2
indent_style = space
```

### Cấu hình tsconfig.json

Set `"target": "ES2015"` và `"baseUrl": "."` trong `compilerOptions`

### Cài tailwindcss

Cài các package dưới đây: Tham khảo [https://tailwindcss.com/docs/guides/vite](https://tailwindcss.com/docs/guides/vite)

```bash
yarn add -D tailwindcss postcss autoprefixer
npx tailwindcss init -p
```

Cấu hình file config

```js
/** @type {import('tailwindcss').Config} */
module.exports = {
  content: ['./index.html', './src/**/*.{js,ts,jsx,tsx}'],
  theme: {
    extend: {}
  },
  plugins: []
}
```

Thêm vào file `src/index.css`

```css
@tailwind base;
@tailwind components;
@tailwind utilities;
```

### Cấu hình vite config

Cài package `@types/node` để sử dụng node js trong file ts không bị lỗi

```bash
yarn add -D @types/node
```

file `vite.config.ts`

```ts
import { defineConfig } from 'vite'
import react from '@vitejs/plugin-react'
import path from 'path'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [react()],
  server: {
    port: 3000
  },
  css: {
    devSourcemap: true
  },
  resolve: {
    alias: {
      src: path.resolve(__dirname, './src')
    }
  }
})
```

### Cài extension và setup VS Code

Các Extension nên cài

- ESLint

- Prettier - Code formatter

- Tailwindcss

- EditorConfig for VS Code

Cấu hình VS Code

- Bật Format On Save
- Chọn Default Formatter là Prettier

> Có 3 môi trường khi làm việc
>
> 1. Môi trường VS Code, khi chúng ta đưa chuột vào click thì chạy đến đúng file
> 2. Môi trường ES Lint
> 3. Môi trường Terminal\*

## Ghi chú code

Code xóa các ký tự đặc biệt trên bàn phím

```ts
export const removeSpecialCharacter = (str: string) =>
  // eslint-disable-next-line no-useless-escape
  str.replace(
    /!|@|%|\^|\*|\(|\)|\+|\=|\<|\>|\?|\/|,|\.|\:|\;|\'|\"|\&|\#|\[|\]|~|\$|_|`|-|{|}|\||\\/g,
    ''
  )
```

Sữa lỗi Tailwindcss Extension không gợi ý class

Các bạn thêm đoạn code này vào `settings.json` của VS Code

```json
{
  //...
  "tailwindCSS.experimental.classRegex": ["[a-zA-Z]*class[a-zA-Z]*='([^']+)'"]
}
```


# Thông tin API

URL: `https://api-ecom.duthanhduoc.com/`
Đối với các route cần xác thực => Gửi token lên bằng headers với key là `authorization`. Token phải bắt đầu bằng 'Bearer '

## Format trả về

Là một object

```ts
interface Response {
  message: string;
  data?: any;
}
```

Ví dụ

```json
{
  "message": "Lấy sản phẩm thành công",
  "data": {
    "_id": "60afb2c76ef5b902180aacba",
    "images": [
      "https://api-ecom.duthanhduoc.com/images/bbea6d3e-e5b1-494f-ab16-02eece816d50.jpg"
    ],
    "price": 3190000,
    "rating": 4.6,
    "price_before_discount": 3990000,
    "quantity": 138,
    "sold": 1200,
    "view": 696,
    "name": "Điện Thoại Vsmart Active 3 6GB/64GB - Hàng Chính Hãng",
    "description": "",
    "category": "60afafe76ef5b902180aacb5",
    "image": "https://api-ecom.duthanhduoc.com/images/bbea6d3e-e5b1-494f-ab16-02eece816d50.jpg",
    "createdAt": "2021-05-27T14:55:03.113Z",
    "updatedAt": "2021-06-12T14:22:55.871Z"
  }
}
```

## Format lỗi

### Trong trường hợp lỗi 422 (thường do form) hoặc lỗi do truyền query / param bị sai

Ví dụ đăng ký email đã tồn tại

```json
{
  "message": "Lỗi",
  "data": {
    "email": "Email đã tồn tại"
  }
}
```

### Trong trường hợp lỗi còn lại

```json
{
  "message": "Lỗi do abcxyz"
}
```

## Register: `/register`

Method: POST
body

```json
{
  "email": "user2@gmail.com",
  "password": "123456"
}
```

Rules

- email: required, length: 5-160, isEmail
- password: required, length: 6-160

Response

```json
{
  "message": "Đăng ký thành công",
  "data": {
    "access_token": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InVzZXIxNUBnbWFpbC5jb20iLCJpZCI6IjYwYzZmNGViNGVhMWRlMzg5ZjM1NjA1YiIsInJvbGVzIjpbIlVzZXIiXSwiY3JlYXRlZF9hdCI6IjIwMjEtMDYtMTRUMDY6MTk6MjMuNzQ5WiIsImlhdCI6MTYyMzY1MTU2MywiZXhwIjoxNjI0MjU2MzYzfQ.WbNgnd4cewdDNpx-ZLebk1kLgogLctBqgh9fc9Mb3yg",
    "expires": "7d",
    "user": {
      "roles": ["User"],
      "_id": "60c6f4eb4ea1de389f35605b",
      "email": "user15@gmail.com",
      "createdAt": "2021-06-14T06:19:23.703Z",
      "updatedAt": "2021-06-14T06:19:23.703Z",
      "__v": 0
    }
  }
}
```

## Login: `/login`

Method: POST
body

```json
{
  "email": "user2@gmail.com",
  "password": "123456"
}
```

Rules

- email: required, length: 5-160, isEmail
- password: required, length: 6-160

Response

```json
{
  "message": "Đăng nhập thành công",
  "data": {
    "access_token": "Bearer eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJpZCI6IjYwOThmNWI1MTY5MDU1MzZlODE4ZjhjYyIsImVtYWlsIjoiYWRtaW5AZ21haWwuY29tIiwicm9sZXMiOlsiVXNlciIsIkFkbWluIl0sImNyZWF0ZWRfYXQiOiIyMDIxLTA2LTE0VDA4OjA4OjI4LjQ5NVoiLCJpYXQiOjE2MjM2NTgxMDgsImV4cCI6MTYyNDI2MjkwOH0.8YITBWt6SXikoaBHf-SlOh_h7ii0UgwY_5-bjCirY",
    "expires": "7d",
    "user": {
      "_id": "6098f5b516905536e818f8cc",
      "roles": ["User"],
      "email": "user2@gmail.com",
      "name": "Real user",
      "date_of_birth": null,
      "address": "",
      "phone": "",
      "createdAt": "2021-05-10T08:58:29.081Z",
      "updatedAt": "2021-05-10T08:58:29.081Z",
      "__v": 0
    }
  }
}
```

## Logout: `/logout`

Method: POST

## Read me: `/me`

Method: GET

Response

```json
{
  "message": "Lấy người dùng thành công",
  "data": {
    "_id": "6098f5b516905536e818f8cc",
    "roles": ["User"],
    "email": "user@gmail.com",
    "name": "Real",
    "date_of_birth": null,
    "address": "",
    "phone": "",
    "createdAt": "2021-05-10T08:58:29.081Z",
    "updatedAt": "2021-05-10T08:58:29.081Z"
  }
}
```

## Read Products: `/products`

Ví du: `products?page=1&limit=30`
Method: GET

Query Params:

- `page`: number. Số trang. Mặc định là 1
- `limit`: number. Số product trên 1 trang. Mặc định là 30
- `order`: 'desc' || 'asc'. Sắp xếp theo thứ tự. Mặc định là 'desc'
- `sort_by`: 'createdAt' || 'view' || 'sold' || 'price'. Sắp xếp theo trường. Mặc định là 'createdAt'.
- `category`: categoryId. Lọc sản phẩm theo category
- `exclude`: productId. Loại trừ sản phẩm nào đó
- `rating_filter`: number. Lọc sản phẩm có số sao lớn hơn hoặc bằng rating_filter
- `price_max`: number. Giá cao nhất
- `price_min`: number. Giá thấp nhất
- `name`: string. Tên sản phẩm (lưu ý Tên sản phẩm tiếng Việt phải gõ đầy đủ dấu)

Response

```json
{
  "message": "Lấy các sản phẩm thành công",
  "data": {
    "products": [],
    "pagination": {
      "page": 1,
      "limit": 30,
      "page_size": 2
    }
  }
}
```

## Read Product Detail: `/products/productId`

Method: GET

## Read Categories: `/categories`

Method: GET

```json
{
  "message": "Lấy categories thành công",
  "data": [
    {
      "_id": "60aba4e24efcc70f8892e1c6",
      "name": "Áo thun"
    },
    {
      "_id": "60afacca6ef5b902180aacaf",
      "name": "Đồng hồ"
    },
    {
      "_id": "60afafe76ef5b902180aacb5",
      "name": "Điện thoại"
    }
  ]
}
```

## Add To Cart: `/purchases/add-to-cart`

Method: POST

Body

```json
{
  "product_id": "60afb1c56ef5b902180aacb8",
  "buy_count": 3
}
```

## Read Purchases: `/purchases`

Method: GET
Query Params:
`status`: Trạng thái đơn hàng

Thông tin `status`:

- -1: Sản phẩm đang trong giỏ hàng
- 0: Tất cả sản phâm
- 1: Sản phẩm đang đợi xác nhận từ chủ shop
- 2: Sản phẩm đang được lấy hàng
- 3: Sản phẩm đang vận chuyển
- 4: San phẩm đã được giao
- 5: Sản phẩm đã bị hủy

## Update purchase: `/purchases/update-purchase`

Method: PUT
Body:

```json
{
  "product_id": "60afb1c56ef5b902180aacb8",
  "buy_count": 3
}
```

## Delete purchases: `/purchases`

Method: DELETE
body: mảng các `purchase_id`

```json
["purchase_id"]
```

## Buy purchases: `/purchases/buy-products`

Method: POST
body: Mảng các object

```json
[{ "product_id": "60afb1c56ef5b902180aacb8", "buy_count": 2 }]
```

## Update me: `/user`

Method: PUT
Body:

```json
{
  "address": "Việt Nam",
  "date_of_birth": "1907-02-18T17:17:56.000Z",
  "name": "Dư Thanh Được",
  "phone": "04511414",
  "avatar": "URL Avatar",
  "password": "Mật khẩu cũ",
  "new_password": "Mật khẩu mới"
}
```

Rules

- name: string, maxLength = 160
- phone: string, maxLength = 20
- address: string, maxLength = 160
- date_of_birth: string, ISO8601
- avatar: string, maxLength 1000
- password: string, length 6-160
- new_password: string, length 6-160

## Upload Avatar: `/user/upload-avatar`

Method: POST

Header: `'Content-Type': 'multipart/form-data'`

Body: FormData với item có key là `image`

Rules

- Ảnh phải bé hơn 1MB
- Phải là định dạng ảnh

Lưu ý:

- Có thể lỗi trả về dạng 422 với key là `image` hoặc không có gì cả
- Server không đảm bảo ảnh của bạn sẽ tồn tại mãi mãi trên server. Có thể tồn tài vài ngày hoặc lâu hơn.
- Vì là upload ảnh nên hạn chế spam và upload quá nhiều ảnh dẫn đến server quá tải ảnh hưởng đến các bạn khác.

## Custom Expire Access Token - Refresh Token

Áp dụng cho `/login` và `/register`

Chỉ cần truyền lên header

- `expire-access-token`: number => số giây hết hạn của access token
- `expire-refresh-token`: number => số giây hết hạn của refresh token

## Refresh Token: `/refresh-access-token`

Method: POST

Body:

```json
{
  "refresh_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJlbWFpbCI6InVzZXIxNUBnbWFpbC5jb20iLCJpZCI6IjYwYzZmNGViNGVhMWRlMzg5ZjM1NjA1YiIsInJvbGVzIjpbIlVzZXIiXSwiY3JlYXRlZF9hdCI6IjIwMjEtMDYtMTRUMDY6MTk6MjMuNzQ5WiIsImlhdCI6MTYyMzY1MTU2MywiZXhwIjoxNjI0MjU2MzYzfQ.WbNgnd4cewdDNpx-ZLebk1kLgogLctBqgh9fc9Mb3yg"
}
```
