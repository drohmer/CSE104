# API and JSON

In the previous chapter, the data provided by the API was an image, and thus could directly be included in the webpage.
In the more general cases, generic data informations should be sent by the server, and used by the client side code.
Two exchange data format are commonly met: __XML__, and __JSON__.

* [XML](https://developer.mozilla.org/en-US/docs/XML_introduction) (eXtensible Markup Language) is a tag based data exchange format.
* [JSON](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/JSON) (JavaScript Object Notation) is a text curly-brackets based data exchange format.

XML is the older and more generic standard. It follows strong rules that can be checked using XML parsers and validators.
JSON is a more recent exchange format, initially developed for JavaScript, but today used as generic exchange format. JSON follows a hierarchical organization described as a pair of key/value elements. JSON is compatible, by design, with JavaScript Objects. It means that JavaScript object can be easilly converted into JSON, and conversely between JSON and JavaScript code.
While JSON is less structured than XML, it is less verbose and more easily read and modified by human as simple text.

## Fetching JSON Data

### Geocoding

In the previous exercise using Google Map, the user had to indicate explicitely the longitude and latitude of the map center point. Most of the time, the user doesn't know the geographic coordinates, but would rather request a view from a textual name or address.

The conversion between a human readable address and geographic coordinates is called Geocoding. Google Map propose an online service able to perform this conversion.

* Type in you browser the following url https://maps.googleapis.com/maps/api/geocode/json?address=ecole%20polytechnique and observe the result obtained as a JSON structure.

__Rem.__
* `%20` encodes the space character.
* The JSON data provides several informations that may varies depending on the scale and available informations on the address. 
* Note that the geographic coordinates of the center point are accessible through the following fields: `results.geometry.location.lat/lng`
* Replacing `json` by `xml` in the url, allows to receive the same response in XML format.

### Fetching data

So far, the JSON data have only been visualized by your browser. The objective is to receive these data from your javascript code.

Requesting data through HTTP protocol can be achieved using the JavaScript function [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API/Using_Fetch).


Similarily to images, the server may not respond immediately to the `fetch` request, or may even fail to respond. Therefore fetch is not returning the result of the request, which would possibly block the execution of the program while waiting for the answer. Instead, fetch immediately returns an object called a [promise](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Promise) immediately. 
__Promise__ are special objects dedicated to handle asynchronous, and possibly failing, responses. Once fetch is called, it return a promise that does not yet contains the answer. The JavaScript program continue its execution.
Once the data has finished to be loaded, the promise is said to be fullfilled, and a specific callback function can be called to handle the data.

The syntax is the following `fetch(url).then(callbackFunction);`


* Consider the following code

```javascript
function fullfilled(response) {
  console.log("Promise fullfilled");
  console.log(response);
}

const url = "https://maps.googleapis.com/maps/api/geocode/json?address=ecole%20polytechnique";

console.log("Calling Fetch ...");
fetch(url).then(fullfilled);
console.log("Fetch is called");
```

Observe in particular that
* The line `Fetch is called` will probably appear before `Promise fullfilled` as the data has to be retrieved from an external server and `fetch` doesn't block the program.
* The resulting response cannot be used directly. This response correspond to the http response from the server, which contains itself JSON data.

The next step consists in converting this http response into usable JavaScript objects. The JavaScript method `.json()` can be applied, and return itself a promise.
A common code template to retrieve usable JSON data is the following

```javascript
function onResponse(response) {
  return response.json();
}

function userCallbackFunction(data) {
  console.log(data);
}

const url = "https://maps.googleapis.com/maps/api/geocode/json?address=ecole%20polytechnique";
fetch(url)
  .then(onResponse)
  .then(userCallbackFunction);
```

* In this case, two promises and fullfillment have been chained. Once when the data are received, and the second when the JSON data are ready.
* Observe in the console that the variable `data` contains the information that you saw previously on the browser. However, this time it is directly accessible as JavaScript object and can be used in the code.


__Q.__ Modify the code of the function userCallbackFunction to print on the webpage the _formatted address_, and the _geographical coordinates_. Try your program with another address.

## Exercise: Adress to Map

__Q.__ Create a code where the user can indicate an address in a textual form. This address is geocoded, and the website should indicates the formatted address, the latitude, longitude, and extra information such as the Country and City if available.
The application should also show the map (from Google Map and Open Street Map) corresponding the the given address, and the user can select the level of Zoom.

![](pics/map.apng)
