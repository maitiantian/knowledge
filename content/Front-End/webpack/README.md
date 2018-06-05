# webpack

> webpack是一个现代JavaScript应用程序的静态模块打包器(module bundler)。当webpack处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个bundle。

**从webpack v4.0.0开始，可以不用引入一个配置文件。**

四个核心概念：
* 入口(entry)

    入口起点(entry point)指示webpack应该使用哪个模块，来作为构建其内部依赖图的开始。进入入口起点后，webpack会找出有哪些模块和库是入口起点（直接和间接）依赖的。

    每个依赖项随即被处理，最后输出到称之为bundles的文件中。

    可以在webpack配置中配置entry属性来指定一个或多个入口起点。默认值为./src：

    ```js
    // webpack.config.js
    module.exports = {
        entry: './path/to/my/entry/file.js'
    };
    ```
* 输出(output)

    output属性告诉webpack在哪里输出它所创建的bundles，以及如何命名这些文件，默认值为./dist。基本上，整个应用程序结构，都会被编译到你指定的输出路径的文件夹中。可以在配置中指定output字段：

    ```js
    // webpack.config.js
    const path = require('path');
    // path模块是一个Node.js核心模块，用于操作文件路径。
    module.exports = {
        entry: './path/to/my/entry/file.js',
        output: {
            path: path.resolve(__dirname, 'dist'),
            filename: 'my-first-webpack.bundle.js'
            // 通过output.filename和output.path属性告诉webpack bundle的名称，
            // 以及我们想要bundle生成(emit)到哪里。
        }
    };
    ```

    > 生成(emitted 或 emit)，它是“生产(produced)”或“释放(discharged)”的特殊术语。
* loader

    loader让webpack能够去处理那些非JavaScript文件（webpack自身只理解JavaScript）。loader可以将所有类型的文件转换为webpack能够处理的有效模块，然后就可以利用webpack的打包能力，对它们进行处理。

    本质上，webpack loader将所有类型的文件，转换为应用程序的依赖图（和最终的bundle）可以直接引用的模块。

    webpack配置中loader有两个目标：
    1. test属性，用于标识出应该被对应的loader进行转换的某个或某些文件；
    2. use属性，表示进行转换时使用哪个loader。

    ```js
    // webpack.config.js
    const path = require('path');

    const config = {
        output: {
            filename: 'my-first-webpack.bundle.js'
        },
        module: {
            rules: [
                { test: /\.txt$/, use: 'raw-loader' }
                // “嘿，webpack 编译器，
                // 当你碰到「在require()/import语句中被解析为'.txt'的路径」时，
                // 在你对它打包之前，先使用raw-loader转换一下。”
            ]
        }
    };

    module.exports = config;
    ```

    ***在webpack配置中定义loader时，要定义在module.rules中，而不是rules。***
