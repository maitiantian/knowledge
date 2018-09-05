# npm

__npm install/i/add packagename@X.Y.Z -S/-D/-E__

-S: --save，把模块的版本信息保存到dependencies（生产环境依赖）中

-D: --save-dev，把模块版本信息保存到devDependencies（开发环境依赖）中

-E: --save-exact，精确安装模块的指定版本，dependencies字段里模块版本号前面的^会消失

### ~ | ^ | *

```json

```

|符号|实例|匹配|
|:---|:---|:---|
|~|~1.2.3|1.2.latest|
|^|^1.2.3|1.latest.latest|
|*|\*|latest.latest.latest|

|Version|Explanation|
|:---|:---|
|v2.0.0, =2.0.0|The v and the = will be removed and the exact version 2.0.0 will be used.|
|latest|Takes the latest version possible. Not the safest thing to use.|
|*, x|Wildcards. Can be any version at all. Crazy stuff.|
|4, 4.*, 4.x, ~4, ^4|Any version that starts with 4. Takes the latest.|
|>4.8.5|Choose any version greater than a specific version. Could break your application.|
|<4.8.5|Choose any version lower than a specific version.|
|>=4.8.5|Anything greater than or equal to a specific version.|
|<=4.8.5|Anything less than or equal to.|
|4.8.3 - 4.8.5|Anything within a range of versions. The equivalent of >=4.8.3 and <=4.8.5|
|~4.8.5|Any version "reasonably close to 4.8.5". This will call use all versions up to, but less than 4.9.0|
|~4.8|Any version that starts with 4.8|
|^4.8.5|Any version "compatible with 4.8.5". This will call versions up to the next major version like 5.0.0. Could break your application if there are major differences in the next major version.|
|~1.2|Any version compatible with 1.2|


Best Practices: __Use the tilde so you don't break your applications, but still get the latest bug fixes.__

Personally, when calling dependencies for my project, I will use the tilde (~). By specifying your express dependency using ~4.8.5, you will be able to get bug fixes when new smaller versions come around, but you won't grab versions that break your project.