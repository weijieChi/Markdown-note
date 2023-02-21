    * 瞭解 block、inline 與 inline-block 之間的差異
    * 能夠使用 display: none 來隱藏元素  

    另外還有 list-item 屬性是 li 元素特有的，基本上跟 block 差不多，唯一的差異是前面會有項目符號 (bullet point)
# display 預設屬性
所有的 HTML 都有預設 `display` 屬性，通常是 `block` 或是 `inline`

# 各 display 特性

## block
為區塊元素預設值，特性是會占滿容器(container)一整行空間，可以設定 `width:` 跟 `hight:`

## inline
為內行元素預設值，特性是會跟文字和同樣是 inline 元素相鄰排列，不會佔滿整行， `width:` 跟 `hight:` 會無效，大小由內容 (conten) 決定

## inline-block
基本上跟 inline 特性差不多，唯一的差別是可以設定 `width:` 跟 `hight:`

## `display: none;`
可以將元素隱藏起來，通常會搭配 javascript 改變 html 跟 css 樣式一起使用

相關的 HTML 元素 block 屬性預設值可以到 [這個網站查看](https://htmlreference.io/)

在瀏覽器 devtools 的 `style` 中 `user agent stylesheet` 欄位代表瀏覽器預設 css 樣式