* 插件(plugins)

    loader被用于转换某些类型的模块，而插件则可以用于执行范围更广的任务。插件的范围包括，从打包优化和压缩，一直到重新定义环境中的变量。

    想要使用一个插件，只需要require()它，然后把它添加到plugins数组中。多数插件可以通过选项(option)自定义。可以在一个配置文件中因为不同目的而多次使用同一个插件，这时需要通过使用new操作符来创建它的一个实例。

    ```js
    // webpack.config.js
    const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装
    const webpack = require('webpack'); // 用于访问内置插件

    const config = {
        module: {
            rules: [
                { test: /\.txt$/, use: 'raw-loader' }
            ]
        },
        plugins: [
            new webpack.optimize.UglifyJsPlugin(),
            new HtmlWebpackPlugin({template: './src/index.html'})
        ]
    };

    module.exports = config;
    ```

    [插件列表](https://webpack.docschina.org/plugins)
* 模式

    通过选择development或production来设置mode参数，可以启用相应模式下的webpack内置的优化。
    ```js
    // webpack.config.js
    module.exports = {
        mode: 'production'
    };
    ```

# <p align="center">入口起点(entry points)</p>
###### [<p align="right">back to top ▲</p>](#目录)

## 单个入口（简写）语法
**entry: string|Array&lt;string&gt;**

```js
// webpack.config.js
const config = {
    entry: './path/to/my/entry/file.js'
};

module.exports = config;

// entry属性的单个入口语法是下面的简写：

const config = {
    entry: {
        main: './path/to/my/entry/file.js'
    }
};
```

使用此语法在扩展配置时有失灵活性。

## 对象语法
**entry: {[entryChunkName: string]: string|Array&lt;string&gt;}**

```js
// webpack.config.js

const config = {
    entry: {
        app: './src/app.js',
        vendors: './src/vendors.js'
    }
};
```

这是应用程序中定义入口的最可扩展的方式。

> “可扩展的webpack配置”是指，可重用并且可以与其他配置组合使用。这是一种流行的技术，用于将关注点(concern)从环境(environment)、构建目标(build target)、运行时(runtime)中分离。然后使用专门的工具（如webpack-merge）将它们合并。

## 常见场景
#### 分离 应用程序(app) 和 第三方库(vendor) 入口

```js
// webpack.config.js
const config = {
    entry: {
        app: './src/app.js',
        vendors: './src/vendors.js'
    }
};
```
webpack从app.js和vendors.js开始创建依赖图(dependency graph)。

这些依赖图是彼此完全分离、互相独立的。

这种方式比较常见于只有一个入口起点（不包括vendor）的单页应用程序(single page application)中。

#### 多页面应用程序
```js
// webpack.config.js
const config = {
    entry: {
        pageOne: './src/pageOne/index.js',
        pageTwo: './src/pageTwo/index.js',
        pageThree: './src/pageThree/index.js'
    }
};
```
在多页应用中，每当页面跳转时服务器将为你获取一个新的HTML文档。页面重新加载新文档，并且资源被重新下载。

# <p align="center">输出(output)</p>
###### [<p align="right">back to top ▲</p>](#目录)

配置output选项可以控制webpack如何向硬盘写入编译文件。即使存在多个入口起点，但只能指定一个输出配置。

## 用法(Usage)

```js
webpack.config.js

const config = {
    // output属性，将它的值设置为一个对象。
    output: {
        filename: 'bundle.js',
        // filename：用于输出文件的文件名。
        path: '/home/proj/public/assets'
        // path：目标输出目录的绝对路径。
    }
};

module.exports = config;
```
此配置将一个单独的bundle.js文件输出到/home/proj/public/assets目录中。

## 多个入口起点
如果配置创建了多个单独的"chunk"（例如，使用多个入口起点或使用像CommonsChunkPlugin这样的插件），则应该使用占位符(substitutions)来确保每个文件具有唯一的名称。

```js
{
    entry: {
        app: './src/app.js',
        search: './src/search.js'
    },
    output: {
        filename: '[name].js',
        path: __dirname + '/dist'
    }
}

// 写入到硬盘：./dist/app.js, ./dist/search.js
```

## 高级进阶
```js
// 以下是使用CDN和资源hash的复杂示例
// webpack.config.js
output: {
  path: "/home/proj/cdn/assets/[hash]",
  publicPath: "http://cdn.example.com/assets/[hash]/"
}
```
在编译时不知道最终输出文件的publicPath的情况下，publicPath可以留空，并且在入口起点文件运行时动态设置。如果你在编译时不知道publicPath，你可以先忽略它，并且在入口起点设置\_\_webpack_public_path\_\_。

```js
__webpack_public_path__ = myRuntimePublicPath

// 剩余的应用程序入口
```

# <p align="center">模式(mode)</p>
###### [<p align="right">back to top ▲</p>](#目录)

mode配置选项告诉webpack使用相应模式的内置优化。

## 用法

在配置中提供mode选项：

```js
module.exports = {
    mode: 'production'
};
```
或者从CLI参数中传递：
```cmd
webpack --mode=production
```

|选项|描述|
|:---|:---|
|development|会将process.env.NODE_ENV的值设为development。启用NamedChunksPlugin和NamedModulesPlugin。|
|production|会将process.env.NODE_ENV的值设为production。启用FlagDependencyUsagePlugin, FlagIncludedChunksPlugin, ModuleConcatenationPlugin, NoEmitOnErrorsPlugin, OccurrenceOrderPlugin, SideEffectsFlagPlugin和UglifyJsPlugin。|

**只设置NODE_ENV，则不会自动设置mode。**

## mode: development
```js
// webpack.development.config.js
module.exports = {
+ mode: 'development'
- plugins: [
-   new webpack.NamedModulesPlugin(),
-   new webpack.DefinePlugin({ "process.env.NODE_ENV": JSON.stringify("development") }),
- ]
}
```

## mode: production
```js
// webpack.production.config.js
module.exports = {
+  mode: 'production',
-  plugins: [
-    new UglifyJsPlugin(/* ... */),
-    new webpack.DefinePlugin({ "process.env.NODE_ENV": JSON.stringify("production") }),
-    new webpack.optimize.ModuleConcatenationPlugin(),
-    new webpack.NoEmitOnErrorsPlugin()
-  ]
}
```

# <p align="center">输出(output)</p>
###### [<p align="right">back to top ▲</p>](#目录)

loader用于对模块的源代码进行转换。loader可以使你在import或“加载”模块时预处理文件。loader类似于其他构建工具中“任务(task)”。loader可以将文件从不同的语言（如TypeScript）转换为JavaScript，或将内联图像转换为data URL。loader甚至允许你直接在JavaScript模块中import CSS文件！

## 示例

你可以使用loader告诉webpack加载CSS文件，或者将TypeScript转为JavaScript。为此，首先安装相对应的loader：

```cmd
npm install --save-dev css-loader
npm install --save-dev ts-loader
```

然后指示webpack对每个.css使用css-loader，以及对所有.ts 文件使用ts-loader：

```js
webpack.config.js

module.exports = {
    module: {
        rules: [
            { test: /\.css$/, use: 'css-loader' },
            { test: /\.ts$/, use: 'ts-loader' }
        ]
    }
};
```

## 使用loader

有三种使用loader的方式：

* 配置（推荐）：在webpack.config.js文件中指定loader；

     这是展示loader的一种简明方式，并且有助于使代码变得简洁。同时让你对各个loader有个全局概览：
    ```js
    module: {
        rules: [
            {
                test: /\.css$/,
                use: [
                    { loader: 'style-loader' },
                    {
                        loader: 'css-loader',
                        options: {
                            modules: true
                        }
                    }
                ]
            }
        ]
    }
    ```
* 内联：在每个import语句中显式指定loader；

    ```js
    // 使用 ! 将资源中的loader分开
    import Styles from 'style-loader!css-loader?modules=true!./styles.css';
    ```

    > 尽可能使用module.rules，这样可以减少源码中的代码量，并且可以在出错时更快地调试和定位loader中的问题。
* CLI：在shell命令中指定它们。

    ```cmd
    webpack --module-bind jade-loader --module-bind 'css=style-loader!css-loader'
    ```
    对.jade文件使用jade-loader，对.css文件使用style-loader和css-loader。

