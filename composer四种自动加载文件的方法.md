# composer四种自动加载文件的方法 #
对于第三方包的自动加载，Composer提供了四种方式的支持，分别是 PSR-0和PSR-4的自动加载（我的一篇文章也有介绍过它们)，生成class-map，和直接包含files的方式。

参考文档：

>http://blog.csdn.net/zhengwish/article/details/51734083

composer四种自动加载类的方式
>http://www.tuicool.com/articles/mARrMj6

如何使用composer的autoload来自动加载自己编写的函数库与类库？
>http://drops.leavesongs.com/php/composer-autoload-class-and-function-written-myself.html



composer autoload参考文档

>http://docs.phpcomposer.com/04-schema.html#autoload



**1.PSR-0**

在 psr-0 key 下你定义了一个命名空间到实际路径的映射（相对于包的根目录）。

>自动加载规范,目前已经弃用

**2.PSR-1**

基本代码规范


**3.PSR-2**

>代码风格规范

**4.PSR-2**

日志接口规范

**5.PSR-4**

这个 PSR 描述的是通过文件路径自动载入类的指南；它作为对 PSR-0 的补充；根据这个指导如何规范存放文件来自动载入；


使用PSR4，我觉得有2个好处：

>1. 减少代码目录的深度
>2. 可以通过前缀快速找到映射目录，提高自动加载的效率

## Classmap ##


你可以用 classmap 生成支持支持自定义加载的不遵循 PSR-0/4 规范的类库。要配置它指向需要的目录，以便能够准确搜索到类文件。



## files ##

files就是需要composer自动帮我们加载的函数库（不含类），只要在后面的数组中将函数库的文件路径写入即可。

- 配置composer.json的autoload:
-
	[root@xls ~]# cat composer.json 
	{
	    "require": {
	        "phpdocumentor/phpdocumentor": "2.*"
	    },
	    "autoload":{
			"files": ["class/function.php"]  
	    }
	}
  
- 加载
-
	[root@xls ~]# composer dump-autoload

- 使用：
-
	<?php
		require_once './vendor/autoload.php';
		demo();
	?>

>class目录与vendor同级
>
>配置好composer.json后执行composer dump-autoload命令后写入autoload_files.php中
>
>files主要用于配置函数库

>参考：http://blog.csdn.net/github_26672553/article/details/51778568



## psr-4 ##

composer.json配置autoload下的psr-4,通过命名空间指向实际路径来加载

	[root@xls ~]# cat composer.json 
	{
	    "require": {
	        "phpdocumentor/phpdocumentor": "2.*"
	    },
	    "autoload":{
		"files": ["class/function.php"],
	        "psr-4":{
			"Class\\":"class/"
			}
	    }
	}

执行composer dump-autoload加载

在 vendor/composer/autoload_psr4.php中就多了一项：

    'Class\\' => array($baseDir . '/class'),

至此class下的类就可以使用了:use \Class\Create


## psr-0 ##

定义了命名空间到实际路径的映射（相对于包的根目录），在composer install/update/dump-autoload 过程中，PSR-0 引用都将被结合为一个单一的键值对数组，存储至 vendor/composer/autoload_namespaces.php 


	[root@xls ~]# cat composer.json 
	{
	    "require": {
	        "phpdocumentor/phpdocumentor": "2.*"
	    },
	    "autoload":{
		"files": ["class/function.php"],
	        "psr-4":{
			"Class\\":"class/"
		},
		"psr-0":{
			"Monolog\\":"class/"	
			}
	    }
	}


[root@xls ~]# cat vendor/composer/autoload_namespaces.php 

 	'Monolog\\' => array($baseDir . '/class'),