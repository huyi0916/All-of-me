# 一、markdown语法

### 1.标题

```xml
    # 你好
    ## 你好
    ### 你好
    #### 你好
    ##### 你好
    ###### 你好
```

### 2.段落

* Markdown 段落没有特殊的格式，直接编写文字就好，段落的换行是使用两个以上空格加上回车。
* 当然也可以在段落后面使用一个空行来表示重新开始一个段落。

***

### 3.字体

```xml
       *斜体*
       _斜体_
      **粗体**
      __粗体__
    ***粗斜体***
    ___粗斜体___
```

### 4.分割线

* 在一行中用三个以上的星号、减号、底线来建立一个分隔线，行内不能有其他东西。你也可以在星号或是减号中间插入空格

```xml
       ***
      * * *
      *****
      - - -
    ----------
```

### 5.删除线

```xml
    ~~BAIDU.COM~~
```

### 6.下划线

```xml
    下划线可以通过 HTML 的 <u> 标签来实现
```

### 7.脚注

* 脚注是对文本的补充说明。
* Markdown 脚注的格式如下:

```xml
    [^要注明的文本]
```

### 8.markdown list(列表)

* Markdown 支持有序列表和无序列表。

* 无序列表使用星号(*)、加号(+)或是减号(-)作为列表标记

```xml
        * 第一项
        * 第二项
        * 第三项

        + 第一项
        + 第二项
        + 第三项

        - 第一项
        - 第二项
        - 第三项
```

* 有序列表使用数字并加上 . 号来表示

```xml
        1. 第一项
        2. 第二项
        3. 第三项
```

* 列表嵌套只需在子列表中的选项添加四个空格即可
        1. 第一项：
            - 第一项嵌套的第一个元素
            - 第一项嵌套的第二个元素
        2. 第二项：
            - 第二项嵌套的第一个元素
            - 第二项嵌套的第一个元素

### 9.Markdown 区块

* Markdown 区块引用是在段落开头使用 > 符号 ，然后后面紧跟一个 空格符号

```xml
        > 区块引用
        > mackdown教程
        > 学的不仅是技术更是梦想
```

* 另外区块是可以嵌套的，一个 > 符号是最外层，两个 > 符号是第一层嵌套，以此类推退

```xml
        > 最外层
        > > 第一层嵌套
        > > > 第二层嵌套
```

* 区块中使用列表

```xml
        > 区块中使用列表
        > 1. 第一项
        > 2. 第二项
        > + 第一项
        > + 第二项
        > + 第三项
```

* 如果要在列表项目内放进区块，那么就需要在 > 前添加四个空格的缩进。

```xml
        * 第一项
            > mackdown教程
            > 学的不仅是技术更是梦想
        * 第二项
```

### 10.Markdown 代码

* 如果是段落上的一个函数或片段的代码可以用反引号把它包起来（`）

```xml
        `printf()` 函数
```

* 代码区块使用 4 个空格或者一个制表符（Tab 键），你也可以用 ``` 包裹一段代码，并指定一种语言（也可以不指定）

```xml
        ```javascript
        $(document).ready(function () {
        alert('RUNOOB');
        });
        ```
```

### 11.Markdown 链接

* 链接使用方法如下：

```xml
        [链接名称](链接地址)
         或者
        <链接地址>
```

    2. 高级链接
        链接也可以用变量来代替，文档末尾附带变量地址：
        这个链接用 1 作为网址变量 [Google][1]
        这个链接用 runoob 作为网址变量 [Runoob][runoob]
        然后在文档的结尾为变量赋值（网址）
        [1]: http://www.google.com/
        [runoob]: http://www.runoob.com/

### 12.Markdown 图片
    1. Markdown 图片语法格式如下：
        ![alt 属性文本](图片地址)
        ![alt 属性文本](图片地址 "可选标题")
        开头一个感叹号 !
        接着一个方括号，里面放上图片的替代文字
        接着一个普通括号，里面放上图片的网址，最后还可以用引号包住并加上选择性的 'title' 属性的文字。

    2.当然，你也可以像网址那样对图片网址使用变量:
        这个链接用 1 作为网址变量 [RUNOOB][1].
        然后在文档的结尾位变量赋值（网址）
        [1]: http://static.runoob.com/images/runoob-logo.png

