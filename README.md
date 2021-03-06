# Rcopy :floppy_disk:
RCopy uses curl to copy files from a remote server and store them to a local directory.

Rcopy.php is a working example that implements the _downloadFile_ class (**Rcopy-downloadFile-class.php**).

RcopyCLI.php is a comand line version and it supports realtime progress reporting and resumable downloads.

___

**The format for using the CLI version is as follows:**

```bash
$ php /path/to/RcopyCLI.php URL  fileName
```

##### For example to download an image called `file.jpeg` from `http://example.com/` and store it as `saved.jpeg`, here is how you'll do it

```bash
$ php RcopyCLI.php http://example.com/file.jpeg saved.jpeg

```
##### **_To resume or retry a download, just enter the same url and file name as before_** 
___

#### Example using `Rcopy-downloadFile-class.php`.  


```php
<?php
require_once("Rcopy-downloadFile-class.php");

$save = new downloadFile();

$filesize = $save->getSize($url);
$returnData = $save->saveFile($url,$folder);
$save->logDownload($returnData,'logs.php.inc');

print_r($returnData);
print_r($filesize);

```

In the example above **$returnData[]** is an array that contains the data returned by the script

> `$returnData[0]` is set to true or false depending on whether the `curl_exec()` returns `true or false`

> `$returnData[1]` contains the name of the `directory` where the file was stored

> `$returnData[2]` contains the url that was copied

> `$returnData[3]` contains the name of the stored file

> `$returnData[4]` contains the path to the new file 

**$save->getSize($url)** returns the size of the file in bytes

**$save->logDownload($returnData,$logFileName)** creates a php array containing the url and the folder in the file `$logFileName`
