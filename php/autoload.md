#### 类的自动加载

> http://php.net/manual/zh/language.oop5.autoload.php

* 一般情况下，如果调用了一个当前上下文中不存在的类，PHP 会去找 __autoload() 函数来加载这个类，如果没有定义 __autoload() 函数会抛出异常。
* spl_autoload_register() 函数提供了更加灵活的类的自动加载方式。
* spl_autoload_functions() 函数返回所有已加载的 __autoload() 函数。

##### 示例

```SHELL 
autoload.php
```
