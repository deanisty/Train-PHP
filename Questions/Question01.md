## Q1:关于PHP你想了解哪些或者有什么疑问？

#### 实用调试技巧

* [php-debug](https://github.com/deanisty/Train-PHP/blob/master/php/debug.md)

* [example](https://github.com/deanisty/Train-PHP/blob/master/php/example.md)

#### 测试过程中过于风控部分的把握

啥意思？

#### PHP服务端接口调用原理

* [http](http/README.md)

#### PHP和web端数据交互有什么要测试注意的没	

* 接口必须正确 - 在大量不同输入值输入的情况下，输出值和预期保持一致
* 接口必须稳定 - 输入值的变化对接口的影响 无论什么输入都不应该导致代码级别的错误
* 接口必须高效 - 在大量请求甚至高并发情况下 都能在有限时间内返回响应

#### PHP和SQL数据库执行效率指什么

PHP执行效率是指代码的执行速度，一般涉及 数据处理速度、不同数据结构对代码速度的影响，实际情况下，对代码效率影响较大的是循环语句，比如 for/foreach,while
，还有递归函数实现的类似循环效果，这些循环语法如果使用不当，或者嵌套过多，很容造成代码效率低下、甚至导致内存消耗殆尽、代码超时等问题。

SQL的效率主要受到 SQL语句 执行速度影响。参看 mysql 部分

#### php晋级提升需要学习哪方面知识	

https://www.jianshu.com/p/1fecafc15772

#### 自动加载 spl_autoload 机制	

https://github.com/deanisty/Train-PHP/blob/master/php/autoload.md

#### php脚本怎么运行的	

[PHP基础](https://github.com/deanisty/Train-PHP/blob/master/php/README.md)

#### php的缓存机制			

* http://php.net/manual/zh/refs.basic.php.php

apc已经被apcu替代，可参看 fsdk -> fc 部分，以及 apcinfo.php 文件

#### 经常在白盒的时候看到新项目使用已有的model下的方法，开发时是如何知道这个是已有的，凭经验？

基本上是的。可以使用编辑器的搜索功能

