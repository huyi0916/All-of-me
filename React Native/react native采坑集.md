# react native运行项目报错问题以及解决方法

## [!] CDN: trunk Repo update failed&[!] CDN: trunk URL couldn't be downloaded: - Dev


```js
[!] CDN: trunk Repo update failed&[!] CDN: trunk URL couldn't be downloaded: - Dev
```
![报错图片](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8zMDk1MTU2LTZlYmI5MDY2YWUyZDljYzMucG5n?x-oss-process=image/format,png)

* 通过 CocoaPods 执行 pod install 升级项目依赖库的时候，终端执行 install 命令后等待许久抛出了如下异常信息：

```js
[!] CDN: trunk Repo update failed - 40 error(s):
CDN: trunk URL couldn't be downloaded: [https://raw.githubusercontent.com/CocoaPods/Specs/master/Specs/7/2/d/GCDWebServer/1.2/GCDWebServer.podspec.json](https://raw.githubusercontent.com/CocoaPods/Specs/master/Specs/7/2/d/GCDWebServer/1.2/GCDWebServer.podspec.json), error: execution expired
```

## 解决办法

* 首先，与网络有关也可能与源有关，通过尝试切换网络后异常失败，便尝试切换源配置

```js
$ cd ~/.cocoapods/repos
$ pod repo remove master
$ git clone https://mirrors.tuna.tsinghua.edu.cn/git/CocoaPods/Specs.git master
```

![](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy8zMDk1MTU2LWIxNWE5OGVmZGIwZWMzOGEucG5n?x-oss-process=image/format,png)

其次，变更成功后进入项目工程并配置对应的 podFile 文件
此次尝试了三种 source 属性，具体如下：

```js
source 'https://mirrors.tuna.tsinghua.edu.cn/git/CocoaPods/Specs.git'
#source 'https://github.com/CocoaPods/Specs.git'
#source 'https://mirrors.tuna.tsinghua.edu.cn/git/CocoaPods/Specs.git'
```

再其次，配置好如上 source 后，执行如下命令清除当前的 trunk

```js

pod repo remove trunk

```

最后，再次尝试 pod install 即可

## ReactNative pod install卡在boost-for-react-native

![](https://img-blog.csdnimg.cn/20200228154327248.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h4bDUxNzExNjI3OQ==,size_16,color_FFFFFF,t_70)

在ios目录下pod install时，总是会卡在boost-for-react-native，因为国内用户拉GitHub的代码会卡住，一直失败

## 解决办法：

在ios目录下Podfile文件中，加入以下代码，再pod install就可以下载下来了。

```js
pod 'boost-for-react-native', :git => 'https://gitee.com/damon-s/boost-for-react-native.git’
```

![](https://img-blog.csdnimg.cn/20200228155005812.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L2h4bDUxNzExNjI3OQ==,size_16,color_FFFFFF,t_70)

## 小技巧

pod install & pod update & pod repo update 加速技巧

使用$ pod repo查看本地的master库

```js
$ pod repo

aliyun
- Type: git (master)
- URL:  https://github.com/aliyun/aliyun-specs.git
- Path: /Users/MountainX/.cocoapods/repos/aliyun

lunboPodWSpec
- Type: git (master)
- URL:  https://github.com/DevaLee/lunboPodWSpec.git
- Path: /Users/MountainX/.cocoapods/repos/lunboPodWSpec

Specs
- Type: git (master)
- URL:  https://github.com/CocoaPods/Specs.git
- Path: /Users/MountainX/.cocoapods/repos/Specs

3 repos

```

使用$ pod repo remove NAME来移除不要的master库

```js

$ pod repo remove master
$ pod repo add master https://gitcafe.com/akuandev/Specs.git //添加pod的repo源
$ pod repo update

```

加速方法：进入到repos目录下，通过git clone直接添加到master库，命令行如下：

```js
$ cd ~/.cocoapods/repos
$ pod repo remove master
$ git clone https://github.com/CocoaPods/Specs.git master
```

首先要把本地老的master分支给移除掉，然后使用git clone从github镜像源上clone一份且设置本地master库。这样本地的repo就是最新的了。

```js
$ git clone https://github.com/CocoaPods/Specs.git master

Cloning into 'master'...
remote: Counting objects: 2067512, done.
remote: Compressing objects: 100% (177/177), done.
remote: Total 2067512 (delta 78), reused 35 (delta 35), pack-reused 2067295
Receiving objects: 100% (2067512/2067512), 529.53 MiB | 95.00 KiB/s, done.
Resolving deltas: 100% (1164658/1164658), done.
Checking out files: 100% (230184/230184), done.
```

此时再进入到当前工程目录下，执行下面的命令行

```js
$ pod install --no-repo-update --verbose
$ pod update --no-repo-update --verbose
```

其中`--verbose`的作用就是打印出执行过程中详细的信息，`--no-repo-update`的作用就是禁止更新repo，这样就避免执行了`git fetch`，从而加快速度。

这样就解决了工程依赖的第三方库版本过低需要更新的问题。

但是我们在clone github镜像源的时候，发现速度还是比较慢的，这是因为国内访问github的速度不给力，这个时候可以考虑挂一个VPN或者使用国内一些网站提供的镜像源。

## 克隆项目时报错： error This module isn't specified in a package.json file.

## 问题原因以及解答：

一、如果刚开始运行，环境没配置，需要依赖的版本迭代一下即可

1. 先卸载：npm uninstall -g react-native-cli
2. npm install -g yarn react-native-cli
3. 升级react-native：npm install --save react-native@0.62.2

二、之前迭代过，重新克隆项目后报错。是因为自己把依赖环境删除了。‘package-lock.json’文件和‘node_modules’文件夹删除等于以来的环境也木有了。这时就像你没有版本迭代一样，需要重复一遍上面的步骤。
