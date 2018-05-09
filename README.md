MacOS终端指令
================

在终端中使用指令操作可以帮助我们减去很多繁琐的操作，大大方便了工作效率，[MacOS][MacOS]系统是全世界第一个基于[FreeBSD][FreeBSD]系统采用“面向对象操作系统”的全面的操作系统，且[FreeBSD][FreeBSD]和[Linux][Linux]又都是[类Unix][Unix]的操作系统（意思就是它们都是基于Unix系统重新开发的），所以两者的指令在很多地方都是相同的，如果你玩的了[Linux][Linux]那么[MacOS][MacOS]系统自然也就不在话下了

**注意：** 以下指令我只在 [`macOS High Sierra 10.13.3`][MacOS_High_Sierra] 版本上测试过，跟其他版本或许有所不同！

正在不断完善中，欢迎 Star！


目录
----
* [系统目录](#系统目录)
* [权限信息](#权限信息)
* [终端的基本指令操作](#终端的基本指令操作)
    - [man](#man)
    - [history](#history)
    - [clear](#clear)
    - [!!](#!!)
    - [cd](#cd)
    - [pwd](#pwd)
    - [ls](#ls)
    - [open](#open)
    - [touch](#touch)
    - [cp](#cp)
    - [mv](#mv)
    - [rm](#rm)
    - [nl](#nl)
    - [wc](#wc)
    - [head](#head)
    - [tail](#tail)
    - [mkdir](#mkdir)
    - [rmdir](#rmdir)
    - [say](#say)
    - [shutdown](#shutdown)
    - [passwd](#passwd)
    - [which](#which)
    - [who](#who)
    - [whoami](#whoami)
    - [alias](#alias)
    - [caffeinate](#caffeinate)
    - [ps](#ps)
* [系统配置](#系统配置)
    - [获取权限](#获取权限)
    - [添加环境变量](#添加环境变量)
    - [开启Terminal自动补全功能](#开启terminal自动补全功能)
    - [使用Touch ID进行sudo身份验证](使用touch-id进行sudo身份验证)
    - [更改系统语言](#更改系统语言)
    - [修改终端电脑名称](#修改终端电脑名称)
    - [终端开启允许安装任何来源App](#终端开启允许安装任何来源app)
    - [显示或隐藏文件](#显示或隐藏文件)
    - [显示文件的扩展名](#显示文件的扩展名)
    - [显示文件路径](#显示文件路径)
    - [更改 Finder 每次打开时默认显示的目录](#更改-finder-每次打开时默认显示的目录)
    - [不显示最近使用的项目](#不显示最近使用的项目)
    - [截图](#截图)
    - [禁止生成 DS_Store 文件](#禁止生成-ds_store-文件)
    - [清理系统](#清理系统)
* [其它的常见问题](#其它的常见问题)
    - [强制退出程序](#强制退出程序)
    - [账户管理权限丢失](#账户管理权限丢失)
    - [重置被遗忘的管理员密码](#重置被遗忘的管理员密码)
    - [前往资源库](#前往资源库)
    - [输入苹果图标](#输入苹果图标)
    - [调出 emoji 表情](#调出-emoji-表情)
    - [查看本地IP地址](#查看本地ip地址)
    - [查看目录或磁盘占用空间](#查看目录或磁盘占用空间)
    - [查看苹果所有的高清图标](#查看苹果所有的高清图标)
    - [去掉副本图标上的箭头](#去掉副本图标上的箭头)
    - [快速建立 www 服务](#快速建立_www_服务)
    - [hosts文件的位置](#hosts文件的位置)

## 系统目录 

[MacOS][MacOS]是基于[FreeBSD][FreeBSD]开发的，而[FreeBSD][FreeBSD]又是[Unix][Unix]派生的，所以你可以理解为[MacOS][MacOS]的最底层是[Unix][Unix]，[Unix][Unix]的所有文件都挂在系统的根目录`/`下面，所以[MacOS][MacOS]也是一样，所以就不要再想象着像[Window][window]系统那样C盘、D盘的概念啦!

**例如：**我在 Macbook 上插了一个叫 empty 的移动硬盘，并且在电脑的桌面上显示了这个硬盘图标，那么它实际位置在哪呐？其实它在`/Volumes`目录下，你执行下`ls /Volumes/empty`看看是不是移动硬盘里面的内容

还有驱动所在位置`/Systme/Library/Extensions`

```
# unix传统的系统目录

/bin   存放unix传统指令的位置「例如：ls、pwd」
/sbin  存放unix传统管理类指令的位置「例如：ifconfig、shutdown」
/usr   第三方程序安装目录，其中/usr/lib目录中存放了共享库「动态链接库」
/etc   unix系统配置文件存放目录。「例如：用户密码文件/etc/passwd，此目录实际为指向/private/etc的链接」
/dev   设备文件存放目录
/tmp   临时文件存放目录，此目录实际为指向/private/tmp的链接
/var   存放经常变化的文件，如日志文件，此目录实际为指向/private/var的链接
```

```
# MAC 特有的系统目录

/Applications 存放应用程序的
/Library      存放系统的数据文件、帮助文件、文档等等
/Network      存放网络节点的
/System       只包含一个名为Library的目录，这个子目录中存放了系统的绝大部分组件，如各种framework以及内核模块和字体文件等等
/Users        存放用户的个人资料和配置，每个用户有自己的单独目录
/Volumes      文件系统挂载点存放目录
/cores        内核转储文件存放目录，当一个进程崩溃时，如果系统允许则会产生转储文件
/private      里面的子目录存放了/tmp、/var、/etc等链接目录的目标目录
```

## 权限信息 

当你执行`ls -l`指令查看一个文件信息的时候，系统会为你列出如下格式的权限信息，共10个字符

```bash
权限信息通用格式：
-rwxr-xr-x　number　user　group　filesize　updatetime　filename
```

第一个字符表示的是文件的类型，后 9 个字符分 3 组，表示该文件对于当前用户、当前用户所在组、其他用户的读/写/执行权限

* 常见的文件类型：
    - `d`：代表的是目录
    - `-`：代表的是文件
    - `l`：代表的是链接文件
* 权限：
    - `w`代表可写
    - `r`代表可读
    - `x`代表可执行
    - `-`代表无权限

**例如**：

```bash
-rwxr-xr-x　3　root　root  288  3  1 19:46 empty
```

* `-`：        这是一个文件
* `rwx`：      文件拥有者对它有读写可执行权限，意思就是完全的拥有权
* `r-x`：      所属组的成员对这个文件只有阅读和执行文件的权利
* `r-x`：      其他用户也是对这个文件只有阅读和执行文件的权利
* `3`：        链接数
* `root`：     当前用户
* `root`：     当前用户所属的组
* `288`：      文件的大小「单位是byte」
* `3 1 19:46`：最后修改的时间是3月1号19:46
* `empty`：    文件名称

**修改权限**

如果其他用户想拥有对某个文件的修改权限怎么办？这时我们就需要到修改权限的指令了，指令格式：

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
# 首先我们先看下权限信息
ls -l empty
-rw-r--r--  1 root  root  0  3  5 11:41 empty

# 使用 chmod 指令，给组其他的成员添加对 empty 文件的修改权限
# 注意 g+w 中间是没有空格的
chmod g+w empty
ls -l empty
-rw-rw-r--  1 root  root  0  3  5 11:41 empty
```

**修改文件所属组**

```
# chgrp [-R] 群组名 文件或目录的名称
-R：递归修改
```

**修改文件拥有者**

```
chown [-R] 用户名:群组名 文件或目录的名称
```

## 终端的基本指令操作 

### man 

`man`是“manual”的缩写，是一个帮助指令，通过`man`指令可以查看 Mac OS X系统中的指令帮助、配置文件帮助和编程帮助等信息

当执行`man cd`时，第一行会出现一个`(1)`，其中的数字代表指令的类型，常用的数字及其类型如下：

```
1   用户在 shell 环境中可以操作的指令或者可执行文件
5   配置文件
8   系统管理员可以使用的管理指令
```

```bash
# 查看 cd 指令帮助信息
man cd

# 除了使用 man 查看指令帮助信息外
# 还可以在指令后面加 --help 选项，也是可以查看该指令的帮助信息的
cd --help
```

### history 

`history`指令用于显示指定数目的指令，读取历史指令文件中的目录到历史指令缓冲区和将历史指令缓冲区中的目录写入指令文件

```bash
# 查看以前所有执行过的终端指令（前提是你没清理过）
history

# 查看最近执行过的 6 条指令
history 6

# 立即清空 history 里的历史指令记录
history -c
```

### clear 

`clear`指令用于清除当前屏幕终端上的任何信息

```bash
clear
```

### !! 

`!!`执行上一条指令

```bash
!!
```

### cd 

`cd`指令用来切换工作目录

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
```

## pwd 

`pwd`指令以绝对路径的方式显示用户当前所在的工作目录位置

```bash
pwd
```

### ls 

`ls`指令用来列出目标目录中所有的子目录和文件。注意参数的大小写

```bash
# 列出当前目录下非隐藏的文件和目录，等价于“ls -C（注意：大写）”
ls

# 列出目录下的所有文件，包括以“.”开头的隐含文件
ls -a
ls -all

# 与上面的“ls -a”指令几乎相同，只不过是此指令不显示“.（当前目录）”和“..（父级目录）”这两个
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

### open 

`open`指令用于打开文件、目录或执行程序。等同于图形界面下的重复“双击”动作

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

### touch

`touch`指令用来创建或修改文件

```bash
# 创建空白文件
touch empty

# 加 -t 选项，修改文件的创建和修改时间
# 时间格式为：[[CC]YY]MMDDhhmm[.ss]
touch -t 20180324192900 empty

# 加 -mt 选项，修改文件的修改和访问时间
touch -mt 20160324192900 empty
```

### cp 

`cp`指令是用来复制文件或目录

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

### mv 

`mv`指令是用改变文件名或所在目录的位置

```bash
# 改变文件或目录名称
mv empty newEmpty

# 移动文件或目录到指定位置
mv empty ~/Downloads/empty

# 先给文件或目录重新命名，然后再移动到指定位置
mv empty ~/Downloads/newEmpty
```

### rm 

`rm`指令是用来删除文件和目录，对于链接文件，只是删除整个链接文件，而原有文件保持不变。使用 rm 指令需要格外小心。因为一旦删除了一个文件，就无法再恢复它

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

### nl 

`nl`指令用来指定文件的行号显示方式

```bash
# 给某个文件添加上行数在终端显示（空白行不会添加）
nl empty.txt
# 或
nl -b t empty.txt

# 不论是否为空行，也同样列出行号
nl -b a empty.txt

# 不添加行号显示
nl -b n empty.txt

# 行号左对齐
nl -n ln empty.txt

# 行号右对齐（默认）
nl -n rn empty.txt

# 行号右对齐（显示六位数的行号，不足六位的前面添加 0）
nl -n rz empty.txt

# 指定行号最多显示的位数（默认为 6）
nl -w 5 empty.txt

# 把行号添加到文件内并另存为一个文件
nl -b t empty.txt > new.txt
```

### wc

`wc`指令是用来统计文件的字符数、词数和行数

```bash
wc empty.txt

# 只统计行数
wc -l empty.txt

# 只统计字节数
wc -c empty.txt

# 只统计字符数
wc -m empty.txt

# 只统计字数
wc -w empty.txt
```

### head

`head`指令从头部开始显示指定文件的内容

```bash
# 显示文件的头 10 行
head 10 empty.txt

# 显示文件的头 10 个字符（注意：一个中文占两个字符）
head -c 10 empty.txt
```

### tail

`tail`指令从尾部开始显示指定文件的内容

```bash
# 显示文件最后的 10 行
tail 10 empty.txt

# 显示文件最后的 10 个字符（注意：一个中文占两个字符）
tail -c 10 empty.txt
```

### mkdir 

`mkdir`指令是用来创建文件目录

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

### rmdir 

`rmdir`指令是用来删除空白文件目录

```bash
# 删除空白文件目录，如果目录下有东西是删除不了的
rmdir empty

# 加 -p 选项
# 如果删除了某个目录，父目录就变为空目录的话，就一块删除
rmdir ~/Downloads/empty

# 删除多个目录
rmdir emptyA emptyB
```

### say

`say`指令是用来文本转换语音的，当然你也可以结合一些其他的指令玩，例如：执行某段程序后，使用`say`指令提示你

```bash
# 朗读文字
say hello

# 更改朗读的人物
# 可以使用“say -v ?”查看，都有哪些人物
say -v Diego

# 朗读一个文件
say -f empty.txt

# 朗读的语音保存成一个音频文件
say -o new.mp3 -f empty.txt
```

### shutdown

`shutdown`指令是用来关机、重启或休眠系统的

```bash
# 此指令需要管理员权限
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

# 关闭shutdown指令
# 当你输入密码回车后，会出现如下信息
# Shutdown at Wed Mar 14 13:51:09 2018.
# shutdown: [pid 80246]
#
# 注意上面的 pid 80246，这个是进程的号
# 如果要关闭 shutdown 指令，只需要终结这个进程号就可以了
# sudo kill 80246
```

### passwd

`passwd`修改登录密码，指令输入完成后回车要求分别输入旧的登陆密码和新的登陆密码，都输入完成后，回车即可更改

### which

`which`指令用来查看某个指令所在的位置

```bash
which ls
```

### who

`who`指令用列出当前登陆的所有用户

### whoami

`whoami`指令用显示当前正进行操作的用户名

### alias

`alias`指令用来定义指令别名

```bash
# 定义一个列出目录树的指令
alias Tree="find . -print | sed -e 's;[^/]*/;|____;g;s;____|; |;g'"

# 删除定义的指令
unalias Tree
```

### caffeinate

`caffeinate`指令用来修改屏幕睡眠时间的

```bash
# 3600 是秒数，可以使 Mac 一小时不进入睡眠状态
caffeinate -t 3600

# 打开 terminal 时，直接输入 caffeinate 指令并回车后
# 当你最小化或隐藏它时，Mac 将会始终保持清醒
# 除非你 Ctrl + C  关闭，Mac 才会进入正常的休眠状态

# 你也可以使用 caffeinate 指令，指定某个程序，例如：
caffeinate /Applications/Notes.app

# -i : 防止系统闲置时进入睡眠状态
# -d : 防止显示器进入睡眠状态
# -m : 防止磁盘空闲时进入睡眠状态
# -s : 电脑在插入电源时，始终保持清醒
```

### ps

`ps`指令用来查看系统进程

```bash
# 查看当前用户下的所有进程
ps -A

# 查看所有进程（包含其他用户，相当于系统下的所有进程）
ps -e
```

## 系统配置 

### 获取权限 

为了防止误操作破坏系统，在用户状态下是没有权限操作系统重要文件的，所以先要取得root权限，然后输入密码，输入密码时没有任何回显，连星号都没有，只管输完回车就行了

```bash
sudo ls -a
```

### 添加环境变量

```bash
# echo 指令的方式添加环境变量
echo "export PATH=xxxxxx:$PATH" >> ~/.bash_profile
source ~/.bash_profile
```

### 开启Terminal自动补全功能

打开终端，输入：

```bash
vim ~/.inputrc
```

粘贴如下语句并保存

```
set completion-ignore-case on set show-all-if-ambiguous on TAB: menu-complete
```

### 使用Touch ID进行sudo身份验证

首先打开终端，输入如下指令：

```bash
sudo vim /etc/pam.d/sudo
```

然后在`# sudo: auth account password session`的下一行添加如下字符串，保存退出即可

```bash
auth       sufficient     pam_tid.so
```

如果想还原的话，再打开此文件删除此字符串即可

### 更改系统语言 

输入 `sudo languagesetup` 回车后输入开机密码，然后输入选项前面的数字，回车后重启你的 Mac，系统就会加载刚刚设置的系统语言，当系统启动完毕后，你就可以看到系统使用的是你熟悉的语言了

### 修改终端电脑名称

```bash
# 查看终端电脑名称
HostName

# 修改终端电脑名称
sudo scutil --set HostName name
```

### 终端开启允许安装任何来源App 

系统有一个保护叫做 [Gatekeeper](https://support.apple.com/zh-cn/HT202491) , 这个是防止第三方应用访问你的隐私信息的。如果你想关掉或者开启在终端里输入

```bash
# 开启
sudo spctl --master-disable

# 关闭
sudo spctl --master-enable
```

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
# 以下两条指令执行其中一个即可，killall Finder 指令是重启 Finder 的作用
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

### 显示文件的扩展名

首先打开 Finder ，然后点击菜单栏中的“Finder” => “偏好设置” => “高级” => “高级”，然后在「显示所有文件扩展名」前面打勾即可

### 显示文件路径 

首先打开 Finder ，然后点击菜单栏中的“Finder” => “显示” => “显示/隐藏路径栏”，或者使用快捷键`command + option + p`

```bash
# 在 Finder 的标题栏处显示文件路径
# 不想显示只需要把 YES 改成 NO 即可
defaults write com.apple.finder _FXShowPosixPathInTitle -bool YES
killall Finder
```

###更改 Finder 每次打开时默认显示的目录 

首先打开 Finder ，然后点击屏幕上面的菜单栏，依次点击“Finder” => “偏好设置” => “通用”，然后在「开启新 Finder 窗口时打开:」项下选择你喜欢的目录即可

### 不显示最近使用的项目

如果你不想显示Finder、Quick Time Player、Sublime Text等等最近使用的项目记录的话，点击“系统偏好设置” => “通用” => “最近使用的项目” => “n 个文稿、应用和服务器”，把数字改成 0 就可以了

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

### 禁止生成 DS_Store 文件

`.DS_Store` 是 macOS 保存文件夹的自定义属性的隐藏文件，如文件的图标位置或背景色，相当于 Windows 的 `desktop.ini`

```bash
# 禁止`.DS_store`生成，执行以下命令
defaults write com.apple.desktopservices DSDontWriteNetworkStores -bool TRUE2

# 恢复`.DS_store`生成，执行
defaults delete com.apple.desktopservices DSDontWriteNetworkStores
```

### 清理系统

```bash
# 清除旧的日志文件，临时和垃圾文件
sudo periodic daily

# Daily脚本清除了旧的日志文件，临时和垃圾文件
# Weely脚本重建locate和whatis数据库
# monthly汇集了每个用户的使用信息并且备份
sudo periodic daily weekly monthly

# 默认运行过程是没有任何反馈的，如果你想看到执行的结果，以执行这个指令
ls -al /var/log/*.out
```


## 其它的常见问题 

### 强制退出程序 

依次点击 “” => “强制退出” => “选择要强制退出的程序” => “强制退出”，快捷键`command + option + esc`

### 账户管理权限丢失 

有一次我点击“系统偏好设置” => “用户与群组” => “🔒” 的时候，要我输入密码，那就输呗！可是怎么输入都是不对，密码明明就是这个啊，这怎么回事？后来我去“用户与群组”里面看了下，一看我当前的账户变成普通用户了，我就去网上查了下，但是搜了很多资料也没解决，最后还是致电了苹果客服才给解决的，在此贴下

首先在重启电脑的时候按住`command + s`键，当出现命令行终端的时候按照以下顺序输入命令「就是那个黑色的全是一行行很小很小的代码界面，注意空格和大小写不要写错了」

```bash
mount -uw /

rm /var/db/.AppleSetupDone

reboot
```

回车后你就可以像刚买来电脑的时候，再次注册下管理账号就可以了，然后从刚注册的账号登进去给丢失管理员权限的账号设置下权限就 OK 了，回来你也可以登陆旧的账号把新的账号给删了，当然新的账号不删保留着也没啥事

**注意**：如果你想把旧的账号给删了的话，需要提前备份下旧账号的资料

### 重置被遗忘的管理员密码

如果你忘记了登陆密码，可以使用此方式更改管理员密码。首先，在系统开机还未进入登录界面时按下`command+S`进入单用户模式。然后输入

```bash
mount -rw /
```

以读写方式挂载文件系统；接着重置管理员 json 的密码，回车后会要求你输入新的密码

```bash
passwd json
```

完成后，输入指令重启

```bash
reboot
```

### 前往资源库

* 打开 Finder 文件夹，点击右上角的菜单栏"前往"选项，然后按住`option`键的同时即可出现资源库选项
* 在终端输入`open ~/libray`

### 输入苹果图标

在需要输入的地方同时按`shift + option + k`键

### 调出 emoji 表情

在需要输入的地方同时按`control + command + space(空格)`键

### 查看本地IP地址

* 按住`option`键，然后再点击屏幕上方的“无线图标”即可显示
* 点击“系统偏好设置” => “网络”后，在右侧的状态中即可看到
* [`ifconfig`](https://blog.edentsai.net/2015-11-22-how-to-use-ifconfig-on-max-osx/)指令
```bash
# 显示当前网络接口配置信息
# 在一大串的参数中找到 en0 参数，里面就有你想要的 IP 地址
ifconfig 

# 只显示网卡的配置信息，注意 en0 中的 0 不是字母 o 哦
ifconfig en0

# 更精确的命令
ipconfig getifaddr en0
```
* 输入下方任意一个苹果脚本代码
```bash
// 显示系统的所有信息
osascript -e "system info" 

// 只显示 IP4
osascript -e "IPv4 address of (system info)"
```

### 查看目录或磁盘占用空间

```bash
# 查看文件或目录的大小
du -h -d 1 ~/Downloads

# 查看磁盘的占用空间
df -h
```

### 查看苹果所有的高清图标

如果你想观摹或临摹一下设计精良的苹果产品icon的话，只需打开Finder，然后同时按住`Command+Shift+G`即可打开 “前往文件夹”的弹出窗口，然后输入以下路径

```bash
/System/Library/CoreServices/CoreTypes.bundle/Contents/Resources/
```

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


### 快速建立 www 服务

在 Terminal 中进入要分享的文件目录下，执行如下指令，可快速建立 www 服务，可以迅速分享文件给同事，关闭服务的话，只需要关闭终端即可

访问时，只需要输入`http://Your IP4 address:8000`

```python
# python2
# 如果你未安装 python3 的话，请执行此命令
python -m SimpleHTTPServer 8000

# python3
python3 -m http.server 8000
```


### hosts文件的位置

```
/etc/hosts
```


## 贡献

如果您想对此项目作出贡献的话，可以按照下列步骤操作

1.首先`Fork`此项目
2.复制拷贝到你 Github 账号下的 macCommand 库的 `SSH` 地址
3.执行`git clone`将此库下载到本地
4.进入该库，新建一个分支并切换到该分支`git checkout -b 分支名`
5.修改内容
6.提交修改`git commit -am "在此输入修改或增加了什么内容"`
7.指定新建的分支跟远程仓库分支之间的链接关系`git push --set-upstream origin 刚才新建的分支名`
8.提交`git push`
9.回到你的 Github，进入刚才`Fork`而来的仓库，这时你会看到一个`Compare & pull request`
10.点击那个按钮提交拉请求

如果不懂的可以按照此库的操作步骤，操作一边 [first-contributions](https://github.com/Roshanjossey/first-contributions/blob/master/README.md)


## 许可

文档和代码根据 [MIT许可证](./LICENSE) 发布


[MacOS]:https://zh.wikipedia.org/wiki/MacOS
[FreeBSD]:https://zh.wikipedia.org/wiki/FreeBSD
[Linux]:https://zh.wikipedia.org/wiki/Linux
[Unix]:https://zh.wikipedia.org/wiki/%E7%B1%BBUnix%E7%B3%BB%E7%BB%9F
[MacOS_High_Sierra]:https://zh.wikipedia.org/wiki/MacOS_High_Sierra
[window]:https://zh.wikipedia.org/wiki/Microsoft_Windows