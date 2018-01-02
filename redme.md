linux-centos-study
```
0.
linux目录：https://www.cnblogs.com/silence-hust/p/4319415.html
Linux文件目录结构详解
　　 整理自《鸟哥的私房菜》

　　 对于每一个Linux学习者来说，了解Linux文件系统的目录结构，是学好Linux的至关重要的一步.，
     深入了解linux文件目录结构的标准和每个目录的详细功能，对于我们用好linux系统只管重要，
     下面我们就开始了解一下linux目录结构的相关知识。

　　 当在使用Linux的时候，如果您通过ls –l / 就会发现，在/下包涵很多的目录，比如etc、usr、var、bin ... ... 等目录，
     而在这些目录中，我们进去看看，发现也有很多的目录或文件。文件系统在Linux下看上去就象树形结构，
     所以我们可以把文件系统的结构形象的称为 树形结构。

 　　文件系统的是用来组织和排列文件存取的，所以她是可见的，
    在Linux中，我们可以通过ls等工具来查看其结构，在Linux系统中，我们见到的都是树形结构；
    比如操作系统安装在一个文件系统中，他表现为由/ 起始的树形结构。
    linux文件系统的最顶端是/，我们称/为Linux的root，也就是 Linux操作系统的文件系统。
    Linux的文件系统的入口就是/，所有的目录、文件、设备都在/之下，/就是Linux文件系统的组织者，也是最上级的领导者。

　　由于linux是开放源代码，各大公司和团体根据linux的核心代码做各自的操作，编程。
    这样就造成在根下的目录的不同。这样就造成个人不能使用他人的linux系统的PC。
    因为你根本不知道一些基本的配置，文件在哪里。。。这就造成了混乱。
    这就是FHS（Filesystem Hierarchy Standard ）机构诞生的原因。
    该机构是linux爱好者自发的组成的一个团体，主要是是对linux做一些基本的要求，不至于是操作者换一台主机就成了linux的‘文盲’。

 　　根据FHS(http://www.pathname.com/fhs/)的官方文件指出， 他们的主要目的是希望让使用者可以了解到已安装软件通常放置于那个目录下，
     所以他们希望独立的软件开发商、操作系统制作者、以及想要维护系统的用户，都能够遵循FHS的标准。
     也就是说，FHS的重点在于规范每个特定的目录下应该要放置什么样子的数据而已。
     这样做好处非常多，因为Linux操作系统就能够在既有的面貌下(目录架构不变)发展出开发者想要的独特风格。

　　事实上，FHS是根据过去的经验一直再持续的改版的，FHS依据文件系统使用的频繁与否与是否允许使用者随意更动，
    而将目录定义成为四种交互作用的形态，用表格来说有点像底下这样：

```
事实上，FHS针对目录树架构仅定义出三层目录底下应该放置什么数据而已，分别是底下这三个目录的定义：

/ (root, 根目录)：与开机系统有关；

/usr (unix software resource)：与软件安装/执行有关；

