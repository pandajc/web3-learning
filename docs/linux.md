
#### 基础命令
```
pwd 当前目录

cd /home/ubuntu
cd .
cd ..
cd ~  家目录
cd -  (上一个目录)：这将带您回到您刚刚所在的上一个目录

ls -a  显示所有文件（包括隐藏文件）
ls -l  以长格式显示文件和目录信息
ll
ls -la  显示所有文件（包括隐藏文件），并以长格式显示

touch test.txt  创建一个名为 test.txt 的空文件
file test.txt  显示 test.txt 文件的类型
cat test.txt  显示 test.txt 文件的内容，它不适合查看大文件，只适用于短内容

less test.txt  分页显示 test.txt 文件的内容，适合查看大文件
q - 用于退出 less 并返回到您的 shell。
Page up, Page down, Up 和 Down - 使用箭头键和翻页键导航。
g - 移动到文本文件的开头。
G - 移动到文本文件的末尾。
/search - 您可以在文本文档中搜索特定文本。在您要搜索的单词前加上 /。
h - 如果您在使用 less 时需要一些关于如何使用 less 的帮助，请使用 help。

grep a test.txt |less  分页显示 test.txt 文件中包含字母 a 的行


history 命令历史记录
想运行之前执行过的相同命令吗？只需按向上箭头键。
想运行上一个命令而无需再次输入吗？使用 !!
clear 清除显示


cp mycoolfile /home/pete/Documents/cooldocs
cp -r Pumpkin/ /home/pete/Documents  递归复制目录中的文件和目录
cp -i mycoolfile /home/pete/Pictures  如果不想被意外覆盖的文件，可以使用 -i 标志（交互式）在覆盖文件之前提示您


mv directory1 directory2  重命名或移动文件/文件夹
mv -i directory1 directory2 如果你 mv 一个文件或目录，它会覆盖同一目录中的任何内容。因此，你可以使用 -i 标志在覆盖任何内容之前提示你
mv -b directory1 directory2 假设你确实想 mv 一个文件来覆盖前一个文件。你也可以备份该文件，它只会将旧版本重命名为带 ~ 的文件

mkdir books paintings  同时创建多个目录
mkdir -p books/hemmingway/favorites 使用 -p（父标志）同时创建子目录

rm file1
rm -f file1 选项-f 或 force 告诉 rm 删除所有文件，无论它们是否受写保护，而无需提示用户（只要您有适当的权限）。
rm -i file  添加 -i 标志，就像许多其他命令一样，会提示您是否真的要删除文件或目录。

rm -r directory 默认情况下，您不能直接 rm 一个目录；您需要添加 -r 标志（recursive）来删除其中的所有文件和任何子目录。
rmdir directory 您可以使用 rmdir 命令删除目录。

find /home -name puppies.jpg  使用 find 命令时，您必须指定要搜索的目录以及要查找的内容
find /home -type d -name MyFolder 您可以指定要查找的文件类型
```

#### 系统管理
```
help echo 这将为您提供 echo 命令的描述以及您可以使用的选项。对于其他可执行程序，约定是有一个名为 --help 或类似名称的选项。
bash --help

man ls 可以使用 man 命令查看某个命令的手册
whatis cat 提供命令行程序的简要描述

alias foobar='ls -la'  如果您需要多次输入一个长命令，最好为此使用别名。要为命令创建别名，您只需指定一个别名名称并将其设置为该命令
unalias foobar 删除别名

exit  要退出 shell，你可以使用 exit 命令或
logout

grep 命令可能是您将使用的最常见的文本处理命令。它允许您在文件中搜索与特定模式匹配的字符。如果您想知道某个文件是否存在于某个目录中，或者想查看某个字符串是否在文件中找到，该怎么办？您当然不会逐行查找文本；您会使用 grep！
grep fox sample.txt  您应该会看到 grep 在 sample.txt 文件中找到了"fox"。
grep -i somepattern somefile  使用 -i 标志进行不区分大小写的 grep 模式搜索
env | grep -i User  如您所见，grep 非常通用。您甚至可以在模式中使用正则表达式：
ls /somedir | grep '.txt$'  这应该会返回 somedir 中所有以 .txt 结尾的文件。
```

