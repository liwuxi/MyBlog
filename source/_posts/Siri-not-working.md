---
title: 解决 macOS 下 Siri 卡住不工作
tags:
- macOS
- MacBook Pro
- Siri
categories:
- 小技巧
thumbnail: https://cdn.blog.hopenet.tech/thumbnail/Siri.jpg
---

macOS 下 Siri 使用程度虽然不多，但也算 Touch Bar 为数不多的功能之一（虽然特别会误触），但总体来说还算方便。

但是在某些特定的情况下，例如 MacBook Pro 在连接 AirPods 后再取消，Siri 有概率会发生“聋”了的情况。并且开启 Siri 的动画会消失。

<!-- more  -->

![](https://cdn.blog.hopenet.tech/article/Siri-not-working.png)

过一会，它会显示连接有点问题，请检查您的麦克风balabala

出现这个情况后，你可以先到 ``设置 - 声音 - 输入 `` 选项卡内查看麦克风是否正常检查你的麦克风是否正常。如果异常，请检查是否为硬件损坏。

排除了麦克风的问题后，就可以默认为 Siri 的软件故障那么我们直接在终端运行

``` 
sudo kill -9 `ps ax|grep 'coreaudio[a-z]' | awk '{print $1}'`
```

Done.