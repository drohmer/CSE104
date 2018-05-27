# GET and POST

Client can send parameters to the server via two methods: GET and POST.
* __GET__ consists in sending parameters explicitely in the url of the page under the textual form: `url/?param1=value1&param2=value2&...`. You already used it when querying maps using JavaScript.
* __POST__ consists in sending parameters implicitely within the request to the server. The parameters are not shown on the URL.

GET and POST parameters are received by the server and can be used as wanted. While using GET or POST is let to the user choice, the following rule is usually followed
* GET is used to query information from a server. The parameters are sent in clear textual form and should not be considered as private information.
* POST is used to send information to a server (that may update its database accordingly). POST can be used to send data that should not be disclosed in public (ex. a user ID, a credit card number, etc).

## Communicating via url parameters

* Consider the following PHP code

```php
<?php
foreach($_GET as $name=>$value) {
  print "<p>($name,$value)</p>";
}
?>
```

* Run the server localy, and query this page with the following url

```bash
http://localhost:8000/?param1=value1&param2=value2
```

* Observe that the server received the pair of (parameter,value) corresponding to your requests. The GET parameters are automatically accessible from the PHP code using the global `$_GET` variable.

__Q.__ Create a php script that print your firstname and lastname given as parameters in the url `url/?firstname=[value]&lastname=[value]` as shown in [this link](https://imagecomputing.net/damien.rohmer/teaching/2017_2018/semester_2/CSE_104/online_exercices/C_server/03_php_get_post/02_get_name/?firstname=John&lastname=Doe). If the parameters are not set, the message "Hello unknown" should appear.

_Tips_: You can check that a parameter is provided using the function [isset](http://php.net/manual/en/function.isset.php) (ex. if( isset($_GET["param"]) {...}` ).

__Q.__ Create a php script that show the image from which the user request within its url.
* You will consider a set of limited pictures with a specific name (ex. `bird.jpg`, `cameleon.jpg`, `cat.jpg`, `dog.jpg`, `squirrel.jpg`) in a directory `pictures/`.
* The user query is expected to match one of the available filename (ex. `?draw=bird`, `?draw=squirrel`, etc.)
* [Example of working script](https://imagecomputing.net/damien.rohmer/teaching/2017_2018/semester_2/CSE_104/online_exercices/C_server/03_php_get_post/03_get_picture/?draw=dog).

## Communicating via HTML forms

While url parameters can be sent in an automatic way, HTML forms containing inputs ([as seen in JavaScript](https://github.com/drohmer/CSE104/tree/master/B_javascript/04_inputs)) are the common way to provide information directly from the user.

The general syntax of an HTML form using the GET method to transfert the information into the `url/file.php` script is the following

```html
<form action="url/file.php">
<input type="someType1" name="nameParameter1">
<input type="someType2" name="nameParameter2">
...
<input type="submit" value="Submit">
</form>
```

__Q.__ Create a form [similar to this page](https://imagecomputing.net/damien.rohmer/teaching/2017_2018/semester_2/CSE_104/online_exercices/C_server/03_php_get_post/04_form/) asking firstname, lastname, and email. When the user click on Submit, a message greeting him by its name and reminding the email is printed.

Observe that GET method is used by default for the query, thus the parameters on the form appears in the url after you click on the Submit button.

## Post message

POST method can also be used to send informations to the server from a form - typically to avoid that all parameters appears on the resulting url.

* To send using POST method, change the HTML form beginning by the following
```html
<form action="url/file.php" method="post">
```

* POST parameters can be retrieved in your php script using the global variable `$_POST`. Its use is similar to the `$_GET` variable used so far.

__Q.__ Modify your previous exercise to send your firstname, lastname, and mail adress using POST method.

## Exercise - Shared email listing

__Q.__ Create an application similar to the [one shown in example](https://imagecomputing.net/damien.rohmer/teaching/2017_2018/semester_2/CSE_104/online_exercices/C_server/03_php_get_post/05_exercise_email_list/).
* The user can add a name (firstname, lastname) and an email to the server.
* The server stores the contact in a csv file (text file where each element is separated by, for instance, a comma). (note that csv files can be read and modified using standard spreadsheet tools such as Excel/LibreOffice).
* The contact should be sent using a POST method to the server.
* The user can also query, from the first and last name, the email of somebody in the file. If somebody is found in the list, its email is shown, otherwise a message indicates that nobody has been found.
* This query should be sent using GET method.

_Note:_ Don't forget that the list is aimed to be hosted on a server. Therefore, every user accessing the website will be sharing the same contact list.