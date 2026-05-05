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

namesilo页面改版以后，这个教程里面apply github是最简单的操作
[将自己的域名绑定在GitHub的个人网页库中（以namesilo为例） - 知乎](https://zhuanlan.zhihu.com/p/448781791)

因为我的域名没有发生变化，所以其他操作都不用执行。
但是github page check custom domain会遇到这个问题：

>Both iulia.moe and its alternate name are improperly configured Domain does not resolve to the GitHub Pages server. For more information, see documentation (NotServedByPagesError).

因为我是旧域名过期，所以可能出现的问题有：
-   **DNS 缓存还没刷新**  
    即使你改对了，全球 DNS 查询需要时间。你本地打开可能看到旧结果，GitHub 的检查服务器也可能暂未刷新。通常等 5～10 分钟再试，或清除本地 DNS 缓存（`ipconfig /flushdns`）。
-   **NameSilo 上的 DNS 记录根本还没设置正确**  
    新买的域名，默认可能会解析到 NameSilo 的停放页，而不是 GitHub。你需要保证在 NameSilo 里已经按前面说的，添加了那 4 条 A 记录，或者指向 `你的用户名.github.io` 的 CNAME。
	
我先等了一会，ping了一下，dns缓存刷新后，重新在github page 页面remove iulia.moe，重新输入iulia.moe save
又出现了一个新问题：
>www.iulia.moe is improperly configured Your site's DNS settings are using a custom subdomain, www.iulia.moe, that is set up as an A record. We recommend you change this to a CNAME record pointing to ywwlia.github.io. For more information, see documentation (InvalidARecordError).

求助d老师后：

这个新报错直接把问题点明了：你的 `www.iulia.moe` 目前在 NameSilo 上被设置成了 **A 记录**，但 GitHub 要求子域名必须用 **CNAME 记录** 指向 `ywwlia.github.io`。

解决起来很简单，只需要去 NameSilo 修改一下 `www` 的记录类型即可。

---

### 🛠️ 操作步骤

1.  **登录 NameSilo 并进入 DNS 管理**
    
    -   登录你的 NameSilo 账户，点击右上角 `My Account`。
        
    -   在 `Domain Manager` 列表中找到 `iulia.moe`，点击旁边的**蓝色小球图标**（`Manage DNS`）。
        
2.  **修改 `www` 的记录**
    
    -   在记录列表里，找到主机记录（Host）为 `www` 的那一条。
        
    -   如果它的类型（Type）是 **A**，请**删除**这一条。
        
    -   然后点击添加新记录，选择类型为 **CNAME**，主机记录填 `www`，记录值 (Value) 填：`ywwlia.github.io`（注意末尾不要有空格）。
        
    -   点击 `Submit` (提交) 保存。
        
3.  **确认根域名的 A 记录保持不变**
    
    -   确保主机记录为 `@` 或 `iulia.moe` 的那 4 条 A 记录仍然存在，分别指向 GitHub 的那四个 IP。

回到github page重新check custom domain，就成功了。

---
因为寒假给我的陈年老台式机重新安装了win11，准备更新blog的时候发现没有node.js和git，部署以后仍有问题，才意识到没部署npm和hexo。
hexo部署好以后generate有问题，主要是原有hexo使用的node v10.13.0，git v2.19.1，hexo旧框架和新版node有冲突。于是在d老师指导下一直在调整这个问题。
经历几次报错，终于修改好了node_module>hexo-front-matter>lib>front_matter.js里isDate的问题。
deploy的时候又出现了问题。
经过一番操作，最后还是卸载了最新版node改用node v10.13.0，又经过一番报错纠错，终于成功了。
一方面觉得太艰难了，一方面又觉得多亏有ai，只需要在ai指导下一步一步纠错，不需要自己人工检索省事很多。真的要好好学习使用ai了，不然马上要被社会淘汰了（抹泪
虽然我们行业对ai的反应还非常迟缓……还能苟一段时间……