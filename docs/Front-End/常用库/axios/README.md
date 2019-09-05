<div style="position: fixed; bottom: 20px; right: 39px; border-radius: 5px; background-color: #797979; z-index: 100;">
    <a href="#目录" style="color: white; border-right: 1px solid white; text-decoration: none; font-size: 14px; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;">back to top ▲</a>
    <a style="cursor: pointer; color: white; border-right: 1px solid white; text-decoration: none; font-weight: bold; display: inline-block; padding: 5px 8px; line-height: 20px;" onclick="(function(){document.querySelector('.btn.pull-left.js-toolbar-action').click()})()"><i class="fa fa-align-justify"></i></a>
</div>

# axios

[axios中文说明](https://www.kancloud.cn/yunye/axios/234845)


* 使用npm： `$ npm install axios`
* 使用CDN： `<script src="https://unpkg.com/axios/dist/axios.min.js"></script>`

#### GET

```javascript
axios.get('/user?ID=12345')
.then(function(response){
    console.log(response);
})
.catch(function(error){
    console.log(error);
});

// 上面的请求也可以这样做
axios.get('/user', {
    params: {
        ID: 12345
    }
})
.then(function(response){
    console.log(response);
})
.catch(function(error){
    console.log(error);
});

axios('/user?ID=12345')
.then(function(response){
    console.log(response);
})
.catch(function(error){
    console.log(error);
});
```

#### POST

```javascript
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
})
.then(function(response){
    console.log(response);
})
.catch(function(error){
    console.log(error);
});

// 上面的请求也可以这样做
axios({
    method: 'post',
    url: '/user',
    data: {
        firstName: 'Fred',
        lastName: 'Flintstone'
    }
})
.then(function(response){
    console.log(response);
})
.catch(function(error){
    console.log(error);
});
```


#### 其它请求方法

* axios.request(config)
* axios.get(url[, config])
* axios.post(url[, data[, config]])
* axios.delete(url[, config])
* axios.head(url[, config])
* axios.put(url[, data[, config]])
* axios.patch(url[, data[, config]])


#### 并发请求

```javascript
axios.all([axios.get('/user/12345'), axios.get('/user/12345/permissions')])
.then(
    // 两个请求都完成后执行
    axios.spread(
        // 函数参数的顺序和数组中请求的顺序相同
        function(response1, response2){
            // do something here
        }
    )
);
```

#### 请求配置结构

```javascript
// 只有 url 是必须要有的
{
    url: '/user',   // 用于请求的服务器 URL
    method: 'get',  // 创建请求时使用的方法，默认是 get

    // baseURL  会自动加在 url 前面，除非 url 是一个绝对 URL
    // 通过设置一个 baseURL 便于为 axios 实例的方法传递相对 URL
    baseURL: 'https://some-domain.com/api/',

    // transformRequest 用于在向服务器发送前修改请求数据
    // 只能用在 'PUT', 'POST' 和 'PATCH' 这几个请求方法上
    // 数组中的函数必须返回一个字符串，或 ArrayBuffer，或 Stream
    transformRequest: [function(data){
        // 对 data 进行任意转换处理
        return data;
    }],

    // transformResponse 用于在传递给 then/catch 前，修改响应数据
    transformResponse: [function(data){
        // 对 data 进行任意转换处理
        return data;
    }],

    // headers 是即将被发送的自定义请求头
    headers: {'X-Requested-With': 'XMLHttpRequest'},

    // params 是 URL 参数
    // 必须是一个无格式对象(plain object)或 URLSearchParams 对象
    params: {
        ID: 12345
    },

    paramsSerializer: function(params){ // 负责 params 序列化的函数
        // (e.g. https://www.npmjs.com/package/qs, http://api.jquery.com/jquery.param/)
        return Qs.stringify(params, {arrayFormat: 'brackets'})
    },

    // data 是作为请求主体被发送的数据
    // 只适用于这些请求方法 'PUT', 'POST', 和 'PATCH'
    // 在没有设置 transformRequest 时，必须是以下类型之一：
    // - string, plain object, ArrayBuffer, ArrayBufferView, URLSearchParams
    // - 浏览器专属： FormData, File, Blob
    // - Node 专属： Stream
    data: {
        firstName: 'Fred'
    },

    timeout: 1000,          // 请求超时毫秒数(0 表示无超时时间)，如果请求超过 timeout 时间，请求将被中断
    withCredentials: false, // 表示跨域请求时是否需要使用凭证，默认为false

    // adapter 允许自定义处理请求，方便测试
    adapter: function(config){
        /* ... */
    },

    // auth 表示应该使用 HTTP 基础验证，并提供凭据
    // 这将设置一个 Authorization 头，覆写掉通过 headers 设置的 Authorization 头
    auth: {
        username: 'janedoe',
        password: 's00pers3cret'
    },

    responseType: 'json',           // 服务器响应的数据类型(arraybuffer|blob|document|json|text|stream)，默认 'json'
    xsrfCookieName: 'XSRF-TOKEN',   // 用作承载 xsrf token 值的 cookie 名称，默认 'XSRF-TOKEN'
    xsrfHeaderName: 'X-XSRF-TOKEN', // 用作承载 xsrf token 值的 HTTP 头名称，默认 'X-XSRF-TOKEN'

    // onUploadProgress，上传进度处理
    onUploadProgress: function(progressEvent){
        // 对原生进度事件的处理
    },

    // onDownloadProgress，下载进度处理
    onDownloadProgress: function(progressEvent){
        // 对原生进度事件的处理
    },

    maxContentLength: 2000, // 允许的响应内容的最大尺寸

    // validateStatus 定义对于给定的 HTTP 响应状态码是 resolve 或 reject promise
    // 如果 validateStatus 返回 (true|null|undefined)，promise 将被 resolve，否则 promise 将被 rejecte
    validateStatus: function (status) {
        return status >= 200 && status < 300; // 默认的
    },

    maxRedirects: 5,    // 在 node.js 中 follow 的最大重定向数目，如果设为0，则不会 follow 任何重定向，默认 5

    // httpAgent 和 httpsAgent 在 node.js 中分别用于定义在执行 http 和 https 时使用的自定义代理
    // keepAlive 默认 false
    httpAgent: new http.Agent({ keepAlive: true }),
    httpsAgent: new https.Agent({ keepAlive: true }),

    // proxy 定义代理服务器的主机名称和端口
    proxy: {
        host: '127.0.0.1',
        port: 9000,
        // auth 表示 HTTP 基础验证应当用于连接代理，并提供凭据
        // 这将设置一个 Proxy-Authorization 头，覆写掉通过 headers 设置的 Proxy-Authorization 头
        auth: {
            username: 'username',
            password: 'password'
        }
    },

    // cancelToken 指定用于取消请求的 cancel token
    cancelToken: new CancelToken(function(cancel){
        /* ... */
    })
}
```


#### 响应结构

```javascript
{
    data: {},         // 服务器提供的响应
    status: 200,      // 服务器响应的 HTTP 状态码
    statusText: 'OK', // 服务器响应的 HTTP 状态信息
    headers: {},      // 服务器响应头
    config: {},       // 请求时提供的配置信息
}
```


#### 设置全局默认值

```javascript
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
```


#### 拦截器

```javascript
// 在请求或响应被 then 或 catch 处理前拦截它们

// 添加请求拦截器
var myRequestInterceptor = axios.interceptors.request.use(
    function(config){
        // 在发送请求之前做些什么
        return config;
    },
    function(error){
        // 对请求错误做些什么
        return Promise.reject(error);
    }
);
// 移除请求拦截器
axios.interceptors.request.eject(myRequestInterceptor);


// 添加响应拦截器
var myResponseInterceptor = axios.interceptors.response.use(
    function(response){
        // 对响应数据做些什么
        return response;
    },
    function(error){
        // 对响应错误做些什么
        return Promise.reject(error);
    }
);
// 移除响应拦截器
axios.interceptors.response.eject(myResponseInterceptor);
```


#### 错误处理

```javascript
axios.get('/user/12345')
.catch(function(error){
    if(error.response){
        // 请求已发出，但服务器响应的状态码不在 2xx 范围内
        console.log(error.response.data);
        console.log(error.response.status);
        console.log(error.response.headers);
    }else{
        // 初始化请求时出现错误
        console.log('Error', error.message);
    }
    console.log(error.config);
});

// 可以使用 validateStatus 配置项自定义 HTTP 状态码的错误范围
axios.get('/user/12345', {
    validateStatus: function(status){
        return status < 500;    // 状态码大于等于500时才会 reject
    }
});
```