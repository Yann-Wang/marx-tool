## 历史沿革
- 该脚手架源于内部项目[MarX框架](https://github.com/wangchao0502/MarX)
- 将MarX框架的脚手架逻辑和核心逻辑进行了拆分，形成了marx-tool 和 marx-core两部分
- marx-tool作为开发依赖引入（里面包含了部分构建逻辑），marx-core作为线上依赖引入

## 环境搭建

推荐node和npm版本如下，npm4有破坏性改动，有些包可能会安装出错，所以不推荐升级。

**node v6.10.0**
**npm v3.10.10**

- 使用脚手架初始化项目目录结构

```shell
  npm i marx-tool -g
  marx create marx-demo
  cd marx-demo
```
- 如果不需要创建新项目，仅仅是开发已有项目，则不需要全局安装marx-tool，初始化的项目中已把marx-tool作为开发依赖引入，可以直接使用marx框架的构建逻辑。
- 开启本地的mysql服务和redis服务，配置文件在`server/config/mysql.json`和`server/config/redis.json`中。记得修改登陆密码哦～

## 启动项目

以下两个命令分别在两个bash窗口执行，`npm start`启动开发环境的node服务，
`npm run watch`启动实时打包功能(该功能暂时不支持，需自行实现（因为依赖了内部工具superman，该工具未开源，所以被砍掉了)）。

> npm start

> npm run watch #暂时还不支持（对内部项目superman有依赖，该项目还未开源）

如果遇到类似下面的提示，请运行`npm rebuild`命令重新编译相关依赖包

> Module version mismatch. Expected 48, got 46

**>>> 以上你的环境就配置好了 <<<**

## 脚手架cli

```bash
marx create|c [options] [name]  # create marx app
marx generate|g [type] [name]   # generate module
marx route|r [options] [url]
```

注意：目前这个脚手架还比较初级，你看下下面的todolist就知道了。

## 脚手架设计思路

### 前端

入口文件都叫做main.js，打包工具会自动扫描。

### 后端

controller：直接调用service代码，不可以直接引用model对象进行数据库操作

service：直接调用model层对象，进行数据库操作。封装不同协议接口，支持数据库操作，socket通信，rpc调用等。

model：对表接口的抽象实体，通过调用sequelize提供的接口进行直接的数据库操作。不使用关联操作。不返回raw对象。

util：可以看做Common Service，用于实现常用的分页功能，关联用户表或其他表的查询功能。

router：通过配置文件进行设置

filter：过滤器，js通过decorator实现

MQ：消息队列

schedule：定时任务

constant：常量设置

config：各种配置

#### 规范
controller，service，model文件名使用大驼峰命名法

controller：IndexController

service：   IndexService

model:      Account, User

### TODO

● 支持LiveReload功能

○ 支持将打包错误显示在浏览器 **[不实用，推迟]**

● 开发router中间键，用更优雅的方式写router

● 每次启动项目生成一个router关联的文件

~~○ 支持yo-generator生成~~

● 开发MarX-CLI(不依赖yo)

● 通过命令展示／查询 url对应的Controller和Action

● 支持命令行自动生成前端代码，controller代码，service代码

● 将一些filter，base，middleware代码放到marx的lib中

● 动态配置boilerplate的package.json版本

● 支持dashboard启动应用

○ babel启动搞得优雅一点

○ 支持unit test

○ 支持自动生成文档

○ 开发消息队列模块

○ 开发定时任务模块

○ 开发WebSocket模块

○ 支持一键持续集成

○ 支持日志分析

○ 支持性能监控

○ 开发自己的ORM，替换sequelize

### LINKS

[SaaS系统12原则](https://12factor.net/zh_cn/)
