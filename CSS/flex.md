# flex
## Reference：

[深入解析 CSS Flexbox](http://www.oxxostudio.tw/articles/201501/css-flexbox.html)  

[Flexbox Froggy](http://flexboxfroggy.com/)

[A Complete Guide to Flexbox](https://css-tricks.com/snippets/css/a-guide-to-flexbox/)

http://zhoon.github.io/css3/2014/08/23/flex.html

https://segmentfault.com/a/1190000006741711

https://segmentfault.com/a/1190000005006056

https://scotch.io/tutorials/a-visual-guide-to-css3-flexbox-properties

------

## Properties for the Parent：

### display

This defines a flex container; inline or block depending on the given value. It enables a flex context for all its direct children.

```css
.container{
    display: flex; /* or inline-flex */
    }
```
### flex-direcction 物件排列方向

![img](https://css-tricks.com/wp-content/uploads/2014/05/flex-direction1.svg)

```css
.container{
  flex-direction: row | row-reverse | column | column-reverse
}
```

- row: Items are placed the same as the text direction.
- row-reverse: Items are placed opposite to the text direction.
- column: Items are placed top to bottom.
- column-reverse: Items are placed bottom to top.



### flex-wrap 

![img](https://css-tricks.com/wp-content/uploads/2014/05/flex-wrap.svg)

By default, flex items will all try to fit onto one line. You can change that and allow the items to wrap as needed with this property. Direction also plays a role here, determining the direction new lines are stacked in.

```css
.container{
  flex-wrap: nowrap | wrap | wrap-reverse;
}
```

- `nowrap` (default): single-line / left to right in `ltr`; right to left in `rtl`
- `wrap`: multi-line / left to right in `ltr`; right to left in `rtl`
- `wrap-reverse`: multi-line / right to left in `ltr`; left to right in `rtl`

### flex-flow

This is a shorthand `flex-direction` and `flex-wrap`properties, which together define the flex container's main and cross axes. Default is `row nowrap`.

### justy-content 操縱物件的水平方向

![img](https://css-tricks.com/wp-content/uploads/2013/04/justify-content.svg)



- flex-start: Items align to the left side of the container.

- flex-end: Items align to the right side of the container.

- center: Items align at the center of the container.

- space-between: Items display with equal spacing between them.

- space-around: Items display with equal spacing around them.

  ​

### property: align-items 操縱物件的垂直方向

![img](https://css-tricks.com/wp-content/uploads/2014/05/align-items.svg)

- flex-start: Items align to the top of the container.
- flex-end: Items align to the bottom of the container.
- center: Items align at the vertical center of the container.
- baseline: Items display at the baseline of the container.
- stretch: Items are stretched to fit the container.


### align-content

![img](https://css-tricks.com/wp-content/uploads/2013/04/align-content.svg)

- `flex-start`: lines packed to the start of the container
- `flex-end`: lines packed to the end of the container
- `center`: lines packed to the center of the container
- `space-between`: lines evenly distributed; the first line is at the start of the container while the last one is at the end
- `space-around`: lines evenly distributed with equal space around each line
- `stretch` (default): lines stretch to take up the remaining space

------

## Properties for the Children

### property: order 用數值表示物件順序 (用在單一物件上)

By default, items have a value of 0, but we can use this property to set it to a positive or negative integer value. 預設是0，數字越小越前面。

![img](https://css-tricks.com/wp-content/uploads/2013/04/order-2.svg)

### property: flex = flex-grow, flex-shrink, flex-basis

The `flex` property is a shorthand for the flex-grow, flex-shrink, and the flex-basis properties.

`Default value:  0 1 auto` 

flex 用來設定子元素如何瓜分父元素的**剩餘空間**，而後面三個是 property: flex的 3個子屬性，需要一起理解。

什麼是剩餘空間呢？具備 flex環境的父容器，通常是有一條主軸和一條側軸，默認情況下主軸就是水平從左向右的，側軸是垂直從上到下的（類似書寫模式）。 剩餘空間就是父容器在主軸的方向上還有多少可用的空間。比如有一網頁結構：

```html
div.container
	span.A
	span.B
	span.C
```

那剩餘空間就是 div.container.width - ( span.A.width + span.B.width + span.C.width) 

方便理解，假設實際數字：

| 元素   | div.container | span.A | span.B | span.C |
| ---- | ------------- | ------ | ------ | ------ |
| 寬度   | 100px         | 20px   | 20px   | 20px   |

則剩餘空間為：100 - ( 20 + 20 + 20 ) = 40px

flex 範例：

```css
.item{
  flex: 2 2 20rem;
  /* 上面一行的意思等同於下面三行 */
  flex-grow: 2;
  flex-shrink: 2;
  flex-basis: 20rem;
}
```



#### flex-grow 物件放大，爭搶剩餘空間比例 

![img](https://css-tricks.com/wp-content/uploads/2014/05/flex-grow.svg)

* 當**剩餘空間 > 0** 時發揮效果。

* 預設值為 0，代表子元素不爭搶剩餘空間。

* Flex-grow計算邏輯-橫向展開

  以下計算步驟只適用於當橫向展開時 flexbox容器寬度大於所有子元素的寬度時：

  1.  首先算出flexbox容器內所有子元素的原始寬度總和initial_space。


  2.  用flexbox容器的總寬度減去initial_space，得到flexbox容器內剩餘空間remained_space。


  3.  獲取flexbox容器中有flex-grow屬性的子元素，算出flex-grow的總和grow_total。


  4.  Flew-grow=0的元素默認按原大小顯示。


  5.  Flew-grow>0的元素，寬度=原寬度+ flexgrow/grow_tatal*remainded_space。

同樣使用上面範例做說明：

```html
div.container.width_100
	span.A.width_20
	span.B.width_20
	span.C.width_20
```

此時若有設定 CSS為

```scss
span.A, span.B{
  flex-grow: 1;
}

span.C{
  flex-grow: 2;
}
```

則各運算要素為

| 要素   | initial_space | remained_space | grow_total |
| ---- | ------------- | -------------- | ---------- |
| 大小   | 60px          | 40px           | 4          |

最終結果

| 元素   | span.A                 | span.B                 | span.C                 |
| ---- | ---------------------- | ---------------------- | ---------------------- |
| 寬度   | 20 + 1 / 4 * 40 = 30px | 20 + 1 / 4 * 40 = 30px | 20 + 2 / 4 * 40 = 40px |

flex-grow 宣告寫法

```css
.item{
  flex-grow: <number>; /* default 0 */
}
```



#### flex-shrink 物件縮小，分擔不足空間的比例

- 當**剩餘空間 < 0** 時發揮效果。

- 預設值為 1，代表子元素按原比例縮小。

- 以下計算步驟只適用於當橫向展開時flexbox容器寬度小於所有子元素的寬度時：

  1.  首先算出flexbox容器內所有子元素的原始寬度總和initial_space。

  2.  用initial_space減去flexbox容器的總寬度，得到超出flexbox容器的那部分空間over_space。

  3.  獲取flexbox容器中flex-shrink>0的子元素，算出flex-shrink的總和shrink_total。

  4.  Flew-shrink=0的元素默認按原大小顯示。

  5.  Flew-shrink>0的元素，寬度=原寬度-flexshrink/shrink_tatal*over_space。

同樣架構做範例說明：

```html
div.container.width_40
	span.A.width_20
	span.B.width_20
	span.C.width_20
```

此時若有設定 CSS為

```scss
span.A, span.B{
  flex-shrink: 1; /* 等於預設值 */
}

span.C{
  flex-shrink: 2;
}
```

則各運算要素為：

| 要素   | initial_space | over_space | shrink_total |
| ---- | ------------- | ---------- | ------------ |
| 大小   | 60px          | 20px       | 4            |

最後結果如下：

| 元素   | span.A                 | span.B                 | span.C                 |
| ---- | ---------------------- | ---------------------- | ---------------------- |
| 寬度   | 20 - 1 / 4 * 20 = 15px | 20 - 1 / 4 * 20 = 15px | 20 - 2 / 4 * 20 = 10px |





#### flex-basis 物件預設寬度

- 如果子元素有flex-basis，就算作子元素的原始width（不包括邊框和補邊）。
- 如果沒有`flex-basis`或其屬性值為`0`，在有`width`的情況下以`width`來計，沒有`width`的話，則按其內容來計。
- 如果同時聲明`width`屬性和`flex-basis`屬性時，會以`flex-basis`的值來計算。
- 如果 flex-basis: content，表示默認使用元素內容大寬度。
- 預設為 auto：無特定寬度值，取決於其它屬性值。


```css
.item{
  flex-basis：<length> | <percentage> | auto | content ;
}
```



#### flex 總結

* 幾個常見的表示法：	 

| 寫法   | flex: 1;      | flex: none;     | flex: auto;     | flex: 0 auto; OR flex: initial; |
| ---- | ------------- | --------------- | --------------- | ------------------------------- |
| 意思表示 | flex: 1 1 0%; | flex: 0 0 auto; | flex: 1 1 auto; | flex: 0 1 auto; 即是 flex的預設值     |

* 如果父級的空間足夠：`flex-grow`有效，`flex-shrink`無效。
* 如果父級的空間不夠：`flex-shrink` 有效，`flex-grow`無效。
* ​

### property: align-self

![img](https://css-tricks.com/wp-content/uploads/2014/05/align-self.svg)

the same values as align-items and its value for the specific item.

```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

