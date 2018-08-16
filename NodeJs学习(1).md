本篇文章交易如何使用NodeJs搭建一个简单版的http server.

## 设备

- MacOS High Sierra

## 环境部署

#### 安装 nvm

> 使用 nvm 方便管理node版本

##### 安装nvm

```powershell
$ brew update
$ brew install nvm
$ mkdir ~/.nvm
$ vim ~/.bash_profile
```

##### 配置变量NVM_DIR

```powershell
$ export NVM_DIR=~/.nvm
$ source $(brew --prefix nvm)/nvm.sh
```

##### 检查

```powershell
$ source ~/.bash_profile
$ echo $NVM_DIR
$ nvm --version
0.33.11
```

##### 删除 nvm

- 删除文件

  ```powershell
  $ rm -rf "$NVM_DIR"
  ```

- 删除 `~/.bash_profile` 中以下配置

  ```powershell
  export NVM_DIR="$HOME/.nvm"
  [ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
  [[ -r $NVM_DIR/bash_completion ]] && \. $NVM_DIR/bash_completion
  ```

  

#### 安装Node

安装最新版的Node.js

```powershell
$ nvm install node
```

使用最新版的Node.js

```powershell
$ nvm use node
```



## 创建Http Server

1. 创建一个 web.js，代码如下：

   ```javascript
   var http = require("http");
   function process_request(req, res) {
        var body = 'Thanks for calling!\n';
        var content_length =  body.length ;
        res.writeHead(200, {
            'Content-Length': content_length,
            'Content-Type': 'text/plain'
        });
        res.end(body);
   }
   var s = http.createServer(process_request);
   s.listen(8080);
   ```

   

2. 运行web.js，监听 8080 端口。

   ```powershell
   $ node web.js
   ```

   

3. 访问 http://localhost:8080 

   ```powershell
   $ curl -i http://localhost:8080
   
   HTTP/1.1 200 OK
   Content-Length: 20
   Content-Type: text/plain
   Date: Mon, 09 Jul 2018 03:03:25 GMT
   Connection: keep-alive
   
   Thanks for calling!
   ```




## Express 应用

1. 安装 express

   ```powershell
   $ npm install express --save
   ```

2. 创建 express 应用

   ```javascript
   const express = require("express");
   const app = express();
   
   app.get("/", function (req, res) {
       res.send("Hello world ! ");
   });
   
   app.listen(8080, function () {
       console.log("app is listening at port 8080 ! ")
   });
   ```

3. 访问 http://localhost:8080 

   ```powershell
   $ curl -i http://localhost:8080
   
   HTTP/1.1 200 OK
   X-Powered-By: Express
   Content-Type: text/html; charset=utf-8
   Content-Length: 14
   ETag: W/"e-SGStovtlAfbXbrr3HXIpSArL2nY"
   Date: Sat, 14 Jul 2018 13:41:23 GMT
   Connection: keep-alive
   
   Hello world ! 
   ```



## 参考资料

- https://nodejs.org/en/
- http://www.java2s.com/Tutorials/Javascript/Node.js_Tutorial/index.htm
- https://github.com/alsotang/node-lessons/tree/master/lesson1