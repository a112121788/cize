# CIZE 是什么？
CIZE 是一个「持续集成」工具，希望能让开发人员更快捷的搭建一个完整、可靠、便捷的 CI 服务。
甚至可以像 Gulp 或 Grunt 一样，仅仅通过一个 ```cizefile.js``` 即可完成几乎所有的工作。

<img src="https://raw.githubusercontent.com/houfeng/cize/master/screenshot/monitor.png" width="888"/>

# 快速搭建
#### 安装 CIZE
```sh
$ sudo install cize -g
```

#### 新建 cizefile 添加 JOB

新建一个 cizefile.js
```
$ mkdir cize_workspace
$ cd cize_workspace
$ vim cizefile.js
```

输入如下内容
```js
/**
 * 配置服务，可以指定「端口」、「密钥」、「工作目录」等
 * port：端口，默认为 9000
 * secret：密且，默认没启用，启用后登录「WEB 版监视界面」需要提供
 * workspace：工作目录，默认为 cizefile.js 所在目录
 **/
cize.config({
  port: 9000,
  secret: '12345',
});

/**
 * 定义「项目」，项目用于为 JOB 分组，第二个参数为「项目配置」
 * {} 不能省略，省略时为获取指定名称的项目
 **/
const demo = cize.project('demo', {});

/**
 * 定义一个 JOB，这是一个最基本的 JOB，
 * 其它各类，都是在此基础之上的「扩展」
 **/
demo.job('hello1', function (self) {
  self.console.log('hello world');
  self.done();
});

/**
 * 定义一个用 SHELL 编写的 JOB
 * 如下用到了 cize.shell，这是多个「内置扩展」中的一个
 **/
demo.job('hello2', cize.shell(function () {
  /*
    echo "hello world"
  */
}));
```

然后，在「工作目录」中执行
```sh
$ cize
```

即可启动 CI 服务
```
$ cize
Strarting...
The server on "localhost:9000" started #30180
The server on "localhost:9000" started #30183
The server on "localhost:9000" started #30182
The server on "localhost:9000" started #30181
```
默认会启动和 CPU 核数相同的「工作进程」。

接下来，可以在浏览器中访问 ```http://localhost/9000```

# 更多内容
- [安装 CIZE](install)
- [认识 cizefile.js](cizefile)
- [基本对象：server、project、job](objects)
- [通过 js 编写 Job](javascript)
- [通过 shell 编写 Job](shell)
- [多个子任务「串行」的 Job](series)
- [多个子任务「并行」的 Job](parallel)
- [定时触发的 Job](cron)
- [通过其它 Job 触发的 Job](by)
- [Shadow Job](shadow)
- [编写一个扩展](plugin)

### 常用扩展
- [Gitlab](gitlab)
- [Github](github)