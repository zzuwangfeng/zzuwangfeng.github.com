---
layout: post
title: "怎么把自己的文件部署到七牛云存储"
date: 2014-04-12 09:10:55 +0800
comments: true
categories: 七牛云存储
---
在部署之前你首先要[注册成为七牛用户](https://portal.qiniu.com/signup?code=3l94gjc9mqzwx)，然后[获取 access_key 和 secret_key](https://portal.qiniu.com/setting/key),新建一个七牛的仓库``（QiNiu_Repository）``,这个文件夹名字可以随便起，然后在里边见一个``public``文件夹和``qiniu.conf``文件。
``qiniu.conf``文件内容如下：

```
{
    "access_key": "Please apply your access key here",
    "secret_key": "Dont send your secret key to anyone",
    "bucket": "Bucket name on qiniu resource storage",
    "sync_dir": "public",
    "async_ops": "",
    "debug_level": 1
}
```
``access_key`` 和 ``secret_key`` 分别填入从七牛云后台得到的 AccessKey 和 SecretKey。
``bucket`` 是你要上传到七牛云存的空间名。

下载同步工具 ``qrsync``。

* Mac OS: [http://devtools.qiniudn.com/qiniu-devtools-darwin_amd64-current.zip](http://devtools.qiniudn.com/qiniu-devtools-darwin_amd64-current.zip)
* Linux 64bits: [http://devtools.qiniudn.com/qiniu-devtools-linux_amd64-current.zip](http://devtools.qiniudn.com/qiniu-devtools-linux_amd64-current.zip)
* Linux 32bits: [http://devtools.qiniudn.com/qiniu-devtools-linux_386-current.zip](http://devtools.qiniudn.com/qiniu-devtools-linux_386-current.zip)
* Windows 32bits: [http://devtools.qiniudn.com/qiniu-devtools-windows_386-current.zip](http://devtools.qiniudn.com/qiniu-devtools-windows_386-current.zip)
* Windows 64bits: [http://devtools.qiniudn.com/qiniu-devtools-windows_amd64-current.zip](http://devtools.qiniudn.com/qiniu-devtools-windows_amd64-current.zip)

解压后把二进制文件拷贝到 path 变量包含的目录中，例如 Mac 下我把他们拷贝到了 ``/usr/local/bin/`` 下，你也可以拷贝到 ``/usr/bin/`` 目录，只要确保你可以从命令行里访问到 ``qrsync``。
最后把你准备上传的文件都拷贝到``public``下,只要执行了下面的操作，你的public文件夹就会和你的七牛对应的空间同步.

然后执行：

	qrsync qiniu.conf
	
Windows 下你需要执行：

	qrsync.exe qiniu.conf
	
同步完成后，你的七牛对应的空间就看可以看到你的``public``文件夹对应的内容。