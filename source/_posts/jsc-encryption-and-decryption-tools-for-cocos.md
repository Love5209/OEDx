---
title: 适用于 Cocos 的 JSC 加解密工具
date: 2018-09-14 17:01:35
tags: Cocos
categories: 客户端
author: "[张韩(khanzhang)](http://khanzhang.cn)"
---

### 脚本地址：[Github](https://github.com/SNGfamily/cocos-jsc-endecryptor)

### 简介

此脚本用于CocosCreator加密编译后 jsc 文件解密为 js 文件和 js 文件加密为 jsc 文件。

CocosCreator构建时，是否勾选Zip压缩选项决定了使用脚本的参数不同。在CocosCreator的构建面板下图的位置中，查看加密密钥和是否开启Zip压缩。
![](https://blog-pic-1251295613.cos.ap-guangzhou.myqcloud.com/1557824277.88SmartPic.png)

> 此脚本在 macOS High Sierra 10.13.6 系统，Python 2.7 下运行正常，其他环境未测试

### 使用说明

命令行使用：

1. 如果使用加密功能，第二个参数设置为 **encrypt**；如果使用解密功能，第二个参数设置为 **decrypt**。此参数为必选参数

2. 如需设置加密密钥，添加 --key 或 -k 参数，并跟上加密密钥字符串。如不设置，会在命令行中提示输入

3. 如需设置为非压缩方案，添加 --nozip 或 -n 参数，并设置为 true。如不设置，默认为压缩方案
    > 非压缩方案是指Cocos编译时没有勾选“Zip 压缩”选项

4. 找到CocosCreator编译出来的 .jsc 文件，一般在工程目录下 **build/jsb-default/src** 文件夹下。你可以在脚本运行时，根据提示输入文件的路径来指定对应文件。也可以添加 --path 或 -p 参数，设置为文件路径。如不设置，会在命令行中提示输入


5. 运行脚本即可
    - encrypt：解密后文件路径为 **decryptOutput/decrypt.js**
    - decrypt: 加密后文件路径为 **encryptOutput/projectChanged.jsc**

6. 举例：
    - ./edc.py encrypt --key yourkey --nozip true
    - ./edc.py decrypt --nozip true
    - ./edc.py decrypt

其他Python脚本中引用：

1. 下载edc.py文件放到你的脚本目录下，通过 **import edc** 进行导入
2. 直接调用 edc.decrypt(is_zip, key, jsc_path) 或 edc.encrypt(is_zip, key, js_path) 即可，可参考 edcExample.py 文件

> 如果是非交互式脚本，请务必在调用方法时传入有效的参数，并保证其正确性

### 参数说明

| 参数名 | 缩写 | 是否必须 | 默认值 |
| ----- | ----- | ---- | ----- |
| encrypt/decrypt | 无 | 是 | - |
| --key | -k | 否 | - |
| --nozip | -n | 否 | false |
| --path | -p | 否 | - |

### 参考文章

- [形同虚设的cocos默认加密](http://blog.shuax.com/archives/decryptcocos.html)
- [cocos2dx lua 反编译](https://bbs.pediy.com/thread-216800.htm)