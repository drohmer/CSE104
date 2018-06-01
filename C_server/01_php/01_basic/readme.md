# Introduction to PHP

PHP (Hypertext Preprocessor) is a programing language enabling to automatise the creation of HTML webpage. PHP code is executed on the server side, which generates and return its result as an HTML page to the client.

## First embedded PHP program

PHP can be embedded inside HTML code, which allows to write HTML in a standard way, while only including PHP when needed.


### Writing PHP

* Create a php file named `index.php` with the following code

```php
<!DOCTYPE html>
<html>

<head>
<title>My first Webpage in PHP</title>
</head>

<body>

</body>

</html>
```

Note that, so far, this code consists only in valid HTML.

* Add the following PHP code between the `<body>` markups

```php
<?php 
print "This text is written by PHP!";
?>
```

Note that the `print` command in PHP allows to print the value within the resulting HTML page.

### Executing PHP

Contrary to HTML and JavaScript, PHP files cannot be executed directly by the browser. PHP are meant to be executed by a PHP interpreter on a server.

* Run the following command from a terminal in the directory of your index.php file.

```bash
php -S localhost:8000
```

This command run the php interpreter and start a server on the address `localhost` on the port 8000 (note that you can use other port number). Note that `localhost` is a common hostname designating the local machine. This emulate the behavior of a server that run locally on your machine.

* Start your browser at the following address `http://localhost:8000/`

You should be able to see the message "This text is written by PHP!" in your browser.

_Explanation_: Your browser queried the server at the address `localhost` on the port 8000 (the local machine). This server was listening and answered in executing the PHP interpreter on the file `index.php` by default. The result is the HTML file you can observe in your browser.

### Loop

The previous program has no advantage compared to basic HTML. However, PHP can automatise task in using conditionals and loops.

* Add the following PHP code and observe the result

```php
for($k=0; $k<10; $k++) {
  print "<p> $k </p>";
}
```

__Note__
* PHP variables are preceded of the $ symbol.
* PHP variables are typed dynamically
* Each PHP sentence should be terminated by a ";"

* Observe the source code of the HTML result in your browser. Note that the PHP source doesn't appear. You only see the resulting HTML code. At the opposite of JavaScript which is executed locally by the client, PHP is executed on the server, thus the client can only observe the result but not the code source.

## Array

PHP arrays are similar to JavaScript arrays as they can contain any element, with, possibly, non-consecutive index.

Example:

```php
$someArray = [8,7,4,"string",1.2];
$someArray[15] = "some other element";
```

* Use the [foreach($arrayName as $elementName)](http://php.net/manual/en/control-structures.foreach.php) statement to loop over and print all elements of the array

* Use the [foreach($arrayName as $key=>$elementName)](http://php.net/manual/en/control-structures.foreach.php) statement to loop over and print the elements of the array and the associated keys.

## Functions

Functions can be defined using the syntax
[function nameFunc($arg_1,$arg_2,...)](http://php.net/manual/en/functions.user-defined.php)

* Copy and test the following php code

```php
<?php 
function sayHello($name) {
  print "<p>Hello $name</p>";
}
?>

<?php
sayHello("John");
sayHello("Dave");
?>
```

## File inclusion

PHP is able to include and concatenate the content from various files using the [include](http://php.net/manual/en/function.include.php) or [require](http://php.net/manual/en/function.require.php) functions. This allows to split your resulting HTML files into separated elements that can be reused in different context.

The behavior of `include` and `require` are similar excepted in the failure case when the file cannot be found. In this case, `include` will emit a warning and the PHP interpretation will continue, while `require` will end the interpretation with a fatal error.

* Create a file `index.php` with the following content

```php
<?php require 'part_1.php'; ?>
<?php require 'part_2.php'; ?>
```

* Create the corresponding `part_1.php` and `part_2.php` with the following content

```php
<?php
$number = 1;
print "<p>This is part $number</p>";
?>
```

and

```php
<p>This is part 2!!</p>"
```

* Observe the inclusion of the two files when loading `index.php` from the local server.
* Observe the behavior when `part_1.php` is not accessible (removed or renamed for instance). Change `require` into `include` and observe that, in this case, the page is loaded but only `part_2` is included.


One of the common use of file inclusion is to reuse common parts in different html pages such as menu, and footer informations. This allows to avoid copy/paste in multiple HTML files, that would lead to complex and error-prone  update process.

__Q.__ Copy the behavior of the [following page](https://imagecomputing.net/damien.rohmer/teaching/2017_2018/semester_2/CSE_104/online_exercices/C_server/01_php/01_basic/index.php) using PHP.
* The website has two main pages: `index.php` and `contact.php` who only differ from their content.
* The menu and the footer are identical in both pages: they should be described only once in a `header.php` and `footer.php`. Their content should be included in `index.php` and `contact.php`.
* The date of the copyright can be automatically computed to the current year using the function [date](http://php.net/manual/en/function.date.php).


