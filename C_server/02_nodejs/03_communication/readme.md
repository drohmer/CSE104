# Client/server communication

While PHP code is very convenient to generate HTML webpage, Node.js code can very efficiently handle more general communication such as fetching informations returned as JSON, or even bi-directional client/server communication using sockets.

## JSON fetch

We remind that fetch [https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) (as used in [this exercise](https://github.com/drohmer/CSE104/tree/master/B_javascript/10_api_json)) is used to contact a server from JavaScript client code.

Fetch can notably be used to send query to a server using GET parameters within the URL, and then receive a response, typically in the form of JSON data.

* Create a HTML/JS client files where the JavaScript code is the following

```javascript
const url = "http://localhost:8000/";

fetch(url)
  .then(onResponse)
  .then(userCallbackFunction);

function onResponse(response) {
  return response.json();
}

function userCallbackFunction(data) {
  console.log(data); // dump JSON data on the console for debug

  // Display the message received from the server
  const newElement = document.createElement("p");
  newElement.textContent = 'The server answered: "'+data.msg+'"';
  document.querySelector("body").appendChild(newElement);
}
```

* Create a server code containing the following

```javascript
const express = require('express');
const app = express();

app.get('/',serverResponse);

app.listen(8000, function () {
  console.log('Server listening on port 8000');
});

function serverResponse(req,res) {
  res.header("Access-Control-Allow-Origin","*"); // Allows fetching from files (or other domain)
  const response = "Hello from the server"; //Some string send as response
  res.send({msg:response}); // return JSON response
}
```

* Start your server
* Then, open in your browser the client HTML file using the client JavaScript code (don't try to contact the server directly from the URL as the JavaScript code is doing it.)
* You should see in your browser the message "Hello from the server" displayed.

### Exercise: Online computing

__Q.__ Create a program where the server compute the roots of the polynomial equation ax^2+bx+c, and return it to the client.
* The client will provide as input the numerical value of a, b, c, and send it to the server.
* The server receives the parameters and compute the real roots when possible.
* Te result is sent back to the client as a JSON value. And the client display it.

## Socket

So far, fetch allows the communication from a client toward the server. However, the server cannot, by itself contact the client. Such bi-directional communication is possible using sockets.

[Soket.io](https://socket.io/) is a module allowing to easily setup socket communication between node.js and JavaScript program.

* Create the following server code

```javascript
const express = require('express');
const app = express();
const http = require('http').Server(app);

// Creation of the socket
const io = require('socket.io')(http);
io.on('connection',onConnection);


http.listen(8000, function () {
  console.log('Server listening on port 8000');
});

function onConnection(socket)
{
  // When a client connect to the socket: send a message
  socket.emit('message',{body:' -- Welcome, your are connected on the server -- '});

  // Listen to message from the client
  socket.on('message',function(message){onMessage(message,socket)});
}

function onMessage(message,socket) {
  // When receiving a message from the client
  console.log('Server received message from client "'+message.body+'"');
}
```

* And the client code

```javascript
const url = "http://localhost:8000/";

// Connect to the socket
const socket = io.connect('http://localhost:8000');

// Listen to messages from the server
socket.on('message',receiveMessageEvent);

// Send a message to the server
socket.emit('message',{body:"Hello from client"});

function receiveMessageEvent(message) {
  // Action when receiving message from the server
  console.log('Client received message from server: "'+message.body+'"');
}
```

* Include the file `socket.io.js` on your client code (including in the HTML)

* Run first the server (after installing socket.io vie npm).
* Open your browser on the client code.
* Check that both client and server are receiving their message.

__Q.__ Create a small chatbox.
* Each message from a client is sent and broadcasted to all the other clients (`socket.broadcast.emit(...);`).