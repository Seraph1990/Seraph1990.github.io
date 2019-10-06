---
layout: post
title:  "《Ubuntu Linux操作系统》读书笔记"
description: 《Ubuntu Linux操作系统》相关读书笔记
date:   2019-10-06 09:51:36
categories: Ubuntu Linux
---
文|Seraph   
本文主要摘录了《Ubuntu Linux操作系统》的相关读书笔记。

#### 一、Ubuntu安装与基本使用
1. Linux是一种起源于UNIX，以可移植操作系统接口（Portable Operating System Interface, POSIX）标准为框架发展起来的开放源代码的操作系统。
2. GNU是“GNU‘s Not UNIX”的递归缩写，其含义是开发出一套与UNIX相似而不是UNIX的系统。
3. GNU包含以下三个协议条款：
* GNU通用公共许可证（GNU General Public License, GPL)
* GNU较宽松公共许可证（GNU Lesser General Public License, LGPL）
* GNU自由文档许可证（GNU Free Documentation License, GFDL）
1991年，Linus Torvalds按照GPL条款发布了Linux。
4. Windows系列操作系统采用为内核体系结构，模块化设计，将对象分为用户模式层和内核模式层。
Linux操作系统是采用但内核模式的操作系统，内核代码结构紧凑，执行速度快。
5. linux内核版本
[主版本].[次版本].[修改版本]-[附版本]
次版本表示内核类型，偶数说明稳定的产品版本，奇数说明是开发中的实验版本。
6. Window系统一般磁盘从C开始分配，因为A和B表示软盘。
7. 初次使用Ubuntu系统，如果要使用root用户，需要使用``sudo passwd root``给root添加密码。
8. 如软件安装包下载失败，可以在``软件和更新``中变更软件源。

