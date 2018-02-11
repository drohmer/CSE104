# Position

Position allow to place elements in a "floating" mode in the page of relative to their containing element.

Position can take the following values
* __static__: default mode, static elements cannot be moved from their position in the page flow.
* __relative__: set an offset from the normal static position.
* __fixed__: set a fixed position with respect to the viewport of the window.
* __absolute__: set a fixed position with respect to the containing element.

The position of the fixed, absolute, or relative position can be set by an offset value given by top, bottom, right, left.

## Relative

__Q.__ Try the following code

```html
<div id="bloc1"> </div>
<div id="bloc2"> </div>
<div id="bloc3"> </div>
```

```css
#bloc1 {
	width: 200px;
	height: 200px;
	background-color: red;
}

#bloc2 {
	display: inline-block;
	width: 200px;
	height: 200px;
	background-color: yellow;

	/*position: relative;*/
	top: -20px;
	left: 40px;
}

#bloc3 {
	display: inline-block;
	width: 200px;
	height: 200px;
	background-color: blue;

	/*position: relative;*/
	top: -60px;
	left: -50px;
}
```

Uncomment the `position: relative`, and observe the new placement of each element.
Note that `top` and `left` have no influence on the default static position.

__Q.__ Add a [z-index](https://developer.mozilla.org/en-US/docs/Web/CSS/z-index) to the yellow and blue box. Change the relative index to make the yellow box appearing in front of the blue one.

Similarily to `z-index` does not apply to elements with static position.

__Q.__ Add a relative position to the red box and a z-index so that it appears in front of the two others.


## Fixed

__Q.__ Try the following code


```html
<p id="fixed"> Text in fixed mode </p>

<p id="normal">
	Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum
</p>
```

```css
#normal {
	margin: 2em;
}

#fixed {
	position: fixed;
	top: 3em;
	left: 10em;

	background-color: yellow;
	border: solid 2px black;
	padding: 0.5em;
}
```

Note that the element in fixed mode is removed from the normal document flow, and placed at the position described by top and left.

__Q.__ Use the fixed mode to model the behavior of a menu that remains constantly on the screen as shown in example `01_fixed_menu`

![](pics/exercice_01.gif)

Hints:
* The transparent color can be defined by `rgba(r,g,b,a)`. The last number (alpha) defines the percentage of opacity (can be a number between 0 and 1).
* The textual content can be filled by automatic [text generator](http://www.blindtextgenerator.com/lorem-ipsum).

## Absolute

Absolute set a position defined with respect to the parent container with a relative position. If no container parent container has relative position, the position is set with respect to the viewport (similar to fixed position).

__Q.__ Try the following code

```html
<div id="bloc1">
    Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum.
    <div id="bloc2"> </div>
    <div id="bloc3"> </div>
</div>
```

```css
#bloc1 {
	width: 400px;
	background-color: lightcyan;
	position: relative;
}

#bloc2 {
	display: inline-block;
	width: 100px;
	height: 100px;
	background-color: rgba(255,0,0,0.4);
	position: absolute;
	top: 15px;
	left: 15px;
}

#bloc3 {
	display: inline-block;
	width: 80px;
	height: 120px;
	background-color: rgba(100,200,0,0.4);
	position: absolute;
	top: 15px;
	right: 15px;
}
```

__Q.__ Create the html and css code following the behavior of the exercice `02_absolute`.

![](pics/absolute_exercice.jpg)

# Float

The float property can also be used to place elements in a relative way.
However, contrary to the `position` property, a `float` element is not removed from the document flow. Thus, surrounding elements will be able to wrap around the floating element.
This behavior can typically be used to place an image wrapped by text.

__Q.__ Try the following code where the red box could be replaced by any image.

```html
<div class="pic float-left"></div>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus imperdiet, nulla et dictum interdum, nisi lorem egestas odio, vitae scelerisque enim ligula venenatis dolor. Maecenas nisl est, ultrices nec congue eget, auctor vitae massa. Fusce luctus vestibulum augue ut aliquet. Mauris ante ligula, facilisis sed ornare eu, lobortis in odio. Praesent convallis urna a lacus interdum ut hendrerit risus congue. Nunc sagittis dictum nisi, sed ullamcorper ipsum dignissim ac. In at libero sed nunc venenatis imperdiet sed ornare turpis. Donec vitae dui eget tellus gravida venenatis. Integer fringilla congue eros non fermentum. Sed dapibus pulvinar nibh tempor porta. Cras ac leo purus. Mauris quis diam velit.
</p>

<div class="pic float-right"></div>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus imperdiet, nulla et dictum interdum, nisi lorem egestas odio, vitae scelerisque enim ligula venenatis dolor. Maecenas nisl est, ultrices nec congue eget, auctor vitae massa. Fusce luctus vestibulum augue ut aliquet. Mauris ante ligula, facilisis sed ornare eu, lobortis in odio. Praesent convallis urna a lacus interdum ut hendrerit risus congue. Nunc sagittis dictum nisi, sed ullamcorper ipsum dignissim ac. In at libero sed nunc venenatis imperdiet sed ornare turpis. Donec vitae dui eget tellus gravida venenatis. Integer fringilla congue eros non fermentum. Sed dapibus pulvinar nibh tempor porta. Cras ac leo purus. Mauris quis diam velit.
</p>
```

```css
body {
	width: 500px;
	margin: auto;
}

.pic {
	margin: 10px;
	width: 100px;
	height: 100px;
	background-color: red;
}

.float-left {
	float: left;
}
.float-right {
	float: right;
}

p {
	text-align: justify;
}
```

Note that `float` elements can only be placed in left or right, they cannot be centered.

## Clearing float

Consider the case where the floating image is now taller than the paragraph of text wrapped around it.
In this situation, the next paragraph will start on the side of the previous floating image, which may not be the expected behavior.

See an example from the following code and note that the content of a container starts before the floating image ends.
```html
<div class="container">
<div class="pic float-left"></div>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus imperdiet, nulla et dictum interdum, nisi lorem egestas odio, vitae scelerisque enim ligula venenatis dolor.
</p>
</div>

<div class="container">
<div class="pic float-right"></div>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus imperdiet, nulla et dictum interdum, nisi lorem egestas odio, vitae scelerisque enim ligula venenatis dolor.
</p>
</div>

<div class="container">
<div class="pic float-left"></div>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus imperdiet, nulla et dictum interdum, nisi lorem egestas odio, vitae scelerisque enim ligula venenatis dolor.
</p>
</div>

<div class="container">
<div class="pic float-right"></div>
<p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Phasellus imperdiet, nulla et dictum interdum, nisi lorem egestas odio, vitae scelerisque enim ligula venenatis dolor.
</p>
</div>
```

```css
body {
	width: 500px;
	margin: auto;
}

.pic {
	margin: 10px;
	width: 200px;
	height: 200px;
	background-color: red;
}

.float-left {
	float: left;
}
.float-right {
	float: right;
}

p {
	text-align: justify;
}

.container {
	margin: 5px;
	border: 2px dashed lightgray;
}
```

The parameter [clear](https://developer.mozilla.org/en-US/docs/Web/CSS/clear) with values `none`, `left`, `right`, `both` allows an element to start after the end of other floating elements.

__Q.__ Add `clear: both;` property to the `.container` rule and observe that the successive paragraphs do not wrap around existing previous floating image.