/var (variable)：与系统运作过程有关。
```


一. 根目录 (/) 的意义与内容：

　　根目录是整个系统最重要的一个目录，因为不但所有的目录都是由根目录衍生出来的，
    同时根目录也与开机/还原/系统修复等动作有关。 由于系统开机时需要特定的开机软件、核心文件、开机所需程序、 函式库等等文件数据，
    若系统出现错误时，根目录也必须要包含有能够修复文件系统的程序才行。
    因为根目录是这么的重要，所以在FHS的要求方面
    ，他希望根目录不要放在非常大的分区， 因为越大的分区内你会放入越多的数据，
    如此一来根目录所在分区就可能会有较多发生错误的机会。

因此FHS标准建议：根目录(/)所在分区应该越小越好， 且应用程序所安装的软件最好不要与根目录放在同一个分区内，保持根目录越小越好。
 如此不但效能较佳，根目录所在的文件系统也较不容易发生问题。说白了，就是根目录和Windows的C盘一个样。

根据以上原因，FHS认为根目录(/)下应该包含如下子目录：



目录

应放置档案内容

/bin



系统有很多放置执行档的目录，但/bin比较特殊。因为/bin放置的是在单人维护模式下还能够被操作的指令。
在/bin底下的指令可以被root与一般帐号所使用，主要有：cat,chmod(修改权限), chown, date, mv, mkdir, cp, bash等等常用的指令。



/boot

主要放置开机会使用到的档案，包括Linux核心档案以及开机选单与开机所需设定档等等。
Linux kernel常用的档名为：vmlinuz ，如果使用的是grub这个开机管理程式，则还会存在/boot/grub/这个目录。



/dev

在Linux系统上，任何装置与周边设备都是以档案的型态存在于这个目录当中。
 只要通过存取这个目录下的某个档案，就等于存取某个装置。
 比要重要的档案有/dev/null, /dev/zero, /dev/tty , /dev/lp*, / dev/hd*, /dev/sd*等等



/etc

系统主要的设定档几乎都放置在这个目录内，例如人员的帐号密码档、各种服务的启始档等等。
 一般来说，这个目录下的各档案属性是可以让一般使用者查阅的，但是只有root有权力修改。
  FHS建议不要放置可执行档(binary)在这个目录中。
  比较重要的档案有：/etc/inittab, /etc/init.d/, /etc/modprobe.conf, /etc/X11/, /etc/fstab, /etc/sysconfig/等等。
   另外，其下重要的目录有：/etc/init.d/ ：所有服务的预设启动script都是放在这里的，
   例如要启动或者关闭iptables的话： /etc/init.d/iptables start、/etc/init.d/ iptables stop

/etc/xinetd.d/ ：这就是所谓的super daemon管理的各项服务的设定档目录。



/etc/X11/ ：与X Window有关的各种设定档都在这里，尤其是xorg.conf或XF86Config这两个X Server的设定档。



/home

这是系统预设的使用者家目录(home directory)。
 在你新增一个一般使用者帐号时，预设的使用者家目录都会规范到这里来。
 比较重要的是，家目录有两种代号：


~ ：代表当前使用者的家目录，而 ~guest：则代表用户名为guest的家目录。



/lib

系统的函式库非常的多，而/lib放置的则是在开机时会用到的函式库，以及在/bin或/sbin底下的指令会呼叫的函式库而已 。
 什么是函式库呢？妳可以将他想成是外挂，某些指令必须要有这些外挂才能够顺利完成程式的执行之意。
  尤其重要的是/lib/modules/这个目录，因为该目录会放置核心相关的模组(驱动程式)。



/media

media是媒体的英文，顾名思义，这个/media底下放置的就是可移除的装置。
 包括软碟、光碟、DVD等等装置都暂时挂载于此。
  常见的档名有：/media/floppy, /media/cdrom等等。



/mnt

如果妳想要暂时挂载某些额外的装置，一般建议妳可以放置到这个目录中。
在古早时候，这个目录的用途与/media相同啦。
只是有了/media之后，这个目录就用来暂时挂载用了。



/opt

这个是给第三方协力软体放置的目录 。
 什么是第三方协力软体啊？举例来说，KDE这个桌面管理系统是一个独立的计画，不过他可以安装到Linux系统中，
 因此KDE的软体就建议放置到此目录下了。
  另外，如果妳想要自行安装额外的软体(非原本的distribution提供的)，那么也能够将你的软体安装到这里来。
  不过，以前的Linux系统中，我们还是习惯放置在/usr/local目录下。



/root

系统管理员(root)的家目录。
 之所以放在这里，是因为如果进入单人维护模式而仅挂载根目录时，该目录就能够拥有root的家目录，
 所以我们会希望root的家目录与根目录放置在同一个分区中。



/sbin

Linux有非常多指令是用来设定系统环境的，这些指令只有root才能够利用来设定系统，其他使用者最多只能用来查询而已。
放在/sbin底下的为开机过程中所需要的，里面包括了开机、修复、还原系统所需要的指令。
至于某些伺服器软体程式，一般则放置到/usr/sbin/当中。
至于本机自行安装的软体所产生的系统执行档(system binary)，则放置到/usr/local/sbin/当中了。常见的指令包括：fdisk, fsck, ifconfig, init, mkfs等等。



/srv

srv可以视为service的缩写，是一些网路服务启动之后，这些服务所需要取用的资料目录。
常见的服务例如WWW, FTP等等。
举例来说，WWW伺服器需要的网页资料就可以放置在/srv/www/里面。
呵呵，看来平时我们编写的代码应该放到这里了。



/tmp

这是让一般使用者或者是正在执行的程序暂时放置档案的地方。
这个目录是任何人都能够存取的，所以你需要定期的清理一下。
当然，重要资料不可放置在此目录啊。
 因为FHS甚至建议在开机时，应该要将/tmp下的资料都删除。


事实上FHS针对根目录所定义的标准就仅限于上表，不过仍旧有些目录也需要我们了解一下，具体如下：



目录

应放置文件内容

/lost+found

这个目录是使用标准的ext2/ext3档案系统格式才会产生的一个目录，目的在于当档案系统发生错误时，将一些遗失的片段放置到这个目录下。
 这个目录通常会在分割槽的最顶层存在，例如你加装一个硬盘于/disk中，那在这个系统下就会自动产生一个这样的目录/disk/lost+found

/proc

这个目录本身是一个虚拟文件系统(virtual filesystem)喔。
 他放置的资料都是在内存当中，例如系统核心、行程资讯(process)（是进程吗?）、周边装置的状态及网络状态等等。
 因为这个目录下的资料都是在记忆体（内存）当中，所以本身不占任何硬盘空间。
 比较重要的档案（目录）例如： /proc/cpuinfo, /proc/dma, /proc/interrupts, /proc/ioports, /proc/net/*等等。呵呵，是虚拟内存吗[guest]？

/sys

这个目录其实跟/proc非常类似，也是一个虚拟的档案系统，主要也是记录与核心相关的资讯。
 包括目前已载入的核心模组与核心侦测到的硬体装置资讯等等。 这个目录同样不占硬盘容量。


　　除了这些目录的内容之外，另外要注意的是，因为根目录与开机有关，开机过程中仅有根目录会被挂载， 其他分区则是在开机完成之后才会持续的进行挂载的行为。
就是因为如此，因此根目录下与开机过程有关的目录， 就不能够与根目录放到不同的分区去。

那哪些目录不可与根目录分开呢？有底下这些：

/etc：配置文件

/bin：重要执行档

/dev：所需要的装置文件

/lib：执行档所需的函式库与核心所需的模块

/sbin：重要的系统执行文件

这五个目录千万不可与根目录分开在不同的分区。请背下来啊。



二. /usr 的意义与内容：

　　依据FHS的基本定义，/usr里面放置的数据属于可分享的与不可变动的(shareable, static)， 如果你知道如何透过网络进行分区的挂载(例如在服务器篇会谈到的NFS服务器)，
    那么/usr确实可以分享给局域网络内的其他主机来使用喔。

　　/usr不是user的缩写，其实usr是Unix Software Resource的缩写， 也就是Unix操作系统软件资源所放置的目录，而不是用户的数据啦。
    这点要注意。 FHS建议所有软件开发者，应该将他们的数据合理的分别放置到这个目录下的次目录，而不要自行建立该软件自己独立的目录。

　　因为是所有系统默认的软件(distribution发布者提供的软件)都会放置到/usr底下，
    因此这个目录有点类似Windows 系统的C:\Windows\ + C:\Program files\这两个目录的综合体，系统刚安装完毕时，这个目录会占用最多的硬盘容量。
     一般来说，/usr的次目录建议有底下这些：

目录

应放置文件内容

/usr/X11R6/

为X Window System重要数据所放置的目录，之所以取名为X11R6是因为最后的X版本为第11版，且该版的第6次释出之意。



/usr/bin/

绝大部分的用户可使用指令都放在这里。请注意到他与/bin的不同之处。(是否与开机过程有关)

/usr/include/

c/c++等程序语言的档头(header)与包含档(include)放置处，当我们以tarball方式 (*.tar.gz 的方式安装软件)安装某些数据时，会使用到里头的许多包含档。



/usr/lib/

包含各应用软件的函式库、目标文件(object file)，以及不被一般使用者惯用的执行档或脚本(script)。
 某些软件会提供一些特殊的指令来进行服务器的设定，这些指令也不会经常被系统管理员操作， 那就会被摆放到这个目录下啦。
 要注意的是，如果你使用的是X86_64的Linux系统， 那可能会有/usr/lib64/目录产生

/usr/local/

统管理员在本机自行安装自己下载的软件(非distribution默认提供者)，建议安装到此目录， 这样会比较便于管理。
举例来说，你的distribution提供的软件较旧，你想安装较新的软件但又不想移除旧版， 此时你可以将新版软件安装于/usr/local/目录下，可与原先的旧版软件有分别啦。
 你可以自行到/usr/local去看看，该目录下也是具有bin, etc, include, lib...的次目录

/usr/sbin/

非系统正常运作所需要的系统指令。最常见的就是某些网络服务器软件的服务指令(daemon)

/usr/share/

放置共享文件的地方，在这个目录下放置的数据几乎是不分硬件架构均可读取的数据， 因为几乎都是文本文件嘛。
在此目录下常见的还有这些次目录：/usr/share/man：联机帮助文件

/usr/share/doc：软件杂项的文件说明

/usr/share/zoneinfo：与时区有关的时区文件



/usr/src/

一般原始码建议放置到这里，src有source的意思。至于核心原始码则建议放置到/usr/src/linux/目录下。



三.  /var 的意义与内容：

　　如果/usr是安装时会占用较大硬盘容量的目录，
   那么/var就是在系统运作后才会渐渐占用硬盘容量的目录。
   因为/var目录主要针对常态性变动的文件，包括缓存(cache)、登录档(log file)以及某些软件运作所产生的文件，
    包括程序文件(lock file, run file)，或者例如MySQL数据库的文件等等。常见的次目录有：

目录

应放置文件内容

/var/cache/

应用程序本身运作过程中会产生的一些暂存档

/var/lib/

程序本身执行的过程中，需要使用到的数据文件放置的目录。在此目录下各自的软件应该要有各自的目录。
 举例来说，MySQL的数据库放置到/var/lib/mysql/而rpm的数据库则放到/var/lib/rpm去

/var/lock/

某些装置或者是文件资源一次只能被一个应用程序所使用，如果同时有两个程序使用该装置时， 就可能产生一些错误的状况，因此就得要将该装置上锁(lock)，
以确保该装置只会给单一软件所使用。 举例来说，刻录机正在刻录一块光盘，你想一下，
会不会有两个人同时在使用一个刻录机烧片？ 如果两个人同时刻录，那片子写入的是谁的数据？
所以当第一个人在刻录时该刻录机就会被上锁， 第二个人就得要该装置被解除锁定(就是前一个人用完了)才能够继续使用

/var/log/

非常重要。这是登录文件放置的目录。里面比较重要的文件如/var/log/messages, /var/log/wtmp(记录登入者的信息)等。

/var/mail/

放置个人电子邮件信箱的目录，不过这个目录也被放置到/var/spool/mail/目录中，通常这两个目录是互为链接文件。

/var/run/

某些程序或者是服务启动后，会将他们的PID放置在这个目录下

/var/spool/

这个目录通常放置一些队列数据，所谓的“队列”就是排队等待其他程序使用的数据。
 这些数据被使用后通常都会被删除。举例来说，系统收到新信会放置到/var/spool/mail/中， 但使用者收下该信件后该封信原则上就会被删除。
 信件如果暂时寄不出去会被放到/var/spool/mqueue/中， 等到被送出后就被删除。如果是工作排程数据(crontab)，就会被放置到/var/spool/cron/目录中。

　　由于FHS仅是定义出最上层(/)及次层(/usr, /var)的目录内容应该要放置的文件或目录数据， 因此，在其他次目录层级内，就可以随开发者自行来配置了。



四. 目录树(directory tree) :

　　在Linux底下，所有的文件与目录都是由根目录开始的。
 那是所有目录与文件的源头, 然后再一个一个的分支下来，因此，我们也称这种目录配置方式为：目录树(directory tree), 这个目录树的主要特性有：

目录树的启始点为根目录 (/, root)；
每一个目录不止能使用本地端的 partition 的文件系统，也可以使用网络上的 filesystem 。举例来说， 可以利用 Network File System (NFS) 服务器挂载某特定目录等。
每一个文件在此目录树中的文件名(包含完整路径)都是独一无二的。
如果我们将整个目录树以图的方法来显示，并且将较为重要的文件数据列出来的话，那么目录树架构就如下图所示：





五. 绝对路径与相对路径

　　除了需要特别注意的FHS目录配置外，在文件名部分我们也要特别注意。因为根据档名写法的不同，也可将所谓的路径(path)定义为绝对路径(absolute)与相对路径(relative)。
 这两种文件名/路径的写法依据是这样的：

绝对路径：

　　由根目录(/)开始写起的文件名或目录名称， 例如 /home/dmtsai/.bashrc；

相对路径：

　　相对于目前路径的文件名写法。 例如 ./home/dmtsai 或 http://www.cnblogs.com/home/dmtsai/ 等等。
反正开头不是 / 就属于相对路径的写法

而你必须要了解，相对路径是以你当前所在路径的相对位置来表示的。举例来说，你目前在 /home 这个目录下， 如果想要进入 /var/log 这个目录时，可以怎么写呢？

cd /var/log   (absolute)

cd ../var/log (relative)

因为你在 /home 底下，所以要回到上一层 (../) 之后，才能继续往 /var 来移动的，特别注意这两个特殊的目录：

.  ：代表当前的目录，也可以使用 ./ 来表示；

.. ：代表上一层目录，也可以 ../ 来代表。

这个 . 与 .. 目录概念是很重要的，你常常会看到 cd .. 或 ./command 之类的指令下达方式， 就是代表上一层与目前所在目录的工作状态。

实例1：如何先进入/var/spool/mail/目录，再进入到/var/spool/cron/目录内？

命令：

cd /var/spool/mail

cd ../cron

说明：

　　由于/var/spool/mail与/var/spool/cron是同样在/var/spool/目录中。如此就不需要在由根目录开始写起了。
这个相对路径是非常有帮助的，尤其对于某些软件开发商来说。 一般来说，软件开发商会将数据放置到/usr/local/里面的各相对目录。 但如果用户想要安装到不同目录呢？就得要使用相对路径。

实例2：网络文件常常提到类似./run.sh之类的数据，这个指令的意义为何？

说明：

　　由于指令的执行需要变量的支持，若你的执行文件放置在本目录，并且本目录并非正规的执行文件目录(/bin, /usr/bin等为正规)，此时要执行指令就得要严格指定该执行档。
./代表本目录的意思，所以./run.sh代表执行本目录下， 名为run.sh的文件。
```


