title: "jquery 插件tablepnp拖动刷新gridview问题"
date: 2015-04-23 18:25:28
categories: 技术
tags: [asp.net, js, jquery]
---

今天调查了一个gridview的行刷新的问题。

使用了ajax进行行的移动操作，当然使用的是jquery的tablepnp插件，还有一个功能就是层级折叠问题，这个使用的viewstate保存的，于是出现了一个这么的问题：
当gridview的行移动之后，然后点击与先前位置改变的带层级的行时，层级关联的几行确实被折叠了，但是，行有恢复了没有移动时的索引位置。

经过半天的调查，在移动行时，发现ajax在请求页面的时候，页面保存的viewstate是没有值的，间接证明了ajax是请求一个完全的新页面，而后进行折叠或者展开，读取页面是可以读到之前的viewstate的，但是读取的行的索引（一个按钮的commandargument参数）是之前在刚一进页面的索引，所以ajax请求的页面和本页的状态都是没有关系的，且在行移动后，页面没有刷新绑定。

结论：
ajax发送的请求页面和本页面刷新的页面状态是隔离的。

找到问题，就好解决了，在ajax请求完成后，使用window.top.location.href=window.location.href从新请求一次页面就可以绑定新的索引值了。这个时候viewstate已经读取不到了，所以需要借用其它的方法。
例如session。
