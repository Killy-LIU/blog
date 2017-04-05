---
title: 博客搭建(1)--使用Github搭建个人博客
date: 2017-04-04 13:59:17
tags: 
    - 技术
    - Github
---


&ensp;ps：因为最近手误删了两次csdn博客，因而决定在个人博客上也备份一份/(ㄒoㄒ)/~~

## 基本准备

 - github账号：可以起一个有意义的名字哦
 &emsp;&ensp;链接地址： https://github.com
 - 域名购买：可以在腾讯云或者阿里云上购买一个域名（都有针对学生的优惠）
 &emsp;&ensp;腾讯云地址：https://www.qcloud.com/?fromSource=gwzcw.5677.5677.5677
 &emsp;&ensp;阿里云链接地址：https://www.aliyun.com/?utm_medium=text&utm_source=bdbrand&utm_campaign=bdbrand&utm_content=se_32492
  
<!-- more --> 
## 创建页面仓库

链接地址：https://github.com/new
填写相应的信息：仓库名，描述，public，可选初始化信息。
![填写基本信息：仓库，描述，初始化](/blogImg/20170404/bg1.jpg)
 
 
创建成功之后点击设置，可以看到具体的信息：
![确认仓库名：仓科名前缀应该和github账号名一样](/blogImg/20170404/bg2.jpg)


下拉并点击主题选择，可以根据自己的喜好设置*（注：这里选择的模板都是jekyll的，之后会调整到hexo）:
![github模板默认都是jekyll](/blogImg/20170404/bg3.jpg)


完成后点击设置可以看到网站链接，便可以访问自己的网站啦啦啦~
![这里可以看到自己照片部署的地址](/blogImg/20170404/bg4.jpg)


## 绑定域名

跳坑：之前的域名存在重复现象：killy-liu.github.io/killyliu.github.io，因此修改自己的repo名与自己的名字一样，这里都改为 killy-liu.github.io 则指向刚刚构建好的页面，地址变为https://killy-liu.github.io。

现在需要在根目录下创建一个CNAME的文件，里面写自己的地址，www.killyliu.com，之后访问内容即会重定向到自己这个地址。
![自定义网站的地址](/blogImg/20170404/bg5.jpg)


与此同时，需要进入云服务中设置域名解析。这里我用的是腾讯云服务。在记录管理中对添加域名记录，如下图所示。
![在购买的腾讯云中定义映射的域名](/blogImg/20170404/bg6.jpg)


在添加完成之后用控制台输入ping命令，查看是否通顺。
![用ping测试域名可用](/blogImg/20170404/bg7.jpg)


试着访问地址即可看到自己的第一个博客页面^_^：http://www.killyliu.com
![](/blogImg/20170404/bg8.jpg)


下一步操作为设置博客样式以及完善内容，并且在思考之后将个人链接由 http://www.killyliu.com 转为 http://blog.killyliu.com 很抱歉之前不能点击链接~~