```
1.
   cat /etc/issue  或cat /etc/redhat-release（Linux查看版本当前操作系统发行版信息）
```

```
2.
   uname －a   （Linux查看版本当前操作系统内核信息）
```

```
3.
  cat /proc/version （Linux查看当前操作系统版本信息）
```

```
4.
  cat /proc/cpuinfo （Linux查看cpu相关信息，包括型号、主频、内核信息等）
```

```
5.
 getconf LONG_BIT  （Linux查看版本说明当前CPU运行在32bit模式下， 但不代表CPU不支持64bit）
```
```
6.
pwd   （查看当前路径命令）
```
```
7. rwx -d:http://blog.csdn.net/sinat_35209943/article/details/52449743
  -rw-r–r– 1 root root 1313 Sep 3 14:59 test.log详解

  查询目录中的内容命令 ls [选项] [文件或目录]
  选项：
  -a 显示所有文件、包括隐藏文件
  -l 显示详细信息
  -d 查看目录属性（目录本身权限）
  -h 人性化显示文件大小（在文件大小后面加上单位）
  -i 显示inode（查看文件id号）

  当使用ls -l命令时会显示所有目录里文件内容详细信息，如图所示：
  这里写图片描述

  先详细描述第一行其中每项代表的含义：
  -rw-r–r–
  1) -文件类型（-文件 d目录 l软链接文件（类似于windows中的快捷方式）），该种类型共7种，还有不常用的块设备文件、字符设备文件、套接字文件、管道文件。
  2）rw-表示可读可写，代表所有者u的权限。
  3）第一个r–表示可读，代表所属组g的权限（相同权限的人放在一起就是一组）；第二个r–表示可读，代表其他人o的权限。
  r 读 w 写 x 执行
  数字2表示该文件被调用次数
  第一个root表示所有者u
  第二个root表示所属组g，在这里表示和root一个组的其他用户
  51是文件大小，单位是字节（byte）
  Aug 31 09:38表示文件最后一次修改时间
  ex是文件名
```


