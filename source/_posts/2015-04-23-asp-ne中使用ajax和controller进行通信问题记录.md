title: "asp.ne中使用ajax和controller进行通信问题记录"
date: 2015-04-23 18:20:44
categories: 技术
tags: asp.net
---

为了页面显示和后端处理分离，使用了html+ajax+mvc的形式进行处理。

在这其中遇到的问题记录：

1. 在使用ajax向controller请求数据的时候，“get”方法会缓存上一次的请求，导致controller方法不能被debug跟踪到，开始以为是vs出错了，到后来才搞清楚。

`解决方法`：请求controller路径时加上随机数，或者使用“post”方法。
2. 在使用“POST”方法时，IE11要小心处理，因为ie会出现怎么都执行不了的情况包含兼容模式，而“get”方法没有任何问题。
3. 如果项目使用了form的验证方式，需要注意controller权限的问题。
    这里还需要controller 32bit和64bit中的maprequest的问题（暂时没有搞清楚）。

##总结：
    动态语言就是为了解决使用html麻烦的问题，本次项目算是一种返祖，不建议，可以使用   其它方式进行前后端分离。