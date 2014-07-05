---
layout: post
title: "安装boost库"
description: "安装boost库"
category: learn
tags: [Visual Studio, C++, boost]
---

{% include JB/setup %}

[boost](http://www.boost.org)是C++最重要的库之一,已上传到[Source Forge](http://sourceforge.net/projects/boost/files/).

64位机可以选择下载[boost_1_55_0-msvc-10.0-64.exe](http://cznic.dl.sourceforge.net/project/boost/boost-binaries/1.55.0-build2/boost_1_55_0-msvc-12.0-64.exe).运行安装到`E:\Program Files\boost_1_55_0`,即可.

创建一个简单的实例.新建`Win32控制台应用程序`项目`06_Boost_Math`.在`解决方案资源管理器`中右击`06_Boost_Math`,选择`属性`,`配置属性`下的`VC++目录`,添加`E:\Program Files\boost_1_55_0`到`包含目录`项,添加`E:\Program Files\boost_1_55_0\lib64-msvc-12.0`到`库目录`项.

<a 
  href="http://tietuku.com/a2d73a0039b61c93" target="_blank">
  <img src="http://i1.tietuku.com/a2d73a0039b61c93.png" width="90%" height="90%"/>
</a>

选择`链接器`下的`常规`,添加`E:\Program Files\boost_1_55_0\lib64-msvc-12.0`到`附加库目录`项.

<a 
  href="http://tietuku.com/ff5b4432e2e567ea" target="_blank">
  <img src="http://i1.tietuku.com/ff5b4432e2e567ea.png" width="90%" height="90%"/>
</a>

在`06_Boost_Math.cpp`中输入代码,

<pre>

#include "stdafx.h"
#include <iostream>
#include <boost/math/distributions/normal.hpp>

using namespace std;

int main()
{
  boost::math::normal s;
	cout << s.mean() << endl;   
	cout << s.standard_deviation() << endl;   
	cout << setprecision(10) << boost::math::pdf(s, 1.0) << endl;   
	cout << quantile(s, 0.95) << endl;
	return 0;
}

</pre>


选择`调试`菜单栏下`开始执行(不调试)`,输出如下.


<a 
  href="http://tietuku.com/980651cbc3569b96" target="_blank">
  <img src="http://i1.tietuku.com/980651cbc3569b96.png" width="90%" height="90%"/>
</a>
