# 目录
* [数据类型](#数据类型)


* 不要使用new Number()、new Boolean()、new String()创建包装对象；
* 用parseInt()或parseFloat()来转换任意类型到number；
* 用String()来转换任意类型到string，或者直接调用某个对象的toString()方法；
* 通常不必把任意类型转换为boolean再判断，因为可以直接写if (myVar) {...}；
* typeof操作符可以判断出number、boolean、string、function和undefined；
* 判断Array要使用Array.isArray(arr)；
* 判断null请使用myVar === null；
* 判断某个全局变量是否存在用typeof window.myVar === 'undefined'；
* 函数内部判断某个变量是否存在用typeof myVar === 'undefined'。


# <p align="center">数据类型</p>

###### [<p align="right">back to top ▲</p>](#目录)

## 五种基本数据类型

#### Undefined类型

* Undefined类型只有一个值，即undefined；
* 在使用var声明变量但未对其加以初始化时，这个变量的值就是undefined；

    ```javascript
    var message;
    alert(message == undefined);    //true
    //等价于
    var message = undefined;
    alert(message == undefined);    //true
    ```

* 对于尚未声明过的变量，只能执行一项操作，即使用typeof操作符检测其数据类型。

    ```javascript
    //下面这个变量没有声明
    // var age;
    alert(age);         //Uncaught ReferenceError: age is not defined
    alert(typeof age);  //"undefined"
    ```

#### Null类型

* Null类型只有一个值，即null；
* null值表示一个空对象指针，所以用typeof检测null值时会返回"object"；
* 如果声明的变量准备在将来用于保存对象，那么最好将该变量初始化为null而不是其他值。这样只要直接检查null值就可以知道该变量是否已经保存了一个对象的引用；

    ```javascript
    if(car != null){
        //对car对象执行某些操作
    }
    ```

* undefined值派生自null值，alert(null == undefined);   //true

#### Boolean类型

* Boolean类型有两个值，true和false；
* Boolean类型的字面值只有两个，但ECMAScript中所有类型的值都有与这两个boolean值等价的值。要将一个值转换为其对应的boolean值，可以调用转型函数Boolean()；

    ```javascript
    var message = "Hello World!";
    var messageAsBoolean = Boolean(message);    //true
    ```

|数据类型|转换为true的值|转换为false的值|
|:---|:---|:---|
|boolean|true|false|
|string|任何非空字符串|""（空字符串）|
|number|任何非零数字值（包括无穷大）|0和NaN|
|object|任何对象|null|
|undefined|不适用|undefined|

#### Number类型

* 整数
    * 十进制："var intNum = 55;"；
    * 八进制：八进制字面值的第一位必须是零（0），然后是八进制数字序列（0～7）。如果字面值中的数值超出了范围，那么前导零将被忽略，后面的数值将被当作十进制数值解析。八进制字面量在严格模式无效，会使JavaScript引擎报错："SyntaxError: Octal literals are not allowed in strict mode."；

        ```javascript
        var octalNum1 = 070;    //八进制的56
        var octalNum2 = 079;    //无效的八进制数值——解析为79
        var octalNum3 = 08;     //无效的八进制数值——解析为8
        ```
    * 十六进制：十六进制字面值的前两位必须是0x，后跟任何十六进制数字（0～9及A～F/a~f）；

        ```javascript
        var hexNum1 = 0xA;  //十六进制的10
        var hexNum2 = 0x1f; //十六进制的31
        var hexNum3 = 0x1g; //Uncaught SyntaxError: Invalid or unexpected token
        ```
    * 进行算术计算时，所有以八进制和十六进制表示的数值最终都将被转换成十进制数值。
* 浮点数

    ```javascript
    var floatNum1 = 1.1
    var floatNum2 = 0.1
    var floatNum3 = .1  //有效，但不推荐
    //保存浮点数需要的内存空间是整数的两倍，
    //因此ECMAScript会不失时机地将浮点数值转换为整数值。
    //如果浮点数值本身表示的就是一个整数（如 1.0），那么该值也会被转换为整数。
    var floatNum4 = 1.      //小数点后没有数字——解析为1
    var floatNum5 = 10.0    //整数——解析为10

    //对于极大或极小的数值，可以用科学计数法表示。
    var floatNum6 = 3.125e7 //等于3125000
    var floatNum7 = 3e-17    //等于0.00000000000000003
    //ECMASctipt默认会将小数点后面带有6个零以上的浮点数值转换为科学计数法。
    var floatNum8 = 0.0000003
    floatNum8   //3e-7

    //浮点数进行算术运算时精确度远不如整数。
    0.1 + 0.2   //0.30000000000000004
    0.05 + 0.25 //0.3
    0.15 + 0.15 //0.3
    if(a + b == 0.3){   //永远不要测试某个特定的浮点数值。
        alert("You got 0.3!")
    }
    ```

* 数值范围

    ```javascript
    Number.MIN_VALUE    //ECMAScript能够表示的最小数值：5e-324
    Number.MAX_VALUE    //ECMAScript能够表示的最大数值：1.7976931348623157e+308

    //如果某次计算结果超出JavaScript数值范围的值，
    //那么这个数值会被自动转换成特殊的Infinity值。
    //如果这个数值是负数，会被转换成-Infinity（负无穷），
    //如果这个数值是正数，会被转换成Infinity（正无穷）。
    //Infinity是不能够参与计算的数值。

    //可以使用isFinite()函数确定一个数值是不是有穷的，
    //这个函数在参数位于最小与最大数值之间时会返回true：
    var result = Number.MAX_VALUE + Number.MAX_VALUE;
    alert(isFinite(result)); //false

    Number.NEGATIVE_INFINITY    //-Infinity
    Number.POSITIVE_INFINITY    //Infinity
    ```

* NaN
    * 非数值（Not a Number），一个特殊的数值，用于表示一个本来要返回数值的操作未返回数值的情况，这样就不会报错了；

        ```javascript
        0/0     //NaN
        正数/0  //Infinity
        负数/0  //-Infinity
        ```

    * 任何涉及NaN的操作都会返回NaN（如NaN/10）；
    * NaN与任何值都不相等，包括NaN本身（alert(NaN == NaN);   //false）;
    * isNaN()，这个函数帮我们确定一个数是否“不是数值”。

        ```javascript
        //isNaN()在接收到一个值之后，会尝试将这个值转换为数值，
        //而任何不能被转换为数值的值都会导致这个函数返回true。   
        alert(isNaN(NaN));      //true
        alert(isNaN(10));       //false（10是一个数值）
        alert(isNaN("10"));     //false（可以被转换成数值10）
        alert(isNaN("blue"));   //true（不能转换成数值）
        alert(isNaN(true));     //false（可以被转换成数值1）

        //isNaN()也适用于对象,
        //用isNaN()测试对象时，会先调用对象的valueOf()方法，确定其返回值是否能转换为数值；
        //如果对象没有valueOf()方法，则调用对象的toString()方法，确定该其返回值是否能转换为数值；
        //如果对象没有valueOf()和toString()方法，返回true；
        ```

* 数制转换
    * Number()：可以用于任何数据类型；
        * Boolean值：true和false将分别被转换为1和0；
        * 数字值：只是简单的传入和返回；
        * null值：返回0；
        * undefined：返回NaN；
        * 字符串，遵循下列规则：
            * 只含数字（包括前面带正号或负号的情况），转换为十进制数值，"1"变成1，"123"变成123，"011"、"0011"变成11（注意：前导的零被忽略）；
            * 包含有效的浮点格式，如"1.1"，转换为对应的浮点数值（同样忽略前导零）；
            * 包含有效的十六进制格式，例如"0xf"，转换为相同大小的十进制整数值；
            * 空串（不包含任何字符），转换为0；
            * 包含除上述格式之外的字符，转换为NaN。
        * 对象：调用对象的valueOf()方法，然后依照前面的规则转换返回的值；如果对象没有valueOf()方法，则调用toString()方法，再前面的规则转换返回的字符串值；如果对象没有valueOf()和toString()方法，则返回NaN。
    * parseInt()：用于转换String类型，其余类型值会先转换为String类型；
        1. 忽略字符串前面的空格，直至找到第一个非空格字符；
        2. 如果第一个字符不是数字字符或者负号，返回NaN（parseInt("")-->NaN，Number("")-->0）；
        3. 如果第一个字符是数字字符，则继续解析第二个字符，直到解析完所有后续字符或者遇到一个非数字字符；
        4. parseInt()能够识别十六进制整数：如果字符串以"0x"开头且后跟数字字符，会将其当作一个十六进制整数；
        5. 在ECMAScript 5 JavaScript引擎中，parseInt()已不具有解析八进制值的能力，parseInt("070")-->70；
        6. 可以为parseInt()提供第二个参数：转换时使用的基数，即多少进制。
            ```javascript
            var num1 = parseInt("0xAF", 16);	//175
            var num2 = parseInt("AF", 16); 		//175，指定16作第二个参数，字符串前可以不带"0x"
            var num3 = parseInt("10", 2); 		//2 （按二进制解析）
            var num4 = parseInt("10", 8); 		//8 （按八进制解析）
            var num5 = parseInt("10", 10); 		//10（按十进制解析）
            var num6 = parseInt("10", 16); 		//16（按十六进制解析）

            //不指定基数意味着让parseInt()决定如何解析输入的字符串，
            //为了避免错误的解析，建议任何情况下都明确指定基数。
            ```
    * parseFloat()：用于转换String类型，其余类型值会先转换为String类型。
        1. 从第一个字符（位置 0）开始解析每个字符；
        2. 一直解析到字符串末尾，或遇见一个无效的浮点数字字符为止；
        3. 字符串中第一个小数点是有效的，第二个小数点是无效的，它后面的字符串将被忽略；
        4. parseFloat()只解析十进制值，它没有用第二个参数指定基数的用法；
        5. 十六进制格式的字符串则始终会被转换成0；
        6. 如果字符串是一个可解析为整数的数（没有小数点，或者小数点后都是零），parseFloat()会返回整数。
        ```javascript
        var num1 = parseFloat("1234blue"); 	//1234 （整数）
        var num2 = parseFloat("0xA"); 		//0
        var num3 = parseFloat("22.5"); 		//22.5
        var num4 = parseFloat("22.34.5"); 	//22.34
        var num5 = parseFloat("0908.5"); 	//908.5
        var num6 = parseFloat("3.125e7"); 	//31250000
        ```
    


#### String类型

字符串：由零或多个16位Unicode字符组成的字符序列。

* 字符字面量：String类型数据包含一些特殊的字符字面量，也叫转义序列，用于表示非打印字符，或者一些特殊字符。

|字面量|含义|
|:---|:---|
|\n|换行|
|\t|制表|
|\b|空格|
|\r|回车|
|\f|进纸|
|\\\ |斜杠|
|\\'|单引号（'），在用单引号表示的字符串中使用。例如：'He said, \\'hey.\\' '|
|\\"|双引号（"），在用双引号表示的字符串中使用。例如："He said, \\"hey.\\" "|
|\xnn|以十六进制代码nn表示的一个字符（其中n为0～F）。例如， \x41表示"A"|
|\unnnn|以十六进制代码nnnn表示的一个Unicode字符（其中n为0～F）。例如，\u03a3表示希腊字符Σ|

这些字符字面量可以出现在字符串中的任意位置，而且也将被作为一个字符来解析：

```javascript
var sigma = "\u03a3";
sigma;          //"Σ"
sigma.length;   //1
```

* 字符串特点：ECMAScript中的字符串是不可变的，字符串一旦创建，它的值就不能改变。要改变某个变量保存的字符串，首先要销毁原来的字符串，再用另一个包含新值的字符串填充该变量。

* 转换为字符串

    要把一个值转换为一个字符串有两种方式：

    1. 使用几乎每个值都有的toString()方法，改方法返回相应值的字符串表现；

        ```javascript
        true.toString();	// 字符串"true"
        "abc".toString();	// 字符串"abc"

        10.toString();	//Uncaught SyntaxError: Invalid or unexpected token
        var num = 10;
        var numAsString = num.toString();	// 字符串"11"
        alert(num.toString());		// "10"
        // 通过传递基数，toString()可以输出二、八、十六进制，乃至任意有效进制格式的字符串值。
        alert(num.toString(2));		// "1010"
        alert(num.toString(8));		// "12"
        alert(num.toString(10));	// "10"
        alert(num.toString(16));	// "a"
        ```

    2. 在不知道要转换的值是不是null或undefined的情况下，可以使用转型函数String()，这个函数能将任何类型的值转换为字符串。

        * 值有toString()方法，调用该方法（没有参数）并返回相应的结果；
        * 值是null，返回"null"；
        * 值是undefined，返回"undefined"。



## 一种复杂数据类型

#### Object类型

ECMAScript中的对象其实就是一组数据和功能的集合。对象可以通过执行new操作符后跟要创建的对象类型的名称来创建：

```javascript
var obj1 = new Object();
// 如果不给构造函数传递参数，可以省略后面的那一对圆括号，但不推荐
var obj2 = new Object;
```

Object的每个实例都具有下列属性和方法：

* constructor：保存用于创建当前对象的函数；
* hasOwnProperty(propertyName)：用于检查给定的属性在当前对象实例中（而不是在实例的原型中）是否存在。作为参数的属性名（propertyName）必须以字符串形式指定（例如：o.hasOwnProperty("name")）；
* isPrototypeOf(object)：用于检查传入的对象是否是传入对象的原型；
* propertyIsEnumerable(propertyName)：用于检查给定的属性是否能够使用for-in语句来枚举。作为参数的属性名必须以字符串形式指定；
* toLocaleString()：返回对象的字符串表示，该字符串与执行环境的地区对应；
* toString()：返回对象的字符串表示；
* valueOf()：返回对象的字符串、数值或布尔值表示。通常与toString()方法的返回值相同。

__在ECMAScript中Object是所有对象的基础，因此所有对象都具有这些基本的属性和方法：__


## 引用类型

引用类型的值（对象）是**引用类型**的一个实例。在 ECMAScript 中，引用类型是一种数据结构，用于将数据和功能组织在一起。

它也常被称为**类**，但这种称呼并不妥当。尽管 ECMAScript 从技术上讲是一门面向对象的语言，但它不具备传统的面向对象语言所支持的类和接口等基本结构。

引用类型有时候也被称为**对象定义**，因为它们描述的是一类对象所具有的属性和方法。

> 虽然引用类型与类看起来相似，但它们并不是相同的概念。

对象是某个特定引用类型的实例。新对象是使用 new 操作符后跟一个构造函数来创建的。

构造函数本身就是一个函数，只不过该函数是出于创建新对象的目的而定义的。

```javascript
var person = new Object();
// 这行代码创建了 Object 引用类型的一个新实例，然后把该实例保存在了变量 person 中。
// Object 是构造函数，为新对象定义了默认的属性和方法。
// ECMAScript 提供了很多原生引用类型（例如 Object），以便开发人员用以实现常见的计算任务。
```


#### Object 类型

虽然 Object 的实例不具备多少功能，但对于在应用程序中存储和传输数据而言，它们确实是非常理想的选择。

创建 Object 实例的方式有两种：

```javascript
// 1. new 操作符后跟 Object 构造函数：
var person = new Object();
person.name = "Nicholas";
person.age = 29;

// 2. 对象字面量表示法：
var person = {
name : "Nicholas",
age : 29
};
// 对象字面量是对象定义的一种简写形式，
// 目的在于简化创建包含大量属性的对象的过程。

// age 是这个对象的最后一个属性，后面不能加逗号，
// 在最后一个属性后面添加逗号，会在 IE7 及更早版本和 Opera 中导致错误。
```

访问对象属性:

```javascript
// 1. 点表示法
alert(person.name); //"Nicholas"

// 2. 方括号表示法
alert(person["name"]); //"Nicholas"

// 2.1 方括号语法的主要优点是可以通过变量来访问属性：
var propertyName = "name";
alert(person[propertyName]); //"Nicholas"

// 2.2 属性名中可以包含非字母非数字，这时需要使用方括号表示法来访问它们：
person["first name"] = "Nicholas";
// "first name"中包含一个空格，所以不能使用点表示法来访问它。

// 除非必须使用变量来访问属性，否则一般建议使用点表示法。
```


#### Array 类型

数组，有序，最多可包含4,294,967,295个项。

1. ECMAScript 数组的每一项可以保存任何类型的数据；
2. ECMAScript 数组的大小可以动态调整。


创建数组的基本方式有两种：

```javascript
// 1. 使用 Array 构造函数：
var colors = new Array();
var colors = new Array(20); // 创建 length 值为 20 的数组
var colors = new Array("red", "blue", "green"); // 创建了一个包含 3 个字符串值的数组
// 使用 Array 构造函数时也可以省略 new 操作符：
var colors = Array(3);      // 创建一个包含 3 项的数组
var names = Array("Greg");  // 创建一个包含 1 项，即字符串"Greg"的数组


// 2. 数组字面量表示法：
var colors = ["red", "blue", "green"];  // 创建一个包含 3 个字符串的数组
var names = [];         // 创建一个空数组

var values = [1,2,];    // 不要这样！这样会创建一个包含 2 或 3 项的数组
var options = [,,,,,];  // 不要这样！这样会创建一个包含 5 或 6 项的数组
// 在 IE 中， values 会成为一个包含 3 个项且每项的值分别为 1、 2 和 undefined 的数组；
// 在其他浏览器中， values 会成为一个包含 2 项且值分别为 1 和 2 的数组。
// 原因是 IE8 及之前版本中的 ECMAScript 实现在数组字面量方面存在 bug。
```

读取和设置数组的值：

```javascript
var colors = ["red", "blue", "green"];  // 定义一个字符串数组
alert(colors[0]);       // 显示第一项
colors[2] = "black";    // 修改第三项
colors[3] = "brown";    // 新增第四项

alert(colors.length);   // 3
alert([].length);   // 0
// 数组的 length 不是只读的
colors.length = 2;
alert(colors[2]);   // undefined
colors.length = 4;
alert(colors[3]);   // undefined
```

```javascript
// 利用 length 属性可以方便地在数组末尾添加新项
var colors = ["red", "blue", "green"];
colors[colors.length] = "black";    //（在位置 3）添加一种颜色
colors[colors.length] = "brown";    //（在位置 4）再添加一种颜色
```

```javascript
var colors = ["red", "blue", "green"];  // 创建一个包含 3 个字符串的数组
colors[99] = "black";   // （在位置 99）添加一种颜色
alert(colors.length);   // 100

// 位置 3 到位置 98 实际上都是不存在的，访问它们都将返回 undefined。
```



检测数组

```javascript
if(value instanceof Array){
    // 对数组执行某些操作
}

if(Array.isArray(value)){
    // 对数组执行某些操作
}
// 支持 Array.isArray()方法的浏览器有 IE9+、 Firefox 4+、 Safari 5+、 Opera 10.5+和 Chrome。
```

转换方法

```javascript
// 所有对象都具有 toLocaleString()、 toString()和 valueOf()方法。

var colors = ["red", "blue", "green"];  // 创建一个包含 3 个字符串的数组
alert(colors.toString());   // red,blue,green
alert(colors.valueOf());    // ["red", "blue", "green"]
alert(colors);              // red,blue,green
// alert()要接收字符串参数，所以它会在后台调用 toString()方法


// 调用数组的 toLocaleString()方法时，也会创建一个数组值的以逗号分隔的字符串，
// 此时为了取得每一项的值，调用的是每一项的 toLocaleString()方法，而不是 toString()方法。
var person1 = {
    toLocaleString : function () {
        return "Nikolaos";
    },
    toString : function() {
        return "Nicholas";
    }
};

var person2 = {
    toLocaleString : function () {
        return "Grigorios";
    },
    toString : function() {
        return "Greg";
    }
};
var people = [person1, person2];
alert(people);  //Nicholas,Greg
alert(people.toString());       //Nicholas,Greg
alert(people.toLocaleString()); //Nikolaos,Grigorios
```

```javascript
// join()接收一个参数，即用作分隔符的字符串，然后返回包含所有数组项的字符串：
var colors = ["red", "green", "blue"];
alert(colors.join(","));    //red,green,blue
alert(colors.join("||"));   //red||green||blue
```

栈方法

栈， LIFO（Last-In-First-Out，后进先出），栈中项的插入（推入）和移除（弹出）只发生在一个位置：栈顶。

结合使用 pop()和 push()方法，可以像使用队列一样使用数组。

```javascript
// push()，接收任意数量的参数，把它们逐个添加到数组末尾，并返回修改后数组的长度；
// pop()，从数组末尾移除最后一项，减少数组的 length 值，然后返回移除的项。

var colors = new Array();   // 创建一个数组
var count = colors.push("red", "green");    // 推入两项，["red", "green"]
alert(count);   // 2
count = colors.push("black");   // 推入另一项
alert(count);   // 3
var item = colors.pop();    // 取得最后一项
alert(item);    // "black"
alert(colors.length);   // 2
```

队列方法

队列， FIFO（First-In-First-Out，先进先出），在列表末端添加项，从列表的前端移除项。

结合使用 shift()和 push()方法，可以像使用队列一样使用数组。

```javascript
var colors = new Array();   // 创建一个数组
var count = colors.push("red", "green");    // 推入两项
alert(count);   // 2
count = colors.push("black");   // 推入另一项
alert(count);   // 3
var item = colors.shift();      // 取得第一项
alert(item);    // "red"
alert(colors.length);   // 2
```