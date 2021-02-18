---
title: Study Notes

---

### Windows Terminal

**Official Doc**: [Windows 终端概述 | Microsoft Docs](https://docs.microsoft.com/zh-cn/windows/terminal/)

* Tutorial (It uses PS5, please also reference tutorial of PS7 listed below)
  [Windows Terminal 自定义 - 少数派](https://sspai.com/post/59380)
  [Windows 终端 Powerline 设置 | Microsoft Docs](https://docs.microsoft.com/zh-cn/windows/terminal/tutorials/powerline-setup)

* 安装字体

    * `ttf` and `ttc` 格式，安装or直接拷贝到`C:\Windows\Fonts`即可

    * 注意字体名称不是文件名而是

      <img src="./img/font name.png" alt="font name" style="zoom:50%;" />

      这将在`wt`的设置里用到，例如(在`wt`中用`Ctrl+,`打开)

      ```json
      {//...
       "list":
              [
                  {
                      // Make changes here to the powershell.exe profile.
                      "guid": "{61c54bbd-c2c6-5271-96e7-009a87ff44bf}",
                      "name": "Windows PowerShell",
                      "commandline": "powershell.exe",
                      "fontFace": "JetBrainsMono Nerd Font Mono",
                      // "fontFace": "MesloLGL NF",
                      // "fontFace": "Cascadia Mono PL",
                      "hidden": false
                  },
                  // ...
              ]
      //...
      }
      ```



#### SSH keep alive

In `~/.ssh/config` file, add

```bash
Host *
    ServerAliveInterval 40
```



#### Install `Chocolately` and `Scoop`

* [Chocolatey Software | Installing Chocolatey](https://chocolatey.org/install)
* [Scoop](https://scoop.sh/)
* 暂时关闭杀毒软件McAfee, and restart WT. The way to stop McAfee, is to stop real-time scanning and auto-update by clicking the gear icon.
* `Windows Terminal` run as admin: Taskbar > `SHIFT` + Right-click > ...
    * `WIN+<num>+Ctrl+Shift`

#### Powershell (PS 7) Configuration

==-----==

*If install powershell 7, please follow this instruction*: [给 PowerShell 带来 zsh 的体验 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/137251716)

now `oh-my-posh3` is also configured using [Themes | Oh my Posh 3](https://ohmyposh.dev/docs/themes)

**Other plugins & some important notices (e.g. proxy)** (including `z`, `sudo`, new `bucket`, new `shell`: [Windows Terminal美化+PowerShell插件配置 - DiaosSama's Blog](https://diaossama.work/2020/05/windows-terminal-powershell.html)

==-----==

**Deprecated**

~~The following is releated to *PS5*, while most of them are similar to *PS7*, so it's ok to reference them.~~

* ~~`notepad $PROFILE` to open profile for powershell: (simple configuration is shown as below)~~

  ```shell
  Import-Module posh-git # 引入 posh-git
  Import-Module oh-my-posh # 引入 oh-my-posh
  
  Set-Theme Powerlevel10k-Classic
  
  Set-PSReadLineOption -PredictionSource History # 设置预测文本来源为历史记录
   
  Set-PSReadlineKeyHandler -Key Tab -Function Complete # 设置 Tab 键补全
  Set-PSReadLineKeyHandler -Key "Ctrl+d" -Function MenuComplete # 设置 Ctrl+d 为菜单补全和 Intellisense
  Set-PSReadLineKeyHandler -Key "Ctrl+z" -Function Undo # 设置 Ctrl+z 为撤销
  Set-PSReadLineKeyHandler -Key UpArrow -Function HistorySearchBackward # 设置向上键为后向搜索历史记录
  Set-PSReadLineKeyHandler -Key DownArrow -Function HistorySearchForward # 设置向下键为前向搜索历史纪录
  
  # Alias for jumping to iCloud
  function Go-To-iCloud { cd C:\Users\jimmy\iCloudDrive\ }
  Set-Alias cd-icloud Go-To-iCloud
  
  # Alias for jumping to Notes
  function Go-To-Notes { cd C:\Users\jimmy\iCloudDrive\Notes\ }
  Set-Alias cd-notes Go-To-Notes
  
  # Alias for jumping to E:\share
  function Go-To-share { cd E:\share\ }
  Set-Alias cd-mnt Go-To-share
  ```

* ~~[Windows 终端 Powerline 设置 | Microsoft Docs](https://docs.microsoft.com/zh-cn/windows/terminal/tutorials/powerline-setup) 配置 `posh-git` and `oh-my-posh`~~

### Windows 修改注册表

```
win + R
regedit
```

#### 更改右键文件（夹）快捷键行为

[怎么删除右键出现的Open Folder as Intellij IDEA Project](https://blog.csdn.net/Piqzem/article/details/94554348)

> - 在注册表中打开“ 计算机 \ HKEY_CLASSES_ROOT \ Directory \ shell \ IDEA Community ”
> - 删除整个“IDEA Community”文件夹

### Apple iTunes Backup

#### Change backup location

* Default location: instead of `%appdata%\Apple Computer`, it is directly located under `<user>\Apple`.
* 建立链接：[iphone备份太大，严重挤占C盘空间，怎么办？ - 知乎](https://zhuanlan.zhihu.com/p/30324383)
    * 在Powershell 中，请使用`cmd /c mklink /J "<link>" "<target>"`, and make sure the directory of `<link>` does not exist (or say be created in advance)
    * More: `mklink /J` link directories  [Windows 中的 mklink 命令 | 始终](https://liam.page/2018/12/10/mklink-in-Windows/)
        * Similar to `ln` command in Linux

### 目录生成器 适用于添加到Markdown

`treer`: [markdown如何写出项目目录结构 - 简书](https://www.jianshu.com/p/e38a07f824a2)

或者命令`tree`

### 终端代理 proxychains

[一次解决所有代理问题](https://guangchuangyu.github.io/cn/2018/09/proxychains/)

### Github 访问速度慢解决方案

Link: [github访问加速 - 知乎](https://zhuanlan.zhihu.com/p/75994966)

**Search for IP Address**: [The Best IP Address, Email and Networking Tools - IPAddress.com](https://www.ipaddress.com/)

[git clone一个github上的仓库，太慢，经常连接失败，但是github官网流畅访问，为什么？ - 知乎](https://www.zhihu.com/question/27159393)

* 解决DNS污染：直接配置本地host

    * Linux/MacOS 请直接更改 `/etc/hosts`

    * Windows 请更改系统hosts文件(需管理员权限，VSCode在保存时可以选择save as admin)，路径：`C:\Windows\System32\drivers\etc\hosts`

        * 结束后，管理员身份运行 `ipconfig /flushdns` 手动刷新系统DNS缓存。

    * 主要配置前四个域名的ip地址映射，请自行通过上述链接查询ip

        * ```bash
      github.com
      github.global.ssl.fastly.net
      assets-cdn.github.com
      raw.githubusercontent.com
      gist.githubusercontent.com
      cloud.githubusercontent.com
      camo.githubusercontent.com
      ```

        * 其余域名如需要，请参考：[访问GitHub很慢的问题解决 | Bruce's Blog](https://a1049145827.github.io/2018/07/31/访问GitHub很慢的问题解决/)

* 可能依旧需要SSR服务

* 一般是1080端口，可以查询SSR选项

* 设置git全局代理（不推荐，仅限http, https）

  ```bash
  git config --global http.proxy http://127.0.0.1:1080
  git config --global https.proxy https://127.0.0.1:1080
  ```

  设置git全局代理（较推荐，仅针对github)

  ```bash
  git config --global http.https://github.com.proxy https://127.0.0.1:1080
  git config --global https.https://github.com.proxy https://127.0.0.1:1080
  ```

  取消全局代理

  ```bash
  git config --global --unset http.proxy
  git config --global --unset https.proxy
  ```

### Gvim (Not finished)

Link: [Vim：gvim安装配置（windows） - 整合侠 - 博客园](https://www.cnblogs.com/lizm166/p/8514129.html)

### Everything (A Global Search Software for Windows)

Link: [voidtools](https://www.voidtools.com/zh-cn/)

### 命令行跳转快捷键

* ctrl+a:光标移到行首
* ctrl+e:光标移到行尾

* ctrl+z : 把当前进程转到后台运行，使用’ fg ‘命令恢复。比如top -d1 然后ctrl+z ，到后台，然后fg,重新恢复

### Vim常用命令

###### 跳转

1. 跳到文本的**最后一行**：按“G”,即“shift+g”
2. 跳到**最后一行**的**最后**一个字符： 先重复1的操作即按“G”，之后按“$”键，即“shift+4”。
3. 跳到第一行的第一个字符：先**按两次“g”**，
4. 跳转到当前行的第一个字符：在当前行按“0”
5. `Ctrl-f`  即 PageDown 翻页
   `Crtl-b`  即 PageUp 翻页

###### 撤销

`u` 撤销上一步的操作
`Ctrl+r` 恢复上一步被撤销的操作

###### 查找

`/word` to search contents containing the word

`/\<word\>` to search the exact word

### Python常用函数

`dict.get(key, default=None)`: default 表示若找不到key则返回缺省值

### Python查看运行时间

###### `time.perf_counter`

* 以秒为单位，参考点未定义，因而用于计算两次连续调用之间的差值
* 具有最高分辨率的时钟，包括了在睡眠期间(sleep)和系统范围内流逝的时间

### pip

###### 生成requirements.txt文件

```bash
pip freeze > requirements.txt
```

###### 安装requirements.txt依赖

```bash
pip install -r requirements.txt
```

### 查询自己的公网ip

`curl ifconfig.me`

### Git 常用建议

###### `git add`

* `git add -u` 更新已track的文件 (或`git add --update`)
* `git add -A` 添加所有文件，包括新增的未track的文件

###### `git help`

`git help <command>`

* `git help -a`
* `git help -g`

###### `git branch`

* `git branch -M [<oldbranch>] <newbranch>`:  `-M` shortcut for `--move -m`, move/rename a branch and corresponding reflog(不知道这是什么)

###### `git config`

* `git config --global`

* `git config --list`

  ```bash
  git config --global user.name <name>
  git config --global user.email <email>
  ```


###### `git push`

* `git push -u origin <branch name>`
    * `-u` is equivalent to `--set-upstream`

###### `git reset`

* 撤销add后staged的文件

  ```bash
  git reset HEAD .
  git reset HEAD <filename>
  ```

###### `git stash`

* `git stash`会把所有未提交的修改（包括暂存的和非暂存的）都保存起来，用于后续恢复当前工作目录

  See: [git-stash用法小结 - Tocy - 博客园](https://www.cnblogs.com/tocy/p/git-stash-reference.html)

###### `git log`

* ```bash
  git log --graph --all
  ```

###### `git commit`

* 对最近一次commit进行修改

  ```bash
  git commit --amend
  ```

  [更改提交消息 - GitHub Docs](https://docs.github.com/cn/github/committing-changes-to-your-project/changing-a-commit-message)

###### `git fetch`

###### fatal: refusing to merge unrelated histories

```bash
git pull --allow-unrelated-histories
```

### apt 命令

###### 更改镜像源

查询版本号 `lsb_release -c`

[【Ubuntu】修改Ubuntu的apt-get源为国内镜像源的方法](https://blog.csdn.net/zgljl2012/article/details/79065174)

### 配置zsh

[写给工程师的 Ubuntu 20.04 最佳配置指南 - 知乎](https://zhuanlan.zhihu.com/p/139305626)

如果遇到443错误，使用国内镜像  [Ubuntu 关于ohmyzsh下载被443拒绝连接](https://blog.csdn.net/qq_35104586/article/details/103604964)

* 另[Oh My Zsh, 『 443:Connection Refused 错误无法安装 』 - 知乎](https://zhuanlan.zhihu.com/p/264161761)

### 配置vim

[chxuan/vimplus: An automatic configuration program for vim (github.com)](https://github.com/chxuan/vimplus)

### Shell

###### 命令执行和搜索机制

`shell`一般作为用户与内核之间的“桥梁”，通过shell命令（or程序语言）可以调用内核或使用已编译好的二进制文件（如`/bin/ls`，而这些二进制文件会通过诸如system call等方式调用内核）

有许多shell解释器（或语言，因其各有对应语法），如`/bin/sh`, `/bin/bash`, `/usr/bin/zsh`， 它们是如何启动的，这个流程过于复杂，暂时没研究清楚，参考资料[Zsh/Bash startup files loading order (.bashrc, .zshrc etc.) | Medium](https://medium.com/@rajsek/zsh-bash-startup-files-loading-order-bashrc-zshrc-etc-e30045652f2e)

###### 脚本第一行

```bash
#!/bin/bash
```

###### 变量

定义时不加美元符号，变量名和等号之间不能有空格

使用变量`$variable` or `${variable}`

```bash
readonly <variable> # make it const
unset <variable> # delete it except for readonly variable
```

###### 字符串

* 单引号内的任何字符都会原样输出，单引号字符串中的变量是无效的

* 单引号字串中不能出现单独一个的单引号（对单引号使用转义符后也不行），但可成对出现，作为字符串拼接使用

* 双引号里可以有变量，双引号里可以出现转义字符

  More: [Shell 变量 | 菜鸟教程](https://www.runoob.com/linux/linux-shell-variable.html)

###### 数组

仅支持一维数组

```bash
array_name=(value0 value1 value2 value3)
${数组名[下标]} # 读取
${array_name[@]} # 所有元素
# 取得数组元素的个数
length=${#array_name[@]}
# 或者
length=${#array_name[*]}
# 取得数组单个元素的长度
lengthn=${#array_name[n]}
```

亦有其它定义方式，见上面的连接

###### 脚本参数

```bash
$0 $1 $2 # $0为执行的文件名（含路径），后面依次为参数
$# # 参数个数
$$ # 脚本运行的当前PID
```

More: [Shell 传递参数 | 菜鸟教程](https://www.runoob.com/linux/linux-shell-passing-arguments.html)

###### 表达式运算

原生bash不支持简单的数学运算，但是可以通过其他命令来实现，例如 awk 和 expr，expr 最常用

```bash
val=`expr 2 + 2`
```

###### 中括号总结及比较参数

See [Shell 中的中括号用法总结 | 菜鸟教程](https://www.runoob.com/w3cnote/shell-summary-brackets.html)

###### PS1 PS2

命令提示符（一级和二级提示符），可以通过环境变量赋值更改`$PS1`,`$PS2`

###### 流程控制语句

See [Shell 流程控制 | 菜鸟教程](https://www.runoob.com/linux/linux-shell-process-control.html)



### Linux/Unix 常用命令

###### slash commands

To call the original command instead of any possible alias, e.g. `\grep` to avoid calling the alias defined by `alias grep='grep --color=auto'`

###### `--` argument

> The first `--` argument that is not an option-argument should be accepted as a delimiter indicating the end of options. Any following arguments should be treated as operands, even if they begin with the `-` character.

`man 1 bash` 指出`-`等价于`--`

> A `--` signals the end of options and disables further option processing. Any arguments after the `--` are treated as filenames and arguments. An argument of `-` is equivalent to `--`.

###### `ps` and `pstree`

```bash
ps -A # 列出所有进程
ps -e # 同上
ps -a # 列出当前终端下的所有进程
ps -u # 以用户为主的进程状态
ps -f # 更完整的输出
ps -ef
```

```bash
pstree -p # 显示PID
pstree -ap # 更详细
pstree -ap | less # 显示上下文
pstree -ap | grep <name or pid or ...>

pstree -ap $pid
```

See: [linux每日命令(34)：ps命令和pstree命令 - 博客园](https://www.cnblogs.com/huchong/p/10065246.html)

###### `kill`

* 通常，终止一个前台进程可以使用Ctrl+C键，但是，对于一个后台进程就须用kill命令来终止，我们就需要先使用ps/pidof/pstree/top等工具获取进程PID，然后使用kill命令来杀掉该进程

* kill命令是通过向进程发送指定的信号来结束相应进程的。在默认情况下，采用编号为`15`的TERM信号。TERM信号将终止所有不能捕获该信号的进程。对于那些可以捕获该信号的进程就要用编号为`9`的kill信号，强行“杀掉”该进程。

```bash
kill <PID>
kill -9 <PID> # 强制杀死进程，除了init进程

```

See: [每天一个linux命令（42）：kill命令 - 博客园](https://www.cnblogs.com/peida/archive/2012/12/20/2825837.html)

###### `which`

###### `type`

```bash
type -a
```

###### `/etc/passwd`

```bash
cat /etc/passwd
```

第六列是home directory 即`~`

###### `env`

列出所有环境变量

in order to use your anaconda version of python type the following command

```bash
sudo env "PATH=$PATH" python <enter python command>
```



###### `chmod`, `chown`, `chgrp`

```bash
chmod +x test.sh
./test.sh
chown username_or_uid file # set the owner of file to be certain user
chgrp group_or_gid file # .. the group of ..
```

###### `usermod`

```bash
sudo usermod -a -G groupName userName
# The -a (append) switch is essential. Otherwise, the user will be removed from any groups, not in the list.
```



###### `wc`

输出文件的行数、字数、字符数(byte)、文件名

###### `users`, `who`, `w`

了解登录到计算机的所有用户的信息

```bash
who -r # 查询系统处于什么运行级别
```

###### `uname`

print system information

* -r内核 -m 32位还是64位 -a所有信息, -n主机名

###### `free`

```bash
free -m # 查询内存状态
```

###### `grep` & 正则表达式

```bash
grep -rnw '/path/to/somewhere' -e 'pattern'
# -r or -R is recursive
# -n is line number
# -w whole word
# -l is to just give file name of matching files
grep -o 'pattern'
# -o print only the matched parts of a matching line
grep --exclude=\*.sh -rnw . -e 'pattern'
grep --include=\*.{c,h} -rnw 'path' -e 'pattern' # only search .c / .h files
grep --exclude-dir={dir1,dir2,*.dst} -rnw . -e 'p'
```

[Regular Expression website with explanation and wiki](https://regex101.com/)

> `^word` ：表示搜索以word开头的内容
>
> `word$` 表示搜索以word结尾的内容
>
> `^$`   表示的是**空行**，不是空格
>
> `.`   代表**且**只能代表任意一个字符
>
> `\`   转义字符，让有着特殊身份意义的字符，脱掉马甲，还原原型。例如\.只表示原始小数点意义
>
> `*` 表示重复0个或多个**前面**的一个字符。**不代表所有**
>
> `.*`  表示匹配**所有**的字符
>
> `^.*` 表示以任意字符开头
>
> `[任意字符]` 匹配字符集内任意一个字符，如`[a-z]`
>
> `[^abc]` `^`在中括号里面是非的意思，不包含之意。意思就是不包含a或b或c的行
>
> {n，m} 表示重复n到m次前一个字符，`{n}`至少n次，多了不限，`{,m}`至多m次
>
> 注：使用grep或sed要对`{}`转义，即`\{\}`，egrep就不需要转义了

###### `find`

```bash
find . -maxdepth 1 -name <name>
```



###### `ls` & long format

```
ls -laihH
```

long format 具体解释：[ls -- list file and directory names and attributes (mkssoftware.com)](https://www.mkssoftware.com/docs/man1/ls.1.asp)

###### `lsattr`, `chattr`

> Linux内核中有大量安全特征。EXT2/3/4**文件系统的扩展属性**（Extended Attributes）可以在某种程度上保护系统的安全
>
> **常见的扩展属性：**
>
> - A（Atime）：告诉系统不要修改对这个文件的最后访问时间。
    >   - **使用A属性可以提高一定的性能**。
> - S（Sync）：一旦应用程序对这个文件执行了写操作，使系统立刻把修改的结果写到磁盘。
    >   - **使用S属性能够最大限度的保障文件的完整性**。
> - a（Append Only）：系统只允许在这个文件之后追加数据，不允许任何进程覆盖或者截断这个文件。如果目录具有这个属性，系统将 只允许在这个目录下建立和修改文件，而不允许删除任何文件。
> - i（Immutable）：系统不允许对这个文件进行任何的修改。如果目录具有这个属性，那么任何的进程只能修改目录之下的文件，不允许建立和删除文件。
    >   - **a属性和i属性对于提高文件系统的安全性和保障文件系统的完整性有很大的好处**。
>
> - 显示扩展属性：`lsattr [-adR] [文件|目录]`
> - 修改扩展属性：`chattr [-R] [[-+=][属性]] <文件|目录>`

###### `lsof`

[lsof 一切皆文件 — Linux Tools Quick Tutorial](https://linuxtools-rst.readthedocs.io/zh_CN/latest/tool/lsof.html)

###### `ln` (硬链接&软链接)

图文详情：[Linux ln 命令 博客园 ](https://www.cnblogs.com/sparkdev/p/11275722.html)

默认硬链接(hard link)，即创建新的文件名指向同一个inode，不占用inode或block空间

> 由于硬链接只是在目录中添加了一条包含文件名和 对应 inode 的记录，所以它几乎不会消耗额外的磁盘容量。
> 另外在删除硬链接所关联的文件时，其实只是删除了一条目录中的记录，真正的文件并不受影响。只有在删除最后一个硬链接时才会真正删除文件的内容数据。

* 仅可以在同一个文件系统中有效

* 不可给目录创建硬链接

  > 由于这两个限制，实际使用中硬链接并没有软链接使用的广泛

  ```bash
  ln <source file or directory> <target>
  ```

软链接(symbolic link)

复制一份inode和占用一个新的data block（该block存储源文件的inode地址）

* 可以指向目录且可以跨文件系统

* 创建软链接并不增加原文件的链接数

```bash
ln -s <source> <target>
```



###### `df`, `stat`

```bash
df -ih # list inode info instead of block usage
stat file # display file or file system status
```

###### `tr`

对来自标准输入的字符进行替换、压缩和删除

###### `sudo`, `su`

```bash
su
sudo -s # both run the shell (generally) as a superuser, this solves the error generated by `sudo cd ...`
su - # this will change the environment variable, essentially it starts the shell as a login shell
```

More: [sudo: cd: command not found-CSDN博客](https://blog.csdn.net/gatieme/article/details/49106865)

###### `awk`

[awk 入门教程 - 阮一峰的网络日志 ](https://www.ruanyifeng.com/blog/2018/11/awk.html)

> [`awk`](https://en.wikipedia.org/wiki/AWK)是处理文本文件的一个应用程序，几乎所有 Linux 系统都自带这个程序。
>
> 它依次处理文件的每一行，并读取里面的每一个字段。对于日志、CSV 那样的每行格式相同的文本文件，`awk`可能是最方便的工具。

```bash
awk '{print $0}' # 将标准输入打印一遍
awk -F ':' '{ print $1 }' demo.txt # 以冒号为分隔符(field separator)，提取每一行的第一个字段
$NF # 当前行有多少个字段
awk -F ':' '{print $1, $(NF-1)}' demo.txt # 倒数第二个字段
awk -F ':' '{print NR ") " $1}' demo.txt # 显示当前处理的是第几行

awk -F ':' '/usr/ {print $1}' demo.txt # 正则表达式过滤器
awk -F ':' 'NR % 2 == 1 {print $1}' demo.txt # 输出奇数行
awk -F ':' '$1 == "root" || $1 == "bin" {print $1}' demo.txt
awk -F ':' '{if ($1 > "m") print $0; else print "---"}' demo.txt # if-else语句
ping 192.168.X.X | awk '{ print $0"\t" strftime("%Y:%m:%d-%H:%M:%S",systime()) fflush() } '>ping.log # 时间戳
```

###### `curl`

> curl is a tool to transfer data from or to a server

```bash
curl https://www.example.com # 不带有任何参数时，curl 就是发出 GET 请求
-s # silent
-S # show error message
-L # redo curl if receiving redirection response
-f # fail silently

-i # also print HTTP response header
```

###### `tee`

tee指令会从标准输入设备读取数据，将其内容输出到标准输出设备，同时保存成文件

对比`cat`命令

###### `cat`

cat（英文全拼：concatenate）命令用于连接文件并打印到标准输出设备上

###### `tar`

归档

```bash
tar -c [-f Archive] File # basic syntax (-c for creation)
tar -cvf /mydata/etc.tar /etc # frequent used form
# -v for verbosely list files processed
```

压缩

```bash
tar -zcvf /mydata/etc.tar.gz /etc # use gzip
tar -jcvf /mydata/etc.tar.bz2 /etc # use bzip2
```

解压

```bash
tar -zxvf /mydata/etc.tar.gz # 解压到当前文件夹 (-x for extract)
tar -zxvf /mydata/etc.tar.gz -C /mydata/etc # 解压到指定文件夹 (-C for changing to the specified directory to perform any operations, this option is order-sensitive)
```

###### `tree`

```bash
tree -L <层数> -d <目录> # 可能需要apt install
```

###### `tmux`

```bash
tmux # 创建一个默认tmux会话及打开该窗口
exit 或 ctrl+d # 退出tmux窗口
ctrl+b ? # 帮助命令
tmux new -s <session-name> # 创建指定名称地会话
tmux detach 或 ctrl+b d# 分离会话与该窗口
tmux ls # list all sessions

# 重新接入已存在的会话
tmux attach -t <session-id or session-name>
tmux a

tmux kill-session -t <session-id or session-name> # kill session
tmux switch -t <session-id or session-name> # switch session
tmux rename-session -t <session-id> <new-name>
```

窗口分屏等其它特性和配置：[Tmux 使用教程 - 阮一峰的网络日志](http://www.ruanyifeng.com/blog/2019/10/tmux.html)

###### `cp`

```bash
cp -r dir1 dir2 # copy recursively
```



### Linux/Unix基本概念

##### 文件系统

[Linux EXT2 文件系统 - sparkdev - 博客园](https://www.cnblogs.com/sparkdev/p/11212734.html)

###### 查看文件系统格式

```bash
mount
cat /etc/fstab
```

###### block

操作系统读取磁盘时的最小单位，一般约4KB，由若干sector组成；sector是磁盘存储的最小单位，一般约512B

###### inode

![“inode”的图片搜索结果](img/1493710190_10-34.jpg)

![img](img/952033-20190726130127224-428242951.png)

[Linux 文件与目录 - sparkdev - 博客园](https://www.cnblogs.com/sparkdev/p/11249659.html)

存储文件的元信息，中文译名：索引节点；存储内容包括链接数，即有多少文件名指向该inode，文件数据block的位置，权限等信息（除了文件名）

inode本身也会消耗磁盘空间，可用`df -i`查询，一般一个inode的大小为128/256字节（Byte），可用`sudo dumpe2fs -h <filesystem_like_/dev/sda5> | grep "Inode size"`

###### major & minor number

Character or block device 的 major number identifies the driver (驱动) with this device. 内核根据major number在`open`的时候用来选择对应的驱动

而minor number只有driver会使用（kernel不会收到这个参数），用来让驱动区分具体这是哪个device

##### 环境变量

The environment variables of a process exist at runtime, and are not stored in some file or so. They are stored in the process's own memory (that's where they are found to pass on to children). But there is a virtual file in

```bash
/proc/pid/environ
```

`env` 可以显示环境变量

##### 根目录的子目录

[Ubuntu根目录下各文件夹的功能详细介绍 - Yudar - 博客园](https://www.cnblogs.com/yudar/p/5809219.html)

英文参考 [Filesystem Hierarchy Standard - Wikipedia](https://en.wikipedia.org/wiki/Filesystem_Hierarchy_Standard)

注意到`Ubuntu 20.04`已有改动，包括建立`/bin`至`/usr/bin`的软链接(symbolic link)等

* `/etc`存放配置文件

* `/var` 包含正在操作的文件，还有记录文件、加密文件、临时文件

* `/proc` 虚拟目录，该目录实际上指向内存而不是硬盘

    * /proc/cpuinfo 处理器的信息

      /proc/devices 当前运行内核的所有设备清单

      /proc/dma 当前正在使用中的DMA通道

      /proc/filesystem 当前运行内核所配置的文件系统

      /proc/interrupts 当前使用的中断和曾经有多少个中断

      /proc/ioports 正在使用的I/O端口

##### 动态链接库

##### 与用户账号有关的系统文件（查看用户/用户组）

######  /etc/passwd——用户账户文件

每个用户都在文件/etc/passwd中有一个对应的记录行，它记录了这个用户的一些基本属性。这个文件对所有用户可读，查看命令为：

```shell
cat /etc/passwd
```

可以看到如下所示的输出：

```shell
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
stu1:x:1001:1001::/media/StudentGroup/stu1/:
stu2:x:1002:1001:I_love_this_test:/media/StudentGroup/stu2/:/bin/bash
```

可以看出，一行记录对应着一个用户，每行记录又被冒号(:)分隔为7个字段，其格式和具体含义如下：
用户名:口令:用户标识号:组标识号:注释性描述:主目录:登录Shell

######  /etc/group——用户组文件

每个用户组会对应文件/etc/group中的一行记录，查看方式如下：

```shell
cat /etc/group
```

此文件的格式也类似于/etc/passwd文件，由冒号(:)隔开若干个字段，这些字段有：
组名:口令:组标识号:组内用户列表

######  /etc/shadow

/etc/shadow中的记录与/etc/passwd中的记录一一对应，并且只有超级管理员才有权限查看，记录着每个用户更为隐私的信息。
它的文件格式与/etc/passwd类似，由若干个字段组成，字段之间用":"隔开。这些字段是：
登录名:加密口令:最后一次修改时间:最小时间间隔:最大时间间隔:警告时间:不活动时间:失效时间:标志。

##### Add User to Group

[How to add existing user to an existing group? - Ask Ubuntu](https://askubuntu.com/questions/79565/how-to-add-existing-user-to-an-existing-group)

```bash
sudo usermod -a -G groupName userName
# The -a (append) switch is essential. Otherwise, the user will be removed from any groups, not in the list.
```



### 虚拟机(mainly VMWare)

##### 虚拟机网络模式

[实例讲解虚拟机3种网络模式(桥接、nat、Host-only) - 博客园](https://www.cnblogs.com/ggjucheng/archive/2012/08/19/2646007.html)

[NAT模式、路由模式、桥接模式 区别对比-CSDN博客](https://blog.csdn.net/bytxl/article/details/35569217)

VMWare 配置：编辑>虚拟网络编辑器

[NAT vs. bridged network: A simple diagram (techgenix.com)](http://techgenix.com/nat-vs-bridged-network-a-simple-diagram-178/)

###### 桥接

###### NAT

###### Host-Only

### Docker

<img src="img/image-20210208151214195.png" alt="image-20210208151214195" style="zoom:50%;" />

> 图源[Docker 架构 | 菜鸟教程](https://www.runoob.com/docker/docker-architecture.html)
>
> docker machine is deprecated / superseded

###### apk和pip下载慢

Dockerfile中添加

```dockerfile
RUN sed -i 's/dl-cdn.alpinelinux.org/mirrors.aliyun.com/g' /etc/apk/repositories
RUN pip config set global.index-url https://mirrors.aliyun.com/pypi/simple \
	&& pip config set install.trusted-host mirrors.aliyun.com
```

###### alpine apk 其它问题

[alpine的Docker镜像使用避坑汇总](https://juejin.cn/post/6850418112237502472)

###### Dockerfile

[Dockerfile reference | Docker Documentation](https://docs.docker.com/engine/reference/builder/)

> Docker can build images automatically by reading the instructions from a `Dockerfile`. A `Dockerfile` is a text document that contains all the commands a user could call on the command line to assemble an image. Using `docker build` users can create an automated build that executes several command-line instructions in succession.

###### Compose file

[Compose file | Docker Documentation](https://docs.docker.com/compose/compose-file/)

###### Volume

<img src="img/image-20210209110045049.png" alt="image-20210209110045049" style="zoom:50%;" />

It will be mounted to (by default) `/var/lib/docker` `volumes` sub-directories; otherwise, specify the directory explicitly like `/data`.

* [Volume | Blog](https://larrylu.blog/using-volumn-to-persist-data-in-container-a3640cc92ce4)
* [Use volumes | Docker Documentation](https://docs.docker.com/storage/volumes/)

##### `docker-compose`

* under running directory `docker-compose up -d`, where `-d` means detached mode

* `docker-compose ps` to view all containers / services

* `docker-compose stop` to stop services once started with `-d` option

  [Compose command-line reference | Docker Documentation](https://docs.docker.com/compose/reference/)

### PostgreSQL

###### Installation on Ubuntu

[Install PostgreSQL on Ubuntu](https://www.postgresqltutorial.com/install-postgresql-linux/)

default port 5432

### Wiki.js

[Wiki.js](https://js.wiki/)

Just follow the official documentation, while PostgreSQL does not officially support searching for Chinese (plugin for postgres is needed) and the features are not quite satisfied for my demand. At least Typora is much better in terms of editing.

### Shadowsocks

> Shadowsocks是一种基于Socks5代理方式的网络数据加密传输包，并采用Apache许可证、GPL、MIT许可证等多种自由软件许可协议开放源代码。shadowsocks分为服务器端和客户端，在使用之前，需要先将服务器端部署到服务器上面，然后通过客户端连接并创建本地代理。目前包使用Python、C、C++、C#、Go语言等编程语言开发。

利用Socks5协议（TCP/IP模型中应用层的协议），本身是不安全的，于是引入了sslocal，local默认监听localhost的1080端口，并代理（在windows上默认影响系统代理）

但看起来，windows上目前是用http进行本地代理的，不只是Socks5（IE不支持Socks5代理）

浏览器一般自动启动系统代理，其它软件一般需要手动配置

> Socks5客户端 <---socks5---> sslocal <–密文–> ss-server <—正常请求—> 目标主机
>
> Shadowsocks的处理方式是将Socks5客户端与Socks5服务器的连接提前，Socks5协议的交互完全是在本地进行的，在网络中传输的完全是利用加密算法加密后的密文，这就很好的进行了去特征化，使得传输的数据不是很容易的被特征识别。

<img src="img/image-20210126155343521.png" alt="image-20210126155343521" style="zoom: 50%;" />

[SS和SSR的原理 | A Big Boy Blog](https://sulangsss.github.io/2018/12/18/Network/SS-SSR 原理/)

[shadowsocks实现原理 | Hexo](https://bingtaoli.github.io/2016/11/23/shadowsocks实现原理/)

<img src="img/image-20210126162307483.png" alt="image-20210126162307483" style="zoom: 25%;" />

[Shadowsocks代理方式 - vimcaw的个人博客](https://vimcaw.github.io/blog/2017/08/13/ShadowsocksR代理方式/)

#### PAC

#### Socket 代理

> 代理分为HTTP代理和SOCKET代理
>
>   HTTP代理是在HTTP协议层的代理服务，只能处理HTTP/HTTPS请求，主要满足用户Web浏览网页需求，由于只处理HTTP请求，处理速度极快。
>   SOCKET代理不解析网络流量，传递数据包而并不关心是何种应用协议,这使得SOCKET代理可以用于多种环境，支持FTP、SMTP、HTTP等，也支持QQ、BT下载等多种应用，典型的有Shadowsocks。通常分为socks 4 和socks 5两种类型，socks 4只支持TCP协议而socks 5支持TCP/UDP协议，还支持各种身份验证机制等协议



### Windows Checksum 效验

```bash
certUtil -hashfile <filename> <algorithm> # built-in command for windows 10
get-filehash -algorithm <algorithm> <filename> # built-in for powershell
# algorithm can take SHA256 MD5 etc
```

### Nginx

[Ubuntu安装配置Nginx（一）——部署Web服务 - SegmentFault 思否](https://segmentfault.com/a/1190000015797789)

[nginx快速入门之配置篇 - 知乎](https://zhuanlan.zhihu.com/p/31202053)

### Supervisor

👍[Python 进程管理工具 Supervisor 使用教程 - restran - 博客园](https://www.cnblogs.com/restran/p/4854623.html)

### InfluxDB

#### 查询语句速览

[influxdb的基本使用 - 简书 (jianshu.com)](https://www.jianshu.com/p/721e4ce4c066)

#### Documentation

Root URL of the Doc. [InfluxDB OSS 1.8 Documentation (influxdata.com)](https://docs.influxdata.com/influxdb/v1.8/)

#### 数据迁移

[influxdb基础（五）——数据的备份与恢复（influxd backup/influxd restore）-CSDN博客](https://blog.csdn.net/weixin_36586120/article/details/109481345)

#### CLI

主要关于启动CLI：[Using influx - InfluxDB command line interface | InfluxDB OSS 1.8 Documentation](https://docs.influxdata.com/influxdb/v1.8/tools/shell/)

#### InfluxQL

This section introduces InfluxQL, the InfluxDB SQL-like query language for working with data in InfluxDB databases.

[Influx Query Language (InfluxQL) | InfluxDB OSS 1.8 Documentation](https://docs.influxdata.com/influxdb/v1.8/query_language/)

**Line Protocol**

[InfluxDB line protocol tutorial | InfluxDB OSS 1.8 Documentation](https://docs.influxdata.com/influxdb/v1.8/write_protocols/line_protocol_tutorial/)

* `insert into <retention policy> <line protocol>`
* line protocol = `<measurement>,[<tag set>] <field set> [timestamp]`
* field set is a must
* tag set and timestamp are optional

**SELECT and FROM clause**

[Explore data using InfluxQL | InfluxDB OSS 1.8 Documentation](https://docs.influxdata.com/influxdb/v1.8/query_language/explore-data/)

* `FROM <database_name>.<retention_policy_name>.<measurement_name>`

* `FROM <database_name>..<measurement_name>`

* `SELECT *::field`

* > A query requires at least one [field key](https://docs.influxdata.com/influxdb/v1.8/concepts/glossary/#field-key) in the `SELECT` clause to return data. If the `SELECT` clause only includes a single [tag key](https://docs.influxdata.com/influxdb/v1.8/concepts/glossary/#tag-key) or several tag keys, the query returns an empty response. This behavior is a result of how the system stores data.



**GROUP BY clause**

> **Note:** You cannot use `GROUP BY` to group fields.

**GROUP BY tags**

**GROUP BY time()**

[Explore data using InfluxQL | InfluxDB OSS 1.8 Documentation](https://docs.influxdata.com/influxdb/v1.8/query_language/explore-data/#group-by-time-intervals)

**INTO clause**

[Explore data using InfluxQL | InfluxDB OSS 1.8 Documentation](https://docs.influxdata.com/influxdb/v1.8/query_language/explore-data/#examples-4)

**Rename a database**

```sql
SELECT * INTO "copy_NOAA_water_database"."autogen".:MEASUREMENT FROM "NOAA_water_database"."autogen"./.*/ GROUP BY *
```

* `GROUP BY *` here preserves the tags from automatically transforming into fields

**Other Usage**

**specify a tag with None value**

###### [Use a regular expression to specify a tag with no value in the WHERE clause](https://docs.influxdata.com/influxdb/v1.8/query_language/explore-data/#use-a-regular-expression-to-specify-a-tag-with-no-value-in-the-where-clause)

```sql
SELECT * FROM "h2o_feet" WHERE "location" !~ /./
```

###### Gossip

**show series**

```sql
SHOW series
```

**show all keys given a tag key**

```sql
SHOW tag values from <measurements> with KEY=<key_name>
```

**Others**

`service influxdb start` to start influxdb daemon

`influx -precision rfc3339` to start influxdb CLI

`0.0.0.0` 比 `127.0.0.1` 好用... 可以连接到外网，TODO: 请查明原因

### How to edit root file with vim

```bash
:w !sudo tee % > /dev/null
```

* tee指令会从标准输入设备读取数据，将其内容输出到标准输出设备，同时保存成文件

* `%` means "the current file name"

* The `> /dev/null` part **explicitly** throws away the standard output

* You can add this to your `.vimrc` to make this trick easy-to-use: just type `:w!!`.

  ```bash
  " Allow saving of files as sudo when I forgot to start vim using sudo.
  cmap w!! w !sudo tee > /dev/null %
  ```

[How does the vim "write with sudo" trick work? - Stack Overflow](https://stackoverflow.com/questions/2600783/how-does-the-vim-write-with-sudo-trick-work)

### Use sudo with redirection

[How do I use sudo to redirect output to a location I don't have permission to write to?](https://stackoverflow.com/questions/82256/how-do-i-use-sudo-to-redirect-output-to-a-location-i-dont-have-permission-to-wr)

```bash
sudo sh -c 'ls -hal /root/ > /root/test.out' # use shell with -c
sudo ls -hal /root/ | sudo tee /root/test.out > /dev/null # use tee with > /dev/null
```

### 时间同步

[Linux系统时间同步的两种方法-Linux运维日志](https://www.centos.bz/2017/08/linux-time-sync/)

```bash
date -R # 查询时间及时区
tzselect # 查询时区对应文件名
cp /usr/share/zoneinfo/Asia/Shanghai /etc/localtime # 配置时区
```

### Linux下删除文件

> Linux系统是通过link的数量来控制文件删除的，只有当一个文件不存在任何link的时候，这个文件才会被删除。一般来说每个文件两个link计数器来控制i_count和i_nlink。当一个文件被一个程序占用的时候i_count就加1。当文件的硬链接多一个的时候i_nlink也加1。删除一个文件，就是让这个文件，没有进程占用，同时i_link数量为0

### 语义化版本(SemVer)

[语义化版本 2.0.0 | Semantic Versioning (semver.org)](https://semver.org/lang/zh-CN/)

* `1.0.0`起，公开API基本稳定；`0.*.*`说明API不稳定，可以不遵循SemVer，一般不使用`0.0.*`以保留他用
* 每一个大版本更新，即`x.y.z`中的x，意味着API不向下兼容
* 每一次更改API但保持向下兼容，则更新`x.y.z`中的y
* 每一次修复API内部实现，则更新`x.y.z`中的z
* 可以添加`-`后缀用来反应`pre-release`等信息，如`1.0.0-alpha.1`
    * Example: `1.0.0-alpha < 1.0.0-alpha.1 < 1.0.0-alpha.beta < 1.0.0-beta < 1.0.0-beta.2 < 1.0.0-beta.11 < 1.0.0-rc.1 < 1.0.0`
* Meta-data 使用 `+`后缀，如`1.0.0-alpha+001, 1.0.0+20130313144700, 1.0.0-beta+exp.sha.5114f85, 1.0.0+21AF26D3—-117B344092BD`
* RegExp: https://regex101.com/r/Ly7O1x/3/ (Support PCRE [Perl Compatible Regular Expressions, i.e. Perl, PHP and R], Python and Go)

### REST

###### Constraints

1. Client-Server
2. Stateless
    1. Each request from client to server must contain all of the information necessary to understand the request, and cannot take advantage of any stored context on the server.
    2. Session state is therefore kept entirely on the client.
    3. Disadvantage:
        1. decrease network performance
        2. hard to maintain consistent application behavior since app becomes dependent on the correct implementation of semantics across multiple client versions
3. Cache
    1. If a response is cacheable, then a client cache is given the right to reuse that response data for later, equivalent requests
    2. Disadvantage: decrease reliability if stale data within the cache differs significantly from the data that would have been obtained had the request been sent directly to the server
4. Uniform Interface
    1. Advantage: the overall system architecture is simplified and the visibility of interactions is improved
    2. Disadvantage: a uniform interface degrades efficiency, since information is transferred in a standardized form rather than one which is specific to an application's needs
        1. The REST interface is designed to be efficient for large-grain hypermedia data transfer, optimizing for the common case of the Web, but resulting in an interface that is not optimal for other forms of architectural interaction
5. Layered System
    1. Disadvantage: latency
        1. Solution: cache
    2. Advantage: add security policies easily like firewalls
6. Code-On-Demand

###### 资源（Resources）

REST的名称"表现层状态转化"中，省略了主语。"表现层"其实指的是"资源"（Resources）的"表现层"。

**所谓"资源"，就是网络上的一个实体，或者说是网络上的一个具体信息。**它可以是一段文本、一张图片、一首歌曲、一种服务，总之就是一个具体的实在。你可以用一个URI（统一资源定位符）指向它，每种资源对应一个特定的URI。要获取这个资源，访问它的URI就可以，因此URI就成了每一个资源的地址或独一无二的识别符。

所谓"上网"，就是与互联网上一系列的"资源"互动，调用它的URI。

###### 表现层（Representation）

"资源"是一种信息实体，它可以有多种外在表现形式。**我们把"资源"具体呈现出来的形式，叫做它的"表现层"（Representation）。**

比如，文本可以用txt格式表现，也可以用HTML格式、XML格式、JSON格式表现，甚至可以采用二进制格式；图片可以用JPG格式表现，也可以用PNG格式表现。

URI只代表资源的实体，不代表它的形式。严格地说，有些网址最后的".html"后缀名是不必要的，因为这个后缀名表示格式，属于"表现层"范畴，而URI应该只代表"资源"的位置。它的具体表现形式，应该在HTTP请求的头信息中用Accept和Content-Type字段指定，这两个字段才是对"表现层"的描述

###### 状态转化（State Transfer）

访问一个网站，就代表了客户端和服务器的一个互动过程。在这个过程中，势必涉及到数据和状态的变化。

互联网通信协议HTTP协议，是一个无状态协议。这意味着，所有的状态都保存在服务器端。因此，**如果客户端想要操作服务器，必须通过某种手段，让服务器端发生"状态转化"（State Transfer）。而这种转化是建立在表现层之上的，所以就是"表现层状态转化"。**

客户端用到的手段，只能是HTTP协议。具体来说，就是HTTP协议里面，四个表示操作方式的动词：GET、POST、PUT、DELETE。它们分别对应四种基本操作：**GET用来获取资源，POST用来新建资源（也可以用于更新资源），PUT用来更新资源，DELETE用来删除资源。**

[RESTful API 设计指南 - 阮一峰](http://www.ruanyifeng.com/blog/2014/05/restful_api.html)

### 如何查看ECDSA的fingerprint

```bash
ssh-keygen -l -f /etc/ssh/ssh_host_ecdsa_key.pub
```

### 使用SCP copy files from remote to local with port specified

```bash
scp -P 24011 -r root@server.acemap.cn:/root/data/influx_backup ./
```

### NPM

###### 镜像

[npm镜像源管理 - 简书 (jianshu.com)](https://www.jianshu.com/p/66f97cadd1eb)

修改registry地址，比如修改为淘宝镜像源。
`npm set registry https://registry.npm.taobao.org/`
如果有一天你肉身FQ到国外，用不上了，用rm命令删掉它
`npm config rm registry`

###### 奇怪问题

ENOTSUP 解决：`npm install -no-bin-links`

### 其它名词解释

###### Blob

* Binary Large OBject

###### VPS

* Virtual private server

  > 虚拟专用服务器，是将一台服务器分割成多个虚拟专用服务器的服务。实现VPS的技术分为容器技术和虚拟机技术。在容器或虚拟机中，每个VPS都可分配独立公网IP地址、独立操作系统、实现不同VPS间磁盘空间、内存、CPU资源、进程和系统配置的隔离，为用户和应用程序模拟出“独占”使用计算资源的体验。

###### 语法糖 Syntactic Sugar

> **语法糖**（英语：Syntactic sugar）是由英国[计算机科学家](https://zh.wikipedia.org/wiki/计算机科学家)[彼得·兰丁](https://zh.wikipedia.org/wiki/彼得·兰丁)发明的一个术语，指[计算机语言](https://zh.wikipedia.org/wiki/计算机语言)中添加的某种语法，这种语法对语言的功能没有影响，但是更方便程序员使用。语法糖让程序更加简洁，有更高的可读性