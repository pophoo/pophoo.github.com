---
layout: post
title: "C#调用R"
description: "C#调用R"
category: learn
tags: [C#, R, Visual Studio, NuGet, R.NET]
---

{% include JB/setup %}

C#读作C Sharp,是微软公司在2000年6月发布的一种新的编程语言,是一种面向对象的,运行于.NET Framework之上的高级程序设计语言.C#可以很快捷的实现图形化界面,和R结合,能够很快生成一个应用工具.

本文介绍如何通过R.NET实现C#调用R.

[R.NET](http://rdotnet.codeplex.com)是一个.NET框架包,该包可以实现.NET框架调用R.

首先,电脑在电脑中安装[Visual Studio](http://www.microsoft.com/en-us/download/details.aspx?id=40778)和[R](http://www.r-project.org).我的测试环境[Visual Studio](http://www.microsoft.com/en-us/download/details.aspx?id=40778)版本是Microsoft Visual Studio Ultimate 2013.R的版本基本信息如下,


{% highlight r %}
sessionInfo()
{% endhighlight %}



{% highlight text %}
## R version 3.1.0 (2014-04-10)
## Platform: x86_64-w64-mingw32/x64 (64-bit)
## 
## locale:
## [1] LC_COLLATE=Chinese (Simplified)_People's Republic of China.936 
## [2] LC_CTYPE=Chinese (Simplified)_People's Republic of China.936   
## [3] LC_MONETARY=Chinese (Simplified)_People's Republic of China.936
## [4] LC_NUMERIC=C                                                   
## [5] LC_TIME=Chinese (Simplified)_People's Republic of China.936    
## 
## attached base packages:
## [1] stats     graphics  grDevices utils     datasets  methods   base     
## 
## other attached packages:
## [1] highlight_0.4.4 knitr_1.6      
## 
## loaded via a namespace (and not attached):
## [1] evaluate_0.5.5 formatR_0.10   stringr_0.6.2  tools_3.1.0
{% endhighlight %}

由于[R.NET](http://rdotnet.codeplex.com)是发布在[NuGet](https://www.nuget.org)上的包,需要在[Visual Studio](http://www.microsoft.com/en-us/download/details.aspx?id=40778)上安装NuGet Package Manager.

打开[Visual Studio](http://www.microsoft.com/en-us/download/details.aspx?id=40778),`工具`菜单栏下`扩展和更新`,选择`联机`下面的`Visual Studio库`,下载`NuGet Package Manager for Visual Studio`,安装并重启[Visual Studio](http://www.microsoft.com/en-us/download/details.aspx?id=40778).

<a 
  href="http://tietuku.com/535b04402fd0bbfd" target="_blank">
  <img src="http://i1.tietuku.com/535b04402fd0bbfd.png" />
</a>

通过[Visual Studio](http://www.microsoft.com/en-us/download/details.aspx?id=40778)新建`C#控制台应用程序`类型解决方案`Hello World`.

<a 
  href="http://tietuku.com/39a9d71519db6533" target="_blank">
  <img src="http://i1.tietuku.com/39a9d71519db6533.png" />
</a>

右击`解决方案资源管理器`的`引用`,选择`管理NuGet程序包`.

<a 
  href="http://tietuku.com/aa0706019bbd2b5f" target="_blank">
  <img src="http://i1.tietuku.com/aa0706019bbd2b5f.png" />
</a>

搜素联机`R.NET`,安装识别码为`R.NET.Community`的`R.NET`.

<a 
  href="http://tietuku.com/c69504c27f048aff" target="_blank">
  <img src="http://i1.tietuku.com/c69504c27f048aff.png" />
</a>

安装成功后,`引用`会多出`RDotNet`和`RDotNet.NativeLibrary`两项.

<a 
  href="http://tietuku.com/068e881eeb90686d" target="_blank">
  <img src="http://i1.tietuku.com/068e881eeb90686d.png" />
</a>

而且[Visual Studio](http://www.microsoft.com/en-us/download/details.aspx?id=40778)的`输出`窗口会有相应输出.

```
------- 正在安装...R.NET.Community 1.5.15 -------
正在安装“R.NET.Community 1.5.15”。
已将文件“RDotNet.dll”添加到文件夹“R.NET.Community.1.5.15\lib\net40”。
已将文件“RDotNet.NativeLibrary.dll”添加到文件夹“R.NET.Community.1.5.15\lib\net40”。
已将文件“RDotNet.NativeLibrary.XML”添加到文件夹“R.NET.Community.1.5.15\lib\net40”。
已将文件“RDotNet.XML”添加到文件夹“R.NET.Community.1.5.15\lib\net40”。
已将文件“R.NET.Community.1.5.15.nupkg”添加到文件夹“R.NET.Community.1.5.15”。
已成功安装“R.NET.Community 1.5.15”。
正在将“R.NET.Community 1.5.15”添加到 Hello World。
用于将程序包“R.NET.Community 1.5.15”添加到目标为“net45”的项目“Hello World”，
>> 正在从“lib\net40” 添加 程序集引用
已将引用“RDotNet”添加到项目“Hello World”
已将引用“RDotNet.NativeLibrary”添加到项目“Hello World”
已将引用“System.Numerics”添加到项目“Hello World”
已添加文件“packages.config”。
已将文件“packages.config”添加到项目“Hello World”
已成功将“R.NET.Community 1.5.15”添加到 Hello World。
==============================
```

在`Program.cs`中,输入如下代码.

```
using RDotNet;
using RDotNet.NativeLibrary;
using System;
using System.Collections.Generic;
using System.IO;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace HelloWorld
{
   class Program
   {
      static void Main(string[] args)
      {
         REngine.SetEnvironmentVariables(); // <-- May be omitted; next line would call it.
         REngine engine = REngine.GetInstance();
         // A somewhat contrived but customary Hello World:
         CharacterVector charVec = engine.CreateCharacterVector(new[] { "Hello, R world!, .NET speaking" });
         engine.SetSymbol("greetings", charVec);
         engine.Evaluate("str(greetings)"); // print out in the console
         string[] a = engine.Evaluate("'Hi there .NET, from the R engine'").AsCharacter().ToArray();
         Console.WriteLine("R answered: '{0}'", a[0]);
         Console.WriteLine("Press any key to exit the program");
         Console.ReadKey();
         engine.Dispose();
      }
   }
}
```

选择`调试`菜单栏下`开始执行(不调试)`,输出如下.

<a 
  href="http://tietuku.com/9159a48b1d96a321" target="_blank">
  <img src="http://i1.tietuku.com/9159a48b1d96a321.png" />
</a>

