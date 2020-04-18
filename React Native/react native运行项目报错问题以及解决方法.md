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