#### 进程管理
```
ps aux  进程，a 显示所有正在运行的进程，包括其他用户运行的进程。u 显示更多关于进程的详细信息。最后，x 列出所有没有关联 TTY 的进程。这些程序将在 TTY 字段中显示 ?；它们在作为系统启动一部分启动的守护进程中最常见

kill -9 12445 
SIGHUP 或 HUP 或 1: Hangup
SIGINT 或 INT 或 2: Interrupt
SIGKILL 或 KILL 或 9: Kill
SIGSEGV 或 SEGV 或 11: Segmentation fault
SIGTERM 或 TERM 或 15: Software termination
SIGSTOP 或 STOP: Stop

sleep 1000 & 在命令后附加一个和号 (&) 将使其在后台运行，这样您仍然可以使用 shell
jobs  查看所有后台作业
fg %1 将作业 1 切换到前台（%1 是作业编号，不是PID）
bg %1 将作业 1 切换到后台
kill %1  终止作业 1


```

#### curl
```
curl -i -w "总响应时间：%{time_total}秒\n" \
  -H "Authorization: Bearer token123" \
  -H "Custom-Header: value" \
  "https://api.example.com/data?user_id=123&sort=desc"
```

```
curl -i  \
  -X POST \
  -H "Content-Type: application/json" \
  -H "Authorization: Bearer token123" \
  -d '{"name": "John", "age": 30, "email": "john@example.com"}' \
  https://api.example.com/users
```

```
curl -i  \
  -X POST \
  -H "Custom-Header: value" \
  -F "username=admin" \
  -F "password=secret" \
  -F "file=@/path/to/file.txt" \
  https://api.example.com/upload
```


#### vim
```
搜索表达式，键入 / 键，然后输入您的搜索词。按下 Enter 键后，您可以按 n 向前或按 N 向后浏览搜索结果，键入? 搜索命令将向后搜索文本文件

:w - 写入或保存文件
:q - 退出 Vim
:wq - 写入然后退出
:q! - 不保存文件退出 Vim
ZZ - 等同于 :wq，但快一个字符
u - 撤销上一个操作
Ctrl-r - 重做上一个操作
你可能觉得 ZZ 没有必要，但最终你会发现你的手指可能会更倾向于使用它而不是 :wq。


根据你想要输入的位置，可以通过不同的方式进入插入模式：
i – 在光标前插入
a – 在光标后追加
I – 在当前行开头插入
A – 在当前行末尾追加
o – 在当前行下方打开新行并开始插入
O – 在当前行上方打开新行并开始插入
提示：你可以在这些命令前加上一个计数。例如，3o 会在下方打开三行新行。
完成文本插入后，按 Esc 返回普通模式。

复制和粘贴（yank 和 put）：
yw – 复制单词
yy – 复制当前行
p – 在光标后或行下方粘贴
P – 在光标前或行上方粘贴

删除（操作符 d）：
x – 删除光标下的字符
dw – 从光标处删除到下一个单词的开头
d$ – 从光标处删除到行尾
dd – 删除当前行
计数适用：3dd 删除三行；2dw 删除两个单词

更改（操作符 c，删除然后进入插入模式）：
cw – 从光标处更改单词
c$ – 更改到行尾
cc – 更改整行

替换和其他便捷编辑：
r{char} – 用 {char} 替换光标下的字符
R – 进入替换模式以覆盖文本
J – 将当前行与下一行连接
. – 重复上次更改


```

