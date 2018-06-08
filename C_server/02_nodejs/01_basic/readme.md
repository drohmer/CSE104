# Introduction to nodejs

Node.js is a stand-alone JavaScript interpreter. Node.js can be used to execute general program written in JavaScript without requiring a browser. Node.js can be very efficient to setup server based programming, notably to handle various request/response between client and server.

## Installing node.js

First make sure that node.js and npm are installed on your machine.

On Linux system, standard package manager are usually handling these two softwares.
If you don't have root access to install packages on your system, you may follow [these methods](https://gist.github.com/isaacs/579814) (the second proposition should work for both node.js and npm).


## First node.js program.

* Create a file `server.js` with the following JavaScript code

```javascript
const express = require('express');
const app = express();

app.listen(8000, function () {
  console.log('Server listening on port 8000');
});
```

This code starts a basic server listening on the port 8000. This code use the node.js module [express.js](https://expressjs.com/) allowing to setup server very efficiently.

* Try to run `node server.js`, observe that you should have an error indicating that the module `express` cannot be found. To locally install `express.js` run the following command

```bash
npm install express
```

* Try again to run `node server.js`. You should see the following message on your command line `Server listening on port 8000`.

* So far, your server is doing nothing. Add the following code in your `server.js` file

```javascript
app.get('/',serverResponse);

function serverResponse(req,res) {
  res.send('Hello, this is a message from the server');
}
```

When a client will query the server at its root `/`, the server will respond with a text message.

* Open your browser at the url `http://localhost:8000/` and observe that the server is responding.

* Observe the source code of your HTML page. In real scenario, a complete response with HTML markup can be made.
