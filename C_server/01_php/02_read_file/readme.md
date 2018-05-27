# File

For security reasons, client based JavaScript code has limited access to the ressources of the host system. Your browser acts as a so called 'sandbox' protecting the rest of your system from external code from the internet. Therefore reading/writing file on the client system is not a basic feature of the JavaScript language.
At the opposite, servers don't execute external code, but their own. Therefore, they are supposed to be able to handle their environment. As a result code executed on a server can easily access to local files on the same server.


## List files in directory

The [scandir](http://php.net/manual/en/function.scandir.php) command allows to list the set of files and directories from a specific path.

* Create a directory `picture/` and place a set of `jpg` images inside it.
* Create a PHP script listing and printing the name of all files within the `picture/` directory.
*  Modify your script to generate an HTML file that draw all images inside the `picture/` directory.

## Read/Write files

The functions [file_get_contents](http://php.net/manual/en/function.file-get-contents.php) and [file_put_contents](http://php.net/manual/en/function.file-put-contents.php) are able to respectively read the content of a file, and write in it.

__Q.__ Create a PHP script that stores and print the total number of times the webpage has been seen.
* The number should be permanently stored (and updated) in a file on the hard-drive.
* Tips: You can create a text file containing initially the value 0. Then your php script, read the content of the file, add 1 to the number, store it in the file, and print it in the HTML.