```
8.vim编辑器的使用
whereis vim （查看vim在哪里？）
 https://www.cnblogs.com/crazylqy/p/5649860.html
```

```
9.
 shutdown -h now （关机-root）
 shutdown -r now (立刻重启-root)
```

```
10.
 ctrl+alt+[F1-F6]进入命令行
 ctrl+alt+[F7]进入xwindow
```

```
11.
 / 根目录
 /bin 存放必要的命令
 /boot 存放内核以及启动所需的文件
 /dev 存放设备文件
 /etc 存放系统配置文件
 /home 普通用户的宿主目录，用户数据存放在其主目录中
 /lib 存放必要的运行库
 /mnt 存放临时的映射文件系统，通常用来挂载使用。
  /proc 存放存储进程和系统信息
 /root 超级用户的主目录
 /sbin 存放系统管理程序
 /tmp 存放临时文件
 /usr 存放应用程序，命令程序文件、程序库、手册和其它文档。 = [unix software resources]
 /var 系统默认日志存放目录  =[variable]
```

```
12.
    Linux必备命令

   默认进入系统，我们会看到这样的字符: [root@localhost ~]#,其中#代表当前是root用户登录，如果是$表示当前为普通用户。

   我们了解linux由很多目录文件构成，那我们来学习第一个Linux命令：
   cd命令， cd  /home  ；解析：进入/home目录

   cd /root 进入/root目录 ；

   cd ../返回上一级目录;cd  ./当前目录；（.和..可以理解为相对路径；例如cd /hom/test ，cd加完整的路径，可以理解为绝对路径）

   接下来继续学习更多的命令：
   ls  ./ 查看当前目录所有的文件和目录。
   ls  -a 查看所有的文件，包括隐藏文件,以.开头的文件。

   pwd显示当前所在的目录。
   mkdir创建目录，用法mkdir  test ，命令后接目录的名称。
   rmdir 删除空目录
   rm 删除文件或者目录，用法 rm –rf  test.txt (-r表示递归，-f表示强制)。
   cp 拷贝文件，用法,cp  old.txt  /tmp/new.txt ，常用来备份；如果拷贝目录
   需要加 –r参数。

   mv 重命名或者移动文件或者目录，用法, mv old.txt new.txt
   touch 创建文件，用法，touch test.txt，如果文件存在，则表示修改当前文件时间。
   Useradd创建用户，用法 useradd wugk ，userdel删除用户。
   Groupadd创建组，用法 groupadd wugk1 ，groupdel删除组。

   touch:创建空白文档

   mkdir:创建一个目录

   vi:同touch一样，都是创建一个空白文档

   举个栗子：touch w;此时创建一个w的空白文档；file w 可以查看文档w的属性，此时显示empty，表示确实是空白文档

   mkdir w2；此时创建一个w2的文件夹；file w2可以查看文件夹w2的属性，此时现实directory，表示确实是建了一个文件夹

   vi e3;此时创建一个w3的空白文档；file w3可以查看文档w3的属性，此时显示empty，表示确实是空白文档，由此可见vi和touch并无区别。

   vim 是vi的升级版本！


   find查找文件或目录，用法 find  /home  -name  “test.txt”,命令格式为:
   find 后接查找的目录，-name指定需要查找的文件名称，名称可以使用*表示所有。

   find  /home  -name  “*.txt” ;查找/home目录下，所有以.txt结尾的文件或者目录。

   vi 修改某个文件，vi有三种模式：
   命令行模式、文本输入模式、末行模式。
   默认vi打开一个文件，首先是命令行模式，然后按i进入文本输入模式，可以在文件里写入字符等等信息。
   写完后，按esc进入命令模式，然后输入:进入末行模式，
   例如输入:wq表示保存退出。
   如果想直接退出，不保存，可以执行:q!， q!叹号表示强制退出。

   cat 查看文件内容，用法 cat test.txt 可以看到test.txt内容

   more 查看文件内容，分页查看，cat是全部查看，如果篇幅很多，只能看到最后的篇幅。
   可以使用cat和more同时使用,例如： cat  test.txt |more 分页显示text内容，|符号是管道符，用于把|前的输出作为后面命令的输入。

   echo 回显，用法 echo ok，会显示ok，输入什么就打印什么。
   echo  ok  > test.txt ；把ok字符覆盖test.txt内容，>表示追加并覆盖的意思。
   >>两个大于符号，表示追加，echo ok >> test.txt,表示向test.txt文件追加OK字符，不覆盖原文件里的内容。
   初学者常见的命令就如上所示，当然还有很多深入的命令需要学习，后面的课程会讲解。
```
```
13.
   Linux用户权限管理

   在Linux操作系统中，root的权限是最高的，相当于windows的administrator，拥有最高权限，能执行任何命令和操作。
   在系统中，通过UID来区分用户的权限级别，UID等于0，表示此用户具有最高权限，也就是管理员。
   其他的用户UID依次增加，通过/etc/passwd用户密码文件可以查看到每个用户的独立的UID。

   每一个文件或者目录的权限，都包含一个用户权限、一个组的权限、其他人权限，
   例如下：
   标红第一个root表示该文件所有者是root用户，
   第二个root代表该文件的所属的组为root组，其他用户这里默认不标出。
    [root@node1 ~]# ls -l monitor_log.sh
   -rw-r--r-- 1 root root 91 May  7 20:21 monitor_log.sh

   [root@node1 ~]#
   如果我们想改变某个文件的所有者或者所属的组，可以使用命令chown
   chown  –R  test:test  monitor_log.sh即可。

   每个Linux文件具有四种访问权限：可读(r)、可写(w)、可执行(x)和无权限(-)。
   利用ls -l命令可以看到某个文件或目录的权限，它以显示数据的第一个字段为
    准。
    第一个字段由10个字符组成，如下：
   [root@node1 ~]# ls -l monitor_log.sh
   -rw-r--r-- 1 root root 91 May  7 20:21 monitor_log.sh
   [root@node1 ~]#
      第一位表示文件类型，-表示文件，d表示目录；后面每三位为一组。
      第一组：2-4位表示文件所有者的权限，即用户user权限，简称u
      第二组：5-7位表示文件所有者所属组成员的权限，group权限，简称g
      第三组：8-10位表示所有者所属组之外的用户的权限，other权限，简称o
   从上面这个文件，我们可以看出，monito_log.sh文件对应的权限为：
   root用户具有读和写的权限，root组具有读的权限，其他人具有读的权限。

   为了能更简单快捷的使用和熟悉权限，rwx权限可以用数字来表示，分别表示为r（4）、w（2）、x（1）。
   Monitor_log.sh权限可以表示为：644
   如果给某个文件授权，命令为chmod：chmod 777 monitor_log.sh
```

