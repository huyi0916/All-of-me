# 配置github仓库

## 在xcold里面安装与配置git

1. 安装xcold---打开一直下一步

2. 检查git是否已安装（一般xcold自带）

终端输入：

```XML

    git

```

3. 检查本地是已有ssh key

      如果文件已经存在，那么你可以跳过步骤4，直接进入步骤5。

      终端输入：

```
        cd ~/.ssh       (进入这个ssh文件夹里面)
        ls             （查看里面有哪些文件）

```

4. 创建ssh key

      终端输入：

```xml
        ssh-keygen -t rsa -C"963132341@qq.com"

```

运行后,会让你输入一个用户名,这里使用默认,直接点击enter键,这样就会生成
`"id_rsa"`和`"id_rsa.pub."`接着输入两次密码,也可不输入(推荐输入该密码是你push文件的时候要输入的密码，而不是github管理者的密码.）

终端输入：

```
        vi ~/.ssh/id_rsa.pub        （打开这个文件）

```

运行后,将里面的代码全都拷贝下来,点击":q!"退出.(点击引号里的冒号:必须写)

5. 进入自己的github,点击自己的图像，然后点击`“settings（设置）”`，左边选择`“SSH and GPG keys（ssh和gpg密钥）”`
      点击`“new ssh key（新的ssh密钥）”`，“title”随便写，然后“key”里面就把刚才复制的粘贴上面去。点击`“add ssh key（添加ssh密钥）”`

6. 测试一下ssh key

终端输入：

```xml
        ssh -T git@github.com

```

运行后,将会得到一个警告代码:

```xml
    The authenticity of host'github.com (207.97.227.239)'can't be established.# RSA key
    fingerprintis16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
    # Are you sure you want tocontinueconnecting (yes/no)?

```

这时,只需输入yes,然后输入刚才设置的密码.密码输入正确后,

你将会看到如下内容:

```xml
      Hi username! You've successfully authenticated, but GitHub does not# provide shell access.

```

如果用户名是正确的,你已经成功设置SSH密钥。如果你看到 “access denied” ，者表示拒绝访问，那么你就需要使用 https 去访问，而不是 SSH 。

7. 进入github,点击你的仓库(没有就创建一个)，新仓库打开后上面会有一个https/ssh的地址，选择ssh然后复制这个地址。

```xml
   “git@github.com:huyi0916/new-git.git”
```

8. 现在就是把仓库克隆到本地，我们把它放到桌面上。

终端输入：

```xml
        ls              (先查看一下当前路径的文件夹)
        cd/Desktop      （我这里直接可以进入桌面）
        git clone git@github.com:huyi0916/new-git.git

```

然后桌面就出现了这个文件夹也就是你的仓库。

9. 在vs code中新创建一个工程，保存的路径为刚刚克隆下来的new-git文件夹下
      提交修改，首先切换到new-git文件路径,

      然后终端输入：

```xml
        echo "# new-git" >> README.md
        git init
        git add README.md
        git commit -m "first commit"
        git remote add origin git@github.com:huyi0916/new-git.git
        git push -u origin master

```

查看GitHub上的项目，new-git已经上传成功啦