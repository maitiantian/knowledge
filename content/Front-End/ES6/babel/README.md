<div style="position: fixed; bottom: 20px; right: 39px; border-radius: 5px; background-color: #797979; z-index: 100;">
    <a href="#目录" style="color: white; border-right: 1px solid white; text-decoration: none; font-size: 14px; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;">back to top ▲</a>
    <a style="cursor: pointer; color: white; border-right: 1px solid white; text-decoration: none; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;" onclick="(function(){document.querySelector('.btn.pull-left.js-toolbar-action').click()})()"><i class="fa fa-align-justify"></i></a>
</div>

# babel

babel-cli
babel-core
babel-runtime
babel-node
babel-polyfill



## babel到底做了什么？怎么做的？

把JavaScript中es2015/2016/2017/2046的新语法转化为es5，让低端运行环境（如浏览器和node）能够认识并执行。



## 使用方法

总共存在三种方式：

使用单体文件（standalone script）
命令行（cli）：package.json中的scripts段落中的某条命令；
构建工具的插件（webpack的babel-loader, rollup的rollup-plugin-babel）：集成在构建工具中。



## 运行方式和插件

babel总共分为三个阶段：解析，转换，生成。

babel本身不具有任何转化功能，它把转化的功能都分解到一个个plugin里面。

因此当我们不配置任何插件时，经过babel的代码和输入是相同的。


插件总共分为两种：

语法插件：在解析这一步就使得babel能够解析更多的语法。（babel内部试用的解析类库叫做babylon，并非babel自行开发）

举个简单的例子，当我们定义或者调用方法时，最后一个参数之后是不允许增加逗号的，如`callFoo(param1, param2,)`就是非法的。如果源码是这种写法，经过babel之后就会提示语法错误。

但最近的JS提案中已经允许了这种新的写法。为了避免babel报错，就需要增加语法插件babel-plugin-syntax-trailing-function-commas

转译插件：在转换这一步把源码转换并输出。这也是我们使用babel最本质的需求。

比起语法插件，转译插件其实更好理解，比如箭头函数`(a) => a`就会转化为`function (a) {return a}`。完成这个工作的插件叫做babel-plugin-transform-es2015-arrow-functions。



## 配置文件

既然插件是babel的根本，那如何使用呢？总共分为2个步骤：

* 将插件的名字增加到配置文件中（根目录下创建.babelrc或者package.json的babel里面，格式相同）
* 使用npm install babel-plugin-xxx进行安装


preset

比如es2015是一套规范，包含大概十几二十个转译插件。如果每次要开发者一个个添加并安装，配置文件很长不说，npm install的时间也会很长。

为了解决这个问题，babel提供了一组插件的集合。（单点和套餐的差别，套餐省下了巨多的时间和配置的精力）



preset分为以下几种：

* env，react，flow，minify等。这里最重要的是env。

* stage-x，这里面包含的都是当年最新规范的草案，每年更新。这里面还细分为
	* Stage 0 - 稻草人: 只是一个想法，经过TC39成员提出即可。
	* Stage 1 - 提案: 初步尝试。
	* Stage 2 - 初稿: 完成初步规范。
	* Stage 3 - 候选: 完成规范和浏览器初步实现。
	* Stage 4 - 完成: 将被添加到下一年度发布。

	* 低一级的stage会包含所有高级stage的内容，例如stage-1会包含stage-2，stage-3的所有内容。
	* stage-4在下一年更新会直接放到env中，所以没有单独的stage-4可供使用。

* es201x, latest
	* 这些是已经纳入到标准规范的语法。例如es2015 包含 arrow-functions，es2017 包含 syntax-trailing-function-commas。但因为 env 的出现，使得 es2016 和 es2017 都已经废弃。所以我们经常可以看到 es2015 被单独列出来，但极少看到其他两个。

	* latest是env的雏形，它是一个每年更新的preset，目的是包含所有es201x。但也是因为更加灵活的env 的出现，已经废弃。




## 执行顺序

很简单的几条原则：

* Plugin会运行在Preset之前；
* Plugin会从前到后顺序执行；
* Preset的顺序则刚好相反（从后向前）。
	* preset的逆向顺序主要是为了保证向后兼容，因为大多数用户的编写顺序是`['es2015', 'stage-0']`。这样必须先执行stage-0才能确保babel不报错。因此编排preset的时候，也要注意顺序，其实只要按照规范的时间顺序列出即可。



