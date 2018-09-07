# npm

## package.json

```json
{
  "name": "project_name",
  "version": "1.0.0",
  "description": "project description",
  "dependencies": {
    "body-parser": "~1.15.1",
    "cookie-parser": "~1.4.3",
    "debug": "~2.2.0",
    "echarts": "^4.0.4",
    "es6-promise": "^4.1.1",
    "express": "~4.13.4",
    "express-http-proxy": "^1.0.4",
    "express-session": "^1.15.3",
    "file-loader": "^1.1.6",
    "http-proxy": "^1.17.0",
    "identity-obj-proxy": "^3.0.0",
    "isomorphic-fetch": "^2.2.1",
    "leaflet": "^1.3.1",
    "lodash": "^4.17.4",
    "moment": "^2.18.1",
    "morgan": "~1.7.0",
    "nock": "^9.0.13",
    "rc-pagination": "^1.9.8",
    "react-datepicker": "^0.53.0",
    "react-draggable": "^3.0.5",
    "react-fontawesome": "^1.6.1",
    "react-treebeard": "^2.0.3",
    "recharts": "^1.1.0",
    "serve-favicon": "~2.3.0",
    "url-loader": "^0.6.2"
  },
  "devDependencies": {
    "@types/react": "^16.3.17",
    "antd": "^3.4.1",
    "autoprefixer": "^7.2.3",
    "babel-cli": "^6.18.0",
    "babel-core": "^6.18.0",
    "babel-eslint": "8.0.1",
    "babel-jest": "^16.0.0",
    "babel-loader": "^7.1.1",
    "babel-plugin-import": "^1.6.2",
    "babel-plugin-react-html-attrs": "^2.1.0",
    "babel-plugin-react-transform": "^3.0.0",
    "babel-polyfill": "^6.26.0",
    "babel-preset-env": "^1.6.1",
    "babel-preset-react": "^6.16.0",
    "babel-preset-react-hmre": "^1.1.1",
    "babel-preset-stage-0": "^6.24.1",
    "css-loader": "^0.25.0",
    "enzyme": "^2.5.1",
    "eslint": "^4.16.0",
    "eslint-config-fbjs": "^2.0.1",
    "eslint-plugin-babel": "^4.1.2",
    "eslint-plugin-flowtype": "^2.41.1",
    "eslint-plugin-jsx-a11y": "^6.0.3",
    "eslint-plugin-react": "^7.5.1",
    "eslint-plugin-relay": "0.0.20",
    "eventsource-polyfill": "^0.9.6",
    "extract-text-webpack-plugin": "^3.0.2",
    "gulp": "^3.9.1",
    "gulp-clean": "^0.3.2",
    "gulp-rename": "^1.2.2",
    "gulp-uglify": "^3.0.0",
    "gulp-watch": "^4.3.11",
    "html-loader": "^0.5.1",
    "html-webpack-plugin": "^2.24.1",
    "immutable": "^3.8.1",
    "jest": "^23.1.0",
    "less": "^3.8.1",
    "less-loader": "^4.1.0",
    "postcss-loader": "^2.0.9",
    "prop-types": "^15.5.10",
    "pump": "^1.0.3",
    "react": "^15.3.2",
    "react-addons-css-transition-group": "^15.4.0",
    "react-addons-test-utils": "^15.3.2",
    "react-color": "^2.13.8",
    "react-dom": "^15.3.2",
    "react-intl": "^2.3.0",
    "react-intl-redux": "^0.6.0",
    "react-motion": "^0.5.0",
    "react-redux": "^5.0.1",
    "react-router": "^3.0.0",
    "react-router-redux": "^4.0.7",
    "react-test-renderer": "^15.3.2",
    "react-transform-hmr": "^1.0.4",
    "reactcss": "^1.2.3",
    "redux": "^3.6.0",
    "redux-auth-wrapper": "^2.0.1",
    "redux-mock-store": "^1.2.1",
    "redux-thunk": "^2.1.0",
    "source-map-loader": "^0.1.5",
    "style-loader": "^0.13.1",
    "uglify-es": "^3.2.0",
    "webpack-cli": "^3.1.0",
    "webpack-dev-server": "^2.9.4",
    "webpack-hot-middleware": "^2.13.0",
    "webpack-stream": "4"
  },
  "jest": {
    "testEnvironment": "jsdom",
    "coverageThreshold": {
      "global": {
        "branches": 60,
        "functions": 60,
        "lines": 60,
        "statements": 60
      }
    },
    "moduleNameMapper": {
      "\\.(css|less|gif|jpg|jpeg|png)$": "identity-obj-proxy"
    },
    "coveragePathIgnorePatterns": [
      "<rootDir>/app/public/"
    ],
    "testPathIgnorePatterns": [
      "<rootDir>/node_modules/",
      "<rootDir>/app/public/",
      "<rootDir>/dist/",
      "__mocks__"
    ],
    "globals": {
      "localStorage": {
        "appLanguage": "zh"
      }
    }
  },
  "scripts": {
    "test": "jest --coverage",
    "lint": "eslint --quiet .",
    "dev:server": "cd server & node server --dev ",
    "dev:client": "webpack-dev-server --public ",
    "dev:client:media": "webpack-dev-server --public media ",
    "dev:client:smartLight": "webpack-dev-server --public smartLight ",
    "dev": "start npm run dev:server &&start npm run dev:client ",
    "dev:media": "start npm run dev:server &&start npm run dev:client:media ",
    "dev:smartLight": "start npm run dev:server &&start npm run dev:client:smartLight ",
    "build:lib": "webpack --config ./ddl.config.js",
    "build": "npm run build:lib & gulp ",
    "build:media": "npm run build:lib & gulp media ",
    "build:smartLight": "npm run build:lib & gulp smartLight ",
    "start": "cd dist & npm start",
    "test:api": "jest --roots \"./app/src/api_\" --verbose"
  },
  "author": "someone",
  "license": "ISC",
  "repository": "http://aaa/bbb/ccc.git"
}
```