```
14.
   Linux网络配置管理

   熟悉了常用的命令和Linux权限，那接下来如何让所在的Linux系统上网呢？管理linux服务器网络有哪些命令呢？
      Linux服务器默认网卡配置文件在/etc/sysconfig/network-scripts/下，
      命名的名称一般为:
      ifcfg-eth0
      ifcfg-eth1 ，
      eth0表示第一块网卡，eth1表示第二块网卡，依次类推。一般DELL R720标配有4块千兆网卡。

      修改网卡的IP，可以使用命令: vi /etc/sysconfig/network-scripts/ifcfg-eth0
   如果是DHCP获取的IP，默认配置如下：
   # Advanced Micro Devices [AMD] 79c970 [PCnet32 LANCE]
   DEVICE=eth0
   BOOTPROTO=dhcp
   HWADDR=00:0c:29:52:c7:4e
   ONBOOT=yes
   TYPE=Ethernet

   如果是静态配置的IP，ifcfg-eth0网卡配置内容如下：
   # Advanced Micro Devices [AMD] 79c970 [PCnet32 LANCE]
   DEVICE=eth0
   BOOTPROTO=static
   HWADDR=00:0c:29:52:c7:4e
   ONBOOT=yes
   TYPE=Ethernet
   IPADDR=192.168.33.10
   NETMASK=255.255.255.0
   GATEWAY=192.168.33.1

   网卡参数详解如下：
   DEVICE=eth0   #物理设备名
   ONBOOT=yes   # [yes|no]（重启网卡是否激活设备）
   BOOTPROTO=static #[none|static|bootp|dhcp]（不使用协议|静态分配|BOOTP协议|DHCP协议）

   TYPE=Ethernet  #网卡类型
   IPADDR=192.168.33.10 #IP 地址
   NETMASK=255.255.255.0 #子网掩码
   GATEWAY=192.168.33.1 #网关地址

   网卡配置完毕，重启网卡，命令: /etc/init.d/network restart 即可。


   查看ip命令：ifconfig 查看当前服务器所有网卡的IP，可以单独指定，ifconfig eth0 查看eth0的IP地址。
   网卡配置完毕，如果来配置DNS，首先要知道DNS配置在哪个目录文件下，vi  /etc/resolv.conf 文件:
   在该文件里面添加如下两条：
   nameserver 202.106.0.20
   nameserver 8.8.8.8
   从上到下，分别表示主DNS，备DNS。配置完毕后，不需要重启网卡,DNS立即生效。
   可以ping www.baidu.com 看看效果:

   IP配置完毕后，我们可以通过远程工具来连接Linux服务器，常见的Linux远程连接工具有:putty、secureCRT（主流）、xshell、xmanger等工具。
   下载安装secureCRT，打开工具，然后如图配置：
   点击左上角quick connect快速连接，弹出界面，然后输入IP，用户名，端口默认是22，然后点击下方的connect连接，会提示输入密码，输入即可。

   弹出输入密码框：

   进入远程界面，与服务器真实登录一样，然后可以执行命令：
```