## 插件和preset的配置项

简略情况下，插件和preset只要列出字符串格式的名字即可。但如果某个preset或者插件需要一些配置项（或者说参数），就需要把自己先变成数组。第一个元素依然是字符串，表示自己的名字；第二个元素是一个对象，即配置对象。

最需要配置的当属env，如下：

```json
"presets": [
    // 带了配置项，自己变成数组
    [
        // 第一个元素依然是名字
        "env",
        // 第二个元素是对象，列出配置项
        {
          "module": false
        }
    ],

    // 不带配置项，直接列出名字
    "stage-2"
]
```


## env（重点）

env最为常用也最重要。

env的核心目的是通过配置得知目标环境的特点，然后只做必要的转换。例如目标浏览器支持es2015，那么es2015 这个preset其实是不需要的，于是代码就可以小一点（一般转化后的代码总是更长），构建时间也可以缩短一些。

如果不写任何配置项，env等价于latest，也等价于es2015 + es2016 + es2017三个相加（不包含stage-x中的插件）。env包含的插件列表维护在这里。


几种比较常用的配置方法：

```json
{
  "presets": [
    ["env", {
      "targets": {
        "browsers": ["last 2 versions", "safari >= 7"]
      }
    }]
  ]
}
```

如上配置将考虑所有浏览器的最新2个版本（safari大于等于7.0的版本）的特性，将必要的代码进行转换。而这些版本已有的功能就不进行转化了。这里的语法可以参考browserslist。

```json
{
  "presets": [
    ["env", {
      "targets": {
        "node": "6.10"
      }
    }]
  ]
}
```

如上配置将目标设置为nodejs，并且支持6.10及以上的版本。也可以用`node: 'current'`来支持最新稳定版本。例如箭头函数在nodejs 6及以上将不被转化，但如果是nodejs 0.12就会被转化了。

另外一个有用的配置项是modules。它的取值可以是amd，umd，systemjs，commonjs和false。这可以让babel以特定的模块化格式来输出代码。如果选择false就不进行模块化处理。




## 其他配套工具

#### babel-cli

cli就是命令行工具。安装了babel-cli就能够在命令行中使用babel命令来编译文件。

在开发npm package时经常会使用如下模式：

1. 把babel-cli安装为devDependencies
2. 在package.json中添加scripts（比如prepublish），使用babel命令编译文件
3. npm publish

这样既可以使用较新规范的JS语法编写源码，同时又能支持旧版环境。因为项目可能不太大，用不到构建工具（webpack或者rollup），于是在发布之前用babel-cli进行处理。

#### babel-node

babel-node是babel-cli的一部分，不需要单独安装。

它的作用是在node环境中，直接运行es2015的代码，而不需要额外进行转码。例如我们有一个js文件以es2015的语法进行编写（如使用了箭头函数）。我们可以直接使用babel-node es2015.js进行执行，而不用再进行转码了。

`babel-node = babel-polyfill + babel-register`

#### babel-register

babel-register模块改写require命令，为它加上一个钩子。此后，每当使用require加载.js、.jsx、.es和.es6后缀名的文件，就会先用babel进行转码。

使用时，必须首先加载require('babel-register')。

需要注意，babel-register只会对require命令加载的文件转码，不会对当前文件转码。

另外，由于它是实时转码，所以只适合在开发环境使用。

#### babel-polyfill

babel默认只转换js语法，而不转换新的API，比如Iterator、Generator、Set、Maps、Proxy、Reflect、Symbol、Promise等全局对象，以及一些定义在全局对象上的方法（比如Object.assign）都不会转码。

举例来说，es2015在Array对象上新增了Array.from方法。babel就不会转码这个方法。如果想让这个方法运行，必须使用babel-polyfill。（内部集成了core-js和regenerator）

使用时，在所有代码运行之前增加require('babel-polyfill')。或者更常规的操作是在webpack.config.js中将 babel-polyfill作为第一个entry。因此必须把babel-polyfill作为dependencies而不是devDependencies。

babel-polyfill 主要有两个缺点：

