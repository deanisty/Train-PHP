#### 简介

> 参考： https://www.kancloud.cn/nickbai/php7/363257

PHP是一种非常流行的高级脚本语言，尤其适合Web开发，快速、灵活和实用是PHP最重要的特点。PHP自1995年由 Lerdorf （拉斯姆斯·勒多夫）创建以来，
在全球得到了非常广泛的应用。

在1995年早期以Personal Home Page Tools (PHP Tools) 开始对外发表第一个版本，Lerdorf写了一些介绍此程序的文档，并且发布了PHP1.0。在这早期的版本中，
提供了访客留言本、访客计数器等简单的功能，之后越来越多的网站开始使用PHP，并且强烈要求增加一些特性，在新的成员加入开发行列之后，
Rasmus Lerdorf 在1995年6月8日将 PHP/FI 公开发布，希望可以通过社群来加速程序开发与寻找错误。这个发布的版本命名为 PHP 2，已经有今日 PHP 的一些雏型，
像是类似 Perl 的变量命名方式、表单处理功能、以及嵌入到 HTML 中执行的能力。程序语法上也类似 Perl，有较多的限制，不过更简单、更有弹性。
PHP/FI加入了对MySQL的支持，从此建立了PHP在动态网页开发上的地位。到了1996年底，有15000个网站使用 PHP/FI。

在1997年，任职于 Technion IIT 公司的两个以色列程序设计师：Zeev Suraski 和 Andi Gutmans，重写了PHP的解析器，成为PHP3的基础，
而 PHP 也在这个时候改称为PHP：Hypertext Preprocessor，1998年6月正式发布 PHP 3。Zeev Suraski 和 Andi Gutmans 在 PHP 3 发布后开始改写 PHP 的核心，
这个在1999年发布的解析器称为 Zend Engine，他们也在以色列的 Ramat Gan 成立了 Zend Technologies 来管理 PHP 的开发。

在2000年5月22日，以Zend Engine 1.0为基础的PHP 4正式发布，2004年7月13日则发布了PHP 5，PHP 5则使用了第二代的Zend Engine。
PHP包含了许多新特色:完全实现面向对象、引入PDO、以及许多性能方面的改进。目前PHP5.X仍然是应用非常广泛的一个版本。

#### 特性

PHP 独特的语法混合了 C、Java、Perl 以及 PHP 自创新的语法，丰富的语法支持、同时支持面向对象、面向过程，相比C、Java等语言具有语法简洁、
使用灵活、开发效率高、容易学习等特点。

* 开源免费：PHP社群有大量活跃的开发者贡献代码
* 快捷：程序开发快，运行快，技术本身学习快，实用性强
* 效率高：PHP消耗相当少的系统资源，自动gc机制
* 类库资源：有大量可用类库供开发者使用
* 扩展性：允许用户使用C/C++扩展PHP
* 跨平台：可以在unix、windows、max os等系统上面使用PHP

#### PHP的相关组成

##### SAPI

PHP本身可以理解为是一个库函数，提供语言的编译与执行服务，它有标准的输入、输出，而SAPI是PHP的接入层，它接收用户的请求，
然后调用PHP内核提供的一些接口完成PHP脚本的执行，所以严格意义上讲SAPI并不算PHP内核的一部分。PHP的角色就好比是leveldb，它实现了基本存储功能，
但是没有网络处理模块，而我们基于leveldb实现的完整存储服务就好比是SAPI。PHP中常用的SAPI有cli、php-fpm，
cli是命令行下执行PHP脚本的实现：bin/php script.php，它是单进程的，处理模型比较简单，而php-fpm相对比较复杂，它实现了网络处理模块，
用于与web服务器交互。

##### Zend引擎

Zend是PHP语言实现的最为重要的部分，是PHP最基础、最核心的部分，它的源码在/Zend目录下，PHP代码从编译到执行都是由Zend完成的。
Zend整体由两个部分组成：

* 编译器： 负责将PHP代码编译为抽象语法树，然后进一步编译为可执行的opcodes，这个过程相当于GCC的工作，编译器是一个语言实现的基础
* 执行器： 负责执行编译器输出的opcodes，也就是执行PHP脚本中编写的代码逻辑

##### 扩展

#### PHP代码执行流程

##### 模块初始化阶段 module startup

这个阶段主要进行PHP框架、Zend引擎的初始化操作。

* 激活 SAPI
* 启动PHP输出：php_output_startup
* 初始化垃圾回收器
* 启动Zend引擎 
* 注册PHP常量
* 解析 php.ini
* 映射PHP、Zend核心的 php.ini 配置
* 注册用于获取 $_GET $_POST $_COOKIE $_SERVER $_ENV $_REQUEST $_FILES 变量的handler
* 注册静态编译的扩展
* 注册动态加载的扩展
* 回调各扩展定义的钩子函数
* 注册 php.ini 中禁用的函数、类


##### 请求初始化阶段 request startup

* 激活输出：php_output_activate()
* 激活 Zend 引擎： zend_activate()
* 激活 SAPI ： sapi_activate()
* 回调各扩展定义的钩子函数

##### 执行PHP脚本阶段 execute script

该阶段包括 词法分析、语法分析、PHP代码的编译、执行，是 Zend 引擎最重要的功能。
在编译阶段PHP代码经历 从 PHP源代码 -> 抽象语法树 -> opline指令，最终 opline 指令 被 Zend 引擎的执行器执行，完成PHP 代码的执行流程。

##### 请求结束阶段 request shutdown

PHP脚本执行完成后进入请求关闭阶段，这个阶段将 flush 输出内容、发送 HTTP 应答 header 、清理全局变量、关闭编译器、关闭执行器等。
该阶段也会回调各扩展定的的 request shutdown 钩子函数。

##### 模块关闭阶段 module shutdown

该阶段在 SAPI 关闭时执行，与模块初始化阶段对应，这个阶段主要进行资源的清理、PHP各模块的关闭操作，同时，将回调各货站定义的 module shutdown 钩子函数
