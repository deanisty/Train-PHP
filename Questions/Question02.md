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


#### ThinkPHP框架优缺点			
#### global配置相是thinkphp框架有什么关系？	
#### ThinkPHP工程的目录结构		
#### 分支下的结构目录详解，例如fun，fsdk
#### url访问与模块控制器之间的关系
