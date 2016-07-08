
# CIZE 是什么？
CIZE 是一个「持续集成」工具，希望能让开发人员更快捷的搭建一个完整、可靠、便捷的 CI 服务。
甚至可以像 Gulp 或 Grunt 一样，仅仅通过一个 ```cizefile.js``` 即可完成几乎所有的工作。

[![npm version](https://badge.fury.io/js/cize.svg)](http://badge.fury.io/js/cize)
[![Build Status](https://travis-ci.org/Houfeng/cize.svg?branch=master)](https://travis-ci.org/Houfeng/cize) 

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
 * 定义一个 JOB，这是一个最基本的 JOB
 **/
demo.job('hello', function (self) {
  self.console.log('hello world');
  self.done();
});

```

然后，在「工作目录」中执行
```sh
$ cize
```

即可启动 CIZE 服务
```
$ cize
Strarting...
The server on "localhost:9000" started 
```
默认会启动和 CPU 核数相同的「工作进程」。

接下来，可以在浏览器中访问 ```http://localhost:9000``` , 
可以在 UI 中手动触发这个名为 ```hello``` 的 Job

# 定义 JOB
假定现在已经有一个定义好的名为 ```demo``` 的 ```project``` 

#### 用 js 编写一个 Job
```js
demo.job('test', function (self) {

});
```
这是最基础的 Job 类型，是其它 Job 类型或「扩展」的基础。

#### 用 shell 编写一个 job
```js
/**
 * 定义一个用 SHELL 编写的 JOB
 * 如下用到了 cize.shell，这是一个「内置扩展」
 **/
demo.job('test', cize.shell(function () {
  /*
    echo "hello world"
  */
}));
```

#### 定时执行的 Job
```
```

#### 监听其它 Job 的 Job
```
```

#### 串行执行的 Job
```
```

#### 并行执行的 Job
```
```

# 更多内容

请访问 wiki: [https://github.com/Houfeng/cize/wiki](https://github.com/Houfeng/cize/wiki)