---
title: 博客搭建(2)--Mac下用Hexo搭建个人博客
date: 2017-04-04 15:54:30
tags: 
    - 技术
    - Hexo
---


 > 在此之前，有人推荐使用jekyll，有人推荐hexo，因而上网查找资料进行简单对比：
  - Jekyll基于Ruby， Hexo基于NodeJs。
  - 两者都支持Markdown。
  - Jekyll的主题相对而言没有Hexo的美观（个人见解）
  - 对于网上所说的Jekyll没有本地服务器，需要纠正一下，其实两者都可以实现本地预览功能，再发布到容器中同步。
 根据个人喜好进行选择，这里我选择了hexo。

<!-- more -->
## 准备工作
**1. 安装node.js**
 > 安装语句：brew install node

 ![brew install node](/blogImg/20170404/mh1.jpg)

**2. 已搭建git环境（或者github管理软件）**
>使用语句查看安装成功：
node -v
npm -v
git --version

 ![node -v; npm -v; git --version](/blogImg/20170404/mh2.jpg)


## 初始化Github环境
在上一篇博客中已经建好了网站，这里直接克隆到本地便于接下来的操作。
选定博客搭建路径后，将仓库克隆到本地：
> git clone https://github.com/Killy-LIU/killy-liu.github.io.git
> cd killy-liu.github.io/
> git init

![](/blogImg/20170404/mh3.jpg)

## 安装Hexo并搭建网站

 **1. 安装执行命令：**
 
   > sudo npm install -g hexo-cli

  ![sudo npm install -g hexo-cli](/blogImg/20170404/mh4.jpg)

 **2. 从控制台进入克隆的文件夹目录下，进行初始化hexo：**

 > hexo init

 ![hexo init](/blogImg/20170404/mh5.jpg)

 **3. 在初始化完成之后，执行本地服务化发现报错。因而重新进行安装配置。**

 > npm install

 文件夹目录结构
 > source：博客资源文件夹
source/_drafts：草稿文件夹
source/_posts：文章文件夹
themes：存放主题的文件夹
themes/landscape：默认的主题
_config.yml：全局配置文件

 **4. 进行本地服务测试。**

 > hexo server

 输入 http://localhost:4000/ 即可打开默认页面：
 ![http://localhost:4000/](/blogImg/20170404/mh6.jpg)

 跳坑： 这里曾经因为无法启动本地服务器，尝试过许多方法(如下)，均无法解决错误 Cannot find module './build/Release/DTraceProviderBindings'，以下是曾经尝试过的方式：
> npm install hexo --no-optional
> npm uninstall hexo + npm install hexo --no-optional
> npm uninstall hexo-cli -g + npm install hexo-cli -g

 最后查找资料得到的解决方案：
  1. 首先我们找到全局hexo的安装目录
  2. 找到文件dtrace-provider.js
  3. 注释如下内容:
 ```
 var builds = ['Release', 'default', 'Debug'];
for (var i in builds) {
    try {
        var binding = require('./build/' + builds[i] + '/DTraceProviderBindings');
        DTraceProvider = binding.DTraceProvider;
        break;
    } catch (e) {
        // if the platform looks like it _should_ have DTrace
        // available, log a failure to load the bindings.
        if (process.platform == 'darwin' ||
            process.platform == 'sunos' ||
            process.platform == 'freebsd') {
            console.error(e);
        }
    }
}
 ```

## 更换主题
现在网站上的主题是默认的，既然是打造属于自己的小窝，必然要考虑换一个更好看的样式了~~在经过仔细比对之后，选择了可以适配网页端和手机端的特色主题yilia，相信自己的审美哦^_^
列出排名前三的主题：
 > 1.https://github.com/iissnan/hexo-theme-next  3510个star。
2.https://github.com/litten/hexo-theme-yilia  1703个star。
3.https://github.com/TryGhost/Casper  679个star

具体操作步骤：

**1. 克隆项目到本地(任意一个不是在博客文件夹里的地址均可)：**
这里我用github克隆的，与控制台的命令语句效果相同：
  > git clone https://github.com/litten/hexo-theme-yilia.git themes/yilia

 ![克隆yilia主题](/blogImg/20170404/mh7.jpg)
 
 
 克隆结束后，将克隆文件夹名更改为 yilia，并放于之前所建目录下的/themes/下，与landscape并列。
 ![](/blogImg/20170404/mh8.jpg)
 
**2. 修改./_config.yml文件：**
> theme: yilia    //默认为landscape
>  

**3. 修改themes/yilia/_config.yml文件：**
 注：根据自己的实际情况做调整：动画效果、友情链接、博友回复等等。

**4. 查看效果**
更改主题之后可以使用命令 hexo server 打开本地服务，再次登录 http://localhost:4000/ 查看效果。
![http://localhost:4000/](/blogImg/20170404/mh9.jpg)


## Github部署
这里连着上一篇博客，将搭建好的网站通过修改配置，完成在github上的部署。

**1. Github设置**
修改./_config.yml文件： 
> 
deploy:
    type: git
    repository:  https://github.com/Killy-LIU/killy-liu.github.io.git
    branch: master
> 

 注：在hexo3.x版本下，type应填git，而非github；冒号后面都有一个英文的空格，不然会报错。

**2. 部署**
部署命令为：
> hexo clean (清理public文件夹，不需要经常用)
> hexo generate
> hexo deploy
> 

 但我的上一条命令 hexo deploy 报错，因而采用下面的命令：
 > npm install hexo-deployer-git--save
 > hexo deploy
 > 

跳坑1：理论上应该部署成功，可是点击网页出现404，发现网页没有对应到我设置的网站上。
 百度一下，需要将CNAME，LICENSE，README.md 放在source文件夹下，部署时才会一起传到github上。
 重新运行
 > hexo generate
> hexo deploy
> 
 
 部署成功^_^
 ![](/blogImg/20170404/mh10.jpg)
 ![](/blogImg/20170404/mh11.jpg)
 
跳坑2：好多博客中写先搭建hexo并选择主题，后部署与github。曾经试过用github将上一期得到的内容直接下载下来，将这里的内容拷贝到文件夹内，但启动时报错：[rejected]        master -> master (non-fast-forward)。原因是两个都是master，有冲突。


