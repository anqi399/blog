# Blog
URL：www.nishuilema.top

## 前言

从很久之前就打算了自己搭一个博客，终于闲下来（开始学习）做一个来记录自己学习历程和心得的博客  
通过各种Google最后选择通过GitHub和Hexo来实现（省钱省事），此篇仅为个人记录

## Git和Github的绑定 
  这个环节全网教程很多，跟科学上网一样属于基础的东西，当然我之前也是经历很多曲折才搞定，那些什么SSH，add，pull，合并冲突等等都花了不少时间，虽然我现在也只能照着做（狗头）  
虽然这些事情很花时间，但当你最后解决某个问题后，带来的成就感和喜悦感不亚于拿五杀的快乐  
tips：如果你觉得输入命令来更新本地和仓库不习惯（麻烦），可以先下一个GitHub Desktop，可以一键clone、pull和commit，省很多事，当然还是建议用传统的Git Bash

## 安装node.js和Hexo
### node.js
这个过程也比较耗时间，简单但是繁琐，因为之前在电脑里面搞过eclipse来跑java代码，然后还用过webstorm写js，所以node.js安装比较轻车熟路，就直接跳过了，按照教程把环境变量搞好就基本上没问题了  
### Hexo
首先新建一个仓库，命名为你的名字加github.io，如图
![image](https://github.com/anqi399/blog/blob/main/images/newrepository.png)  
然后开始安装Hexo，先找个盘新建文件夹命名为Blog，鼠标右键Git Bush Here，通过npm命令安装  
`npm install -g hexo-cli`  
完成后进行初始化  
`hexo init`  
然后静态部署  
`hexo g`  
最后就可以打开看看了  
`hexo s`  
![images](https://github.com/anqi399/blog/blob/main/images/hexo_s.jpg)  
根据提示，浏览器输入http://localhost:4000 然后就可以看到首页了，看完了记得Ctrl+C关闭  
接下来要将Hexo与你的github合起来，打开之前的Blog文件夹，里面有一个_config.yml 文件，用记事本打开，在末尾添加你的仓库地址，如下     
```
deploy:
  type: git  
  repository: https://github.com/anqi399/anqi399.github.io.git //你的仓库地址  
  branch: main
```
tips:  
①仓库地址在你的仓库页，点击Clone，然后就会显示HTTPS的地址  
②上面的barnch: main，网上大多数教材为branch: master 这里是因为现在github已经把默认主分支设为main了，所以改为main更好

然后再回到Blog文件下，打开GIt Bash，进行Git的插件部署  
`npm install hexo-deployer-git --save`  
再继续输入下面三条命令（搬砖），主要是清楚默认环境，然后给你初始化一个新的页面    
```
hexo clean   #清除缓存文件 db.json 和已生成的静态文件 public
hexo g       #生成网站静态文件到默认设置的 public 文件夹(hexo generate 的缩写)
hexo d       #自动生成网站静态文件，并部署到设定的仓库(hexo deploy 的缩写)
```
这个步骤完成后就可以打开你的浏览器，输入你的地址，例如我的：https://anqi399.github.io/，  注意这里和仓库地址有点不一样，不需要前面的地址了。  

到这一步，前期工程就已经完成了，后面剩下的就是域名和美化问题，如果你觉得github.io不够个性化（因为是github提供的网页），没有那种输入woshishuaige.com高端，那么就需要花点钱买个域名。

## 域名
### 花钱
阿里云、腾讯云等等都可以，刚开始找个大平台比较简单放心，我选择的是[万网](https://wanwang.aliyun.com/ "万网链接")-阿里云  
大概流程就是，登陆注册（这里可以直接支付宝扫码登陆，然后实名就可以直接解决了），然后选择你自己喜欢的域名，后缀就看你个人爱好一般.com和.cn比较贵，其他的便宜，我选择的.top首年才9块钱，试试水  
接着建一个个人信息模板，填填邮箱电话还有上传身份证之类的，搞完后等待认证通过就行，一般来说挺快的，我十几分钟就收到通过短信通知了。最后，付款就可以了。
### 解析  
打开你买域名的地方，找到域名的控制台，选择解析，这里以万网为例  
![imgage](https://github.com/anqi399/blog/blob/main/images/DNS.jpg)
添加两条解析记录，分别用于www和@  

www选CNAME（链接到另一个地方，因为要把你的域名链接到之前的github.io），然后线路默认，TTL十分钟  
@选择A（即的github.io的ip地址），ip地址又回到了那门水的不行的计算机网络，cmd一下打开你的终端，ping一下就可以看到了  
`ping anqi399.github.io   //自己的地址`  

![imgage](https://github.com/anqi399/blog/blob/main/images/ipaddress.jpg)  
### 绑定  
接下来就是将CNAME和你的gitHub仓库绑定在一起  
参考他人的经验，首先在桌面新建一个txt文件命名为，CNAME.txt，在里面输入你的网页地址  
`nishuilema.com   //自己的地址`  
文件里面就写个地址就行，不需要加www，这样访问的时候不用必须加www就可以进入，最后删除txt的后缀保存  
![imgage](https://github.com/anqi399/blog/blob/main/images/CNAME.jpg) 
再回到你Blog文件，进入resource，把刚刚那个文件剪切到此处  
最后，回到Blog主文件，右键Git Bash，把常规的三条命令来一遍  
```
hexo clean
hexo g
hexo d
```  
最最后，去你的仓库看看有没有CNAME这个文件，假如没有（我就遇到了这个问题），就去add file那里手动添加一个，然后把你的地址放进去就行了  
最最最后，去你的仓库，Settings，找到Pages，看你的网址有没有保存成功  
![imgage](https://github.com/anqi399/blog/blob/main/images/pages.jpg)  
如果save那里没有，试着手动尝试把地址输入进去，假如save按钮为灰色，之前的CNAME文件也没有自动上传，那么恭喜你，你将继续Google寻找解决办法  
最最最最后，浏览器输入地址验证是否能正常访问  
## 最后
这个Blog的建立过程，短则几小时，长则一两天，运气与细节并存  
总体上来说算是搭建完成了，接下来就是漫长的美化和内容填充（学习）了，在github上有很多好看的开源主题，也可自己设计  
本篇主要目的是做一个记录，关于Hexo的搭建网上有更好更详细的教程，共勉！

## 记录
最近在更换主题上出现了不少的问题，在这里记录一下，大多数问题都能在网上找到答案  
①在git clean g d 三件套时出现OpenSSL SSL_read: Connection was reset, errno 10054（还有类似这条的报错问题）    
解决方案：`git config --global http.sslVerify "false"`  
还是没有解决后，经过不懈的查找最后发现是因为挂了梯子的原因，关掉代理之后就没有问题了  
此处更新：  
出现OpenSSL SSL_connect: Connection was reset in connection to github-releases.githubusercontent.com:443问题  
解决方案：[链接](https://blog.csdn.net/qq_37555071/article/details/114260533?utm_medium=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.base&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-2%7Edefault%7EBlogCommendFromMachineLearnPai2%7Edefault-1.base)  
出现登陆问题例如Logon failed, use ctrl+c to cancel basic credential prompt.  
解决方案：[链接](https://blog.csdn.net/weixin_41010198/article/details/101040291)  
此处按照评论区也有更新git版本的解决方案  
`git update-git-for-windows`  
②更新博客后出现404  
去到博客的仓库——Settings——Pages，发现域名有红色警告，然后点击后面的rename就可以了  
如果不行的话，检查仓库名与_condig.yml中设置的是不是一致  
补充：缺少index.html文件也会出现404  
解决方案： 
`npm install hexo-generator-index --save`   

此处二次更新，短暂出现404后有可能是还没来得及反应，需要等待一会儿。另外，我发现每次更新后，page处的域名绑定会自动把域名后缀改成.com，而我自己就是用的.top，因此每次*hexo d*更新后都要去手动改回来，不然也会404！  
<br>
③更新博客后出现页面排版错乱问题  
主要是由标签和分类产生的错乱，在网上多次查找原因，发现大部分问题是由layout引起的，有的主题文件里会有标签页或者分类页的布局文件，一定要保证每一篇post前面的tags等的写法要一致，注意就算某一篇不用给他分类或者打标签，也要保持写法一致，可以空着但是不能不写！我的问题就出在有的post写了tags，但是有的post又没写，然后就会发生错乱