```
   通过这几章的学习，我们已经熟练了Linux常用命令的操作，权限网络、网络配置、远程连接等知识，那接下来我们还能做什么呢？
   我们已经差不多入门了，接下来就是更进一步的服务配置，Linux系统到底用来做什么呢？接下来的章节将跟大家一起来学习。

   Linux系统的应用，我们最开始介绍的时候简单介绍过，目前大中型企业都用它来承载web网站、数据库、虚拟化平台等，
   那接下来我们将在Linux系统安装各种服务和软件来实现Linux真正的价值。

   2.1. 5         Linux软件包管理必备命令

   2.   Linux服务篇
   3.1            Linux服务部署

   3.1. 1         构建NTP时间服务器

   NTP服务器是用于局域网服务器时间同步使用的，可以保证局域网所有的服务器与时间服务器的时间保持一致，某些应用对时间实时性要求高的必须统一时间。
   互联网的时间服务器也有很多，例如ntpdate ntp.fudan.edu.cn 复旦大学的NTP免费提供互联网时间同步。
   NTP服务器监听端口为UDP的123，那就需要在本地防火墙开启运行客户端访问123端口，vi /etc/sysconfig/iptables添加如下规则：
   -A INPUT -m state --state NEW -m udp -p udp --dport 123 -j ACCEPT
   NTP时间服务器配置：
   yum install ntp ntpdate -y 即可！
   修改ntp.conf配置文件
   cp  /etp/ntp.conf /etc/ntp.conf.bak
   vi /etc/ntp.conf 只修改如下两行，把#号去掉即可！
   server 127.127.1.0     # local clock
   fudge  127.127.1.0 stratum 10
   以守护进程启动ntpd
   /etc/init.d/ntpd start 即可
   （注意*： ntpd启动后，客户机要等几分钟再与其进行时间同步，否则会提示“no server suitable for synchronization found”错误。）
   配置时间同步客户机
   crontab -e
   增加一行，在每天的6点10分与时间同步服务器进行同步
   10 06 * * * /usr/sbin/ntpdate ntp-server的ip >>/usr/local/logs/crontab/ntpdate.log
   备注：如果客户机没有ntpdate，可以yum –y install ntp 即可！
   以下是ntp服务器配置文件内容(局域网NTP，如果需要跟外网同步，添加外网server即可)
   driftfile /var/lib/ntp/drift
   restrict default kod nomodify notrap nopeer noquery
   restrict -6 default kod nomodify notrap nopeer noquery
   restrict 127.0.0.1
   restrict -6 ::1
   server  127.127.1.0     # local clock
   fudge   127.127.1.0 stratum 10
   includefile /etc/ntp/crypto/pw
   keys /etc/ntp/keys
   下面是参数详解：

   restrict default ignore	# 关闭所有的 NTP 要求封包
   restrict 127.0.0.1	# 开启内部递归网络接口 lo
   restrict 192.168.0.0 mask 255.255.255.0 nomodify	#在内部子网里面的客户端可以进行网络校时，但不能修改NTP服务器的时间参数。
   server 198.123.30.132	#198.123.30.132作为上级时间服务器参考
   restrict 198.123.30.132	#开放server 访问我们ntp服务的权限
   driftfile /var/lib/ntp/drift	在与上级时间服务器联系时所花费的时间，记录在driftfile参数后面的文件内
   broadcastdelay 0.008	#广播延迟时间

   自此NTP服务搭建完毕，然后在所有客户端crontab里面添加如下语句：
   0  0   *  *  * /usr/sbin/ntpdate  10.0.0.155 >>/data/logs/ntp.log 2>&1

   3.1. 2         构建DHCP服务器

   DHCP(Dynamic Host Configuration Protocol，动态主机配置协议)是一个局域网的网络协议，使用UDP协议工作，主要用途：给内部网络或网络服务供应商自动分配IP地址，DHCP有3个端口，其中UDP67和UDP68为正常的DHCP服务端口，分别作为DHCP Server和DHCP Client的服务端口。
   DHCP可以部署在服务器、交换机或者服务器，可以控制一段IP地址范围，客户机登录服务器时就可以自动获得DHCP服务器分配的IP地址和子网掩码。其中DHCP所在服务器的需要安装TCP/IP协议，需要设置静态IP地址、子网掩码、默认网关。
   正式安装DHCP服务：
   Yum  install  dhcp dhcp-devel –y 即可，然后修改DHCP /etc/dhcpd.conf配置文件内容如下：
   ddns-update-style interim;
   ignore client-updates;
   next-server  192.168.0.79;
   filename "pxelinux.0";
   allow booting;
   allow bootp;
   subnet 192.168.0.0 netmask 255.255.255.0 {
   # --- default gateway
   option routers          192.168.0.1;
   option subnet-mask      255.255.252.0;
   #   option nis-domain       "domain.org";
   #  option domain-name "192.168.0.10";
   #   option domain-name-servers  192.168.0.11;
   #   option ntp-servers      192.168.1.1;
   #   option netbios-name-servers  192.168.1.1;
   # --- Selects point-to-point node (default is hybrid). Don't change this unless
   # -- you understand Netbios very well
   #   option netbios-node-type 2;
   range  dynamic-bootp  192.168.0.100 192.168.0.200;
   host ns {
   hardware ethernet  00:1a:a0:2b:38:81;
   fixed-address 192.168.0.101;}
   }
   参数解析如下：

   选    项	解    释

   ddns-update-style interim|ad-hoc|none	 参数用来设置DHCP服务器与DNS服务器的动态信息更新模式：interim为DNS互动更新模式，ad-hoc为特殊DNS更新模式，none为不支持动态更新模式。
   next-server ip	pxeclient远程安装系统，指定tftp server 地址
   filename	开始启动文件的名称，应用于无盘安装，可以是tftp的相对或绝对路径
   ignore client-updates	为忽略客户端更新
   subnet-mask	为客户端设定子网掩码
   option routers	为客户端指定网关地址
   domain-name	为客户端指明DNS名字
   domain-name-servers	为客户端指明DNS服务器的IP地址
   host-name	为客户端指定主机名称
   broadcast-address	为客户端设定广播地址
   ntp-server	为客户端设定网络时间服务器的IP地址
   time-offset	为客户端设定格林威治时间的偏移时间，单位是秒
   注意如上配置，需要修改成对应服务器网段IP，然后重启DHCP服务，/etc/init.d/dhcpd restart即可。
   客户端要从这个DHCP服务器获取IP，需要做简单的设置，如果是linux需要把/etc/sysconfig/network-scritps/ifcfg-eth0里BOOTPROTO相改成dhcp即可，windows机器的话，需要修改本地连接，把它设置成自动获取IP即可。
   BOOTPROTO=dhcp

   3.1. 3         搭建Samba服务器

   Samba是在Linux和UNIX系统上实现SMB协议的一个免费软件，由服务器及客户端程序构成，
   SMB（Server Messages Block，信息服务块）是一种在局域网上共享文件和打印机的一种通信协议，它为局域网内的不同计算机之间提供文件及打印机等资源的共享服务。
   SMB协议是客户机/服务器型协议，客户机通过该协议可以访问服务器上的共享文件系统、打印机及其他资源。通过设置“NetBIOS over TCP/IP”使得Samba不但能与局域网络主机分享资源，还能与全世界的电脑分享资源。
   安装SAMBA服务器：
   Yum install  samba –y
   安装完毕，然后做如下设置（过滤#号行、空行如下命令）
   cp /etc/samba/smb.conf /etc/samba/smb.conf.bak ;egrep -v "#|^$" /etc/samba/smb.conf.bak |grep -v "^;" >/etc/samba/smb.conf
   查看smb.conf配置文件如下：
   [global]
           workgroup = MYGROUP
           server string = Samba Server Version %v
           security = share
           passdb backend = tdbsam
           load printers = yes
           cups options = raw

   [temp]
        comment=Temporary file space
        path=/tmp
        read only=no
        public=yes

   [data]
        comment=Temporary file space
        path=/data
        read only=no
        public=yes
   根据需求修改之后重启服务：
   [root@node1 ~]# /etc/init.d/smb restart
   Shutting down SMB services:                                [FAILED]
   Shutting down NMB services:                                [FAILED]
   Starting SMB services:                                     [  OK  ]
   Starting NMB services:                                     [  OK  ]


   workgroup =	WORKGROUP 设Samba Server 所要加入的工作组或者域。
   server string = Samba Server Version %v	Samba Server 的注释，可以是任何字符串，也可以不填。宏%v表示显示Samba的版本号。




   security = user	1.share：用户访问Samba Server不需要提供用户名和口令, 安全性能较低。
   2. user：Samba Server共享目录只能被授权的用户访问,由Samba Server负责检查账号和密码的正确性。账号和密码要在本Samba Server中建立。
   3. server：依靠其他Windows NT/2000或Samba Server来验证用户的账号和密码,是一种代理验证。此种安全模式下,系统管理员可以把所有的Windows用户和口令集中到一个NT系统上,使用Windows NT进行Samba认证, 远程服务器可以自动认证全部用户和口令,如果认证失败,Samba将使用用户级安全模式作为替代的方式。
   4. domain：域安全级别,使用主域控制器(PDC)来完成认证。
   comment = test	是对该共享的描述，可以是任意字符串。
   path = /home/test	共享目录路径
   browseable= yes/no 	用来指定该共享是否可以浏览。
   writable = yes/no	writable用来指定该共享路径是否可写。
   available = yes/no	available用来指定该共享资源是否可用
   admin users = admin	该共享的管理者
   valid users = test	允许访问该共享的用户
   invalid users = test	禁止访问该共享的用户
   write list = test	允许写入该共享的用户
   public = yes/no	public用来指定该共享是否允许guest账户访问。

   在浏览器里面访问方式为：\\192.168.33.10 （SMB文件共享服务端IP），如何没有权限访问，需要注意防火墙和selinux设置，可以使用如下命令关闭：
   /etc/init.d/iptables stop ;sed  –i   ‘/SELINUX/s/enforcing/disabled’  /etc/sysconfig/selinux


   3.1. 4         搭建NFS服务器

   NFS 是Network File System的缩写，即网络文件系统。一种使用于分散式文件系统的协定，由Sun公司开发，于1984年向外公布。功能是通过网络让不同的机器、不同的操作系统能够彼此分享个别的数据，让应用程序在客户端通过网络访问位于服务器磁盘中的数据，是在类Unix系统间实现磁盘文件共享的一种方法。
   NFS在文件传送或信息传送过程中依赖于RPC协议。RPC，远程过程调用 (Remote Procedure Call) 是能使客户端执行其他系统中程序的一种机制。NFS本身是没有提供信息传输的协议和功能的。
   NFS应用场景，常用于高可用文件共享，多台服务器共享同样的数据，可扩展性比较差，本身高可用方案不完善，取而代之的数据量比较大的可以采用MFS、TFS、HDFS等等分布式文件系统。
   NFS安装配置：
   Yum  install nfs*  portmap  -y 如下图，安装成功即可。

   NFS安装完毕，需要创建共享目录，共享目录在/etc/exports文件里面配置，可配置参数如下：
   /data/      192.168.33.11(rw,sync,no_hide,no_all_squash)
   在配置文件中添加如上一行，然后重启Portmap，NFS服务即可，/etc/init.d/portmap restart ;/etc/init.d/nfs restart
   第一列/data/表示需要共享的目录。
   IP表示允许哪个客户端访问。
   IP后括号里的设置表示对该共享文件的权限。
   ro                      只读访问
   rw                      读写访问
   sync                    所有数据在请求时写入共享
   hide                    在NFS共享目录中不共享其子目录
   no_hide                 共享NFS目录的子目录
   all_squash              共享文件的UID和GID映射匿名用户anonymous，适合公用目录。
   no_all_squash           保留共享文件的UID和GID（默认）
   root_squash             root用户的所有请求映射成如anonymous用户一样的权限（默认）
   no_root_squas           root用户具有根目录的完全管理访问权限


   Linux客户端，如何想使用这个NFS文件系统，需要在客户端挂载，挂载命令为：
   Mount –t  nfs  192.168.33.10:/data/    /mnt 即可。如果有报错根据错误信息排查。常见问题有rpc服务没有启动、防火墙没关闭、selinux未关闭等问题。（拓展* 有兴趣的童鞋可以研究MFS（分布式文件系统）。）

   3.1. 5         搭建FTP服务器

   FTP 是文件传输协议，正是由于这种协议使得主机间可以共享文件。 FTP 使用TCP 生成一个虚拟连接用于控制信息，然后再生成一个单独的 TCP 连接用于数据传输。
   vsftpd是一款在Linux发行版中最主流的FTP服务器程序；特点是小巧轻快，安全易用；能让其自身特点得发发挥和掌握。
   目前在开源操作系统中常用的FTP服务器程序主要有vsftpd、ProFTPD、PureFTPd和wuftpd等，这么多FTP服务器程序，关键在于自己熟练哪一个就使用哪一个。今天我们来研究一下VSFTPD简单安装及使用。安装命令: yum  install vsftpd*  -y

   修改配置文件如下：
   #vsftpd config 2014 by wugk
   anonymous_enable=NO    //禁止匿名用户访问
   local_enable=YES  //允许本地用户登录FTP
   write_enable=YES   //运行用户在FTP目录有写入的权限
   local_umask=022   //设置本地用户的文件生成掩码为022，默认是077
   dirmessage_enable=YES //激活目录信息,当远程用户更改目录时,将出现提示信息
   xferlog_enable=YES   //启用上传和下载日志功能
   connect_from_port_20=YES  //启用FTP数据端口的连接请求
   xferlog_std_format=YES  //是否使用标准的ftpd xferlog日志文件格式
   listen=YES  //使vsftpd处于独立启动监听端口模式
   pam_service_name=vsftpd //设置PAM认证服务配置文件名称，文件存放在/etc/pam.d/目录
   userlist_enable=YES   //用户列表中的用户是否允许登录FTP服务器,默认是不允许
   tcp_wrappers=YES    //使用tcp_wrqppers作为主机访问控制方式

   1)    第一种方法就是使用系统用户登录FTP，但是也是比较危险的，先测试系统用户登录FTP，在Linux系统上创建useradd  test 用户，并为其设置名，然后在xp客户端打开我的电脑资源里面访问 ftp://192.168.33.10，输入用户名和密码即可访问，进行创建和删除操作。
   2)    第二种方法比较安全，配置相对复杂一点，就是使用vsftpd虚拟用户登录FTP服务器进行常见的操作。
   Ø       首先安装FTP 虚拟用户需要用到的软件及认证模块
   yum install pam* db4* --skip-broken –y
   创建并生成vsftpd数据库文件vi /etc/vsftpd/ftpusers.txt，内容如下：
   第一行为FTP虚拟用户，登录用户名，第二行为密码，第三行为用户名，依次类推。
   wugk
   1
   wugk1
   1
   Ø       生成数据库文件命令：
   db_load -T -t hash -f /etc/vsftpd/ftpusers.txt /etc/vsftpd/vsftpd_login.db
   chmod 700 /etc/vsftpd/vsftpd_login.db
   Ø       配置PAM验证文件：
   在配置文件vi /etc/pam.d/vsftpd 行首加入如下两行认证语句：（如果是32位，lib64需改成lib，如果RedHat，加入的语句不一样，需注意）
   auth    sufficient      /lib64/security/pam_userdb.so     db=/etc/vsftpd/vsftpd_login
   account sufficient      /lib64/security/pam_userdb.so      db=/etc/vsftpd/vsftpd_login
   Ø       创建vsftpd映射本地用户:
   所有的FTP虚拟用户需要使用一个系统用户，这个系统用户不需要密码，也不需要登录。主要用来做虚拟用户映射使用。
   useradd  –d /home/ftpuser –s /sbin/nologin ftpuser
   Ø       修改完整版配置文件内容如下：
   anonymous_enable=NO
   local_enable=YES
   write_enable=YES
   local_umask=022
   dirmessage_enable=YES
   xferlog_enable=YES
   connect_from_port_20=YES
   xferlog_file=/var/log/vsftpd.log
   xferlog_std_format=YES
   ascii_upload_enable=YES
   ascii_download_enable=YES
   listen=YES

   guest_enable=YES
   guest_username=ftpuser
   pam_service_name=vsftpd
   user_config_dir=/etc/vsftpd/vsftpd_user_conf
   virtual_use_local_privs=YES

      保存重启,/etc/init.d/vsftpd restart 即可使用虚拟用户登录，这时候所有的虚拟用户共同使用/home/ftpuser目录上传下载，如果想使用自己独立的目录，可以在/etc/vsftpd/vsftpd_user_conf目录创建各自的配置文件，如给wugk创建独立的配置文件：
   vi /etc/vsftpd/vsftpd_user_conf/wugk ，内容如下，建立自己的FTP目录。
   local_root=/home/ftpsite/wugk
   write_enable=YES
   anon_world_readable_only=YES
   anon_upload_enable=YES
   anon_mkdir_write_enable=YES
   anon_other_write_enable=YES
    重启，使用客户端登录FTP，测试即可。关于FTP讲解就到此，windows还可以使用Server-U来搭建FTP服务器端，有兴趣的童鞋可以研究一下。
   Ø       FTP主被动模式
   FTP主动模式：客户端从一个任意的非特权端口N（N>1024）连接到FTP服务器的port 21命令端口。然后客户端开始监听端口N+1，并发送FTP命令“port N+1”到FTP服务器。接着服务器会从它自己的数据端口（20）连接到客户端指定的数据端口（N+1）。
   FTP被动模式：客户端从一个任意的非特权端口N（N>1024）连接到FTP服务器的port 21命令端口。然后客户端开始监听端口N+1，同时客户端提交 PASV命令。服务器会开启一个任意的非特权端口（P >1024），并发送PORT P命令给客户端。然后客户端发起从本地端口N+1到服务器的端口P的连接用来传送数据。
```