### 13.Markdown 表格
        1. Markdown 制作表格使用 | 来分隔不同的单元格，使用 - 来分隔表头和其他行。

           |  表头   | 表头  |
           |  ----  | ----  |
           | 单元格  | 单元格 |
           | 单元格  | 单元格 |

        2. 对齐方式，我们可以设置表格的对齐方式：
           -: 设置内容和标题栏居右对齐。
           :- 设置内容和标题栏居左对齐。
           :-: 设置内容和标题栏居中对齐。

           | 左对齐 | 右对齐 | 居中对齐 |
           | :-----| ----: | :----: |
           | 单元格 | 单元格 | 单元格 |
           | 单元格 | 单元格 | 单元格 |

### 14.Markdown 高级技巧
       1. 支持的 HTML 元素
          不在 Markdown 涵盖范围之内的标签，都可以直接在文档里面用 HTML 撰写。
          目前支持的 HTML 元素有：<kdb> <b> <i> <em> <sup> <sub> <br>等 ，如：
          使用 <kbd>Ctrl</kbd>+<kbd>Alt</kbd>+<kbd>Del</kbd> 重启电脑

       2. 转义
          Markdown 使用了很多特殊符号来表示特定的意义，如果需要显示特定的符号则需要使用转义字符，Markdown 使用反斜杠转义特殊字符：
                 **文本加粗**
             \*\* 正常显示星号 \*\*

       3. Markdown 支持以下这些符号前面加上反斜杠来帮助插入普通的符号：

             \   反斜线
             `   反引号
             *   星号
             _   下划线
             {}  花括号
             []  方括号
             ()  小括号
             #   井字号
             +   加号
             -   减号
             .   英文句点
             !   感叹号

# 二、配置github仓库，且可以上传代码

# 在xcold里面安装与配置git

1. 安装xcold---打开一直下一步

2. 检查git是否已安装（一般xcold自带）

      终端输入：
```
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

```
        ssh-keygen -t rsa -C"963132341@qq.com"

```

      运行后,会让你输入一个用户名,这里使用默认,直接点击enter键,这样就会生成"id_rsa"和"id_rsa.pub."
      接着输入两次密码,也可不输入(推荐输入该密码是你push文件的时候要输入的密码，而不是github管理者的密码.）

      终端输入：

```
        vi ~/.ssh/id_rsa.pub        （打开这个文件）

```

      运行后,将里面的代码全都拷贝下来,点击":q!"退出.(点击引号里的冒号:必须写)

5. 进入自己的github,点击自己的图像，然后点击“settings（设置）”，左边选择“SSH and GPG keys（ssh和gpg密钥）”
      点击“new ssh key（新的ssh密钥）”，“title”随便写，然后“key”里面就把刚才复制的粘贴上面去。点击“add ssh key（添加ssh密钥）”

6. 测试一下ssh key

      终端输入：
```
        ssh -T git@github.com

```
      运行后,将会得到一个警告代码:

```
    The authenticity of host'github.com (207.97.227.239)'can't be established.# RSA key
    fingerprintis16:27:ac:a5:76:28:2d:36:63:1b:56:4d:eb:df:a6:48.
    # Are you sure you want tocontinueconnecting (yes/no)?

```
      这时,只需输入yes,然后输入刚才设置的密码.密码输入正确后,

      你将会看到如下内容:
```
      Hi username! You've successfully authenticated, but GitHub does not# provide shell access.

```
      如果用户名是正确的,你已经成功设置SSH密钥。如果你看到 “access denied” ，者表示拒绝访问，那么你就需要使用 https 去访问，而不是 SSH 。

7. 进入github,点击你的仓库(没有就创建一个)，新仓库打开后上面会有一个https/ssh的地址，选择ssh然后复制这个地址。

```
   “git@github.com:huyi0916/new-git.git”
```

8. 现在就是把仓库克隆到本地，我们把它放到桌面上。

      终端输入：
```
        ls              (先查看一下当前路径的文件夹)
        cd/Desktop      （我这里直接可以进入桌面）
        git clone git@github.com:huyi0916/new-git.git

```

      然后桌面就出现了这个文件夹也就是你的仓库。

9. 在vs code中新创建一个工程，保存的路径为刚刚克隆下来的new-git文件夹下
      提交修改，首先切换到new-git文件路径,

      然后终端输入：

```
        echo "# new-git" >> README.md
        git init
        git add README.md
        git commit -m "first commit"
        git remote add origin git@github.com:huyi0916/new-git.git
        git push -u origin master

```

      查看GitHub上的项目，new-git已经上传成功啦