
**1. composer是什么**

>composer是php依赖关系管理工作，是用php开发，被称为php的未来，就相当于python的pip

**2. composer能做什么**



- 应用在**项目**中，你的项目依赖于若干个库，其中一些库又依赖于其他库。Composer 会找出哪个版本的包需要安装，并安装它们（将它们下载到你的项目中）。



- Packagist 上发布自己的包


**3.资料**


中文文档

>http://docs.phpcomposer.com

官网：

>https://packagist.org

资源库：

>packagist 是 Composer 的主要资源库官网：packagist.org


**4.常用**


- 平台软件包：

	php ext-gd hhvm lib-curl

	查看：composer show --platform


- 错误解决

	  [RuntimeException]                                                                                                    
	  The openssl extension is required for SSL/TLS protection but is not available. If you can not enable the openssl ext  
	  ension, you can disable this error, at your own risk, by setting the 'disable-tls' option to true.    


	**composer config -g -- disable-tls true**



- 发布到VCS(线上版本控制系统)上通过composer进行安装

本地项目安装：

	{
	    "name": "acme/blog",
	    "repositories": [
	        {
	            "type": "vcs",
	            "url": "https://github.com/username/hello-world"
	        }
	    ],
	    "require": {
	        "acme/hello-world": "dev-master"
	    }
	}


>只要项目中包含composer.json即可

>repositories:库


- 发布到packagist
>就可不需要指定repositories即可安装了


有效性检测 validate


- 创建项目 create-project


>这相当于执行了一个 git clone 或 svn checkout 命令后将这个包的依赖安装到它自己的 vendor 目录。


- 打印自动加载索引 dump-autoload

- 诊断 diagnose

	composer diagnose

- 归档 archive