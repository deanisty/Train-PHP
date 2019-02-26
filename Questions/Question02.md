## Q2:ThinkPHP框架相关


#### 框架整体运作及各部调用		

##### 版本 未知

版本可能在 2.x 到 3之间，由于进行过多次二次开发，框架被改的面目全非，因此不再适合更新版本，可能会一直使用下去

##### MVC架构

Model -> View -> Controller 

##### index.php 入口

App::init()

* 设定错误和异常处理
* 预编译项目 - 生成压缩版的配置文件和项目共用方法到 ~app.php  ThinkPHP 公共方法 到 ~Runtime.php
* 设置系统时区
* 注册 ThinkPHP 自身的 AUTOLOAD方法
* Session初始化
* URL调度 解析 URL 、分析路由、确定访问的模块->控制器->具体方法
* 加载特定的配置文件（二次开发新增的）包括 全局配置文件、全局跟踪码、模块配置文件
* 语言检查、模板检查、HTML缓存
* 初始化HTML标签插件

App::exec()

* 请求分组/模块名称合法性检测
* 从配置中获取设置的分组和模块
* 加载模块
* 执行请求的Action对应的方法
* Action对应的方法可以直接输出结果（ajax）也可以调用模板的display()方法展示页面（HTML）

#### ThinkPHP框架优缺点

##### 优点

* 简单，容易上手
* 基于MVC架构，逻辑简单
* 缓存机制，提高运行速度
* URL模式支持 普通模式、PATHINFO模式、REWRITE模式和兼容模式
* 可配置，通过修改配置文件覆盖默认配置可以实现自定义功能
* 动态模型，无需创建任何对应的模型类，轻松完成CURD操作
* AJAX支持：内置AJAX数据返回方法，支持JSON、XML和EVAL格式返回

##### 缺点

* 不支持命名空间，当项目规模增大时很容易出现类命令冲突问题
* 目录名不支持驼峰格式，在windows和linux间迁移项目容易出错
* 缺少命令行工具的支持
* 自带工具库功能太少，缺少常用功能的封装
* 不支持 PHP 版本的升级
* 文档过于简单，部分功能只能通过代码了解
* 控制器目录只支持两级，会导致action目录下文件过多
* 缺少 autoload 机制，部分 model 类需要手动引入
* 缺少 URL 参数自动注入功能
* 不支持 REST 开发风格
* 模板引擎种类少
* 缺少单元测试模块支持
* 等...

#### global配置相是thinkphp框架有什么关系？	

thinkphp 框架启动后会加载项目本身的 Conf目录下的配置，同名的配置会被覆盖，达到自定义配置的效果

#### ThinkPHP工程的目录结构

* Common  - 通用全局函数，通用配置
* Conf   -  环境相关的配置
* Cron  -  后台脚本目录
* Lib/Action   - 控制器目录
* Lib/Model   -  模型目录
* Lib/ORG   -  第三方库目录
* Runtime   -  运行时缓存目录
* Tpl     -   视图模板目录
* index.php   -  项目入口文件

#### 分支下的结构目录详解，例如fun，fsdk

* fun 依赖 thinkphp 框架 结构同上题 
* fsdk 不依赖 thinkphp 框架 入口文件为 ThinkPHP\Common\functions.php

#### url访问与模块控制器之间的关系

* 域名/分组/模块/控制器/方法名
* 分组列表配置 ： APP_GROUP_LIST
* 分组缺失取配置文件中的 DEFAULT_GROUP
* 方法名缺失默认取 DEFAULT_ACTION    ThinkPHP\Common\convention.php
* 对应目录为 Lib/分组名/模块名