* 使用babel-polyfill会导致打出来的包非常大，因为babel-polyfill是一个整体，把所有方法都加到原型链上。比如我们只使用了Array.from，但它把Object.defineProperty也给加上了，这就是一种浪费了。这个问题可以通过单独使用core-js的某个类库来解决，core-js都是分开的。
* babel-polyfill会污染全局变量，给很多类的原型链上都作了修改，如果我们开发的也是一个类库供其他开发者使用，这种情况就会变得非常不可控。

因此在实际使用中，如果我们无法忍受这两个缺点（尤其是第二个），通常我们会倾向于使用babel-plugin-transform-runtime。

但如果代码中包含高版本js中类型的实例方法，如`[1,2,3].includes(1)`，还是要使用polyfill。



#### babel-runtime和babel-plugin-transform-runtime（重点）

常在项目中看到.babelrc中使用babel-plugin-transform-runtime，而package.json中的dependencies（注意不是devDependencies）又包含了babel-runtime，那这两个是不是成套使用的呢？他们又起什么作用呢？

先说babel-plugin-transform-runtime。

babel会转换js语法，之前已经提过了。以async/await举例，如果不使用这个plugin（即默认情况），转换后的代码大概是：

```javascript
// babel添加一个方法，把async转化为generator
function _asyncToGenerator(fn) { return function () {....}} // 很长很长一段

// 具体使用处
var _ref = _asyncToGenerator(function* (arg1, arg2) {
  yield (0, something)(arg1, arg2);
});
```

这个\_asyncToGenerator在当前文件被定义，然后被使用了，以替换源代码的await。但每个被转化的文件都会插入一段\_asyncToGenerator这就导致重复和浪费了。

在使用了babel-plugin-transform-runtime了之后，转化后的代码会变成

```javascript
// 从直接定义改为引用，这样就不会重复定义了。
var _asyncToGenerator2 = require('babel-runtime/helpers/asyncToGenerator');
var _asyncToGenerator3 = _interopRequireDefault(_asyncToGenerator2);

// 具体使用处是一样的
var _ref = _asyncToGenerator3(function* (arg1, arg2) {
  yield (0, something)(arg1, arg2);
});
```

从定义方法改成引用，那重复定义就变成了重复引用，就不存在代码重复的问题了。

我们也发现babel-runtime出场了，它就是这些方法的集合处，也因此，在使用babel-plugin-transform-runtime的时候必须把babel-runtime当做依赖。

babel-runtime，它内部集成了：

* core-js：转换一些内置类（Promise, Symbols等等）和静态方法（Array.from等）。绝大部分转换是这里做的。自动引入；

* regenerator：作为core-js的拾遗补漏，主要是generator/yield和async/await两组的支持。当代码中有使用generators/async时自动引入；

* helpers, 如上面的asyncToGenerator就是其中之一，其他还有如jsx，classCallCheck等等，可以查看babel-helpers。在代码中有内置的helpers使用时（如上面的第一段代码）移除定义，并插入引用（于是就变成了第二段代码）。


babel-plugin-transform-runtime不支持实例方法，如`[1,2,3].includes(1)`。



#### babel-loader

大型的项目都会有构建工具（如webpack或rollup）来进行代码构建和压缩（uglify）。理论上来说，我们也可以对压缩后的代码进行babel处理，但那会非常慢。因此如果在uglify之前就加入babel处理，岂不完美？

所以就有了babel插入到构建工具内部这样的需求。以webpack为例，webpack有loader的概念，因此就出现了babel-loader。

和babel-cli一样，babel-loader也会读取.babelrc或者package.json中的babel段作为自己的配置，之后的内核处理也是相同。唯一比babel-cli复杂的是，它需要和webpack交互，因此需要在webpack这边进行配置。比较常见的如下：

```javascript
module: {
	rules: [
		{
			test: /\.js$/,
			exclude: /(node_modules|bower_components)/,
			loader: 'babel-loader'
		}
	]
}
```

如果想在这里传入babel的配置项，也可以把改成：

```javascript
module: {
	rules: [
		{
			test: /\.js$/,
			exclude: /(node_modules|bower_components)/,
			use: {
				loader: 'babel-loader',
				options: {
					// 配置项在这里
				}
			}
		}
	]
}
```

这里的配置项优先级是最高的。但放到单独的配置文件中更加清晰合理，可读性强一些。



