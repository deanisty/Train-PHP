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

* error_reporting

* display_errors

#### 类 var_dump() 函数断点调试
