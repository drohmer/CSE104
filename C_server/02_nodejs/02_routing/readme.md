# Routing


[Routing](https://expressjs.com/en/guide/routing.html) is the ability to provide specific page and content depending on the URL provided by the client.

Express.js proposes a convenient way to handle routing with parameters. 

## Example of routing

* Consider the following code

```javascript
const express = require('express');
const app = express();

app.get('/',homeServerResponse);
app.get('/hello/:firstname/:lastname',helloResponse);

app.listen(8000, function () {
  console.log('Server listening on port 8000');
});

function homeServerResponse(req,res) {
  const response = `<!DOCTYPE html>
  <html>
    <h1> Home </h1>
  </html>
  `;
  res.send(response);
}

function helloResponse(req,res) {
  const firstname = req.params.firstname;
  const lastname = req.params.lastname;
  const response = `<!DOCTYPE html>
  <html>
    <h1> Hello ${firstname} ${lastname} </h1>
  </html>
  `;
  res.send(response);
}
```

* When querying the root directory, the server answer with an HTML page displaying 'Home'.
* When querying the directory `/hello/firstname/lastname`, the server respond with an HTML page displaying `Hello firstname lastname`, where `firstname` and `lastname` are parameters set on the url.

## Handlebars to render template HTML

So far, we handled HTML return as basic JavaScript string. This approach is very general, but not always practical as it may leads to long JavaScript code mixing HTML string and JS functions.

[Handlebars.js](https://handlebarsjs.com/) is a node.js module (working with express.js) allowing to generate HTML file from template one. Then you can write a basic external HTML with the expected variables within handlebars `{{ }}` that are going to be filled by the server.

* Create a directory `views/` in which you place the following file `hello.handlebars`

```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1">

  <title>CSE104</title>
</head>

<body>
<h1>Hello {{firstname}} {{lastname}}</h1>
</body>

</html>
```

* Create the file `server.js` on the root directory

```javascript
// Setup express and handlebars
const expressHandlebars = require('express-handlebars');
const express = require('express');
const app = express();
const handlebards = expressHandlebars.create();
app.engine('handlebars',handlebards.engine);
app.set('view engine','handlebars');

// Setup routing
app.get('/hello/:firstname/:lastname',helloResponse);

app.listen(8000, function () {
  console.log('Server listening on port 8000');
});

// Render views/hello with the first and last name as parameters
function helloResponse(req,res) {
  const firstnameParam = req.params.firstname;
  const lastnameParam = req.params.lastname;

  const placeholders = {firstname:firstnameParam, lastname:lastnameParam};
  res.render('hello',placeholders);
}
```

* Run your server (you need to install express-handlebars and express using npm) on the url `localhost:8000/hello/firstname/lastname`.

Note that this approach allows to separate the HTML page structure from the parameter handling in the node.js application.

## Exercise

__Q.__ Following the same approach, create a page accessible through the URL `/hello/name/color` that display `Hello name`, and change the background-color of the page depending on the value `color`.