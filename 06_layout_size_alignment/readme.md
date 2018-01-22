# Layout

We call _layout_ the visual structure of the different parts of the page.
Before coding directly the final version of the webpage with the text and images, it can be interesting to set up first the general layout of the containing boxes.

We already saw some properties allowing to set the layout of elements. As for instance:
* Display (inline, block, inline-block), allowing to set the main flow organization of elements (left to right, top to bottom), as well as their behavior with respect to interior elements.
* Margin (left, right, top, bottom), and padding, allowing respectively to set the position of the box with respect to the surrounding elements, and the content with respect to the border of the box.
* Text-align (left, center, right), allowing to set the horizontal position of the content of a box.


### Vertical alignment

When using inline and inline-block elements (such as text and images) exhibiting different size, it is possible to adjust their respective vertical alignement though the use of [vertical-align](https://developer.mozilla.org/en-US/docs/Web/CSS/vertical-align).

__Q.__ Try the following code

```html
Position of inline text.

<div class="top"></div>
<div class="middle"></div>
<div class="bottom"></div>

<img class="top" src="house.jpg">
<img class="middle" src="house.jpg">
<img class="bottom" src="house.jpg">
```

```css
p {
	display: inline;
	width: 30px;
	height: 30px;
	background-color: yellow;
}
.top {
	vertical-align: text-top;
}
.middle {
	vertical-align: middle;
}
.bottom {
	vertical-align: text-bottom;
}
div {
	display: inline-block;
	width: 50px;
	height: 54px;
	background-color: green;
}
```

__Q.__ Try to create a webpage with the layout shown in the exercice _Image and box_

_Hint:_ You may use `vertical-align: top` and `bottom` in order to align elements with the tallest/lowest element instead of `text-top` and `text-bottom` computing the alignment with respect to the text.


### More usefull layout parameters


#### Margin auto

The command `margin: auto;` enable the browser to automatically compute the left and right space to center horizontally the element with respect to the parent. 
Note that the element to be centered must be have a block display.

Exemple:
```html
<div class="wrapper">
<div class="box color1">Text in centered box. </div>
</div>

<div class="wrapper">
<div class="box color2">Text in centered box. </div>
</div>
```

```css
.wrapper {
	display: inline-block;
	width: 400px;
	height: 600px;
	background-color: lightyellow;
	border: 2px solid black;
	padding: 15px;

	margin: 15px;
}
.box {
	width: 200px;
	height: 60px;
	border: 2px solid black;

	margin: auto;
}
.color1 {
	background-color: salmon;
}
.color2 {
	background-color: lightgreen;
}
```

#### Adapting size

It is possible to set the size of the box model with max and min values instead of fixed one. 
Max ad min are typically used to enhance responsive appearance of website (appearance that adapts to various window size).

* [max-width](https://developer.mozilla.org/en-US/docs/Web/CSS/max-width)
* [min-width](https://developer.mozilla.org/en-US/docs/Web/CSS/min-width)
* [max-height](https://developer.mozilla.org/en-US/docs/Web/CSS/max-height)
* [min-height](https://developer.mozilla.org/en-US/docs/Web/CSS/min-height)

#### Units 

The size of the containers can be set in various units.

* __px__ allow to define the size in number of pixels. Websites are however typically seen from several hardwares (smartphones, tablets, computers, ...) with various resolution and window size. Hard-coding all element size in pixel size may look good on computer screen size under a specific resolution and window size, but not on smartphone and conversely. 

It is possible to use relative sizes, thus allowing the render to adapt to the context of the screen and resolution.

* __%__ define the size of an element in percent with respect to the parent one.
* __vw/vh__ define the size of an element in percent with respect to the viewport width

__Q.__ Test the following code. Resize you window and note the automatic adaptation of the elements (the gray box always span 75% of the viewport width and height, while the yellow and salmon box have a span a specific percentage of their parent grey box size).

```html
<div class="container">
	<div class="A"></div>
	<div class="B"></div>
</div>
```

```css
.container {
	width: 75vw;
	height: 75vh;
	background: lightgray;
}

.A {
	width: 75%;
	height: 25%;
	background-color: yellow;
}

.B {
	width: 25%;
	height: 50%;
	background-color: salmon;
}
```

* __em__ is a unit to define a size with respect to the current element font-size.

Exemple:

```html
Base size, <span class="twice">twice larger</span>.
<h2> Base title size, <span class="twice">twice larger</span>.</h2>
```

```css
.twice {
	font-size: 2em;
}
```


You can met also __rem__ defining the size with respect to the root element font-size.


As a summary:
* Prefer, when possible, to define size of elements in percentage rather than fixed pixel size.
* Traditionaly, percent are used to defined containing box size, while em are used to handle text-related elements (defining the text size in percent is also valid, but less common).




## Flex Box

Flex box is a new display type, designed to be more flexible (/responsive) than previous inline/block/block-inline display. Flex-box is specifically adapted to define the layout of an array of elements inside a container.


Consider the following code

```html
<div class="container">
	<div class="item">1</div>
	<div class="item">2</div>
	<div class="item">3</div>
	<div class="item">4</div>
	<div class="item">5</div>
</div>
```

```css
.container {
	
	height: 75vh;
	width: 75vw;
	margin-left: auto;
	margin-right: auto;
	margin-top: 5vh;
	background-color: lightgray;

	display: flex;
}

.item {
	background-color: yellow;
	border: 2px solid black;
	text-align: center;
	font-size: 1.5em;

	margin: 5px;
	width: 100px;
	height: 100px;
}
```

### Property of the container

* __flex-direction__ allow to set the direction of the items (left to right, top to bottom, etc).
<br/>
Try the following direction:
  * row (default)
  * row-reverse
  * column
  * column-reverse

* __flex-wrap__ allow the items to wrap inside the container when needed.
<br/>
Try the following options:
  * no-wrap (default)
  * wrap
  * wrap-reverse


* __justify-content__ allow to set the horizontal placement of the items and space between items.
<br/>
Try the following options:
  * flex-start (default)
  * flex-end
  * center
  * space-between
  * space-around

* __align-content__ allow to set the vertical placement and space between lines of items. Align-content acts when items span several lines of contents.
<br/>
Test the following options (change the width of the items to ensure that they span multiple lines):
  * stretch (default, items should not have fixed height)
  * center
  * flex-start
  * flex-end
  * space-between
  * space-around

* __align-items__ allow to set the vertical placement and size of the items, even if there is only one line of items.
<br/>
Comment out the height of item in the CSS, and try the following options:
  * stretch (default, items should not have fixed height)
  * center
  * flex-start
  * flex-end

### Property of items

Items can have specific properties.

* __flex-grow__ / __shrink__: allow to define the ability of an item to grow/shrink within the container.

Exemple:
```html
<div class="container">
	<div class="item">1</div>
	<div class="item">2</div>
	<div class="item grow">3</div>
	<div class="item">4</div>
	<div class="item">5</div>
</div>
```

```css
.item {
	background-color: yellow;
	border: 2px solid black;
	text-align: center;
	font-size: 1.5em;

	margin: 5px;
	flex-grow: 1;
	height: 100px;
}

.grow  {
	flex-grow: 2;
}
```

Note that the third item will grow twice more than the other items.

* Note: seting `margin: auto;` for an item in a flex container allows to center it both in horizontal and vertical axis.


### Grid layout

Flex-box focuses on arranging array of items. A newer CSS layout is also developed to handle grid type items: [CSS-grid](https://www.mozilla.org/en-US/developer/css-grid/).

Note that CSS-grid is still recent, and older browser may not be able to handle it.


## Exercices