## Babel 7.x

最近babel发布了7.0。上面部分是针对6.x写的，下面我们来关注一下7.0带来的变化（核心机制方面没有变，插件，preset，解析转译生成这些都没有变）


#### preset的变更：淘汰es201x，删除stage-x，强推env（重点）

淘汰es201x的目的是把选择环境的工作交给env自动进行，而不需要开发者投入精力。凡是使用es201x的开发者，都应当使用env进行替换。但这里的淘汰（原文deprecated）并不是删除，只是不推荐使用了，不好说babel 8就真的删了。

stage-x直接被删了。因为babel团队认为为这些“不稳定的草案”花费精力去更新preset相当浪费。stage-x虽然删除了，但它包含的插件并没有删除，只是被更名了，我们依然可以显式地声明这些插件来获得等价的效果。

为了减少开发者替换配置文件的机械工作，babel开发了一款babel-upgrade的工具，它会检测babel配置中的stage-x并且替换成对应的plugins。

#### npm package名称的变化（重点）

babel 7的一个重大变化，把所有babel-重命名为@babel/，例如：

* babel-cli变成了@babel/cli
* babel-preset-env变成@babel/preset-env。还可以省略preset简写为@babel/env
* babel-plugin-transform-arrow-functions变成@babel/plugin-transform-arrow-functions。可简写为@babel/transform-arrow-functions

这个变化不单单应用于package.json的依赖中，包括.babelrc的配置（plugins，presets）也要这么写，为了保持一致。例如

```json
{
  "presets": [
-   "env"
+   "@babel/preset-env"
  ]
}
```

上面提过的babel解析语法的内核babylon现在重命名为@babel/parser。

stage-x被删除了，它包含的插件虽然保留，但也被重命名了。babel团队希望通过在名字中增加proposal更明显地区分已位于规范中的插件（如es2015的babel-plugin-transform-arrow-functions）和仅仅位于草案中的插件（如stage-0的@babel/plugin-proposal-function-bind），所有包含在stage-x的转译插件都使用proposal前缀，语法插件不在其列。

最后，如果插件名称中包含了规范名称（-es2015-，-es3-之类的），一律删除。例如babel-plugin-transform-es2015-classes变成了@babel/plugin-transform-classes。

#### 不再支持低版本node

babel 7.0开始不再支持nodejs 0.10，0.12，4，5这四个版本，要求nodejs >= 6。

这里的不再支持指在这些低版本node环境中不能使用babel转译代码，但babel转译后的代码依然能在这些环境上运行。

#### only和ignore匹配规则的变化

* 在babel 6时，ignore选项如果包含.foo.js，实际上的含义（转化为glob）是 ./\*\*/.foo.js，也就是当前目录包括子目录的所有foo.js结尾的文件，这可能和开发者常规的认识有悖；
* 于是在babel 7，相同的表达式.foo.js只作用于当前目录，不作用于子目录。如果依然想作用于子目录的，要按照glob的完整规范书写为./\*\*/.foo.js才可以；
* only也是相同。

这个规则变化只作用于通配符，不作用于路径。所以node_modules依然包含所有它的子目录，而不单单只有一层。

#### @babel/node从@babel/cli中独立了

和babel 6不同，如果要使用@babel/node，就必须单独安装，并添加到依赖中。

#### babel-upgrade

它的目的是帮助用户自动化地从babel 6升级到7。

这款升级工具的功能包括：

* package.json
	* 把依赖（和开发依赖）中所有的babel-替换为@babel/；
	* 把这些@babel/\*依赖的版本更新为最新版（例如 ^7.0.0）；
	* 如果scripts中有使用babel-node，自动添加@babel/node为开发依赖；
	* 如果有babel配置项，检查其中的plugins和presets，把短名（env）替换为完整的名字（@babel/preset-env）。

* .babelrc
	* 检查其中的plugins和presets，把短名（env）替换为完整的名字（@babel/preset-env）；
	* 检查是否包含preset-stage-x，如果有则替换为对应的插件并添加到plugins。

使用方式如下：

```bash
# 不安装到本地而是直接运行命令，npm 的新功能
npx babel-upgrade --write
# 或者常规方式
npm i babel-upgrade -g
babel-upgrade --write
```
