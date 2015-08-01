---
layout: post
keywords: blog
description: blog
title: Android 客户端和服务端通过session交互
categories: api
tags: session、cookie
---

### 背景
好久没更新了博客了，看看前面的博客，感觉都好水啊！最近换了系统，用Ubuntu 。换一个系统换一个心情！今后尽量把博客写好点 ☻

* 1.什么时候使用session？

    - 一般情况下，我们需要访问某个页面可能需要先登陆，然后登陆之后所有的页面一般都需要用户登陆权限才可以访问
    - 在Android里提供了Apache的HttpClient来给我我们使用，其中就有设计到session cookie
       
* 2.session、cookie分别代表着什么？

    - Cookie和Session都为了用来保存状态信息，都是保存客户端状态的机制，它们都是为了解决HTTP无状态的问题而所做的努力。Session可以用Cookie来实现，也可以用URL回写的机制来实现。
    - Cookie将状态保存在客户端，Session将状态保存在服务器端
    
----

### 实现步骤

```  java
以java.net.HttpURLConnection发起请求为例：
获取Cookie： 
URL url = new URL(requrl);
 HttpURLConnection con= (HttpURLConnection) url.openConnection(); 
// 取得sessionid. 
String cookieval = con.getHeaderField("set-cookie"); 
String sessionid; 
if(cookieval != null) { 
sessionid = cookieval.substring(0, cookieval.indexOf(";")); 
}
//sessionid值格式：JSESSIONID=AD5F5C9EEB16C71EC3725DBF209F6178，是键值对，不是单指值
发送设置cookie： 
URL url = new URL(requrl);
HttpURLConnectioncon= (HttpURLConnection) url.openConnection(); 
if(sessionid != null) { 
con.setRequestProperty("cookie", sessionid); 
}
```

---

### 总结

>**写的不容易啊。。给你赞☻**