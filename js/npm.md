# npm
[TOC]
## 一 概述
npm是世界上最大的js包管理工具。
### 1 历史
### 2 常识 
1. 相关网址
    - npm被依赖榜单:[https://www.npmjs.com/browse/depended](https://www.npmjs.com/browse/depended)
    - npm getting-started:[https://www.npmjs.com/browse/depended](https://www.npmjs.com/browse/depended)
## 二 安装配置
### 1 win
1. 直接安装nodeJS，里面带有npm
2. 配置

    win的npm配置文件`.npmrc`的默认位置是`C:\\Users\\Administrator\\.npmrc`,包安装的默认位置是`C:\Users\xxx\AppData\Roaming\npm`
    1. 换源：`npm config set registry https://registry.npm.taobao.org`

### 2 linux
#### 2.1 ubuntu
1. sudo apt install npm
2. 配置源，虽然仓库没有被qiang，但是速度较慢：
    1. 临时使用
    2. 使用cnpm(本质是安装)
    3. 配置`~/.npmrc`(推荐，一劳永逸)：
    ```bash
    registry =https://registry.npm.taobao.org
    ```

### 3 mac
1. mac下home目录默认没有`.npmrc`文件,使用`npm config set registry https://registry.npm.taobao.org`命令会生成并配置好`.npmrc`,一步到位.

## 三. 基础
### 1 安装卸载命令
1. 安装模块`npm install`(简写`npm i`)

    1. 不加参数使用:会根据目录下的package.json配置文件下载所需的模块.
    2. 本地安装`npm install xxx`:会安装在当前目录的node_modules目录(没有则自动创建该目录)里.
    3. 全局安装则加上参数`-g`(`--global`):安装全局依赖，如果没有指定包名，则将当前目录中的包安装至全局(?)。
    4. 参数`--dry-run`:走一遍安装的流程并报告结果，但实际上没有安装任何依赖
    5. 关于模块名后的版本号(即版本发布时的tag)
        
        包名后可以直接跟[@version]即包的版本号来安装制定版本,也可以用通用的版本名称,如
        - `@latest`或`@next`:最新版本
    6. 参数`--save`:安装模块并写入到当前项目`package.json`文件的`dependencies`中
    7. 参数`--save-dev`:安装模块并写入到当前项目`package.json`文件的`ddevDependencies`中
        
2. 卸载模块`npm uninstall`

    删除制定的依赖包并且完全移除为了该包而安装的任何文件
    1. 常用参数，和install一样
    2. 别名:`remove 、rm、r、un、unlink`
    3. 之前卸载之后还需要执行`npm cache clean`清理,但是npm@5之后还要加上`--force`,但是可能会导致一些不必要的问题,所以慎用,清理之后使用`npm cache verify`(待补充).具体见缓存部分.
3. `npm update`

    升级所有依赖包至版本规则允许的最高版本,并安装缺失的依赖包
    1. 常用参数
        - `-depth Infinity`:npm@2.6.1k开始，update命令默认只升级最顶层的依赖，即直接的依赖，加上该命令则升级所有依赖
        - `--save`:升级同时将升级的版本号记录到package.json
4. 清除未用到的模块`npm prune`

### 2 查看命令
1. 查看已安装模块:`npm list`

    显示模块名和版本信息
    1. 一般使用`npm list [moduleName]`:默认查看本地模块
    2. 参数`-g`查看全局安装的模块
    3. 参数`--depth=[num]`:限制模块的等级,比如查看最顶层模块,可以用`npm list -g --depth=0`
2. 查看安装目录:`npm root`
    1. 直接使用:查看项目中模块所在的目录
    2. 参数`-g`:查看全局安装的模块所在的目录
3. 查看模块的`package.json`相关信息
    1. 直接使用`npm view [moduleName]`
    2. 参数`dependencies`:查看包对其他包依赖信息(但我试了没用,待补充)
    2. 参数`version`:查看包
4. 查看过时的包:`npm outdated`
5. 查看模块的主页和文档
    - `npm home [moduleName]`
    - `npm docs [moduleName]`
### 3 配置命令
1. 查看所有配置:`npm config ls -l`
2. 查看某个配置:`npm config get xxx`
    - 比如查看cache目录,可以用`npm config get cache`

### 4 缓存
在 npm@5 以前，每个缓存的模块在 ~/.npm 文件夹中以模块名的形式直接存储，例如 koa 模块存储在 ~/.npm/koa 文件夹中。而 npm@5 版本开始，数据存储在 ~/.npm/_cacache 中，并且不是以模块名直接存放。
npm 的缓存是使用 pacote 模块进行下载和管理，基于 cacache 缓存存储。由于 npm 会维护缓存数据的完整性，一旦数据发生错误，就回重新获取。因此不推荐手动清理缓存，除非需要释放磁盘空间，这也是要强制加上 --force 参数的原因。

目前没有提供用户自己管理缓存数据的命令，随着你不断安装新的模块，缓存数据也会越来越多，因为 npm 不会自己删除数据。

1. `npm cache clean`

    删除缓存目录下的所有数据。从 npm@5 开始，为了保证缓存数据的有效性和完整性，需要加上 --force 参数。
2. `npm cache verify`
    
    验证缓存数据的有效性和完整性，清理垃圾数据。

### 4 运行相关命令
1. 更改包后重建:`npm rebuild [moduleName]`
### 5 package.json
一般每个项目的根目录下都有该配置文件,可通过`npm init`交互式生成
1. 版本控制

    npm的版本号遵循semver2.0规范([语义化版本2.0.0](https://semver.org/lang/zh-CN/))
    1. semver的版本号简单概括是：

        XYZ （主版本号.次版本号.修订号）修复问题但不影响API 时，递增修订号；API 保持向下兼容的新增及修改时，递增次版本号；进行不向下兼容的修改时，递增主版本号。
    2. semver不仅仅是概念,还有自己的js包,为发布版本设计的
    3. npm的版本限定(`semver-ranges`)
        - 波浪号`~`:不改变大版本和中版本号,且不低于指定版本的最新的版本.比如`~1.2.2`,则表示安装`1.2.x`的最新版本,不低于`1.2.2`且不超过`1.3.0`
        - 脱字符`^`
            * 如果大版本号不为0:不改变大版本号,其他类似`~`,比如`^1.2.2`,表示安装`1.x.x`的最新版本.
            * 如果大版本号为0:跟`~`一样
        - `latest`或`*`:安装最新版本
        - 大于,小于,等于
        - `x`:任意版本,如`1.2.x`
        - `||`和`&&`
        - `alpha`/`beta`/`rc`:
2. 字段说明
    1. `scripts`:指定运行脚本命令的npm命令行缩写,比如比如`start`指定了运行`npm run start`时，所要执行的命令,如

        ```json
        "scripts": {
            "preinstall": "echo here it comes!",
            "postinstall": "echo there it goes!",
            "start": "node index.js",
            "test": "tap test/*.js"
        }
        ```
    2. `dependencies`和`devDependencies`

        前者指定了项目运行所依赖的模块，后者指定项目开发所需要的模块。其中键是模块名,值是模块的版本范围
    3. `peerDependencies`

        假如项目同时依赖A和B模块的1.0版本,但A模块又依赖B模块的2.0版本,大多数情况下B的两个版本可以共存,不会构成问题.但是，有一种情况，会出现问题，就是这种依赖关系将暴露给用户:最典型的场景就是插件.这个时候就需要提醒用户，如果A和B一起安装，那么B必须是2.0模块。如,

        ```json
        {
        "name": "chai-as-promised",
            "peerDependencies": {
                "chai": "1.x"
            }
        }
        ```
        上面代码指定，安装`chai-as-promised`模块时，主程序`chai`必须一起安装，而且`chai`的版本必须是1.x。如果你的项目指定的依赖是`chai`的2.0版本，就会报错。
        注意npm3.0版开始，`peerDependencies`不再会默认安装了
    5. `bin`:指定各个内部命令对应的可执行文件的位置
    6. `main`:指定了加载的入口文件，`require('moduleName')`就会加载这个文件。这个字段的默认值是模块根目录下面的`index.js`。
    7. `config`:用于添加命令行的环境变量,如下`package.json`,

        ```json
        {
            "name" : "foo",
            "config" : { "port" : "8080" },
            "scripts" : { "start" : "node server.js" }
        }
        ```
        然后就可以在server.js中引用config字段的值,如
        ```javascript
        http
            .createServer(...)
            .listen(process.env.npm_package_config_port)
        ```
    8. `engines`:指明了该模块运行的平台，比如Node或npm的某个版本或者浏览器
### 相关文件说明
#### npm-shrinkwrap.json
用于将项目的模块版本进行精确锁定,使用流程如下
1. `npm install ...`安装模块
2. `npm prune`:清除未使用的模块
3. `npm shrinkwrap`:生成`npm-shrinkwrap.json`
4. 提交该json文件到git,这样其他人clone项目之后执行`npm install`所还原的依赖树就是一样的.
#### npm-debug.log
npm的错误报告

## 四 经验
### 1. 发布包的步骤
1. npmadduser登录
2. npminit
    1. 提问，根据回答生成package.json文件
3. npm publish
    1. 版本tag:默认是`latest`
4. npm unpublish（不推荐使用）
5. npm deprecate:表示放弃一个包，该包在npm中没有取消，安装该包的用户会看到警告信息
6. npm view：显示一个包(在npm上)的详细信息
## 六 问题
### 1 已解决
1. 用`npm list -g`命令出现大量的`npm ERR! extraneous:...`

    当时我的npm版本是3.10.10，升级之后(5.6.0)问题解决

2. "Unexpected end of JSON input while parsing near"

    `npm cache clean --force`
### 2 未解决
1. 淘宝镜像
    1. cnpm uninstall并不能生效，不知道为什么
2. package-lock.json
3. 注册npm账户的好处,除了记录自己使用的仓库,还有什么?
4. 深入 Node 模块的安装和发布；[https://segmentfault.com/a/1190000004221514](https://segmentfault.com/a/1190000004221514)
5. npm link是什么东西,和angular的ng如何配置使用?
    [CLI tool for Angular](https://github.com/angular/angular-cli)