#### 输入输出
```
echo Hello World > peanuts.txt 看到一个名为 peanuts.txt 的文件。查看该文件，你应该会看到文本"Hello World"。
echo Hello World  将"Hello World"打印到屏幕上
`>` 是一个重定向运算符，它允许我们改变标准输出的去向。它允许我们将 echo Hello World 的输出发送到文件而不是屏幕。如果文件不存在，它会为我们创建它。但是，如果它确实存在，它会覆盖它（你可以添加一个 shell 标志来防止这种情况，具体取决于你使用的 shell）。
假设我不想覆盖我的 peanuts.txt。幸运的是，也有一个重定向运算符可以做到这一点：>>。
echo Hello World >> peanuts.txt  这会将"Hello World"附加到 peanuts.txt 文件的末尾。如果文件不存在，它会为我们创建它，就像 > 重定向器一样！


echo $HOME  环境变量。您可以通过输入以下命令来查看它们：
env  这会输出大量关于您当前设置的环境变量的信息。这些变量包含 shell 和其他进程可以使用的有用信息。
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/bin
PWD=/home/user
USER=pete
一个特别重要的变量是 PATH 变量。您可以通过在变量名前面加上 $ 来访问这些变量，如下所示：

$ echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/bin
这会返回一个由冒号分隔的路径列表，您的系统在运行命令时会搜索这些路径。假设您手动从互联网下载并安装了一个软件包，并将其放入一个非标准目录，并且您想运行该命令。您输入 $ coolcommand，提示符显示"command not found"。这很奇怪；您正在文件夹中查看二进制文件，并且知道它存在。发生的情况是 $PATH 变量没有在该目录中检查此二进制文件，因此它会抛出错误。
假设您想从该目录运行大量二进制文件；您可以修改 PATH 变量，将该目录包含在您的 PATH 环境变量中。


head /var/log/syslog  显示文件的前 10 行
head -n 15 /var/log/syslog 看前 15 行
tail /var/log/syslog  默认显示文件的最后 10 行
tail -n 10 /var/log/syslog  更改你想要查看的行数
tail -f /var/log/syslog  使用 -f (follow) 标志；这会随着文件的增长而跟踪文件，当你与系统交互时，你的 syslog 文件会不断变化，
```

#### 压缩解压
```
gzip 是一个用于在 Linux 中压缩文件的程序；它们以 .gz 扩展名结尾。
gzip mycoolfile  压缩文件
gunzip mycoolfile.gz  解压缩文件

使用 tar 创建归档
遗憾的是，gzip 无法为我们添加多个文件到一个归档中。幸运的是，我们有 tar 程序可以做到这一点。当您使用 tar 创建归档时，它将具有 .tar 扩展名。

tar cvf mytarfile.tar mycoolfile1 mycoolfile2
c - 创建
v - 告诉程序详细输出，让我们看到它正在做什么
f - tar 文件的文件名必须在此选项之后；如果您正在创建 tar 文件，则必须想一个名称
使用 tar 解包归档

要提取 tar 文件的内容，请使用：
tar xvf mytarfile.tar
x - 提取
v - 告诉程序详细输出，让我们看到它正在做什么
f - 您要提取的文件
使用 tar 和 gzip 压缩/解压缩归档
很多时候，您会看到一个已压缩的 tar 文件，例如：mycompressedarchive.tar.gz。您所需要做的就是由外而内操作，所以首先使用 gunzip 解除压缩，然后您可以解包 tar 文件。或者，您可以选择使用 tar 的 z 选项，它只是告诉它使用 gzip 或 gunzip 工具。

创建压缩的 tar 文件：
tar czf myfile.tar.gz
解压缩和解包：
tar xzf file.tar
```

#### 包管理
##### rpm 和 dpkg
```
您可以使用包管理命令：rpm 和 dpkg。这些工具用于安装包文件；但是，它们不会安装包的依赖项
.deb 用于基于 Debian 的发行版，.rpm 用于基于 Red Hat 的发行版
安装包
Debian: $ dpkg -i some_deb_package.deb
RPM: $ rpm -i some_rpm_package.rpm
i 代表安装（install）。您也可以使用更长的格式 --install。
移除包
Debian: $ dpkg -r some_deb_package.deb
RPM: $ rpm -e some_rpm_package.rpm
Debian: r 代表移除（remove）
RPM: e 代表擦除（erase）
列出已安装的包
Debian: $ dpkg -l
RPM: $ rpm -qa
Debian: l 代表列表（list）
RPM: q 代表查询（query），a 代表所有（all）
```

