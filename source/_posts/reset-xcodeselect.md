---
title: 解决Xcode导致 node-gyp 安装失败的问题
date: 2020-2-01 16:28:01
tags:
- Xcode
- Node
categories:
- 小技巧
thumbnail: 
---
在 Catalina 版本中，可能会因为 Xcode 的问题导致 NPM 安装依赖时无法安装 `node-gyp`

<!-- more -->

# 问题

大致报错信息如下

```
No receipt for 'com.apple.pkg.CLTools_Executables' found at '/'.

No receipt for 'com.apple.pkg.DeveloperToolsCLILeo' found at '/'.

No receipt for 'com.apple.pkg.DeveloperToolsCLI' found at '/'.

```

# 解决方法

如遇到该问题，可能是 `xcode-select` 未安装导致的，你可以先运行

```
xcode-select --install
```

如果提示

```
Andy@Mac ~ % xcode-select --install
xcode-select: error: command line tools are already installed, use "Software Update" to install updates
```

那么说明已经安装过了，你需要删除 `xcode-select` 后重新安装

```
// 查看路径
sudo xcode-select -print-path

// 删除 xcode-select
sudo rm -rf $(xcode-select -print-path)

// 重新安装
xcode-select --install

// 同意使用条款
sudo xcodebuild -license accept
```

现在，你可以尝试重新安装 `node-grp` 了！

> 参考链接：[github.com/nodejs/node-gyp](https://github.com/nodejs/node-gyp/blob/master/macOS_Catalina.md)