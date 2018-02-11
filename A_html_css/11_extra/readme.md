# Extra

## Fonts

Extra fonts can be included in the webpage. 

Two methods are possible
1. In the HTML file using a link tag
```html 
<link href='FontURL' rel='stylesheet'>
```
1. In the CSS document using `import`
```css
@import url('FontURL');
```

Once the font is loaded, it can be used from the [font-family](https://developer.mozilla.org/en-US/docs/Web/CSS/font-family) property.

```css
font-family: FontName;
```

As fonts may not be available all the time, it is requiered that you also provide generic base font in the `font-family` values as a fall-back such as serif, sans-serif, monospace, etc.

ex. 
```css
font-family: FontName, serif;
```

### Exemple

* Consider the following code

```html
<!DOCTYPE html>
<html>

<head>
	<title> CSE104 </title>
	<link rel="stylesheet" href="style.css">
	<link href="https://fonts.googleapis.com/css?family=Sacramento" rel="stylesheet"> 
</head>

<body>
<article>
	<p> Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua. Ut enim ad minim veniam, quis nostrud exercitation ullamco laboris nisi ut aliquip ex ea commodo consequat. Duis aute irure dolor in reprehenderit in voluptate velit esse cillum dolore eu fugiat nulla pariatur. Excepteur sint occaecat cupidatat non proident, sunt in culpa qui officia deserunt mollit anim id est laborum. </p>
</article>

</body>
</html>
```

```css
p {
	font-size: 2.5em;
	font-family: "Sacramento", serif;
}
```

* Try to load the font using `import` tag in the CSS file.

* Look at other fonts available from [Google Font repository](https://fonts.google.com/).