## npm install

__npm install/i/add packagename@~/^/*X.Y.Z -S/-D/-E__

* -S: --save，把模块的版本信息保存到dependencies（生产环境依赖）中
* -D: --save-dev，把模块版本信息保存到devDependencies（开发环境依赖）中
* -E: --save-exact，精确安装模块的指定版本，dependencies字段里模块版本号前面的^会消失

#### ~ | ^ | *

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


## npm scripts

__npm run xxx__

__npm脚本原理：__

* 每当执行npm run xxx，就会新建一个Shell，在这个Shell里执行指定的脚本命令。因此，只要是Shell（一般是Bash）可以运行的命令，就可以写在npm脚本里面;
* 比较特别的是，npm run xxx新建的这个Shell会将当前目录的node\_modules/.bin子目录加入PATH变量，执行结束后，再将PATH变量恢复原样。所以当前目录的node_modules/.bin子目录里的所有脚本，都可以直接用脚本名调用，不必加上路径;
    ```json
    {
        ...
        "scripts": {
            "test": "mocha test"
            不用写成"test": "./node_modules/.bin/mocha test"
        }
        ...
    }
    ```
* npm脚本的唯一要求是可以在Shell执行，因此它不一定是Node脚本，任何可执行文件都可以写在里面;
* npm脚本的退出码也遵守Shell脚本规则：如果退出码不是0，npm就认为这个脚本执行失败。

#### npm run：查看当前项目的所有npm脚本命令

#### 通配符

npm脚本就是Shell脚本，因此可以使用Shell通配符：

```json
{
    ...
    "scripts": {
        "lint": "jshint **/*.js"
        *表示任意文件名，**表示任意一层子目录
    }
    ...
}
```

#### 传参

向npm脚本传入参数，要使用--标明：
```json
"lint": "jshint **.js"
向上面的命令传参数，必须写成下面这样：
$ npm run lint --reporter checkstyle > checkstyle.xml

也可以在package.json里面再封装一个命令：
"lint": "jshint **.js",
"lint:checkstyle": "npm run lint --reporter checkstyle > checkstyle.xml"
```

#### 执行顺序

* 并行执行，&：
    ```bash
    $ npm run script1.js & npm run script2.js
    ```
* 继发执行（前一个任务成功，才执行下一个任务），&&：
    ```bash
    $ npm run script1.js && npm run script2.js
    ```

#### 默认值

npm对两个脚本提供了默认值。也就是说，这两个脚本不用定义，就可以直接使用：

```json
npm run start的默认值是node server.js，前提是项目根目录下有server.js这个脚本
"start": "node server.js"，
npm run install的默认值是node-gyp rebuild，前提是项目根目录下有binding.gyp文件
"install": "node-gyp rebuild"
```

#### 钩子

npm脚本有pre和post两个钩子。举例来说，build脚本命令的钩子就是prebuild和postbuild：

```json
"prebuild": "echo I run before the build script",
"build": "cross-env NODE_ENV=production webpack",
"postbuild": "echo I run after the build script"

