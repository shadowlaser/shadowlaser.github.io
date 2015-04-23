title: "C#查询数据库时问题: Min(1) must be less than or equal to max(-1) in Range object"
date: 2015-04-23 17:41:55
categories: 
tags: [asp.net, database, sql]
---

这个问题是由于自己的粗心引起,当时定位到代码了,但是完全没有头绪,知道自己在实现上找到了问题.
    下面就是出错的代码:
```
DataRow[] tmpdrlist = tmpdt.Select(string.Format("UserGroup = {0}" ,dr["UserGroup"].ToString()));
```
上面的代码没有任何语法问题,只有在运行的时候出现了问题,当时百思不得其解,最后从业务实现上找到了,数据库字段UserGroup是字符串,就是这个原因,修改之后代码如下:
```
DataRow[] tmpdrlist = tmpdt.Select(string.Format("UserGroup = '{0}'" ,dr["UserGroup"].ToString()));
```
就是这个单引号的问题,这种问题真是令人无语.

总结:
    1. 如果编译时不报错,但是运行时报错,那么一般就是业务实现不正确或者其它的特性,所以这个时候你需要做的是检查业务和逻辑实现,而不是语法错误.
    2. 怎么提高这种细节处理是一个比较重要的问题,这个有点浪费时间.