#### 二、图形界面与命令行
1. Linux图形架构
![ Linux图形架构](https://imgconvert.csdnimg.cn/aHR0cHM6Ly91cGxvYWQtaW1hZ2VzLmppYW5zaHUuaW8vdXBsb2FkX2ltYWdlcy80NTU3NjY1LWE2YTRlNjhjZTUxZDY1OTQucG5n?x-oss-process=image/format,png)
2. ``Ctrl+Alt+T``打开仿真终端窗口
3. ``Ctrl+Alt+Fn``切换控制台界面，linux系统允许用户同时打开6个虚拟控制台（tty1～tty6）。
4. Shell是用户和系统交互的接口
Ubuntu默认使用的Shell程序是bash
5. 正则表达式
* 通配符

|符号|含义|
|---|---|
|*|表示任何字符串|
|?|表示任何单个字符|
|[]|表示一个字符序列|
|!|在[]中使用！表示排除其中任意字符|
|^|只在一行的开头匹配字符串|
|$|只在行尾匹配字符串|

* 模式表达式
模式表达式是那些包含一个或多个通配符的字符串，各模式之间以竖线（|）分开

|符号|含义|
|---|---|
|*|匹配任意多个模式|
|+|匹配1个或多个模式|
|?|匹配模式表中任何一个模式|
|@|仅匹配模式表中一个给定模式|
|!|除了给定模式表中的一个模式之外，它可以匹配其他任何字符串|
6. Shell中的特殊字符
* 单引号括起来的字符串视为普通字符串
* 双引号括起来的的字符串，除$、\、单引号和双引号仍然作为特殊字符并保留其特殊功能外，其他都视为普通字符对待
* 反单引号括起来的字符串被Shell解释为命令行
7. 环境变量

|环境变量|含义|
|---|---|
|PATH|可执行命令的搜索路径|
|HOME|用户主目录|
|LOGNAME|当前用户的登录名|
|HOSTNAME|主机名|
|PSI|当前命令提示符|
|SHELL|用户当前的Shell|

8. 一个命令行中使用多个命令，用``；``隔开；
用 ``\``表示命令行持续到下一行。
9. Ctral+D结束输入符
Ctrl+C强制中断

#### 三、用户与组管理
1. Ubuntu初始使用时，root没有密码的，所以不能使用``su root``切换，但是可以使用``sudo su root``命令。
2. UID，root账户的UID为0，系统账户的UID的范围为1～499，还包括65534，常规用户的UID默认从1000开始顺序编号。
3. GID，root组的GID为0，系统组的GID的范围为1～499，自定义组由管理员创建，GID默认从1000开始。
4. 一个用户可以同时属于多个组，其中某个组为该用户的主要组，其他组为该用户的次要组。
5. Linux用户账户的其相关信息（除密码外）均存放在``/etc/passwd``配置文件中
每条信息格式含义如下：
``账户名:密码:UID:GID:注释:主目录:Shell``
如果要禁用某个账户，可以在passwd文件中该账户记录行前加`*`。
6. 账户密码信息保存在``/etc/shadow``中，且密码都是由MD5加密后保存的。
每条密码信息格式含义如下：
``账户名:密码:最近一次修改:最短有效期:最长有效期:过期前警告器:过期日期:禁用:保留用于未来扩展``
日期格式从1970年1月1日到修改日期的天数。
7. 组账户配置文件``/etc/group``
信息格式如下：
``组名:组密码:GID:组成员列表``
该文件中，用户的主要组不会将该用户自己作为成员列出。
8. 组密码配置文件``/etc/gshadow``
信息格式如下：
``组名:加密后的组密码:组管理员:组成员列表``
9. 安装“用户与组”管理命令
``sudo apt install gnome-system-tools``
10. 文本分析工具``awk``
如下命令可以列举出passwd文件中所有用户
``awk -F':' '{print $1}' /etc/passwd``
11. 添加用户账户``useradd``
用法格式：
``useradd [选项] <用户名>``
对于没有指定选项的情况，系统将根据``/etc/default/useradd``配置文件中的定义为新建用户账户提供默认值。
``-D``选项用于显示默认的``useradd``配置。
相似命令：``adduser``
12. 管理用户账户密码``passwd``
用法格式：
``passwd [选项] <用户名>``
13. 修改用户账户``usermod``
用法格式：
``usermod [选项] <用户名>``
14. 更该用户的个人信息``chfn``
用法格式：
``chfn [选项] <用户名>``
15. 删除用户``userdel``
用法格式：
``userdel [-r] <用户名>``
如果选择``-r``，则在删除该账户的同时，一并删除该账户对应的主目录和邮件目录。
相似命令：``deluser``
16. 创建组账户命令``groupadd``
用法格式：
``groupadd [选项] <组名>``
相似命令：``addgroup``
17. 修改组账户命令``groupmod``
18. 删除组账户命令``groupdel``
相似命令：``delgroup``
19. 显示某用户所属的全部组命令``groups``
如果没有指定用户，则显示当前用户。
20. 向组中添加或删除用户命令``gpasswd``
相似命令：``adduser deluser``
21. 查看用户信息命令``id``
22. 查看的登录用户命令``who``
23. 查看系统的历史登录情况命令``last``

#### 四、文件与目录管理
1. 特殊目录符号

|符号|含义|
|---|---|
|. 或 ./|当前目录|
|.. 或 ../|上一层目录|
|~|当前用户的主目录|

2. FHS(Filesystem Hierarchy Standard)规范

|目录|存放内容|
|---|---|
|/bin|存放用于系统管理维护的常用实用命令文件|
|/boot|存放用于系统启动的内核文件和引导装载程序文件|
|/dev|存放设备文件|
|/etc|存放系统配置文件|
|/home|各个用户的主目录|
|/lib|存放动态连接共享库|
|/media|为光盘软盘等设备提供的默认挂载点|
|/mnt|为某设备提供的默认挂载点|
|/root|root用户主目录|
|/proc|系统自动产生的映射文件|
|/sbin|存放系统管理员或者root用户使用的命令文件|
|/usr|存放应用程序和文件|
|/var|保持经常变化的内容，如系统日志、打印|

3. 文件结构：索引节点（包含文件权限/所有者/大小等信息）+数据
4. 文件类型：普通文件、目录文件、设备文件、链接文件
* 目录文件：当文件添加到一个目录中时，该目录的大小会增加，当删除文件时，目录的尺寸并未减少，内核对该目录项做上特殊标记，以便下次添加一个文件时重新使用它；
* 链接文件：分为符号链接（类似Windows快捷方式）和硬链接（对原文件的建立的别名，无法区分硬链接与原文件）
5. Linux将文件访问者身份分为：所有者（owner）、所属组（group）、其他用户（others）。
文件访问权限：读（read）、写（write）、执行（execute）。
6. ``ls -l``执行后文件信息格式如下
``rwxr-xr-x 2 liushupeng liushupeng 4096 Dec 28 2018 Videos``
``文件权限    链接 所有者 所属组 容量 修改日期 文件名 ``
第一列的文件权限含义：
字符1：文件类型（d表示目录，-表示文件，l表示链接文件，b表示块设备文件，c表示字符设备文件）
字符2~4：所有者权限（r表示读，w表示写，x表示执行）
字符5~7：所属组权限
字符8~10：其他用户的权限
7. 文件权限数字表示法：r(4) w(2) x(1)
8. umask命令查询默认文件访问权限掩码



#### 五、磁盘存储管理
1. MBR分区格式，一个磁盘最多4个主分区，最多16个分区（全分成逻辑分区的情况下）
2. GPT分区格式，磁盘最多可以创建128个主分区
3. 扩展分区下的逻辑分区从5开始命名
4. Linux分区作用：比如/boot分区，单独给他挂载分区的话，当根分区出了问题，linux也依然能启动
5. swap一般建议为物理内存的2~2.5倍
6. 磁盘管理工具：fdisk、parted
7. 创建文件系统命令：mkfs
8. 查询文件系统的UUID命令：blkid
9. 设置和清除文件系统的UUID命令：tune2fs
10. 目录挂载命令：mount
11. 查询磁盘占用情况命令：df
12. 查询文件和目录的磁盘使用情况命令：du
13. 磁盘分区工具：Gparted
14. 备份和恢复命令：dump、restore
15. 光盘刻录：cdrecord
16. 镜像生成：mkisofs

#### 六、软件包管理
1. 常见的软件包格式：
``RPM(RedHat Package Manager)``，已成为目前Linux各发行版中应用最广泛的软件包格式，使用rpm工具来管理； 
``Deb(Debian packager)``，是Debian和Ubuntu系列发行版本使用的软件包格式，使用dpkg命令进行管理。
使用这两种包管理都需要自己考虑软件包**依赖性**。
2. 高级软件包管理工具：
``Yum(Yellow dog Updater, Modified)``是基于RPM包的软件包管理；
``APT(Advanced Packaging Tools``是Debian及派生发行版的软件包管理器。
使用这两种高级软件包管理器，可以自动处理依赖性关系。但如果安装过程中由于兼容问题、安装源等问题停止，则需要用户自己来解决软件依赖问题。
3. PPA(Personal Package Archive)是个人软件包档案，Ubuntu官方仓库收录的软件比较正式，版本也就相对滞后，PPA则可以第一时间体验到最新版本软件。
PPA维护网站地址[launchpad.net](https://launchpad.net)
添加PPA源命令：``add-apt-repository ppa:user/ppa-name``
删除PPA源命令： ``add-apt-repository -r ppa:user/ppa-name``
添加PPA源后记得更新软件更新列表，再安装。
4. Ubuntu的  ``/var/lib/apt/lists``目录存放的是已经下载的各软件源的元数据；
  ``var/lib/dpkg/states``目录存放的是Ubuntu软件中心和APT安装和卸载软件的信息。
软件更新器通过比较这两个目录信息来判断是否更新。
5. apt-cache 查询软件包
``apt-cache pkgnames ``列出当前所有可用的软件包
``apt-cache search xxx``搜索包含xxx名字的所有软件
``apt-cache show 软件包名``查看指定名称的软件包的详情
``apt-cache depends 软件包名``查看软件包所依赖的软件包
``atp-cache rdepends 软件包名``查看软件包被哪些软件包所依赖
``apt-cache showpkg 软件包名``查看软件包的依赖关系信息
``apt-cache policy 软件包名``显示软件包的安装状态和版本信息

6. apt-get 操作软件包

|子命令|说明|
|---|---|
|apt-get update|获取最新的软件包列表，同步/etc/apt/sources.list和/etc/apt/sources.list.d中列出的源的索引|
|apt-get upgrade|更新当前系统中所有已安装的软件包，并同时更新这些软件包所依赖的软件包|  
|apt-get install|下载、安装软件包并自动解决依赖关系|
|apt-get remove|卸载指定的软件包|
|apt-get autoremove|自动卸载所有未使用的软件包|
|apt-get purge|卸载指定的软件包及其配置文件|
|apt-get source|下载软件包的源代码|
|apt-get clean|清理已下载的软件包，实际上是清理``/var/cache/apt/archives``目录中的软件包|
|apt-get autoclean|删除已卸载的软件的软件包备份|

* APT会将下载的Deb包缓存在硬盘上的目录``/var/cache/apt/archives``下


7.  升级的最新版本来源于``/etc/apt/sources.list``列表中给出的安装源，另外与该文件功能相同的是``/etc/apt/sources.list.d/``目录下的.list文件。
sources.list文件软件源记录信息含义：
eg. ``deb http://us.archive.ubuntu.com/ubuntu/ trusty-backports main restricted universe multiverse``
第1个字段用于指示软件包的类型；
第2个字段定义URL，表示提供软件源的CD-ROM、HTTP或FTP服务器的URL地址；
第3个字段定义软件包的发行版本或分类，用于帮助APT命令遍历软件库。这些字段是用空格隔开的字符串，每个字符串分别对应相应的目录结构。如下：
``main`` Canonical支持的开源软件，大部分都是从这个分支获取的；
``universe`` 社区维护的开源软件
``restricted ``由设备生产商专用的设备驱动软件
``multiverse``受版权或者法律保护的相关软件
``security``重要的安全更新
 ``updates``推荐的一般更新
``proposed``预览版的更新
``backports``无支持的更新，这种更新一般存在一些bug
这些信息实际上指向的是``http:archive.ubuntu.com/ubuntu/``下dists目录。
如要修改sources.list文件，需记得先使用cp命令备份一下文件

8. 新立得界面软件包管理器(Synaptic Package Manager)安装``apt-get install synaptic``

9. 使用``alien``可以将.rpm格式转换为.deb。

10. .run与.bin下载以后，给文件添加执行软件，安装即可
``chmod +x 文件名.run``
通常安装目录下回提供反安装脚本uninstall，如没有则会提供维护工具，例如QT的MaintenanceTool。
11. 使用源码安装比较复杂，再说。。。

#### 七、系统高级管理
1. 静态查询进程命令``ps``。
常用命令``ps -aux``显示的部分列信息含义如下：
VSZ表示占用虚拟内存的数量
RSS表示驻留内存的数量
TTY表示进程的控制终端(?表示与控制终端没有关联)
STAT表示进程运行状态(R准备就绪 S可中断的休眠状态 D不可中断的休眠状态 T暂停执行 Z不存在但暂时无法消除 W无足够内存页面可分配 <高优先级 N低优先级 L内存页面被锁定 s创建会话的进程 1多线程进程 +前台进程组）
2. 动态查询进程命令``top``，按空格键立即刷新。
部分列信息含义如下：
PR表示优先级
NI表示nice值(负值表示高优先级，正值表示低优先级）
VIRT表示进程使用的虚拟内存总量(单位kb)
RES表示进程使用的、未被换出的物理内存大小(单位kb)
SHR表示共享内存大小
S表示进程状态

3. 进程管理
* 进程终止键 Ctrl+Z
* 结束进程命令 kill（killall）
* 设置进程优先级 nice；调整进程优先级 renice

4. 系统启动
GRUB配置文件``/boot/grub/grub.cfg``，该文件是由``grub-mkconfig``命令根据``/etc/grub.d``中的模板和``/etc/default/grub``中的设置自动生成的。
所以我们编辑``/etc/default/grub``后，输入``update-grub``命令后修改内容便会自动更新至``/boot/grub/grub.cfg``文件中。

5. Ubuntu运行级别
Linux标准的运行级别从0~6，Debian系列的Linux版本一般讲运行级别2作为默认启动的级别。
Ubuntu与Redhat的运行级别如下：

|级别|Ubuntu|Redhat|
|---|---|---|
|0|关机(halt)|关机|
|1|单用户模式。以root身份开启一个虚拟控制台，主要用于管理员维护系统|同Ubuntu|
|2|带显示器(GUI)的完整多用户模式|多用户模式，不支持NFS。除不启动网络功能外，级别与3相同|
|3|带显示器(GUI)的完整多用户模式|完整多用户模式。允许所有用户登录，拥有完整的功能，但是以文本模式进入系统|
|4|带显示器(GUI)的完整多用户模式|保留。用户自定义环境|
|5|带显示器(GUI)的完整多用户模式|X11图形模式。与级别3功能一样，拥有完整功能，以图形界面模式进入系统|
|6|重启|重启|

6. Ubuntu现在采用Upstart与System V initialzation启动服务。

7. Linux使用Internet网络服务文件``/etc/services``来定义网络服务名和它们对应使用的端口号及协议。
Linux系统的端口范围为0~65535，分为三个不同意义的范围：
* 公认端口(端口0~1023)
* 已注册端口(端口1024~49151)，分配给用户进程或应用程序
* 动态或私有端口，又称临时端口
8. Ubuntu会将服务的启动脚本存放在``/etc/init.d``目录下。
Ubuntu将各个运行级别对应的脚本文件存放在``/etc/rcn.d``目录中。这些目录下存放的是指向``/etc/init.d``目录中脚本程序的符号链接。
命名规则为：S表示启动，K表示停止，后面接的数字表示执行顺序。
9. 从所有运行级别中删除指定服务的启动项
``update-rc.d -f 服务名 remove``
向所有运行级别中添加指定服务的启动项
``update-rc.d -f 服务名 defaults``

10. 使用Linux服务启动脚本管理服务语法：
``/etc/init.d/服务启动脚本名 {start|stop|status|restart|reload|force-reload}``
其中reload指不重新启动服务的前提下加载该服务的配置文件。
也可使用``service``命令来替代脚本的全路径。
``service 服务启动脚本名 {start|stop|status|restart|reload|force-reload}``

11. 配置服务启动状态
其它Linux发行版通常使用chkconfig工具来配置服务启动状态，Ubuntu可以使用sysv-rc-conf工具：
* ``sysv-rc-conf --list``命令将显示所有服务各个运行级别(1-6)的启动状态。
* ``sysv-rc-conf 服务名 <on|off>`` 启动或关闭某项指定服务
* ``sysv-rc-conf --level <运行级别列表> 服务名 <on|off>`` 设置指定运行级别中服务的启动状态
亦可以使用``update-rc.d``配置服务：
* ``update-rc.d [-f]  服务名 disable|enable [S|2|3|4|5]`` 

12. 自动化周期任务配置
* 使用``/etc/crontab``定义系统级周期性任务
* 使用``/etc/cron.d``添加指定时间计划任务
* 使用``crontab [-u 用户名] [-e|-l|-r]``，该命令生成的cron调度文件位于``/var/spool/cron/crontabs``目录下

13. 一次性任务配置at（batch类似）
* ``at 时间参数`` 
* ``atq``查看为未执行的at任务
* ``atrm  序号``删除指定的at作业
其中时间参数格式如下：
* ``HH:MM`` 时刻
* ``MMDDYY、MM/DD/YY、MM.DD.YY`` 日期格式
* 月日年英文格式(例如：``January 15 2018``) 
* 特定时间(``midnight``表示12:00 AM、``noon`` 12:00PM、 ``teatime`` 4:00 PM)
* ``now + n[minutes/hours/days/weeks]`` 从现在开始多少时间可以执行

14. 系统日志管理
一些Linux版本采用的是syslog工具，日志配置文件是``/etc/syslog.conf``
而Ubuntu采用的是rsyslog工具，日志配置文件为``/etc/rsyslog.conf``，并且将所有配置文件放置``/etc/rsyslog.d``目录下，默认的是``/etc/rsyslog.d/50-default.conf``。
每天信息配置格式：
``信息来源.优先级  处理方式``
* 信息来源如下

|信息来源|说明|信息来源|说明|
|---|---|---|---|
|authpriv|安全/授权|mail|电子邮件系统|
|cron|at或cron定时执行|news|网络新闻系统|
|daemon|守护进程|syslog|syslogd内部|
|ftp|ftp守护进程|user|一般用户级别|
|kern|内核|uucp|UUCP系统|
|lpr|打印系统|localN|保留|
* 优先级

|优先级|说明|优先级|说明|
|---|---|---|---|
|debug|调试排错信息，仅对程序开发人员有用|err|一般的错误信息|
|info|一般信息，可以忽略|crit|关键状态信息|
|notice|正常提示信息|alert|需特别注意的警报信息，一般要迅速更正|
|warn|可能是由问题的警告信息|emerg|最严重，紧急状况，一般是系统不可用|

15. 大部分日志文件放置在``/var/log``目录心中。


#### 八、Ubuntu桌面应用
1. FileZilla
2. GIMP图像处理
3. Inkscape矢量图像编辑器
4. Dia图表编辑器
5. VLC媒体播放
6. Audacity音频编辑工具
7. Openshot视频编辑工具
8. LibreOffice组件：Writer(文本文档 .odt)、Cacl(电子表格 .ods)、Impress(演示文稿 .odp)、Draw(绘图 .odg)、Math(公式 .odf)、Base(数据库 .odb)

#### 九、Shell编程
1. HelloWorld示例
```
#!/bin/bash
echo "Hello World!"
echo -n “当前日期和时间”
date
echo "当前登录用户名：`whoami`"
```
其中``#!/bin/bash``表示使用的Shell解析器是bash
``echo``命令用来显示提示信息，参数``-n``表示在显示信息时不自动换行
反引号用于命令转换，所以执行``whoami``命令

2. 包含外部脚本文件用法
`` . 脚本文件名``
或
``source 脚本文件名``

3. 执行Shell脚本方式
* 给脚本文件添加执行权限后，直接运行
* 指定Shell执行
``bash 脚本名称 [参数]``
*  重定向到Shell脚本
``bash < 脚本名``

4. 调试Shell脚本
``bash [选项] 脚本名``
* ``-v`` ``-x``选项都是允许用户查看Shell程序的读入和执行，不同的是``-v``打印的是命令行的原始内容，而``-x``打印的是替换后的命令行内容。

5. Shell变量类型分三种：
* 用户自定义
* 环境变量
* 内部变量，如下表

|内部变量|说明|
|---|---|
|$0|当前脚本的文件名|
|$n|传递给脚本或函数的参数。n表示第几个参数，当参数超过10时，用``{}``界定|
|$#|传递给脚本或函数的参数个数|
|$*|传递给脚本或函数的所有参数|
|$@|传递给脚本或函数的所有参数。被双引号包含时，会将各个参数分开输出|
|$?|上个命令的退出状态或返回值|
|$$|当前Shell进程ID|
可以使用``set [参数列表]``为位置参数重新赋值。

6. printf命令格式
``printf 格式字符串 [参数列表...]``

7. echo输出显示
单引号字符串不进行转义。

8. 变量值读取
``read 变量``
* ``-p``用于定义提示语句
* ``-n``用于设置最大读取长度

9.  变量替换
* ``${var}`` 替换为变量本来的值
* ``${var:-word}`` 如果变量var为空或已被删除，则返回word，但不改变var的值
* ``${var:=word}``如果变量var为空或已被删除，则返回word，并将var值设置为word
* ``${var:?message}`` 如果变量var为空或已被删除，则将消息message发送至标准错误输出
* ``${var:+word}`` 如果变量var被定义，则返回word，但不改变var的值

10. 数组
* 定义 ``myarray=(A B C D)``
* 读取 ``${myarrsy[下标]}``
* 读取所有 ``${myarrsy[*]}`` 或 ``${myarrsy[@]}``
* 读取元素个数 ``${#myarrsy[@]}``
* 读取数组单个元素长度 ``${#myarrsy[n]}``

11. 表达式
* ``expr 表达式``
* 需要计算如：``val=${5+3}``或``let val=5+3``

12. 逻辑表达式
* ``test 逻辑表达式``或``[ 逻辑表达式]``

13. 整数关系云算法
* ``-eq`` 相等
* ``-ne`` 不相等
* ``-gt`` 大于
* ``-lt`` 小于
* ``-ge`` 大于等于
* ``-le`` 小于等于

14. 字符检测云算法
* ``=`` 检测两个字符是否相等
* ``!=`` 检测两个字符是否不相等
* ``-z`` 检测字符是否长度是否为0
* ``-n`` 检测字符长度是否不为0

15. 文件测试运算符

|文件测试运算符|含义|
|---|---|
|-b|检测文件是不是块文件|
|-c|检测文件是不是字符设备文件|
|-d|检测文件是不是目录|
|-f|检测文件是不是普通文件|
|-g|检测文件是不是设置了SGID位|
|-k|检测文件是否设置了粘着位|
|-p|检测文件是不是具体管道|
|-u|检测文件是否设置了SUID位|
|-r|检测文件是否可读|
|-w|检测文件是否可写|
|-x|检测文件是否可执行|
|-s|检测文件是否为空|
|-e|检测文件或目录是否存在|

16. 布尔运算
* ``-a`` 与运算
* ``-o`` 或运算
* ``!`` 非运算

17. if语句
```
if [ 条件表达式1 ]
then
  语句序列1
elif [ 条件表达式2 ]
then
  语句序列2
else
  语句序列3
fi
```

18. case语句
```
case 值 in
模式1)
  语句序列1
;;
模式2)
  语句序列2
;;
......
模式n)
  语句序列n
;;
*)
  其它语句序列
esac
```

18. while语句
```
while 测试条件
do
  语句序列
done
```

19. until语句
```
until 测试条件
do
  语句序列
done
```

20. for语句
```
for 变量 [in 列表]
do
  语句序列
done
```

21. break、continue语句
``break [n]``表示跳出几层循环。

22. exit语句
``exit [n]``n是设定的退出值。

23. 函数定义和调用
```
[function] 函数名()
{
  命令序列
  [return 返回值]
}
```
直接使用函数名即能调用函数。


#### 十、C/C++编程
1. Emacs编辑器
2.

后面两章为JAVA、Android开发和LAMP平台与PHP开发环境的搭建，暂时不需要，就不记录了。


