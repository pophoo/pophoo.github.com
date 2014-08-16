---
layout: post
title: "安装MySQL和RMySQL"
description: "安装MySQL和RMySQL"
category: learn
tags: [R, MySQL, RMySQL]
---

{% include JB/setup %}

## 安装MySQL

[MySQL Installer](http://dev.mysql.com/downloads/windows/installer/)提供一个易于安装,向导化的MySQL安装包.点击[mysql-installer-community-5.6.20.0.msi](http://dev.mysql.com/get/Downloads/MySQLInstaller/mysql-installer-community-5.6.20.0.msi)即可下载.最新MySQL的版本是5.6,安装路径是:`C:\Program Files\MySQL`.打开`MySQL Workbench`,可以看到`MySQL`默认安装包括`world`数据库,数据库下包括`country`等表.

<a 
  href='http://tietuku.com/c6a778d5a1adf3d9'>
  <img 
    src='http://i2.tietuku.com/c6a778d5a1adf3d9.png'
    width="80%" 
    height="80%"
  />
</a>

## 安装RMySQL

安装RMySQL之前,需要进行一系列设置.

1.安装R语言到`C:\Program Files\R`,并安装相应版本的[Rtools](http://cran.r-project.org/bin/windows/Rtools/).

2.新建文本文档,输入以下内容,

```
MYSQL_HOME=C:/Program Files/MySQL/MySQL Server 5.6/
```

,保存为`C:\Program Files\R\etc\Renviron.site`.

3.在`C:\Program Files\MySQL\MySQL Server 5.6\lib`文件夹中新建`opt`文件夹,将`C:\Program Files\MySQL\MySQL Server 5.6\lib`文件夹
中的`libmysql.lib`复制到`opt`文件夹.

4.将`C:\Program Files\MySQL\MySQL Server 5.6\lib`文件夹中的`libmysql.dll`复制到`opt`文件夹,`C:\Program Files\R\bin\i386`,`C:\Program Files\R\bin\x64`和`C:\Program Files\MySQL\MySQL Server 5.6\bin`.

运行`install.packages('RMySQL',type ='source')`即可安装`RMySQL`包.运行`Sys.getenv("MYSQL_HOME")`,验证`RMySQL`是否安装成功.如果正确输出`Renviron.site`设置的路径即安装成功.

{% highlight r %}
Sys.getenv("MYSQL_HOME")
{% endhighlight %}

{% highlight text %}
## [1] "C:/Program Files/MySQL/MySQL Server 5.6/"
{% endhighlight %}

## 代码示例

使用`RMySQL`读取`country`表,代码如下,

{% highlight r %}
library(RMySQL)
mysql = dbDriver("MySQL")
world = dbConnect(mysql,dbname="world","root","********")
country = dbGetQuery(world,"select * from country")
dbDisconnect(world)
dbUnloadDriver(mysql)
{% endhighlight %}




