---
layout: post
title: "安装QuantLib"
description: "安装QuantLib"
category: learn
tags: [Visual Studio, boost, QuantLib]
---

{% include JB/setup %}

[QuantLib](http://quantlib.org/index.shtml)是一个免费开源的C++量化金融库.

安装[QuantLib](http://quantlib.org/index.shtml)之前,首先需要[安装boost库](http://pophoo.github.io/learn/2014/07/02/Install-Boost/).
从[Source Forge](http://sourceforge.net/projects/quantlib/files/).
下载[QuantLib-1.4.zip](http://ncu.dl.sourceforge.net/project/quantlib/QuantLib/1.4/QuantLib-1.4.zip).解压到`E:\Program Files\QuantLib-1.4`.

打开`QuantLib_vc11.sln`,在`解决方案资源管理器`中右击`解决方案QuantLib_vc11.sln`,选择`配置属性`下的`配置`.点击`配置管理器`,设置`活动解决方案配置`为`Release (static runtime)`,设置`活动解决方案平台`为`x64`.

<a 
  href="http://tietuku.com/67aa70c7d8a9028c" target="_blank">
  <img src="http://i1.tietuku.com/67aa70c7d8a9028c.png" width="90%" height="90%"/>
</a>

设置全部15个项目如下,在`解决方案资源管理器`中右击项目名,选择`属性`,`配置属性`下的`VC++目录`,添加`E:\Program Files\boost_1_55_0`到`包含目录`项,添加`E:\Program Files\boost_1_55_0\lib64-msvc-12.0`到`库目录`项.

<a 
  href="http://tietuku.com/a2d73a0039b61c93" target="_blank">
  <img src="http://i1.tietuku.com/a2d73a0039b61c93.png" width="90%" height="90%"/>
</a>

选择`链接器`下的`常规`,添加`E:\Program Files\boost_1_55_0\lib64-msvc-12.0`到`附加库目录`项.

<a 
  href="http://tietuku.com/ff5b4432e2e567ea" target="_blank">
  <img src="http://i1.tietuku.com/ff5b4432e2e567ea.png" width="90%" height="90%"/>
</a>

在`解决方案资源管理器`中右击`解决方案QuantLib_vc11.sln`,选择`生成解决方案`.

生成成功后,`输出`窗口会有相应输出.

<pre>
<body> 
2>  Tests completed in 17 m 32 s
2>  
2>  
2>  Test suite "Master Test Suite" passed with:
2>    1001873 assertions out of 1001873 passed
2>    567 test cases out of 567 passed
2>  
========== 全部重新生成:  成功 15 个，失败 0 个，跳过 0 个 ==========
</body>
</pre>

创建一个简单的实例.新建`Win32控制台应用程序`项目`TestingQuantLib`.在`解决方案资源管理器`中右击`TestingQuantLib`,选择`属性`,`配置属性`下的`VC++目录`,添加`E:\Program Files\boost_1_55_0`和`E:\Program Files\QuantLib-1.4`到`包含目录`项,添加`E:\Program Files\boost_1_55_0\lib64-msvc-12.0`和`E:\Program Files\QuantLib-1.4\lib`到`库目录`项.

<a 
  href="http://tietuku.com/0fe128e7217dfff8" target="_blank">
  <img src="http://i1.tietuku.com/0fe128e7217dfff8.png" />
</a>

选择`链接器`下的`常规`,添加`E:\Program Files\boost_1_55_0\lib64-msvc-12.0`和`E:\Program Files\QuantLib-1.4\lib`到`附加库目录`项.

<a 
  href="http://tietuku.com/3d5fdf6db373ae71" target="_blank">
  <img src="http://i1.tietuku.com/3d5fdf6db373ae71.png" />
</a>

在`TestingQuantLib`中输入代码,

<pre>
#include "stdafx.h"
#include &lt;iostream&gt;
#include <ql/quantlib.hpp>

using namespace std;

int main()
{
  QuantLib::Calendar myCal = QuantLib::UnitedKingdom();
	QuantLib::Date newYearsEve(31, QuantLib::Dec, 2008);
	std::cout << "Name: " << myCal.name() << std::endl;
	std::cout << "New Year is Holiday: " << myCal.isHoliday(newYearsEve) << std::endl;
	std::cout << "New Year is Business Day: " << myCal.isBusinessDay(newYearsEve) << std::endl;

	std::cout << "--------------- Date Counter --------------------" << std::endl;

	QuantLib::Date date1(28, QuantLib::Dec, 2008);
	QuantLib::Date date2(04, QuantLib::Jan, 2009);

	std::cout << "First Date: " << date1 << std::endl;
	std::cout << "Second Date: " << date2 << std::endl;
	std::cout << "Business Days Betweeen: " << myCal.businessDaysBetween(date1, date2) << std::endl;
	std::cout << "End of Month 1. Date: " << myCal.endOfMonth(date1) << std::endl;
	std::cout << "End of Month 2. Date: " << myCal.endOfMonth(date2) << std::endl;

	double tmp;
	std::cin >> tmp;

	return 0;
}
</pre>


<p>选择`调试`菜单栏下`开始执行(不调试)`,输出如下.</p>


<a 
  href="http://tietuku.com/fd1ba1d57eb825bf" target="_blank">
  <img src="http://i1.tietuku.com/fd1ba1d57eb825bf.png" />
</a>
