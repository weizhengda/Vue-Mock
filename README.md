# vue-mock

## 配置流程

1. 全局安装 $ npm install -g json-server

2. 在项目根目录下创建 mock 文件夹

3. mock 文件夹下添加 db.json 文件

```json
   // example
   {
  "posts": [
    { "id": 1, "title": "json-server", "author": "typicode" }
  ],
  "comments": [
    { "id": 1, "body": "some comment", "postId": 1 }
  ],
  "profile": { "name": "typicode" }
}
```

4. package.json 添加命令

```js
   "mock": "json-server --watch mock/db.json",
   "mockdev": "npm run mock & npm run dev"
   
```

5. 启动 mock 服务器

```js
   npm run mock 
```

6. faker.js 批量生成伪数据

* 全局安装 faker

```js
   cnpm install faker -g
```
* 本地安装 faker
```js
   cnpm install faker --save-dev
```
* mock 目录下创建 faker-data.js，内容如下

```js
   module.exports = function () {
    var faker = require("faker");
    faker.locale = "zh_CN";
    var _ = require("lodash");
    return {
        people: _.times(100, function (n) {
            return {
                id: n,
                name: faker.name.findName(),
                avatar: faker.internet.avatar()
            }
        }),
        address: _.times(100, function (n) {
            return {
                id: faker.random.uuid(),
                city: faker.address.city(),
                county: faker.address.county()
            }
        })
    }
}

```

*  package.json 添加命令

```js
   "faker" : "json-server mock/faker-data.js"
```

* 随机生成伪数据

```js
   npm run faker
```

7. 代理设置,在 config/index.js 的 proxyTable 将请求映射到 http://localhost:3000

```js
  
   proxyTable: {
      '/api/': {
        target: 'http://localhost:3000',
        changeOrigin:true,
        pathRewrite: {
          '^/api': ''
        }
    }
```

8. 代码中添加请求以测试效果

```js
  
   mounted() {
      this.getAllPeople();
    },
    methods: {
      getAllPeople: function() {
        this.$http
          .get("/api/people", {})
          .then(
            m => this.peopleList = m.data
          );
      }
    }

```

9. 启动带mock 数据的本地服务

```js
   npm run mockdev 
```

## 使用在线 MockHttp 

1. [线上文档](http://www.mockhttp.cn/html/help.html)
2. [本项目中的线上MockHttp](https://www.easy-mock.com/mock/5a220ee567862f4d0c0d6e56/weizhengda/posts#!method=get)