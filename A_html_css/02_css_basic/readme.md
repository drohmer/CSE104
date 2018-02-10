# Introduction to CSS

## Style file sheet

CSS stands for __Cascading Style Sheet__. CSS allows to finely tune the visual appearance of HTML content.

* Consider the following basic HTML file

```html
<!DOCTYPE html>

<html>

<head>
	<title> CSE104 </title>
</head>

<body>
       <h1>My first webpage</h1>
       <p>This is HTML code.</p>
</body>

</html>
```

* Create a new file named _style.css_ with the following content

```css
body {
    text-align: center;
    background-color: rgb(15,15,15);
    color: white;
}

h1 {
    color: red;
    font-variant: small-caps;
}
```

* Add the following entry in the header of your HTML document allowing to link the CSS code with the HTML

```html
<link rel="stylesheet" href="style.css">
```

* Observe the new appearance of the webpage in your browser. Change some values such as the color of some elements and reload to page.

## CSS Structure

CSS documents is organized as follow

```css
selector {
	property: value;
	property: value;
	...
	/* CSS Comment */
}
```

The `selector` allows to select a subset of HTML tags on which the pair `property:value` will be applied.
This unit containing a `selector` and a set of `property:value` is called a CSS rule.

There exists a large amount of CSS properties. Don't hesitate to check the [reference](https://www.w3schools.com/cssref/default.asp) to check for specific properties.

## Cascading selection

In the previous example, the text `My first webpage` is included in both `body` and `h1` tags. It is therefore selected in two different rules.

This is where the __Cascading__ evaluation of CSS has to be considered:
Each element inherit the style from its parent. When there is a conflicting property defined several times, the one associated to the [more specific](https://developer.mozilla.org/en-US/docs/Web/CSS/Specificity) selector is applied.
In this case, the `body` selector is considered as less specific than `h1` (body contains all the content of the webpage body).
In the case where two selectors have the same specificity, the rule which is declared last is applied.

This cascading behavior allows to organize the visual appearance of the webpage in a structured and hierarchical manner. Designing a good CSS structure is one of the role of the so called `front page web development`.

## Selector combination

Selector can be combined to refine the selected elements, the most common combination are (there is more possible [combinations of elements](https://www.w3schools.com/cssref/css_selectors.asp))

* `e1, e2`: is the union of all elements `e1` and all elements `e2`
* `e1 e2`: is the elements `e2` child of element `e1`



ex. Consider the following HTML body

```html
<section>
       <h1> A </h1>
       <p> text A </p>
</section>

<h1> B </h1>
<p> text B </p>

<footer>
       <h1> C </h1>
       <p> text C </p>
</footer>
```

and

```css
footer {
    background-color: rgb(230,230,230);
}
section {
    background-color: rgb(200,200,200);
}
h1, p {
	color: blue;
}
section h1{
	color: red;
}
```

* `h1, p` apply the rule on all `<h1>` and `<p>` elements.
* `section h1` applies its rule only to `<h1>` element which is a child of `<section>`

__Q.__ Create the rule such that all the `<h1>` titles, and the `<p>` elements which are inside a `<footer>` tag are underlined (see [text-decoration](https://www.w3schools.com/cssref/pr_text_text-decoration.asp) property).

