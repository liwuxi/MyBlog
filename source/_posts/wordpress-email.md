---
title: Mail函数禁用下添加WordPress评论回复邮件通知
tags:
  - WordPress
  - Mail
categories:
  - 技术栈
date: 2016-08-03 15:38:19
thumbnail: https://cdn.blog.hopenet.tech/thumbnail/smtp-email.png
---

本次教程利用插件在虚拟主机 Or VPS 在 Mail 函数被禁用的情况下，添加WordPress评论回复邮件通知功能，更好的对用户进行交流。

<!--more-->

自己折腾了好久，一直Google不出一个心目中完美的解决方案

只能借助插件，[WP-Mail-SMTP](https://wordpress.org/plugins/wp-mail-smtp/) ，插件作者：[Callum Macdonald](http://www.callum-macdonald.com/)

附上一个我的设置方法吧

WP后台 - 设置 - Email

![smtp](https://cdn.blog.hopenet.tech/article/wordpress-email/smtp.png)

不同的邮箱有不同的设置方法，具体仅需要修改：host、port、encryption 这三项内容

设置好后可以在Send a Test Email下输入自己的邮箱，进行测试，是否配置成功。

好了，SMTP设置好后就可以进入正题：添加WordPress评论回复邮件通知功能

仅仅需要做的只是拷贝代码到 functions.php

样式一：

    /* comment_mail_notify v1.0 by willin kan. (所有回复都发送邮件) */
    function comment_mail_notify($comment_id) {
      $comment = get_comment($comment_id);
      $parent_id = $comment->comment_parent ? $comment->comment_parent : '';
      $spam_confirmed = $comment->comment_approved;
      if (($parent_id != '') && ($spam_confirmed != 'spam')) {
        $wp_email = 'e-mail@' . preg_replace('#^www\.#', '', strtolower($_SERVER['SERVER_NAME'])); //e-mail发出点, no-reply可改为可用的e-mail.
        $to = trim(get_comment($parent_id)->comment_author_email);
        $subject = '您在[' . get_option("blogname") . ']的留言有了回应';
        $message = '
        <div style="background-color:#eef2fa; border:1px solid #d8e3e8; color:#111; padding:0 15px; -moz-border-radius:5px; -webkit-border-radius:5px; -khtml- border-radius:5px; border-radius:5px;">

    Hi！' . trim(get_comment($parent_id)->comment_author) . '

    您曾在 ' . get_option("blogname") . ' - 《' . get_the_title($comment->comment_post_ID) . '》的留言:
    '
           . trim(get_comment($parent_id)->comment_content) . '

    ' . trim($comment->comment_author) . '给您的回应:
    '
           . trim($comment->comment_content) . '

    您可以点击[ 'comment'))) . '">直接回复Ta！]()

    (此邮件由系统自动发出, 请勿直接回复。)

        </div>';
        $from = "From: \"" . get_option('blogname') . "\" <$wp_email>";
        $headers = "$from\nContent-Type: text/html; charset=" . get_option('blog_charset') . "\n";
        wp_mail( $to, $subject, $message, $headers );
        //echo 'mail to ', $to, '
     ' , $subject, $message; // for testing
      }
    }
    add_action('comment_post', 'comment_mail_notify');

样式二：

    //评论回复邮件
    function comment_mail_notify($comment_id) {
    $comment = get_comment($comment_id);
    $parent_id = $comment->comment_parent ? $comment->comment_parent : '';
    $spam_confirmed = $comment->comment_approved;
    if (($parent_id != '') && ($spam_confirmed != 'spam')) {
    $wp_email = 'no-reply@' . preg_replace('#^www\.#', '', strtolower($_SERVER['admin@perdel.cn']));//发件人e-mail地址
    $to = trim(get_comment($parent_id)->comment_author_email);
    $subject = '您在 [' . get_option("blogname") . '] 的留言有了回应';
    $message = '<div style="border-right:#666666 1px solid;border-radius:8px;color:#111;font-size:12px;width:702px;border-bottom:#666666 1px solid;font-family:微软雅黑,arial;margin:10px auto 0px;border-top:#666666 1px solid;border-left:#666666 1px solid"><div class="adM">
    </div><div style="width:100%;background:#666666;min-height:60px;color:white;border-radius:6px 6px 0 0"><span style="line-height:60px;min-height:60px;margin-left:30px;font-size:12px">您在[' . get_option('blogname') . ']() 上的留言有回复啦！</span> </div>
    <div style="margin:0px auto;width:90%">

    ' . trim(get_comment($parent_id)->comment_author) . ', 您好!

    您于' . trim(get_comment($parent_id)->comment_date) . ' 在文章《' . get_the_title($comment->comment_post_ID) . '》上发表评论: 

    ' . nl2br(get_comment($parent_id)->comment_content) . '

    ' . trim($comment->comment_author) . ' 于' . trim($comment->comment_date) . ' 给您的回复如下: 

    ' . nl2br($comment->comment_content) . '

    您可以点击 [查看回复的完整內容]()

    感谢你对 [' . get_option('blogname') . ']() 的关注，如您有任何疑问，欢迎在博客留言，我会一一解答

    (此邮件由系统自动发出，请勿回复。)
    </div></div>';
    $from = "From: \"" . get_option('blogname') . "\" <$wp_email>";
    $headers = "$from\nContent-Type: text/html; charset=" . get_option('blog_charset') . "\n";
    wp_mail( $to, $subject, $message, $headers );
    //echo 'mail to ', $to, '
     ' , $subject, $message; // for testing
    }
    }
    add_action('comment_post', 'comment_mail_notify');


如果没用的话不用着急，这是因为WP-MAIL-SMTP插件的问题

插件默认的情况下非管理员邮件是不会进行发信的

那么只需要在后台找到以下代码进行注释即可

    // If the from email is not the default, return it unchanged
    if ( $orig != $default_from ) {
    	return $orig;
  	}

之后你可以在文章下进行测试，如果成功你可以收到这么一封邮件！

![email](https://cdn.blog.hopenet.tech/article/wordpress-email/email.png)

大功告成！ ;-) 