##### yum 和 apt
```
配备了所有必要的工具，使包的安装、删除和更改变得更容易，包括安装包依赖项
Yum 专属于 Red Hat 系列，而 apt 专属于 Debian 系列。

从仓库安装软件包
Debian: $ apt install package_name
RPM: $ yum install package_name
移除软件包
Debian: $ apt remove package_name
RPM: $ yum erase package_name
更新仓库中的软件包
在安装和更新软件包之前，最好始终更新您的软件包仓库，使其保持最新。

Debian: apt update; apt upgrade
RPM: yum update
获取已安装软件包的信息
Debian: apt show package_name
RPM: yum info package_name
```

##### 编译源代码
```
通常，您会遇到一个晦涩的软件包，它只以纯源代码的形式提供。您需要使用一些命令来编译并将该源代码包安装到您的系统上。
首先，您需要安装能够编译源代码的工具。
sudo apt install build-essential
完成此操作后，提取软件包文件的内容，最可能是 .tar.gz 文件。
tar -xzvf package.tar.gz
在执行任何操作之前，请查看软件包内的 README 或 INSTALL 文件。有时会有特定的安装说明。
根据开发人员使用的编译方法，您需要使用不同的命令，例如 cmake 或其他命令。
然而，最常见的是基本的 make 编译，所以我们将讨论它：
软件包内容中会有一个 configure 脚本。此脚本检查系统上的依赖项，如果您缺少任何内容，您将看到错误，并且需要修复这些依赖项。
./configure
./ 允许您在当前目录中执行脚本。
make
软件包内容中有一个名为 Makefile 的文件，其中包含构建软件的规则。当您运行 make 命令时，它会查看此文件来构建软件。
sudo make install
此命令实际上安装了软件包；它会将正确的文件复制到您计算机上的正确位置。
如果要卸载软件包，请使用：
sudo make uninstall
使用 make install 时要小心；您可能没有意识到后台实际发生了多少事情。如果您决定删除此软件包，您可能无法实际删除所有内容，因为您没有意识到系统添加了什么。相反，忘记我刚刚向您解释的关于 make install 的所有内容，并使用 checkinstall 命令。此命令将为您创建一个 .deb 文件，您可以轻松安装和卸载它。
sudo checkinstall
此命令将实质上"make install"并构建一个 .deb 包并安装它。这使得以后更容易删除软件包。
```

#### 文件系统
##### 磁盘利用率
```

pete@icebox:~$ df -h
Filesystem     1K-blocks    Used Available Use% Mounted on
/dev/sda1       6.2G  2.3G  3.6G  40% /
df 命令显示当前挂载文件系统的利用率。-h 标志以人类可读的格式显示。您可以查看设备是什么以及使用了多少容量和可用容量。
假设您的磁盘快满了，您想知道哪些文件或目录占用了这些空间；为此，您可以使用 du 命令。
du -h  这显示了您当前所在目录的磁盘使用情况。您可以使用 du -h / 查看根目录，但这可能会有点混乱。
```

##### 目录介绍
```
/ - 整个文件系统层次结构的根目录；所有内容都嵌套在此目录下。
/bin - 必要的即用程序（二进制文件）；包括 ls 和 cp 等最基本的命令。
/boot - 包含内核引导加载程序文件。
/dev - 设备文件。
/etc - 核心系统配置目录；应仅包含配置文件，不包含任何二进制文件。
/home - 用户的个人目录；存放您的文档、文件、设置等。
/lib - 存放二进制文件可以使用的库文件。
/media - 用作可移动媒体（如 USB 驱动器）的挂载点。
/mnt - 临时挂载的文件系统。
/opt - 可选的应用程序软件包。
/proc - 有关当前运行进程的信息。
/root - root 用户的家目录。
/run - 自上次启动以来有关运行系统的信息。
/sbin - 包含必要的系统二进制文件，通常只能由 root 运行。
/srv - 由系统提供的特定站点数据。
/tmp - 临时文件的存储。
/usr - 这个命名不幸；它通常不包含家庭文件夹意义上的用户文件。它旨在用于用户安装的软件和实用程序；但是，这并不是说您不能在其中添加个人目录。此目录内部有 /usr/bin、/usr/local 等子目录。
/var - 可变目录；它用于系统日志记录、用户跟踪、缓存等。基本上是所有经常变化的内容。
```