用户执行npm run build的时候，会自动按照下面的顺序执行：
npm run prebuild && npm run build && npm run postbuild

可以在这两个钩子里面，完成一些准备工作和清理工作：
"clean": "rimraf ./dist && mkdir dist",
"prebuild": "npm run clean",
"build": "cross-env NODE_ENV=production webpack"
```

__双重的pre和post无效：prepretest和postposttest是无效的。__

npm提供一个npm\_lifecycle\_event变量，返回当前正在运行的脚本名称，如pretest、test、posttest等等。可以利用这个变量，在同一个脚本文件里面，为不同的npm scripts命令编写代码：

```javascript
const TARGET = process.env.npm_lifecycle_event;

if (TARGET === 'test') {
  console.log(`Running the test task!`);
}

if (TARGET === 'pretest') {
  console.log(`Running the pretest task!`);
}

if (TARGET === 'posttest') {
  console.log(`Running the posttest task!`);
}
```

#### 简写

四个常用的npm脚本有简写形式：

* npm start = npm run start
* npm stop = npm run stop
* npm test = npm run test
* npm restart = npm run stop && npm run restart && npm run start

#### 变量

npm脚本可以使用npm的内部变量：

1. 通过npm\_package\_前缀，npm脚本可以拿到package.json里面的字段：
    ```json
    {
        ...
        "name": "foo", 
        "version": "1.2.5",
        "scripts": {
            "view": "node view.js"
        }
        ...
    }

    变量npm_package_name返回foo，变量npm_package_version返回1.2.5。
    // view.js
    console.log(process.env.npm_package_name);      // foo
    console.log(process.env.npm_package_version);   // 1.2.5

    上面代码通过环境变量process.env对象，拿到package.json的字段值；
    如果是Bash脚本，可以用$npm_package_name和$npm_package_version取到这两个值。
    ```
2. npm\_package\_前缀也支持嵌套的package.json字段：
    ```json
    {
        ...
        "repository": {
            "type": "git",
            "url": "xxx"
        },
        scripts: {
            "view": "echo $npm_package_repository_type"
        }
        ...
    }

    上面代码中，repository字段的type属性，可以通过npm_package_repository_type取到。
    ```
3. npm脚本还可以通过npm\_config\_前缀，拿到npm的配置变量，即npm config get xxx命令返回的值。比如，当前模块的发行标签，可以通过npm\_config\_tag取到：

    ```json
    {
        ...
        "scripts": {
            "view": "echo $npm_config_tag",
        }
        ...
    }
    ```

    注意，package.json里面的config对象，可以被环境变量覆盖：

    ```json
    { 
        ...
        "name" : "project_name",
        "config" : { "port" : "8080" },
        "scripts" : { "start" : "node server.js" }
        ...
    }
    ```

    上面代码中，npm_package_config_port变量返回的是8080，这个值可以用下面的方法覆盖：

    ```bash
    $ npm config set project_name:port 80
    ```
4. env命令可以列出所有环境变量：

    ```json
    {
        ...
        "scripts" : { "env" : "env" }
        ...        
    }
    ```

#### 常用脚本示例

```json
// 删除目录
"clean": "rimraf dist/*",
// 本地搭建一个 HTTP 服务
"serve": "http-server -p 9090 dist/",
// 打开浏览器
"open:dev": "opener http://localhost:9090",
// 实时刷新
 "livereload": "live-reload --port 9091 dist/",
// 构建 HTML 文件
"build:html": "jade index.jade > dist/index.html",
// 只要 CSS 文件有变动，就重新执行构建
"watch:css": "watch 'npm run build:css' assets/styles/",
// 只要 HTML 文件有变动，就重新执行构建
"watch:html": "watch 'npm run build:html' assets/html",
// 部署到 Amazon S3
"deploy:prod": "s3-cli sync ./dist/ s3://example-com/prod-site/",
// 构建 favicon
"build:favicon": "node scripts/favicon.js",
```
