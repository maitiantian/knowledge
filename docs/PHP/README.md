# PHP

[PHP官方文档](https://www.php.net/manual/zh/)

# 预定义变量

## 超全局变量

“Superglobal”，又称自动化的全局变量，在全部作用域中始终可用的内置变量，在函数或方法中无需执行 `global $variable;` 就可以访问它们。

#### $GLOBALS

一个包含了所有全局变量的全局组合数组，数组的键就是变量名。

与所有其他超全局变量不同，$GLOBALS在PHP中总是可用的。

```php
<?php
function test() {
    $foo = "local variable";
    echo '$foo in global scope: ' . $GLOBALS["foo"] . "\n";
    echo '$foo in current scope: ' . $foo . "\n";
}
$foo = "Example content";
test();
?>

// $foo in global scope: Example content
// $foo in current scope: local variable
```

#### $_SERVER

一个包含了诸如头信息(header)、路径(path)、以及脚本位置(script locations)等等信息的数组。这个数组中的项目由 Web 服务器创建，__不能保证每个服务器都提供全部项目__。
如果以命令行方式运行 PHP，下面列出的元素几乎没有有效的(或是没有任何实际意义的)。

* PHP\_SELF：当前执行脚本的文件名，与 document root 有关。如在地址为 http://example.com/foo/bar.php 的脚本中使用 $\_SERVER['PHP_SELF'] 将得到 /foo/bar.php；
* argv：传递给该脚本的参数的数组；
    * 当脚本以命令行方式运行时，argv 变量传递给程序 C 语言样式的命令行参数；
    * 当通过 GET 方式调用时，该变量包含query string。
* argc：包含命令行模式下传递给该脚本的参数的数目；
* GATEWAY\_INTERFACE：服务器使用的 CGI 规范的版本，如 “CGI/1.1”；
* SERVER\_ADDR：当前运行脚本所在的服务器的 IP 地址；
* SERVER\_NAME：当前运行脚本所在的服务器的主机名；
    > 在 Apache 2 里，必须设置 UseCanonicalName = On 和 ServerName。否则该值会由客户端提供，就有可能被伪造。上下文有安全性要求的环境里，不应该依赖此值。
* SERVER\_SOFTWARE：服务器标识字符串，在响应请求时的头信息中给出；
* SERVER\_PROTOCOL：请求页面时通信协议的名称和版本，如 “HTTP/1.0”；
* REQUEST\_METHOD：访问页面使用的请求方法，“GET”, “HEAD”，“POST”，“PUT”；
    > 如果请求方法为 HEAD，PHP 脚本将在发送 Header 头信息之后终止。
* REQUEST\_TIME：请求开始时的时间戳；
* REQUEST\_TIME\_FLOAT：请求开始时的时间戳，微秒级别的精准度；
* QUERY\_STRING：query string（查询字符串）；
* DOCUMENT\_ROOT：当前运行脚本所在的文档根目录，在服务器配置文件中定义；
* HTTP\_ACCEPT：当前请求头中 Accept 项的内容；
* HTTP\_ACCEPT\_CHARSET：当前请求头中 Accept-Charset 项的内容，如 “iso-8859-1,*,utf-8”；
* HTTP\_ACCEPT\_ENCODING：当前请求头中 Accept-Encoding 项的内容，如 “gzip”；
* HTTP\_ACCEPT\_LANGUAGE：当前请求头中 Accept-Language 项的内容，如 “en”；
* HTTP\_CONNECTION：当前请求头中 Connection 项的内容，如 “Keep-Alive”。
* HTTP\_HOST：当前请求头中 Host 项的内容；
* HTTP\_REFERER：引导用户代理到当前页的前一页的地址（如果存在）。由 user agent 设置决定，并不是所有的用户代理都会设置该项，有的还提供了修改 HTTP_REFERER 的功能。因此该值并不可信；
* HTTP\_USER\_AGENT：当前请求头中 User-Agent 项的内容，包含了访问该页面的用户代理的信息，如Mozilla/4.5 [en] (X11; U; Linux 2.2.9 i586)。
    * 还可以通过 get_browser() 来使用该值，从而定制页面输出以便适应用户代理的性能。
* HTTPS：如果脚本是通过 HTTPS 协议被访问，则被设为一个非空的值。
    > 注意当使用 IIS 上的 ISAPI 方式时，如果不是通过 HTTPS 协议被访问，这个值将为 off。
* REMOTE\_ADDR：浏览当前页面的用户的 IP 地址；
* REMOTE\_HOST：浏览当前页面的用户的主机名。DNS 反向解析不依赖于用户的 REMOTE_ADDR；
    > 服务器必须被配置以便产生这个变量。例如在 Apache 中，需要在 httpd.conf 中设置 HostnameLookups On 来产生它。参见 gethostbyaddr()。
* REMOTE\_PORT：用户机器上连接到 Web 服务器所使用的端口号；
* REMOTE\_USER：经验证的用户；
* REDIRECT\_REMOTE\_USER：验证的用户，如果请求已在内部重定向；
* SCRIPT\_FILENAME：当前执行脚本的绝对路径；
    > 如果在命令行界面（Command Line Interface, CLI）使用相对路径执行脚本，如 file.php 或 ../file.php，那么 $\_SERVER['SCRIPT_FILENAME'] 将包含用户指定的相对路径。
* SERVER\_ADMIN：Apache 服务器配置文件中的 SERVER_ADMIN 参数。如果脚本运行在一个虚拟主机上，则该值是那个虚拟主机的值；
* SERVER\_PORT：Web 服务器使用的端口，默认“80”，如果使用 SSL 安全连接，则这个值为用户设置的 HTTP 端口；
    > 在 Apache 2 里，为了获取真实物理端口，必须设置 UseCanonicalName = On 以及 UseCanonicalPhysicalPort = On，否则此值可能被伪造。上下文有安全性要求的环境里，不应该依赖此值。
* SERVER\_SIGNATURE：服务器版本和虚拟主机名的字符串；
* PATH\_TRANSLATED：当前脚本所在文件系统（非文档根目录）的基本路径，这是在服务器进行虚拟到真实路径的映像后的结果；
    > 自 PHP 4.3.2 起，PATH\_TRANSLATED 在 Apache 2 SAPI 模式下不再和 Apache 1 一样隐含赋值，而是若 Apache 不生成此值，PHP 便自己生成并将其值放入 SCRIPT\_FILENAME 服务器常量中。这个修改遵守了 CGI 规范，PATH\_TRANSLATED 仅在 PATH\_INFO 被定义的条件下才存在。Apache 2 用户可以在 httpd.conf 中设置 AcceptPathInfo = On 来定义 PATH_INFO。
* SCRIPT\_NAME：当前脚本的路径，这在页面需要指向自己时非常有用；
    * \_\_FILE\_\_ 常量包含当前脚本(例如包含文件)的完整路径和文件名。
* REQUEST\_URI：要访问的页面，如 “/index.html?a=1&b=2”；
* PHP\_AUTH\_DIGEST：当作为 Apache 模块运行时，进行 HTTP Digest 认证的过程中，此变量被设置成客户端发送的“Authorization” HTTP 头内容（以便作进一步的认证操作）；
* PHP\_AUTH\_USER：当 PHP 运行在 Apache 或 IIS（PHP 5 是 ISAPI）模块方式下，并且正在使用 HTTP 认证功能，这个变量便是用户输入的用户名；
* PHP\_AUTH\_PW：当 PHP 运行在 Apache 或 IIS（PHP 5 是 ISAPI）模块方式下，并且正在使用 HTTP 认证功能，这个变量便是用户输入的密码；
* AUTH\_TYPE：当 PHP 运行在 Apache 模块方式下，并且正在使用 HTTP 认证功能，这个变量便是认证的类型；
* PATH\_INFO：包含由客户端提供的、跟在真实脚本名称之后并且在查询语句（query string）之前的路径信息。例如如果当前脚本通过 URL http://www.example.com/php/path_info.php/some/stuff?foo=bar 被访问，那么 $\_SERVER['PATH\_INFO'] 将包含 /some/stuff。

```php
<table border="1">
	<?php 
		foreach($_SERVER as $key=>$value){
			echo "<tr><td>".$key."</td><td>".$value."</td><tr>";
		}
	 ?>
</table>
```


#### $_GET

通过 URL 参数传递给当前脚本的变量组成的关联数组。

```php
<?php
    echo 'Hello ' . htmlspecialchars($_GET["name"]) . '!';
?>

// http://example.com/?name=Hannes
// Hello Hannes!
```


#### $_POST

当 HTTP POST 请求的 Content-Type 是 application/x-www-form-urlencoded 或 multipart/form-data 时，传递给当前脚本的所有变量组成的关联数组。

```php
<?php
    echo 'Hello ' . htmlspecialchars($_POST["name"]) . '!';
?>

// 通过 HTTP POST 方式传递了参数 name=Hannes
// Hello Hannes!
```


#### $_FILES

当 HTTP POST 请求的 Content-Type 是 multipart/form-data 时，上传到当前脚本的所有文件组成的关联数组。

```html
<!-- The data encoding type, enctype, MUST be specified as below -->
<form enctype="multipart/form-data" action="__URL__" method="POST">
    <!-- MAX_FILE_SIZE must precede the file input field -->
    <input type="hidden" name="MAX_FILE_SIZE" value="30000" />
    <!-- Name of input element determines name in $_FILES array -->
    Send this file: <input name="userfile" type="file" />
    <input type="submit" value="Send File" />
</form>
```

* $\_FILES['userfile']['name']：文件的原名称；
* $\_FILES['userfile']['type']：文件的 MIME 类型，如 “image/gif”。MIME 类型在 PHP 端并不检查，因此不一定会有这个值；
* $\_FILES['userfile']['size']：已上传文件的大小，单位字节；
* $\_FILES['userfile']['tmp_name']：文件被上传后在服务端储存的临时文件名；
* $\_FILES['userfile']['error']：和该文件上传相关的错误代码。
    * UPLOAD\_ERR\_OK，值为 0：没有错误，文件上传成功；
    * UPLOAD\_ERR\_INI\_SIZE，值为 1：文件超过了 php.ini 中 upload\_max\_filesize 限制的值；
    * UPLOAD\_ERR\_FORM\_SIZE，值为 2：文件超过了 HTML 表单中 MAX\_FILE\_SIZE 限制的值；
    * UPLOAD\_ERR\_PARTIAL，值为 3，文件只有部分被上传；
    * UPLOAD\_ERR\_NO\_FILE，值为 4，没有文件被上传；
    * UPLOAD\_ERR\_NO\_TMP\_DIR，值为 6，找不到临时文件夹；
    * UPLOAD\_ERR\_CANT\_WRITE，值为 7，文件写入失败。

文件被上传后，默认储存在服务端的默认临时目录中，除非 php.ini 中的 upload\_tmp\_dir 设置为其它的路径。


#### $_COOKIE

通过 HTTP Cookies 方式传递给当前脚本的变量组成的关联数组。


#### $_SESSION

当前脚本可用 SESSION 变量的数组。


#### $_REQUEST

默认情况下包含了 $\_GET，$\_POST 和 $\_COOKIE 的关联数组。


#### $_ENV

通过环境方式传递给当前脚本的变量组成的关联数组。


