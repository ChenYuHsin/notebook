# background

## background-attachment

If a [`background-image`](https://developer.mozilla.org/en-US/docs/Web/CSS/background-image) is specified, the **background-attachment** [CSS](https://developer.mozilla.org/en-US/docs/CSS) property determines whether that image's position is fixed within the viewport, or scrolls along with its containing block.

## background-repeat

If a background image is specified, the `background-repeat` property defines whether the image is repeated (tiled), and how.

Repeating a background image happens after it has been [sized](http://tympanus.net/codrops/css_reference/background-size) and [positioned](http://tympanus.net/codrops/css_reference/background-position).

## background-origin

規定了指定背景圖片[`background-image`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-image) 的 **background positioning area**，即是背景圖片的渲染區域。

預設值是 `bakcground-origin: padding-box;`

注意：當使用 [`background-attachment`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/background-attachment) 為fixed時，該屬性將被忽略不起作用。



### syntax

```scss
background-origin: border-box
background-origin: padding-box 
background-origin: content-box
```

### value

#### border-box

背景將會延伸到延伸到外邊界的邊框，但是**邊框在上，背景在下**，這個用border-style 為dashed可以直接看得出來。

#### padding-box （此為預設值）

背景描繪在padding盒子，邊框裡不會有背景出現。同樣，背景將會延伸到最外邊界的padding.

#### content-box

背景描繪在內容區範圍.



## background-position

指定背景圖片的初始位置，這個位置是相對於 background-origin定義的 **background positioning area**。

預設值是 `background-psotion: 0% 0%;`

![xy示意圖](xy.png)

### value

有兩大表示方式：1. length表示 2. percentage表示 3. 文字表示

#### length

![左上角邊緣示意圖](offset.png)

上圖代表 `background-position: 30px 25px;`

#### percentage

![百分比表示圖](percentage.png)

上圖代表 `background-posiotion: 50% 75%;`

#### 文字表示

```scss
// When only one offset value is specified, the second value is assumed to be center. 
// Example 1:
background-position: top;
// is equal to 
background-position: top center;
background-position: center top;
background-position: 50% 0%
// Example 2:
background-position: left;
// is equal to 
background-position: left center;
background-position: 0% 50%;

// Other Examples
background-position: 20px; 
background-position: 20px 50px; 
background-position: 30% 75%;
background-position: top left; 
background-position: top 100px; 
background-position: -300px 45px; /* 300px to the left and 45px downwards */
```



## background-size

The `background-size` property is used to specify the size of background images.

**Note:** If the value of this property is not set in a [`background`](https://developer.mozilla.org/en-US/docs/Web/CSS/background) shorthand property that is applied to the element after the `background-size` CSS property, the value of this property is then reset to its initial value by the shorthand property.

### syntax

```scss
/* Keywords syntax */
background-size: cover;
background-size: contain;

/* One-value syntax */
/* the width of the image (height set to 'auto') */
background-size: 50%;
background-size: 3em;
background-size: 12px;

/* Two-value syntax */
/* first value: width of the image, second value: height */
background-size: 50% auto;
background-size: 3em 25%;
background-size: auto 6px;
background-size: auto auto;

/* Multiple backgrounds values by background-image */
/* Do not confuse this with background-size: auto auto */
background-size: auto, auto;
background-size: 50%, 25%, 25%;
background-size: 6px, auto, contain;

/* Global values */
background-size: inherit;
background-size: initial;
background-size: unset;
```

### values

#### auto 

按照背景圖片本身原本大小與比例。

#### `<percentage>`

A `<percentage>` value that scales the background image in the corresponding dimension to the specified percentage of the **background positioning area**, which is determined by the value of **background-origin**. 

The background positioning area is, by default, the area containing the content of the box and its padding; the area may also be changed to just the content or to the area containing borders, padding, and content. 

If the background's attachment is fixed, the background positioning area is instead the entire area of the browser window, not including the area covered by scrollbars if they are present. Negative percentages are not allowed.

#### contain

等比例縮放背景圖片以完全裝入背景區，若有設置 background-repeat: no-repeat的話，可能背景區部分空白。

A keyword that scales the image as large as possible and maintains image aspect ratio (image doesn't get squished). Image is letterboxed within the container. 

#### cover

等比例縮放背景圖片以完全覆蓋背景區，部分背景圖片會被裁切。

A keyword that is the inverse of contain. Scales the image as large as possible and maintains image aspect ratio (image doesn't get squished). The image "covers" the entire width or height of the container. When the image and container have different dimensions, the image is clipped either left/right or top/bottom.