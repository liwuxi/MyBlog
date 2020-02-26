---
title: 配置Wordpress使网站强制HTTPS访问
tags:
  - HTTPS
  - WordPress
categories:
  - 技术栈
date: 2016-01-26 10:37:41
thumbnail: https://img.perdel.cn/thumbnail/wordpress-https.png

---
HTTPS协议越来越普及，Google、百度等搜索引擎也大大地对HTTPS增加友好度各大网站也开启了全站SSL，比如淘宝、百度等，也意味着互联网HTTPS时代的到来。

为了跟上互联网时代的热潮，大家跟我一起来简单的配置即可开启全站HTTPS强制访问！

<!--more-->

* * *

1.将配置好的SSL证书添加到服务器/面板，并手动输入：https://你的网站/

2.进入WP后台，进入设置-常规 将WordPress地址（URL）、站点地址（URL）两项修改为：https

3.修改config.php文件，在末尾添加代码

```php
/* 强制后台和登录使用 SSL */
define('FORCE_SSL_LOGIN', true);
define('FORCE_SSL_ADMIN', true);
```
修改完成后你会发现打开网站后，进入文章、后台，已经自动帮你跳转到https了

4.既然修改了网址，那最基本的图片也要让它变成https！

在function.php文件末尾处添加代码：
```php
/* 替换图片链接为 https */
function my_content_manipulator($content){
    if( is_ssl() ){
        $content = str_replace('http://cehu.top/wp-content/uploads', 'https://cehu.top/wp-content/uploads', $content);
    }
    return $content;
}
add_filter('the_content', 'my_content_manipulator');
`
```

将代码上的cehu.top修改为你的域名

5.配置.htaccess文件，使网站301重定向到HTTPS (注意！这个操作会使网站无法正常访问http)

在你博客空间的www目录（有的可能是 public_html）下，找到.htaccess文件，编辑它，在里边填入下列代码：
```
#网站定制化开启 HTTPS 的301重定向
&lt;IfModule mod_rewrite.c&gt;
RewriteEngine On
RewriteCond %{HTTPS} !^on$ [NC]
RewriteRule (.*) https://%{SERVER_NAME}%{REQUEST_URI} [L,R=301]
RewriteBase /
RewriteRule ^index\.php$ - [L]
RewriteCond %{REQUEST_FILENAME} !-f
RewriteCond %{REQUEST_FILENAME} !-d
RewriteRule . /index.php [L]
&lt;/IfModule&gt;
```
ls -a 即可看到.htaccess文件

一切皆以完成！