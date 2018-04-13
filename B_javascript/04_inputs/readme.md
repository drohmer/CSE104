# GUI and buttons

We call `widget` a graphical element which can interact with the user. Buttons, checkbox, text entry, etc. are common widgets.

HTML describes a set of basic widgets using the [input tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/input) that can be used "as it is" with default behavior set for contact forms. However, the behavior of these widget may be finely adapted to your needs using JavaScript.


* Consider the following code

```html
<input id="button" type="button" value="click me"> <br>
Type some text: <input id="textEntry" type="text">
```

```javascript
"use strict";

// Button
const button = document.querySelector("#button");
button.addEventListener('click',buttonClicked);

function buttonClicked(event) {
  console.log('clicked');
}

// Text entry
const textEntry = document.querySelector("#textEntry");
textEntry.addEventListener('change',textModified);

function textModified(event) {
  console.log('text modified into ',textEntry.value);
}
```

* Check the console when you click on the button, or write some text in the corresponding widget.

* Adapt the code such that the message `You typed the following text: ${TEXT}` appears when the user click on the button, where `${TEXT}` corresponds to the content of the text widget.


## Exercise: Color Gradient

__Q.__ Create the code allowing to parameterize the extreme color of a rectangular box, as well as its length, as seen in the following example

![](pics/exercise.apng)


_Hints_: 
* Widget allowing color selection and slider can be set using the `color` and `range` type.
* The event `input` is called every time the value of the widget is modified.


## Security and good practice

### Text content

Consider the following code

```html
Type some text: <input id="textEntry" type="text">
<p>You typed the following text: <span id="textRender"></span> </p>
```

```javascript
const textEntry = document.querySelector("#textEntry");
textEntry.addEventListener('change',textModified);

function textModified(event) {
  const textRender = document.querySelector("#textRender");
  textRender.textContent = textEntry.value;
}
```

* This code basically copies the content of the input into the textContent entry of the HTML.
* Note that writing HTML tag (ex. `<p>Hello</p>`) in the textEntry input is only copied and pasted as string, and not interpreted as HTML.

### innerHTML

Now consider this new JavaScript line `text.innerHTML = textEntry.value;` instead of `textRender.textContent = textEntry.value;`.

[innerHTML](https://developer.mozilla.org/en-US/docs/Web/API/Element/innerHTML) creates a new HTML content from the string parameter. It means that, at the opposite of [textContent](https://developer.mozilla.org/en-US/docs/Web/API/Node/textContent) that was only describing a pure text input, innerHTML is able to interpret HTML tags.

* Type `<p>Hello</p>` in the textEntry, and observe that, this time, the `<p>` tag is interpreted and Hello appears on a new line.
This may lead to more possibility of user inputs (ex. insert `<p style="font-size:300%;color:red">Text</p>`), however this also let your code open to external one.

* In addition of changing the style of the webpage (which may already not be expected), the user may _inject_, from the text input, some JavaScript code.
  * Type the following in the text Entry `<img src=x onerror=alert("Hello")>`.
This open a `popup` through the execution of the JavaScript [alert](https://developer.mozilla.org/en-US/docs/Web/API/Window/alert) function, which is probably not the expected behavior of the program. (worse actions can be performed (adding/removing DOM elements from the webpage, inserting fake contents, etc).)

Note that this JavaScript only runs on the client side, thus such code injection is not a real _security risk_ as it cannot impact other distant users or database. However, the principle of code injection on servers can be similar, and may leads to more dramatic security issues.


### Good Practice

As a general good practice rule:
* Avoid the use of innerHTML.
* Prefer the use of more focused modifiers such as textContent, or class modification from a limited set described in the CSS file.

As a global security good practice:
* Take care not to let the user having a possible action on something unexpected when using user inputs.
* Always prefer specific functions that cannot execute/evaluate such inputs.