#### 进程
```
top
shift+p按照CPU排序

第 1 行：这是您运行 uptime 命令时会看到的信息
字段从左到右依次是：

当前时间
系统已运行多长时间
当前登录的用户数量
系统平均负载（更多内容即将推出）
  第 2 行：正在运行、休眠、停止和僵尸进程的任务
  第 3 行：CPU 信息
  us：用户 CPU 时间 - CPU 时间中用于运行未经过 nice 处理的用户进程的百分比。
  sy：系统 CPU 时间 - CPU 时间中用于运行内核和内核进程的百分比。
  ni：nice CPU 时间 - CPU 时间中用于运行经过 nice 处理的进程的百分比。
  id：CPU 空闲时间 - CPU 时间中处于空闲状态的百分比。
  wa：I/O 等待 - CPU 时间中等待 I/O 的百分比。如果此值较低，则问题可能不是磁盘或网络 I/O。
  hi：硬件中断 - CPU 时间中用于处理硬件中断的百分比。
  si：软件中断 - CPU 时间中用于处理软件中断的百分比。
  st：窃取时间 - 如果您正在运行虚拟机，这是从您那里窃取用于其他任务的 CPU 时间百分比。
  第 4 行和第 5 行：内存使用和交换使用
  当前正在使用的进程列表
  PID：进程 ID
  USER：进程所有者用户
  PR：进程优先级
  NI：nice 值
  VIRT：进程使用的虚拟内存
  RES：进程使用的物理内存
  SHR：进程的共享内存
  S：指示进程状态：S=休眠，R=运行，Z=僵尸，D=不可中断，T=停止
  %CPU：此进程使用的 CPU 百分比
  %MEM：此进程使用的 RAM 百分比
  TIME+：此进程的总活动时间
  COMMAND：进程名称

  如果您只想跟踪某些进程，也可以指定进程 ID：
  top -p 1

  第一步
  top命令，然后按shift+p按照CPU排序，找到占用CPU过高的进程的pid
  第二步
  top -H -p [进程id]
  找到进程中消耗资源最高的线程的id
  第三步
  echo 'obase=16;[线程id]' | bc或者printf "%x\n" [线程id]
  将线程id转换为16进制（字母要小写）
  bc是linux的计算器命令
  第四步（jstack 是java应用）
  jstack [进程id] |grep -A 10 [线程id的16进制]"
  查看线程状态信息


  vmstat 监控内存使用情况

  netstat -anp 查看网络详细信息

  ping 

  您可以通过查看文件 /etc/services 来获取知名端口列表
  ftp             21/tcp
  ssh             22/tcp
  smtp            25/tcp
  domain          53/tcp  # DNS
  http            80/tcp
  https           443/tcp
  ..etc..
```

#### regex (正则表达式)
```

sally sells seashells
by the seashore
以 ^ 开头
^by
would match the line "by the seashore"
以 $ 结尾
seashore$
would match the line "by the seashore"
匹配任意单个字符
b.
would match by
使用 [] 和 () 的方括号表示法
d[iou]g
would match: dig, dog, dug
当在方括号中使用时，前面的锚点 ^ 表示除了方括号内的字符之外的任何字符。
d[^i]g
would match: dog and dug but not dig
方括号也可以使用范围来增加您想要使用的字符数量。
d[a-c]g
will match patterns like dag, dbg, and dcg
但请注意，方括号是区分大小写的：
d[A-C]g
will match dAg, dBg and dCg but not dag, dbg and dcg

```

#### wc
```
wc（word count）命令显示文件中单词的总数。
$ wc /etc/passwd
 96     265    5925 /etc/passwd
它分别显示行数、单词数和字节数。
要只查看某个字段的计数，请分别使用 -l、-w 或 -c 选项。
$ wc -l /etc/passwd
96
另一个可以用来检查文件中行数的命令是 nl（number lines）命令。
$ nl file1.txt
1. i
2. like
3. turtles

```

