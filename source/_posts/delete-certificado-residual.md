---
title: '[翻译] 删除iOS系统残余证书'
date: 2018-02-24 21:07:07
tags:
    - iOS
    - 证书
categories:
    - 小技巧
thumbnail: https://cdn.blog.hopenet.tech/thumbnail/delete-certificado.png
---

不知何时起，我的iPhone从iOS10开始就出现了一个叫 “WoSign CA Limited” 的垃圾证书。

依稀记得好像是因为小黄车使用的是 WoSign 的证书，那段时间 Apple 开始不信任，所以按照说明手动安装了证书。

后续卸载了 ofo 后并没有自动移除证书，就一直残留。 ~~fuck ofo~~

<!-- more  -->

这种情况强迫症不能忍😠，当然我们也不可能为此大费周章地重新安装系统。

### 开始

1. 使用 iTunes 或者 iMazing 将iPhone备份。（取消加密备份）
2. iMazing > 文件系统 > 备份 > KeychainDomain > 找到 TrustStore.sqlite3 > 拷贝到 ~/ 目录

![拷贝文件](https://cdn.blog.hopenet.tech/article/delete-certificado-residual/1.png)

3. 前往 [ADVTrustStore](https://github.com/ADVTOOLS/ADVTrustStore) 下载 ADVTrustStore 用于编辑iOS CA证书
4. 下载完成后，将 iosCertTrustManager.py 同样复制到 ~/
5. 由于 macOS 自带了 Python 所以可以直接在终端运行以下命令

``` ./iosCertTrustManager.py -t ~/TrustStore.sqlite3 -e ~/foo.crt ```

![运行命令](https://cdn.blog.hopenet.tech/article/delete-certificado-residual/2.png)

如图所示，你可以看到 ADVTrustStore 重新生成了 WoSign CA Limited, CN 证书

6. 如果你是Mac用户你可以直接试用 Airdrop ~~隔空投递~~ 选中生成的证书，发送到iPhone进行安装。（你也可以使用Email发送到你的手机）
7. 现在你可以到iPhone > 设置 > 通用 > 描述文件 中找到并删除它。

你可以惊奇地发现它在 证书信任设置 中消失了。
<br />

> 原文链接：[stackexchange.com](https://apple.stackexchange.com/questions/300203/how-can-i-delete-a-certificate-that-got-restored-from-a-backup-under-ios-10-11)