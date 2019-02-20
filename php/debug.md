### 扩展提供的调试功能

#### xdebug

一个PHP扩展，非官方。

> 官网： https://xdebug.org/index.php
 
Xdebug是一个PHP扩展用来协助调试和开发。

* 它包含一个单步调试器，可以在IDE下使用

* 它改进了PHP的 var_dump() 函数，支持可控的打印结果

* 它对 Notices, Warnings, Errors and Exceptions 这些级别的错误增加了代码堆栈的追踪

* 它拥有函数调用和磁盘变量分配记录的功能

* 它包含一个分析器

* 它提供代码覆盖功能，可以和 PHPUnit 一起使用


### PHP本身的调试功能

#### 错误输出控制

> php.ini 文件 [ Error handling and logging ] 部分
> 官方文档： http://php.net/manual/zh/errorfunc.configuration.php

* error_reporting - 控制 PHP 是否捕捉错误

* display_errors - 控制 是否展示错误信息，生产环境设置关闭

* display_startup_errors - 是否显示启动期间的错误，一般用于检测配置文件是否正确，，生产环境设置关闭

* log_errors - 是否将错误记录到日志

* log_errors_max_len - 设置 log_errors 的最大字节数

* error_log - 日志文件的路径

#### 使用 var_dump() 函数断点调试

如果代码没有错误，但是有 bug ，需要使用 类似 var_dump() 的类似函数进行手动断点调试。
