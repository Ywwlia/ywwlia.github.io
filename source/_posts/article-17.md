---
title: 更新Blog域名
comments: true
noindex: true
date: 2026-05-06 01:13:21
tags:
categories:
---
一次艰难的更新……
<!--more-->
突然想起来Blog域名过期了，之前也发生过类似情况，但是当时发现的比较及时，只需要续费就行。这次过期太久需要重新绑定域名到github。
按照惯例搜索namesilo教程，但是namesilo页面改版，对于小白来说老教程基本无法使用。遂一边检索，一边求助d老师，kimi提问一次就算力不足，差评！

## 域名更新
namesilo页面改版以后，这个教程里面apply github是最简单的操作
[将自己的域名绑定在GitHub的个人网页库中（以namesilo为例） - 知乎](https://zhuanlan.zhihu.com/p/448781791)

因为我的域名没有发生变化，所以其他操作都不用执行。
但是github page check custom domain会遇到这个问题：

>Both 新域名 and its alternate name are improperly configured Domain does not resolve to the GitHub Pages server. For more information, see documentation (NotServedByPagesError).

因为我是旧域名过期，所以可能出现的问题有：
-   **DNS 缓存还没刷新**  
    即使你改对了，全球 DNS 查询需要时间。你本地打开可能看到旧结果，GitHub 的检查服务器也可能暂未刷新。通常等 5～10 分钟再试，或清除本地 DNS 缓存（`ipconfig /flushdns`）。
-   **NameSilo 上的 DNS 记录根本还没设置正确**  
    新买的域名，默认可能会解析到 NameSilo 的停放页，而不是 GitHub。你需要保证在 NameSilo 里已经按前面说的，添加了那 4 条 A 记录，或者指向 `你的用户名.github.io` 的 CNAME。
	
我先等了一会，ping了一下，dns缓存刷新后，重新在github page 页面remove 旧域名，重新输入 新域名 save
又出现了一个新问题：
>www.新域名 is improperly configured Your site's DNS settings are using a custom subdomain, www.新域名, that is set up as an A record. We recommend you change this to a CNAME record pointing to 你的用户名.github.io. For more information, see documentation (InvalidARecordError).

求助d老师后：

这个新报错直接把问题点明了：你的 `www.新域名` 目前在 NameSilo 上被设置成了 **A 记录**，但 GitHub 要求子域名必须用 **CNAME 记录** 指向 `你的用户名.github.io`。

解决起来很简单，只需要去 NameSilo 修改一下 `www` 的记录类型即可。

### 🛠️ 操作步骤

1.  **登录 NameSilo 并进入 DNS 管理**
    
    -   登录你的 NameSilo 账户，点击右上角 `My Account`。
        
    -   在 `Domain Manager` 列表中找到 `新域名`，点击旁边的**蓝色小球图标**（`Manage DNS`）。
        
2.  **修改 `www` 的记录**
    
    -   在记录列表里，找到主机记录（Host）为 `www` 的那一条。
        
    -   如果它的类型（Type）是 **A**，请**删除**这一条。
        
    -   然后点击添加新记录，选择类型为 **CNAME**，主机记录填 `www`，记录值 (Value) 填：`你的用户名.github.io`（注意末尾不要有空格）。
        
    -   点击 `Submit` (提交) 保存。
        
3.  **确认根域名的 A 记录保持不变**
    
    -   确保主机记录为 `@` 或 `新域名` 的那 4 条 A 记录仍然存在，分别指向 GitHub 的那四个 IP。

回到github page重新check custom domain，就成功了。

---

## 老电脑重装win11系统后重新部署Hexo

因为寒假给我的陈年老台式机重新安装了win11，准备更新blog的时候发现没有node.js和git，部署以后仍有问题，才意识到没部署npm和hexo。
hexo部署好以后generate有问题，主要是原有hexo使用的node v10.13.0，git v2.19.1，hexo旧框架和新版node有冲突。于是在d老师指导下一直在调整这个问题。
经历几次报错，终于修改好了node_module>hexo-front-matter>lib>front_matter.js里isDate的问题。
deploy的时候又出现了问题。
经过一番操作，最后还是卸载了最新版node改用node v10.13.0，又经过一番报错纠错，终于成功了。
一方面觉得太艰难了，一方面又觉得多亏有ai，只需要在ai指导下一步一步纠错，不需要自己人工检索省事很多。真的要好好学习使用ai了，不然马上要被社会淘汰了（抹泪
虽然我们行业对ai的反应还非常迟缓……还能苟一段时间……

---

## 多台电脑更新Blog

### 🖥️ 第一部分：在当前电脑上备份源码到 GitHub
1️⃣ 为源码创建 Git 仓库并关联远程
打开 Git Bash，进入 Hexo 博客目录：

>bash
>
>cd D:\Hexo
>git init

2️⃣ 创建 .gitignore 文件（防止把不需要的文件传上去）
>bash
>
>echo "node_modules/" >> .gitignore
>echo "public/" >> .gitignore
>echo ".deploy_git/" >> .gitignore
>echo "db.json" >> .gitignore
这样只会把文章、主题、配置等核心文件传到 GitHub，不会上传生成的文件和依赖包。

3️⃣ 将源码推送到 GitHub
注意： 你的用户名.github.io 仓库的主分支已经被网站文件占用，所以不能用主分支。我们创建一个新分支 hexo 来存源码。

>bash
>
>git add .
>git commit -m "备份 Hexo 源码"
>git branch -M hexo
>git remote add origin https://github.com/你的用户名/你的用户名.github.io.git
>git push -u origin hexo
推送时会提示输入用户名和 个人访问令牌（和之前部署时一样）。




### 🖥️ 第二部分：多台新电脑部署Hexo

#### 🖥️ 每台新电脑的初始安装（每台都做一遍）

1.  **安装 Git** 和 **Node.js v10.13.0**（从 [https://nodejs.org/download/release/v10.13.0/node-v10.13.0-x64.msi](https://nodejs.org/download/release/v10.13.0/node-v10.13.0-x64.msi) 下载）
    
2.  **安装 Hexo 命令行工具**：
    
   > bash
   >
   >npm install \-g hexo-cli
    
3.  **克隆源码**（在 Git Bash 中）：
    
   > bash
   >  
   > git clone \-b hexo https://github.com/你的用户名/你的用户名.github.io.git Hexo
   > cd Hexo
   > npm install
    
4.  **配置 Git 用户信息**（每台电脑设置一次）：
    
   >bash
   >
   > git config \--global user.name "你的GitHub用户名"
   > git config \--global user.email "你的GitHub邮箱"
    

#### ✍️ 日常协作流程

假设你在 **电脑A** 写完文章，**电脑B** 想继续写，流程如下：

##### 在电脑A上写完并发布

>bash
>
>cd D:\\Hexo
>hexo new post "article-n"
>\# 编辑 source/\_posts/article-n.md
>hexo clean && hexo generate && hexo deploy   \# 更新线上网站
>git add .
>git commit \-m "更新文章 article-n"
>git push origin hexo                        \# 把源码同步到 GitHub

##### 换到电脑B时，先拉取最新源码

>bash
>
>cd D:\\Hexo
>git pull origin hexo                        \# 获取电脑A的最新文章
>npm install                                 \# 如果没新增插件一般不需要，但保险起见跑一下
>hexo generate                               \# 保证本地站点是最新状态（可选）

然后电脑B就可以接着写新文章，重复上面的发布与推送步骤。


#### ⚠️ 注意事项

1.  **不要同时编辑同一篇文章**  
    如果两台电脑同时修改了同一文件，`git push` 时会冲突。解决冲突较麻烦，最好是不同时操作。
    
2.  **始终先 `git pull`，再开始写文章**  
    避免在旧版本上修改，导致推送时冲突。
    
3.  **图片等资源**  
    放在 `source/images` 下，会随源码同步，无需额外处理。
    
4.  **Node 版本必须一致（v10.13.0）**  
    如果某台电脑不小心装了高版本 Node，又会出现之前的 `isDate`、`mode` 等错误。务必保持版本一致。
    
5.  **个人访问令牌**  
    每台电脑第一次 `git push` 时都需要输入 GitHub 用户名和令牌。建议设置凭据缓存，避免每次输入：
    
   >bash
   >
   > git config \--global credential.helper manager-core
    

#### ✅ 总结

-   每台电脑只需一次初始安装，之后就是**拉取→写作→推送源码→部署网站**的循环。
    
-   只要坚持“先 pull 再写”的纪律，两台电脑（甚至更多）都能无缝切换。

---

## 📋 回顾：你现在拥有的完整工作流

|操作|命令|作用|
|---|---|---|
|1.同步其他电脑文章|`git pull origin hexo`\获取其他电脑的最新文章|
|2. 写文章|`hexo new post "标题"`|创建新文章|
|3. 编辑|用编辑器修改 `source/_posts/xxx.md`|撰写内容|
|4. 部署网站|`hexo clean && hexo generate && hexo deploy`|更新线上博客 (`master` 分支)|
|5. 备份源码|`git add . && git commit -m "备注" && git push origin hexo`|同步文章源文件 (`hexo` 分支)||