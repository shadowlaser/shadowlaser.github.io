title: "asp.net调用xps对象GetFixedDocumentSequence出现异常"
date: 2015-04-23 17:51:22
categories: 
tags: [asp.net]
---

昨天在web端调用别人写的word处理dll时，出现了如下错误:

`The invocation of the constructor on type 'System.Windows.Documents.DocumentReference' that matches the specified binding constraints threw an exception.' Line number '2' and line position '21'.`

于是写了一个cs端程序进行问题确认，测试程序可以正常执行，这块可以排除代码逻辑的问题，有可能是环境或者其它方面考虑不足。

同事指出可以查看详细的异常信息：在抛出异常的地方找到的innerexception是sta的问题，这个具体没有把信息保留下来.
根据innerexception的提示，发现了xps对象和其中的方法是STA的，但是aspx页面是MTA，经过几番周折找到遇到一样问题的人，链接如下:

[http://stackoverflow.com/questions/24058070/how-to-read-a-xps-file-in-c-sharp-using-asp-net](http://stackoverflow.com/questions/24058070/how-to-read-a-xps-file-in-c-sharp-using-asp-net)

问题真的是一样的，然后按照里面提供的链接(第二个)添加
```
<%@ Page Language="C#" AspCompat="true" %>
```
经过测试，上面的代码是没有用，由于.httphandler 自己还不熟，于是写了一个线程来调用出力xps文档的那个方法，于是成功搞定，代码示例如下:
 
```
//调用的地方
System.Threading.Thread thread = 
               new System.Threading.Thread(
               new System.Threading.ParameterizedThreadStart(ThreadMethod));
            thread.Start(value);
            thread.Join();//等待结束
//线程函数
 
private void ThreadMethod(object parameter)
{
    //这里写的就是对xps处理的代码
}
```
#总结:
    1. STA、MTA的概念需要熟悉，其它的线程，线程同步，线程池等概念需要再巩固一下了。