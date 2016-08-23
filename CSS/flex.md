# flex
參考資料：  
[深入解析 CSS Flexbox](http://www.oxxostudio.tw/articles/201501/css-flexbox.html)   
[Flexbox Froggy](http://flexboxfroggy.com/)



起始宣告：
```css
#pand{
    display: flex;
    }
```
## 1.property: justy-content 操縱物件的水平方向
- flex-start: Items align to the left side of the container.
- flex-end: Items align to the right side of the container.
- center: Items align at the center of the container.
- space-between: Items display with equal spacing between them.
- space-around: Items display with equal spacing around them.

## 2. property: align-items 操縱物件的垂直方向

- flex-start: Items align to the top of the container.
- flex-end: Items align to the bottom of the container.
- center: Items align at the vertical center of the container.
- baseline: Items display at the baseline of the container.
- stretch: Items are stretched to fit the container.

## 3.property: flex-direcction 物件排列方向
- row: Items are placed the same as the text direction.
- row-reverse: Items are placed opposite to the text direction.
- column: Items are placed top to bottom.
- column-reverse: Items are placed bottom to top.

## 4.property: order 用數值表示物件順序 (用在單一物件上)
By default, items have a value of 0, but we can use this property to set it to a positive or negative integer value. 預設是0，數字越小越前面。

## 5.property: align-self
the same values as align-items and its value for the specific item.

