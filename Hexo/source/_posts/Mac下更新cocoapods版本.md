---
title: Mac下更新cocoapods版本
---
### 一、删除旧版本

*备注：如果之前没安装过cocoapods则可以略过本步骤*

在Mac终端中执行以下命令。

1. 执行` rm -rf /usr/local/bin/pod` ，删除目录下已有的pod
2. 执行 `gem list | grep cocoapods  ` ，查看所有与cocoapods相关的已安装的组件

``` bash
cocoapods (1.0.1)
cocoapods-core (1.0.1)
cocoapods-deintegrate (1.0.0)
cocoapods-downloader (1.1.0)
cocoapods-plugins (1.0.0)
cocoapods-search (1.0.0)
cocoapods-stats (1.0.0)
cocoapods-trunk (1.0.0)
cocoapods-try (1.1.0)
```

3. 执行 `sudo gem uninstall cocoapods` ，卸载全部组件，出现以下提示，回复 `Y` 进行卸载操作

``` bash
Remove executables:
	pod, sandbox-pod

in addition to the gem? [Yn]
```

### 二、更新ruby

1. 官网下载最新版本ruby:[ruby官网](http://www.ruby-lang.org/en/downloads/)
2. 解压缩文件ruby-2.4.0，并cd进入文件夹里按顺序在终端执行以下操作
   - `./configure` 等待配置完成
   - `sudo make` 提示输入密码，回车，等待编译完成
   - `sudo make install` 等待安装完成
3. `ruby -v` 查看ruby 版本 ，出现如下信息

``` bash
ruby 2.4.0p0 (2016-12-24 revision 57164) [x86_64-darwin16]
```

### 三、升级更新Gem

依次执行以下内容：

1. 执行 `sudo gem update --system`
2. 执行 `sudo gem install rubygems-update`
3. 执行 `sudo update_rubygems`

### 四、CocoaPods的下载及安装

前面操作都顺利完成后，就可以进行CocoaPods的安装和更新

1、执行 `sudo gem install cocoapods`

2、会出现错误提示

```
ERROR:  While executing gem ... (Gem::Exception)

    Unable to require openssl, install OpenSSL and rebuild ruby (preferred) or use non-HTTPS sources
```

3、解决方法是：

检查你的ruby源 `gem source - l`

出现如下信息

```
* CURRENT SOURCES *

https://ruby.taobao.org/
```

4、删除原有ruby源： `gem sources --remove https://ruby.taobao.org/`

5、添加新的ruby源： `gem sources -a http://rubygems.org/ ` 看清楚地址里的 `http` 是没有 `s` 的

6、再次执行安装指令  `sudo gem install cocoapods`

等待一会，会出现如下提示，代表安装成功。

```
pods after 15 seconds

28 gems installed
```

### 五、CocoaPods的更新

在终端中输入： `pod search  'AFNetworking'`（注：不一定选择非得 'AFNetworking'，其他知名的第三方开源框架也可以） 会出现如下提示：

```
Setting up CocoaPods master repo

  $ /usr/bin/git clone https://github.com/CocoaPods/Specs.git master --progress

  Cloning into 'master'...
```

接着会出现一段安装进度，等到终端出现Setup completed字样就代表可以正式使用CocoaPods的功能了

```
remote: Counting objects: 1060736, done.        

  remote: Compressing objects: 100% (309/309), done.        

  remote: Total 1060736 (delta 105), reused 2 (delta 2), pack-reused 1060410        

  Receiving objects: 100% (1060736/1060736), 373.19 MiB | 77.00 KiB/s, done.

  Resolving deltas: 100% (492423/492423), done.

  Checking connectivity... done.

  Checking out files: 100% (134682/134682), done.

Setup completed
```

