MacOS终端命令
================

在终端（Terminal）中使用命令执行一定的任务可以帮助我们减去很多繁琐的操作，提高我们的工作效率。命令行（command line），也称为`CLI`，我们中有很多人一看见黑窗口就很怕使用它，但其实只要你知道一些基本的命令和概念，就没什么好怕的了

我们与计算机进行交互主要用到的是 [Shell](https://zh.wikipedia.org/wiki/%E6%AE%BC%E5%B1%A4) 脚本语言，光使用 Shell 还不行，我们还需要有个 Shell 脚本解释器才可以正常的与计算机进行交互。MacOS 为我们内置了很多 Shell 脚本解释器，你可以打开终端执行一下`cat /etc/shells`命令查看系统都内置了那些解释器。MacOS 默认使用的是 [bash](https://zh.wikipedia.org/wiki/Bash) 登录式脚本解释器，也可以使用命令打印一下当前Shell的执行环境看看`echo $SHELL`

**系统环境及其工具**

- 系统版本：MacOS High Sierra 10.13.3+
- 系统终端：Terminal.app
- Shell脚本解释器：Bash3.2

在下列文章中将会使用字符串`empty`代替文件，`directory`代替目录，阅读时请注意

正在不断完善中，欢迎 Star！


目录
----
* [系统目录](#系统目录)
* [权限信息](#权限信息)
* [终端的基本命令操作](#终端的基本命令操作)
    - [基础操作](#基础操作)
        + [clear](#clear)
        + [man](#man)
        + [say](#say)
        + [!!](#above)
        + [type](#type)
        + [which](#which)
        + [alias](#alias)
        + [who](#who)
        + [whoami](#whoami)
        + [open](#open)
        + [history](#history)
    - [日期时间](#日期时间)
        + [cal](#cal)
        + [date](#date)
    - [文件相关操作](#文件相关操作)
        + [touch](#touch)
        + [cp](#cp)
        + [mv](#mv)
        + [rm](#rm)
        + [cat](#cat)
        + [more](#more)
        + [head](#head)
        + [tail](#tail)
        + [nl](#nl)
        + [wc](#wc)
    - [目录相关操作](#目录相关操作)
        + [mkdir](#mkdir)
        + [rmdir](#rmdir)
        + [ls](#ls)
        + [tree](#tree)
        + [cd](#cd)
        + [pwd](#pwd)
    - [磁盘管理](#磁盘管理)
        + [du](#du)
    - [进程相关操作](#进程相关操作)
        + [ps](#ps)
    - [安全相关操作](#安全相关操作)
        + [chmod](#chmod)
        + [chown](#chown)
        + [chgrp](#chgrp)
        + [passwd](#passwd)
    - [系统关机和重启](#系统关机和重启)
        + [caffeinate](#caffeinate)
        + [shutdown](#shutdown)
* [系统相关文件及其配置](#系统相关文件及其配置)
    - [获取root权限](#获取root权限)
    - [添加环境变量](#添加环境变量)
    - [随机生成MAC地址](#随机生成mac地址)
    - [开启Terminal自动补全功能](#开启terminal自动补全功能)
    - [使用Touch ID进行sudo身份验证](#使用touch-id进行sudo身份验证)
    - [更改系统语言](#更改系统语言)
    - [本地化目录](#本地化目录)
    - [修改终端电脑名称](#修改终端电脑名称)
    - [终端开启允许安装任何来源App](#终端开启允许安装任何来源app)
    - [显示或隐藏文件](#显示或隐藏文件)
    - [查看苹果所有的高清图标](#查看苹果所有的高清图标)
    - [显示文件的扩展名](#显示文件的扩展名)
    - [显示文件路径](#显示文件路径)
    - [hosts文件的位置](#hosts文件的位置)
    - [更改 Finder 每次打开时默认显示的目录](#更改-finder-每次打开时默认显示的目录)
    - [更改 Finder 默认窗口的显示风格](#更改-Finder-默认窗口的显示风格)
    - [不显示最近使用的项目](#不显示最近使用的项目)
    - [截图](#截图)
    - [禁止生成 DS_Store 文件](#禁止生成-ds_store-文件)
    - [bash相关的文件](#bash相关的文件)
    - [CFUserTextEncoding文件](#CFUserTextEncoding文件)
    - [容器中的其他卷宗](#容器中的其他卷宗)
    - [重置NVRAM或PRAM](#重置nvram或pram)
    - [重置SMC](#重置smc)
* [其它的系统故障及其常见疑问](#其它的系统故障及其常见疑问)
    - [强制退出程序](#强制退出程序)
    - [账户管理权限丢失](#账户管理权限丢失)
    - [重置被遗忘的管理员密码](#重置被遗忘的管理员密码)
    - [前往资源库](#前往资源库)
    - [输入苹果图标](#输入苹果图标)
    - [输入或查询偏僻字](#输入或查询偏僻字)
    - [调出 emoji 表情](#调出-emoji-表情)
    - [查看本地IP地址](#查看本地ip地址)
    - [查看目录或磁盘占用空间](#查看目录或磁盘占用空间)
    - [去掉副本图标上的箭头](#去掉副本图标上的箭头)
    - [快速建立 www 服务](#快速建立-www-服务)
    - [ssh 端口转发科学上网](#ssh-端口转发科学上网)
    - [终端下出现bogon的解决办法](#终端下出现bogon的解决办法)
    - [剪切文件或文件夹](#剪切文件或文件夹)
    - [安全清空垃圾桶](#安全清空垃圾桶)
    - [清理系统垃圾](#清理系统垃圾)

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

系统目录
----
由于 MacOS 系统最底层是建立在 [Unix][Unix] 基础上，而 Unix 的所有文件都挂在系统的根目录`/`下面，所以 MacOS 系统也是一样，它跟 Linux 系统的目录比较相似。以下列出 MacOS 系统目前还保留的 Unix 目录，以及 MacOS 独有的目录

```
# unix传统的系统目录

/home  用户的家目录(MacOS 的家目录是根目录下的 Users)
/tmp   临时文件存放目录，此目录实际为指向 /private/tmp 的链接
/usr   第三方程序安装目录，其中 /usr/lib 目录中存放了共享库「动态链接库」
/opt   可选应用软件包，常常以 /opt/软件名 的目录层级出现，例如：vagrant
/etc   系统范围内的配置文件
/bin   存放unix传统命令的位置「例如：ls、pwd」
/sbin  存放unix传统管理类命令的位置「例如：ifconfig、shutdown」
/dev   设备文件存放目录
/var   存放经常变化的文件，如日志文件，此目录实际为指向 /private/var 的链接
```

```
# MAC 特有的系统目录

/Users        存放用户的个人资料和配置，每个用户有自己的单独目录
/Applications 存放应用程序的
/Library      存放系统的数据文件、帮助文件、文档等等
/Network      存放网络节点的
/System       只包含一个名为Library的目录，这个子目录中存放了系统的绝大部分组件，如各种framework以及内核模块和字体文件等等
/Volumes      文件系统挂载点存放目录（意思就是你插入的硬盘等都会显示在此目录下）
/cores        内核转储文件存放目录，当一个进程崩溃时，如果系统允许则会产生转储文件
/private      里面的子目录存放了/tmp、/var、/etc等链接目录的目标目录
```

**例如**：我在 Macbook 上插了一个叫 empty 的移动硬盘，并且在电脑的桌面上显示了这个硬盘图标，那么它实际位置在哪呐？其实它在`/Volumes`目录下，你执行下`ls /Volumes/empty`看看是不是移动硬盘里面的内容

还有驱动所在位置`/Systme/Library/Extensions`

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 权限信息 

当你执行`ls -l`命令查看一个文件信息的时候，系统会为你列出如下格式的权限信息，共10个字符

```bash
-rwxr-xr-x　number　user　group　filesize　updatetime　filename
```

第一个字符表示的是文件的类型，后` 9 `个字符分` 3 `组，分别表示当前用户、当前用户所在组、其他用户对该文件的读/写/执行权限

* 第1个字符表示的含义：
    - `d`：代表的是目录
    - `-`：代表的是文件
    - `l`：代表的是链接文件
* 后9个字符，每个字符表示的含义：
    - `w`代表可写`write`，数字权重`2`
    - `r`代表可读`read`，数字权重`4`
    - `x`代表可执行`execute`，数字权重`1`
    - `-`代表无权限

**例如**：

```bash
-rwxr-xr-x　3　root　root  288  3  1 19:46 empty
```

* `-`：        这是一个文件
* `rwx`：      文件拥有者对它有读写可执行权限，意思就是你对它拥有所有权限，数字权重`7(4+2+1)`
* `r-x`：      所属组的成员对这个文件只有阅读和执行文件的权利，数字权重`5(4+0+1)`
* `r-x`：      其他用户也是对这个文件只有阅读和执行文件的权利，数字权重`5(4+0+1)`
* `3`：        链接数
* `root`：     当前用户
* `root`：     当前用户所属的组
* `288`：      文件的大小「单位是byte」
* `3 1 19:46`：最后修改的时间是3月1号19:46
* `empty`：    文件名称

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

**修改权限** <span id="chmod"></span>

如果其他用户想拥有对某个文件的修改权限怎么办？这时我们就需要到修改权限的命令了，命令格式：

```
chmod [<权限范围><权限操作><具体权限>] [文件或目录…]
```

* 权限范围
    - `u`：User， 文件或目录的拥有者
    - `g`：Group，文件或目录的所属组
    - `o`：Other，除了文件或目录拥有者或所属组之外，其他用户皆属于这个范围
    - `a`：All，  全部的用户，包含拥有者，所属群组以及其他用户
* 权限操作
    - `+`：增加权限 
    - `-`：取消权限 
    - `=`：设定唯一的权限
* 具体权限
    - `w`
    - `r`
    - `x`
    - `-`

**例如：**

```bash
# 首先我们先看下 empty 文件的权限信息
ls -l empty
-rw-r--r--  1 root  root  0  3  5 11:41 empty

# 使用 chmod 命令，给用户所属组添加对 empty 文件的可写权限
# 用户所属组使用`g`表示（group），添加权限使用`+`操作符，可写权限使用`w`表示（write 缩写）
# 即`g+w`，注意 g+w 中间是没有空格的
chmod g+w empty
ls -l empty
-rw-rw-r--  1 root  root  0  3  5 11:41 empty

# 使用数字类型直接修改权重
chmod 664 empty
# 664分别对应`-rw-rw-r--`10个字符里的三个组，每一个组用一个数字表示
# 例如用户的权限是`rw-`，即r(4)+w(2)+x(0) = 6
ls -l empty
-rw-rw-r--  1 root  root  0  3  5 11:41 empty
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

**修改文件所属组** <span id="chgrp"></span>

```bash
chgrp [-R(递归修改)] 群组名 文件或目录的名称

# 修改文件的所属组
chgrp wheel empty

# 修改目录里所有文件所属组
chgrp -R wheel directory
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

**修改文件拥有者** <span id="chown"></span>

```bash
chown [-R] 用户名:群组名 文件或目录的名称

# 修改文件的拥有者
chown qinlzhu empty

# 修改目录里所有文件的拥有者
chown -R qinlzhu directory

# 修改文件拥有者的同时也修改所属组
chown qinlzhu:wheel empty
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

终端的基本命令操作
---- 
### 基础操作

#### clear 

`clear`命令用于清除当前屏幕终端上的任何信息

```bash
clear
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### man 

`man`是“manual”的缩写，是一个帮助命令，通过`man`命令可以查看 Mac OS X系统中的命令帮助、配置文件帮助和编程帮助等信息

当执行`man cd`时，第一行会出现一个`(1)`，其中的数字代表命令的类型，常用的数字及其类型如下：

```
1   用户在 shell 环境中可以操作的命令或者可执行文件
5   配置文件
8   系统管理员可以使用的管理命令
```

```bash
# 查看 cd 命令帮助信息
man cd

# 除了使用 man 查看命令帮助信息外
# 还可以在命令后面加 --help 选项，也是可以查看该命令的帮助信息的
cd --help
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### alias

`alias`命令用来定义命令别名

```bash
# 定义一个列出目录树的命令
alias Tree="find . -print | sed -e 's;[^/]*/;|____;g;s;____|; |;g'"

# 删除定义的命令
unalias Tree

# 打印已经设置的命令别名
alias
# 或
alias -p
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### say

`say`命令是用来文本转换语音的，当然你也可以结合一些其他的命令玩，例如：执行某段程序后，使用`say`命令提示你

```bash
# 朗读文字
say hello

# 更改朗读的人物
# 可以使用“say -v ?”查看，都有哪些人物
say -v Diego

# 朗读一个文件
say -f "empty"

# 朗读的语音保存成一个音频文件
say -o new.mp3 -f "empty"
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### !! <span id="above"><span>

`!!`执行上一条命令

```bash
!!

# 执行命令历史列表里第二条命令
!2

# 执行命令历史列表里倒数第二条命令
!-2

# 打印命令历史列表里倒数第二条命令,不执行
!-2:p

# 执行含有ls字符串的最新命令
!?ls?
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### type

`type`命令用来判断某命令是不是 bash 内置命令，或是来自外部

```bash
# cd is a shell builtin
# 表示 cd 是 bash 内置命令
type cd

# ls is hashed (/bin/ls)
# 表示 ls 是外部命令，后面是程序路径
type ls

# sublime is aliased to `open -a /Applications/Sublime\ Text.app'
# 表示 sublime 是用 alias 自定义的命令别名，后面是定义内容
type sublime
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### which

`which`命令用来查看某个命令所在的位置

```bash
which ls
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### who

`who`命令用列出当前登陆的所有用户

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### whoami

`whoami`命令用显示当前正进行操作的用户名

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### open 

`open`命令用于打开文件、目录或执行程序。等同于图形界面下的重复“双击”动作

```bash
# 打开指定文件
# 需要书写文件所在位置的完整路径，并且某格式的文件用某格式文件默认的编辑器打开
open ~/Downloads/file.epub

# 加 -a 选项使用自行选择的程序打开此文件
open -a sublime\ text.app ~/Downloads/file.txt

# 加 -e 选项，强制使用TextEdit编辑器打开此文件
open -e ~/Downloads/file.txt

# 打开终端当前所在的根目录
open .

# 打开终端当前所在的根目录的上一级目录
open ..

# 打开用户根目录下一个叫 Downloads 的文件夹
open ~/Downloads/

# 使用默认浏览器打开指定网址
# 需要书写完整的 URL 地址，并且超文本传输安全协议 http 或 https 也不能省略
open https://github.com/

# 使用指定浏览器打开指定网址
# 应用程序名称如果空白的话，需要使用反斜杠转义一下
open -a Google\ Chrome https://github.com/
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### history 

`history`命令用于显示指定数目的命令，读取历史命令文件中的目录到历史命令缓冲区和将历史命令缓冲区中的目录写入命令文件

```bash
# 查看以前所有执行过的终端命令（前提是你没清理过）
history

# 查看最近执行过的 6 条命令
history 6

# 立即清空 history 里的历史命令记录
history -c
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 日期时间

#### cal 

显示日历

```bash
# 显示当月日历
cal

# 显示2014年9月份的日历
cal 9 2014
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### date

显示系统的当前日期和时间

```
date
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 文件相关操作

#### touch

`touch`命令用来创建或修改文件

```bash
# 创建空白文件
touch empty

# 加 -t 选项，修改文件的创建和修改时间
# 时间格式为：[[CC]YY]MMDDhhmm[.ss]
touch -t 20180324192900 empty

# 加 -mt 选项，修改文件的修改和访问时间
touch -mt 20160324192900 empty
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### cp 

`cp`命令是用来复制文件或目录

```bash
# 复制文件
cp empty

# 将文件复制到用户根目录下
cp empty ~

# 复制目录下所有以 js 结尾的文件到 Downloads/Js 目录下
# 如果 Downloads 目录下没有 Js 文件夹的话，将会自动创建一个
cp *.js ~/Downloads/Js

# 加 -r 选项，复制目录下所有的文件以及子目录
cp -r . ~/Downloads/Js

# 复制一个文件并且重新命名
cp empty newEmpty

# 复制一个文件并且重新命名，然后移动到指定位置
cp empty ~/Downloads/newEmpty
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>


#### mv 

`mv`命令是用改变文件名或所在目录的位置

```bash
# 改变文件或目录名称
mv empty newEmpty

# 移动文件或目录到指定位置
mv empty ~/Downloads/empty

# 先给文件或目录重新命名，然后再移动到指定位置
mv empty ~/Downloads/newEmpty
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### rm 

`rm`命令是用来删除文件和目录，对于链接文件，只是删除整个链接文件，而原有文件保持不变。使用 rm 命令需要格外小心。因为一旦删除了一个文件，就无法再恢复它

```bash
# 普通的删除文件
rm ~/Downloads/empty

# 把欲删除的文件的硬连接数据删除成0，删除该文件
rm -d ~/Downloads/empty

# 强制删除
rm -f ~/Downloads/empty

# 删除文件之前先逐一询问下你是否要删除该文件
rm -i ~/Downloads/empty

# 递归删除目录下所有的文件以及子目录
rm -r empty

# 命令执行完成后，显示都是删除了那些文件或目录
rm -v empty
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### cat 

`cat`命令用来显示文件的内容

```bash
# 终端显示文件内容
cat "empty"

# 终端显示文件内容时在每行前面加上行数
cat -n "empty"

# 和-n相似，只不过对于空白行不加行数
cat -b "empty"

# 遇到有连续两行以上的空白行，就代换为一行的空白行
cat -s "empty" 

# 把 A 和 B 文件合并成一个新的 C 文件
cat A B > C
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### more

`more`命令是一个基于vi编辑器文本过滤器，它以全屏幕的方式按页显示文本文件的内容，支持vi中的关键字定位操作

```bash
# 指定每屏显示的行数
# 当你按空格键时，每屏只会显示四行内容
more -4 "empty"

# 从20行处显示
more +20 "empty"

# 将多个空行压缩成一行显示
more -s "empty"
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### head

`head`命令从头部开始显示指定文件的内容

```bash
# 显示文件的头 10 行
head 10 "empty"

# 显示文件的头 10 个字符（注意：一个中文占两个字符）
head -c 10 "empty"
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### tail

`tail`命令从尾部开始显示指定文件的内容

```bash
# 显示文件最后的 10 行
tail 10 "empty"

# 显示文件最后的 10 个字符（注意：一个中文占两个字符）
tail -c 10 "empty"
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### nl 

`nl`命令用来指定文件的行号显示方式

```bash
# 给某个文件添加上行数在终端显示（空白行不会添加）
nl "empty"
# 或
nl -b t "empty"

# 不论是否为空行，也同样列出行号
nl -b a "empty"

# 不添加行号显示
nl -b n "empty"

# 行号左对齐
nl -n ln "empty"

# 行号右对齐（默认）
nl -n rn "empty"

# 行号右对齐（显示六位数的行号，不足六位的前面添加 0）
nl -n rz "empty"

# 指定行号最多显示的位数（默认为 6）
nl -w 5 "empty"

# 把行号添加到文件内并另存为一个文件
nl -b t "empty" > new.txt
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### wc

`wc`命令是用来统计文件的字符数、词数和行数

```bash
wc "empty"

# 只统计行数
wc -l "empty"

# 只统计字节数
wc -c "empty"

# 只统计字符数
wc -m "empty"

# 只统计字数
wc -w "empty"
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 目录相关操作

#### mkdir 

`mkdir`命令是用来创建文件目录

```bash
# 创建一个空白的目录
mkdir empty

# 创建一个有子目录的目录
# -p 选项是，如果要创建的目录的父级目录不存在的话，一并创建
mkdir -p ~/Downloads/New/empty

# 一次性创建多个目录
mkdir emptyA emptyA ~/Downloads/emptyC

# 一次性创建多个目录，并且某个要创建的目录拥有多个字目录
mkdir emptyA emptyB/{emptyB-A, emptyB-B, emptyB-C}
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### rmdir 

`rmdir`命令是用来删除空白文件目录

```bash
# 删除空白文件目录，如果目录下有东西是删除不了的
rmdir empty

# 加 -p 选项
# 如果删除了某个目录，父目录就变为空目录的话，就一块删除
rmdir ~/Downloads/empty

# 删除多个目录
rmdir emptyA emptyB
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### ls 

`ls`命令用来列出目标目录中所有的子目录和文件。注意参数的大小写

```bash
# 列出当前目录下非隐藏的文件和目录，等价于“ls -C（注意：大写）”
ls

# 列出目录下的所有文件，包括以“.”开头的隐含文件
ls -a
ls -all

# 与上面的“ls -a”命令几乎相同，只不过是此命令不显示“.（当前目录）”和“..（父级目录）”这两个
ls -A

# 列出当前目录下非隐藏的文件和目录，并用逗号“,”分割
ls -m

# 列出当前目录下所有的文件或目录详细信息
ls -l

# 列出指定文件的详细信息
ls -l empty

# 用文件或目录修改的时间进行排序
ls -t

# 递归显示文件，会把此根目录下的所有文件都显示出来
ls -R
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### tree 

`tree`命令以树状图列出文件目录结构，需要单独安装

```bash
# 使用 brew 安装 tree
brew install tree

# 显示指定层级的目录
tree -L 2

# 列出权限标示
tree -p
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### cd 

`cd`命令用来切换工作目录

```bash
# 进入用户根目录
cd
# 或
cd ~

# 进入系统根目录
cd /

# 回到上次所在目录
cd -

# 回到上一级目录
cd ..

# 进入到指定目录下，例如：.Trash「回收站」
cd ~/.Trash

# 前往其他卷
cd /Volumes/

# 利用bash 的 $_ 变量，创建一个目录并立即进入该目录
# $_ 代表前一个命令的最后一个参数的值，如果没有参数的话，就是命令本身的名字
mkdir directory && cd $_
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### pwd 

`pwd`命令以绝对路径的方式显示用户当前所在的工作目录位置

```bash
pwd
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 磁盘管理

#### du 

`du`命令显示每个文件和目录的磁盘使用空间

```bash
# 显示当前目录及其当前目录下所有子目录的大小(以byte为单位)
du 

# 显示指定文件及其目录的大小
du "empty"

# 显示多个文件及其目录的大小
du "empty" "emptyTwo"

# 只显示总和，只列出最后加总的值
du -s
# 或
du -s directory

# 以K，M，G为单位，提高信息的可读性
du -h "empty"
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 进程相关操作

#### ps

`ps`命令用来查看系统进程

```bash
# 查看当前用户下的所有进程
ps -A

# 查看所有进程（包含其他用户，相当于系统下的所有进程）
ps -e
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### kill

`kill`命令用来终结进程

```bash
# kill 9 强制终止进程
kill 9 40142
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 安全相关操作

#### passwd

`passwd`修改登录密码，命令输入完成后回车要求分别输入旧的登陆密码和新的登陆密码，都输入完成后，回车即可更改

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 系统关机和重启

#### caffeinate

`caffeinate`命令用来修改屏幕睡眠时间的

```bash
# 3600 是秒数，可以使 Mac 一小时不进入睡眠状态
caffeinate -t 3600

# 打开 terminal 时，直接输入 caffeinate 命令并回车后
# 当你最小化或隐藏它时，Mac 将会始终保持清醒
# 除非你 Ctrl + C  关闭，Mac 才会进入正常的休眠状态

# 你也可以使用 caffeinate 命令，指定某个程序，例如：
caffeinate /Applications/Notes.app

# -i : 防止系统闲置时进入睡眠状态
# -d : 防止显示器进入睡眠状态
# -m : 防止磁盘空闲时进入睡眠状态
# -s : 电脑在插入电源时，始终保持清醒
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

#### shutdown

`shutdown`命令是用来关机、重启或休眠系统的

```bash
# 此命令需要管理员权限
# 立刻关机
sudo shutdown -h now

# 立刻重启
sudo shutdown -r now

# 10分钟后重启
sudo shutdown -r +10

# 今天10:00休眠
sudo shutdown -s 10:00

# 2030年12月12日18时00分关机
sudo shutdown -h 203012121800

# 立刻关机
sudo halt

# 立刻重启
sudo reboot

# 如果当你输入完命令后突然不想关机了
# 可以按照以下步骤操作（此方式不适合立刻关机和重启的命令）
# 
# 关闭shutdown命令
# 当你输入完命令和密码后，会出现如下信息
# Shutdown at Wed Mar 14 13:51:09 2018.
# shutdown: [pid 80246]
#
# 注意上面的 pid 80246，这个是进程的号
# 如果要关闭 shutdown 命令，只需要终结这个进程号就可以了
# sudo kill 80246
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>


系统相关文件及其配置 
----
### 获取root权限 

为了防止误操作而人为因素破坏电脑系统，在终端下执行跟系统有关的操作时，需要先获得root权限

```bash
sudo ls -a
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 添加环境变量

```bash
# echo 命令的方式添加环境变量
echo "export PATH=xxxxxx:$PATH" >> ~/.bash_profile
source ~/.bash_profile
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 随机生成MAC地址

按住`option`键点击屏幕上方的“无线”图标，查看下 MAC 地址是多少，然后打开 Terminal 终端输入`ifconfig`，找到你 MAC 地址对应的参数，例如：我的是在`en0`下的`ether`里

```bash
# 随机生成一个MAC地址
# 系统重启恢复到原本的地址
sudo ifconfig en0 ether `openssl rand -hex 6 | sed 's/\(..\)/\1:/g; s/.$//'`
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 开启Terminal自动补全功能

打开终端，输入：

```bash
vim ~/.inputrc
```

粘贴如下语句并保存

```
set completion-ignore-case on set show-all-if-ambiguous on TAB: menu-complete
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 使用Touch ID进行sudo身份验证

首先打开终端，输入如下命令：

```bash
sudo vim /etc/pam.d/sudo
```

然后在`# sudo: auth account password session`的下一行添加如下字符串，保存退出即可

```bash
auth       sufficient     pam_tid.so
```

如果想还原的话，再打开此文件删除此字符串即可

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 更改系统语言 

输入 `sudo languagesetup` 回车后输入开机密码，然后输入选项前面的数字，回车后重启你的 Mac，系统就会加载刚刚设置的系统语言，当系统启动完毕后，你就可以看到系统使用的是你熟悉的语言了

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 本地化目录

当我们设置系统语言是中文时，Finder 内很多目录名称会本地化显示中文，在 Terminal 下其实还是英文名称。经常使用终端操作的可能会注意到这样一个细节，我们在 Finder 内创建一个中文目录后在 Terminal 下使用`cd`进目录的时候总是要不停的切换输入法，这样非常繁琐！

其实 MacOS 系统本身内建了多语言结构，可以到`/System/Library/CoreServices/SystemFolderLocalizations/zh_CN.lproj`下查看`SystemFolderLocalizations.strings`文件，该文件是二进制文件，查看时需要提前转换成我们能看懂的格式

```bash
cd /System/Library/CoreServices/SystemFolderLocalizations/zh_CN.lproj/

# plutil -convert 指定要转换的格式
sudo plutil -convert json SystemFolderLocalizations.strings

# 查看后再转换回去
sudo plutil -convert binary1 SystemFolderLocalizations.strings
```

转换 JSON 格式后的文件

```json
{
    "Library":"资源库",
    "Movies":"影片",
    ... ...
    "My Applications":"我的应用程序",
    "Compositions":"Compositions",
    "Documents":"文稿",
    "Downloads":"下载"
}
```

例如：我们要汉化 Virtial Machines 目录的话，只需在其中添加如下一行即可：

```json
"Virtual Machines":"虚拟机"
```

随后保存再把该文件转换成二进制文件，再回到 Virtual Machines 目录，在该目录下创建一个空白文件`.localized`，告诉 Finder 该目录是 localizing 目录

最后`killall Finder`即可生效，不过不建议大家这么做！

我们可以直接在访达内新建一个 Virtial Machines 目录，并给该目录添加一个`.localized`后缀，然后再在此目录内新建一个`.localized`目录，并在此目录下新建一个`zh_CN.strings`文件，添加`"Virtual Machines" = "虚拟机";`内容,这样保存后 Virtial Machines 就会显示成虚拟机，不过以后要进到该目录需要在终端下敲写`Virtial\ Machines.localized`带后缀的全称而已，不影响使用

```bash
mkdir -p Virtial\ Machines.localized/.localized && cd $_
vim zh_CN.strings # 添加 "Virtual Machines" = "虚拟机"; 然后保存退出
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 修改终端电脑名称

```bash
# 查看终端电脑名称
HostName

# 修改终端电脑名称
sudo scutil --set HostName name
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 终端开启允许安装任何来源App 

系统有一个保护叫做 [Gatekeeper](https://support.apple.com/zh-cn/HT202491) , 这个是防止第三方应用访问你的隐私信息的。如果你想关掉或者开启在终端里输入

```bash
# 开启
sudo spctl --master-disable

# 关闭
sudo spctl --master-enable
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 显示或隐藏文件 

隐藏文件的开头都会有一个点`「.」`，默认情况下你是看不到的，不过你想看的话，也是可以的，快捷键是`command + shift + .`

```bash
# 隐藏某个文件或目录
chflags hidden [File]

# 重新显示
chflags nohidden [File]

# 隐藏桌面所有文件
# 在 Finder - 桌面 内还可以看到，只不过是开机时或直接去桌面上看时是不显示的
defaults write com.apple.finder CreateDesktop -bool false
killall Finder

# 显示
defaults write com.apple.finder CreateDesktop -bool true
killall Finder

# 显示 Finder 内的隐藏文件
# 以下两条命令执行其中一个即可，killall Finder 命令是重启 Finder 的作用
defaults write com.apple.finder AppleShowAllFiles -bool true
killall Finder

defaults write com.apple.finder AppleShowAllFiles  YES
killall Finder

# 隐藏 Finder 内的隐藏文件
defaults write com.apple.finder AppleShowAllFiles -bool false
killall Finder

defaults write com.apple.finder AppleShowAllFiles  NO
killall Finder
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 查看苹果所有的高清图标

如果你想观摹或临摹一下设计精良的苹果产品icon的话，只需打开Finder，然后同时按住`Command+Shift+G`即可打开 “前往文件夹”的弹出窗口，然后输入以下路径

```bash
/System/Library/CoreServices/CoreTypes.bundle/Contents/Resources/
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 显示文件的扩展名

首先打开 Finder ，然后点击菜单栏中的“Finder” => “偏好设置” => “高级” => “高级”，然后在「显示所有文件扩展名」前面打勾即可

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 显示文件路径 

首先打开 Finder ，然后点击菜单栏中的“Finder” => “显示” => “显示/隐藏路径栏”，或者使用快捷键`command + option + p`

```bash
# 在 Finder 的标题栏处显示文件路径
# 不想显示只需要把 YES 改成 NO 即可
defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES
killall Finder
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### hosts文件的位置

如需Google等最新服务器地址的请移步到https://github.com/googlehosts/hosts

```bash
# hosts文件位置
/etc/hosts

# 修改 hosts 文件时需要注意的
# IP 和 域名之间需要两个空格，否则不会生效，格式如下：
192.168.1.11  www.qinlzhu.com
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 更改 Finder 每次打开时默认显示的目录 

首先打开 Finder ，然后点击屏幕上面的菜单栏，依次点击“Finder” => “偏好设置” => “通用”，然后在「开启新 Finder 窗口时打开:」项下选择你喜欢的目录即可

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 更改 Finder 默认窗口的显示风格

```bash
# 按照图标方式排列
defaults write com.apple.Finder FXPreferredViewStyle icnv
killall Finder

# FXPreferredViewStyle 后的值有以下几种
#
# Nlsv：系统默认值，按照列表形式
# icnv：按照图标形式
# clmv：按照列视图形式
# Flwv：按照画廊形式
#
# 如果设置后发现在某些目录里显示效果与设置的不一样，删除该目录下的.DS_Store文件即可
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 不显示最近使用的项目

如果你不想显示Finder、Quick Time Player、Sublime Text等等最近使用的项目记录的话，点击“系统偏好设置” => “通用” => “最近使用的项目” => “n 个文稿、应用和服务器”，把数字改成 0 就可以了

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 截图 

截取屏幕全部区域：`command + shift + 3`
截取屏幕全部区域到剪贴板：`command + control + shift + 3`
截取窗口（不包含菜单栏和程序坞）：`command + shift + 4 + space`
截取所选区域：`command + control + shift + 4`
截取所选区域到剪贴板：`command + shift + 4`
截取触摸栏：`command + shift + 6`

```bash
# 更改截图的保存位置
defaults write com.apple.screencapture location ~/Desktop

# 更改截图的保存格式
defaults write com.apple.screencapture type jpg

# 去除截图的阴影，要想改回来只需要把 true 改成 false 即可
defaults write com.apple.screencapture disable-shadow -bool true

# 更改“屏幕快照+时间”的截图命名方式
defaults write com.apple.screencapture name newFlieName

# 重启服务
killall SystemUIServer

# 自定义截图时间、保存名称和图片格式
# 数字3，是多少秒后开始截图
# empty.jpg 则是图片的名称和格式
screencapture -T 3 empty.jpg
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 禁止生成 DS_Store 文件

`.DS_Store` 是 macOS 保存文件夹的自定义属性的隐藏文件，如文件的图标位置或背景色，相当于 Windows 的 `desktop.ini`

```bash
# 禁止`.DS_store`生成，执行以下命令
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool TRUE2

# 恢复`.DS_store`生成，执行
defaults delete com.apple.desktopservices DSDontWriteNetworkStores
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### bash相关的文件

Mac 下自带了很多解析 Shell 脚本的解释器，例如：bash、zsh等。如果想查看 Mac 都内置了那些 Shell 脚本的解释器，可以输入以下任意一个命令查看

```bash
cat /etc/shells

# 或
ls -l /bin/*sh
```

以下是 Mac 下跟 Bash 解析器有关的文件/文件夹

- `.bash_history` 记录了以前执行过的 bash 命令
- `.bash_profile` Mac 配置环境变量的文件(交互式登陆)
- `.bash_sessions` 里面包含了每次使用 bash 所做的操作的文件列表（文件夹）

**Mac 下为什么没有`.bashrc`文件？**

在 Unix 和 Linux 下正常情况是，`.bash_profile`执行登录Shell(login shell)，同时`.bashrc`执行交互式非登录Shell(no-login shell)

在 Linux 下，当用户登录到一个图形界面，然后打开一个终端 Terminal，那些 Shell 是 non-login shell。然而，在 OS X 登录的时候，并没有运行着一个 Shell，所以，在运行 Terminal 的时候，其实是一个 login shell，所以它就没有`.bashrc`文件

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### CFUserTextEncoding文件

`~/.CFUserTextEncoding`存储用户的默认文本编码和首选语言的文件

```
# 参考博客地址
http://www.kbase101.com/question/38628.html

# Mac OS X 参考库技术说明2228
https://developer.apple.com/library/archive/technotes/tn2228/_index.html
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 容器中的其他卷宗

点击``-`关于本机`-`储存空间`，可以看到储存条中有个白色的加斜杠的块，当你把鼠标移上去后，会显示此块是“容器中的其他卷宗”，这是格式升级成APFS后会多出來的东西

你也可以在终端中输入如下命令：
```bash
# 查看磁盘结构的命令
diskutil list

# 回车后会出现如下信息
/dev/disk0 (internal):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      GUID_partition_scheme                         251.0 GB   disk0
   1:                        EFI EFI                     314.6 MB   disk0s1
   2:                 Apple_APFS Container disk1         250.7 GB   disk0s2

/dev/disk1 (synthesized):
   #:                       TYPE NAME                    SIZE       IDENTIFIER
   0:      APFS Container Scheme -                      +250.7 GB   disk1
                                 Physical Store disk0s2
   1:                APFS Volume Macintosh HD            181.5 GB   disk1s1
   2:                APFS Volume Preboot                 42.8 MB    disk1s2
   3:                APFS Volume Recovery                512.8 MB   disk1s3
   4:                APFS Volume VM                      3.2 GB     disk1s4

# 如下三条就是就是“容器中的其它宗卷”，其中VM，是可变的，里面是系统必须的睡眠文件和交换文件，路径是/private/var/vm

    2:                APFS Volume Preboot                 42.8 MB    disk1s2
    3:                APFS Volume Recovery                512.8 MB   disk1s3
    4:                APFS Volume VM                      3.2 GB     disk1s4
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 重置NVRAM或PRAM

如果电脑出现跟内核、时区、分辨率以及磁盘相关的问题时，可以重置NVRAM或PRAM。具体操作是开机时同时按住`command`+`option`+`P`+`R`键10到20秒

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 重置SMC

如果电脑出现了跟电源、电池、键盘背光、状态指示灯及其热能相关的问题时，可以重置SMC。具体操作是关机后同时按住`shift`+`control`+`Option`+`关机键`键10秒，然后松开所有键再开机

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>


其它的系统故障及其常见疑问
----
### 强制退出程序 

1、调出“强制退出”窗口方式退出应用

依次点击 “” => “强制退出” => “选择要强制退出的程序” => “强制退出”，快捷键`command + option + esc`

2、直接强制退出应用的方式

在要退出的应用界面同时按`command + option + shift + esc`

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 账户管理权限丢失 

有次点击“系统偏好设置” => “用户与群组” => “🔒”输入密码的时候，怎么输都不对！后来去“用户与群组”里面看了下，一看登陆账户变成普通用户了，立马就去网上查了下，但是搜了很多资料也没能解决，最后实在没办法致电了苹果客服，在她们的帮助下才得以解决此问题，在此贴下

首先在重启电脑的时候按住`command + s`键，当出现命令行终端的时候按照以下顺序输入命令「就是那个黑色的全是一行行很小很小的代码界面，注意空格和大小写不要写错了」

```bash
mount -uw /

rm /var/db/.AppleSetupDone

reboot
```

回车后你就可以像刚买来电脑的时候，再次注册下管理账号就可以了，然后从刚注册的账号登进去给丢失管理员权限的账号设置下权限就 OK 了，回来你也可以登陆旧的账号把新的账号给删了，当然新的账号不删保留着也没啥事

**注意**：如果你想把旧的账号给删了的话，需要提前备份下旧账号的资料

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 重置被遗忘的管理员密码

如果你忘记了登陆密码，可以使用此方式更改管理员密码。首先，在系统开机还未进入登录界面时按下`command+S`进入单用户模式。然后输入

```bash
mount -rw /
```

以读写方式挂载文件系统；接着重置管理员 json 的密码，回车后会要求你输入新的密码

```bash
passwd json
```

完成后，输入命令重启

```bash
reboot
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 前往资源库

1、打开Finder文件夹，点击右上角的菜单栏“前往”选项，然后按住`option`键的同时即可出现资源库选项

2、在终端输入`open ~/libray`

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 输入苹果图标

在需要输入的地方同时按`shift + option + k`键

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 输入或查询偏僻字

例如：想查询“龘”这个字怎么读

1、首先先看下这个字的组成部分，它是由三个龙组成，使用MAC自带的输入法，打出三个`龙龙龙 longlonglong`，然后按`shift + 空格键` 你就会看到这个字了，同时旁边也会有它的发音

2、`shift + control + 空格键`调出鼠绘面板，写出你要查询或者输入的字

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 调出 emoji 表情

在需要输入的地方同时按`control + command + space(空格)`键

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 查看本地IP地址

1、按住`option`键，然后再点击屏幕上方的“无线图标”即可显示

2、点击“系统偏好设置” => “网络”后，在右侧的状态中即可看到

3、终端下使用[`ifconfig`](https://blog.edentsai.net/2015-11-22-how-to-use-ifconfig-on-max-osx/)命令
```bash
# 显示当前网络接口配置信息
# 在一大串的参数中找到 en0 参数，里面就有你想要的 IP 地址
ifconfig 

# Centos7+ 查看命令
ip addr

# 只显示网卡的配置信息，注意 en0 中的 0 不是字母 o 哦
ifconfig en0

# 更精确的命令
ipconfig getifaddr en0
```

4、终端内输入苹果脚本代码

```bash
// 显示系统的所有信息
osascript -e "system info" 

// 只显示 IP4
osascript -e "IPv4 address of (system info)"
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 查看目录或磁盘占用空间

```bash
# 查看文件或目录的大小
du -h -d 1 ~/Downloads

# 查看磁盘的占用空间
df -h
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 去掉副本图标上的箭头

打开Finder，然后同时按住`Command+Shift+G`即可打开 “前往文件夹”的弹出窗口，然后输入以下路径

```bash
/System/Library/CoreServices/CoreTypes.bundle/Contents/Resources/
```

把该目录下的`AliasBadgeIcon.icns`文件更改为`AliasBadgeIcon-no.icns`，然后打开Terminal重启Finder后会立即生效

```bash
killall Finder
```

如果想还原，只需要把文件名重新命名成`AliasBadgeIcon.icns`即可

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 快速建立 www 服务

在 Terminal 中进入要分享的文件目录下，执行如下命令，可快速建立 www 服务，可以迅速分享文件给同事，关闭服务的话，只需要关闭终端即可

访问时，只需要输入`http://Your IP4 address:8000`

```python
# python2
# 如果你未安装 python3 的话，请执行此命令
python -m SimpleHTTPServer 8000

# python3
python3 -m http.server 8000
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### ssh 端口转发科学上网

ssh 端口转发的方式也称之为FQ方法，使用该方法的前提是你的有一台境外的VPS主机

第一步在本机建立一个端口通道
```bash
ssh -D 7000 vpsuser@vpshost

# 7000 是你要使用的端口可以任意修改
# vpsuser 是VPS上的账户
# vpshost 是VPS主机地址
```

最后找到 “系统偏好设置” => “网络” => “高级” => “代理” => “Socks代理” 勾选上，输入：
```bash
localhost ：7000
```

确认即可FQ啦

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 终端下出现bogon的解决办法

```bash
# 1.将DNS设置为Google的DNS服务器地址 8.8.8.8
# 在“系统偏好设置” => “Wi-Fi” => “高级” => “DNS” => “+” 中添加

# 2.终端内修改
sudo hostname your-desired-host-name
sudo scutil --set LocalHostName $(hostname)
sudo scutil --set HostName $(hostname)
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 剪切文件或文件夹

1、复制需要剪切的文件/文件夹（右键`拷贝`或快捷键`command` + `c`），然后在需要粘贴的位置按住`option`键右击，会出现`将项目移到这里`的选项，点击它就会把刚才的项目剪切到此处

2、快捷键`command` + `c`复制，`command` + `option` + `v`粘贴

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 安全清空垃圾桶

```bash
sudo rm -rfv ~/.Trash /Volumes/*/.Trashes
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>

### 清理系统垃圾

```bash
# 清除旧的日志文件，临时和垃圾文件
sudo periodic daily

# Daily脚本清除了旧的日志文件，临时和垃圾文件
# Weely脚本重建locate和whatis数据库
# monthly汇集了每个用户的使用信息并且备份
sudo periodic daily weekly monthly

# 默认运行过程是没有任何反馈的，如果你想看到执行的结果，以执行这个命令
ls -al /var/log/*.out

# 清除QuickLook缓存文件
sudo rm -rf /private/var/folders/

# 清除缓存文件（注意此操作会清除浏览器的收藏夹、插件和数据等）
sudo rm -rf ~/Library/Caches/*
```

<p style="font-size: 14px;margin-bottom: 25px;"><a href="#">⬆回到顶部</a></p>



[MacOS]:https://zh.wikipedia.org/wiki/MacOS
[FreeBSD]:https://zh.wikipedia.org/wiki/FreeBSD
[Linux]:https://zh.wikipedia.org/wiki/Linux
[Unix]:https://zh.wikipedia.org/wiki/%E7%B1%BBUnix%E7%B3%BB%E7%BB%9F
[MacOS_High_Sierra]:https://zh.wikipedia.org/wiki/MacOS_High_Sierra
[window]:https://zh.wikipedia.org/wiki/Microsoft_Windows