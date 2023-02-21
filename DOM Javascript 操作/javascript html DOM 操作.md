# 選取特定 DOM 節點

```js
querySelector('css 選擇器') // 當有多個相同節點時候會回傳第一個選到的節點
// ex.
let item = querySelector('.my-class-name')

querySelectorAll('css 選擇器') // 回傳唯讀陣列資料，只能對陣列作唯讀操作
// ex.
let item2 = querySelectorAll('li')

// 較舊的 javascript 語法
getElementBy* // 系列
// ex.
getElementById('id 名稱')

getElementsBy*  // 系列 // 同 querySelectorAll ，回傳唯讀陣列
```

# 創造 DOM 操作

基本語法
`document.createElement(tagName)`

```js
let h1 = document.createElement('h1')  // 沒有特殊意義的話可以直接用 html 元素名稱當變數名稱

```