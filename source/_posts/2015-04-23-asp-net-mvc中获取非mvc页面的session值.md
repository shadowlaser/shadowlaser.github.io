title: "asp.net mvc中获取非mvc页面的session值"
date: 2015-04-23 18:22:39
categories: 技术
tags: asp.net
---

项目中部分功能由mvc机制做的还有一部分纯aspx页面做的代码。

想在mvc的controller中直接获取session值后，发现完全没有值，然后经过debug发现aspx页面中session中已经赋值了，那么猜测mvc和传统的非mvc 页面使用的是不同的session机制。

经过跟踪查看，发现传统的非mvc使用的session是System.Web.HttpContext.Current.Session
而mvc使用的是((System.Web.Mvc.Controller)(this)).Session，至此问题已经明确了。

##总结：
    asp.net mvc使用了自己的一套Session系统。