# 100% width

## What Does 「width: 100%」 Do in CSS?

### Blocks Don't Need 100% Width

When we understand the difference between **block-level** elements and **inline** elements, we'll know that a block element (such as a `<div>`, `<p>`, or `<ul>`, to name a few) will, by default expand to fit the width of its containing, or parent, element (minus any margins it has or padding its parent has).

![A Block-Level Element Expands Naturally](https://www.impressivewebs.com/images/block-element-noneed.jpg)

## What 100% really means

When you give an element a width of 100% in CSS, you're basically saying :

> Make this element's content area exactly equal to the explicit width of its parent — but only if its parent has an explicit width. 

So, if you have a parent container that's 400px wide, a child element given a width of 100% will also be 400px wide, and **will still be subject to margins, paddings, and borders —** **on top of the 100% width setting**. The image below attempts to illustrate this:

![The child's content area will equal the parent's](https://www.impressivewebs.com/images/child-equal.jpg)



