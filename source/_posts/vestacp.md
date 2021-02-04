---
title: 极致好用！一款开源的VestaCP面板
tags:
  - Linux
  - VPS
  - 面板
categories:
  - 测评
date: 2016-01-16 16:33:44
thumbnail: https://cdn.blog.hopenet.tech/thumbnail/vests.png
---

VestaCP是由俄罗斯的人编写的VPS主机控制面板，支持中文，Vestacp功能强大，基本上已经和Cpanel看齐。支持Apache、Nginx、Bind、Exim、Dovecot、vsftpd、MySQL等，提供可视化的网站管理面板，非常适合新手用户使用。

<!--more-->

* 什么是VestaCP

VestaCP是linux下的一款免费开源主机管理面板！环境核心包括Apache、Nginx、MySQL等

* VestaCP可做什么？

一键式搭建WEB运行环境，WEB交互方式在线管理，整合WHMCS做主机销售等等等等···

* WEB交互面板好吗？

一键式创建虚拟主机，控制流量，控制主机文件使用容量，图表式资源使用查看等等

* VestaCP本地化吗？

在2014年的时候，VestaCP已经进驻中国，并有了中文简体语言支持！

> **注意事项：**
到目前为止VestaCP现在支持的操作系统为:

1. RHEL 5, RHEL 6

2. CentOS 5, CentOS 6,CentOS 7

3. Debian 7

4. Ubuntu 12.04, Ubuntu 12.10, Ubuntu 13.04, Ubuntu 13.10, Ubuntu 14.04

## VestaCP安装方式/Install ##

如您服务器非纯净版的系统，或安装过Apache等组件，请卸载，并使用下面的命令来安装：

    bash vst-install.sh -f

安装成功后，请使用SSL方式（Https）访问后台地址：https://localhost:8083

### 开始安装 ###

    curl -O http://vestacp.com/pub/vst-install.sh 
    bash vst-install.sh 
    `</pre>
    注：如果不能跟官方的安装方式一样直接进入安装，那么我们只需复制上面的脚本
    <pre>`bash vst-install-rhel.sh --force

进入后按y开始安装，并输入自己的邮箱

仅仅需要几分钟安装就完成了 （安装速度与VPS的性能和带宽有关）

![开始安装](https://cdn.blog.hopenet.tech/article/vestacp/1.png)

安装完成界面，可以复制下密码，忘记了也没关系，他可以通过你前面输入的邮箱进行找回！

![操作界面](https://cdn.blog.hopenet.tech/article/vestacp/2.png)

友善的图形界面

不懂英文？没关系，点击进入admin

在Language选项选择CN保存即可

![语言设置](https://cdn.blog.hopenet.tech/article/vestacp/3.png)

安装完成！是否还沉浸在安装的愉悦中？这一切都已完成！~

VestaCP唯一的缺点：没有文件管理系统，FTP传文件比较麻烦。