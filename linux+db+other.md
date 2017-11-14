# linux 命令 

## 基本操作

### bash 和常用命令

- 用户名@主机
- 虚拟机下无界面  ctrl+alt+F2 有界面  ctrl+alt+F7
- 命令三部分：命令、参数、文件
- 历史命令搜索 history  +  ctrl+R，使用以前命令  !num
- [tldr python 客户端及其配置](https://github.com/tldr-pages/tldr-python-client)
- 后台作业：&、jobs、bg、fg
- 修改用户名密码 passwd
- 暂停某个程序 ctrl+z
- alias 别名
- date 查看当前日期
- sudo date -s 修改当前时间
- hwclock 硬件时间
- cal 日历
- uptime 查看系统运行时间

#### 环境变量
- env: 用户变量变量
- set: shell变量，包括私有变量和用户变量不同的shell有不同的私有变量bash
- export: 只是一种命令工具。不能算是环境变量。显示(设置)当前导出的用户变量的shell变量

#### 输出查看命令
- echo 显示输出内容
- cat 查看文件内容
- head，tail，more，less 显示内容，more或者less使用q退出

#### 查看硬件信息
- lspci 查看pci设备(相当于任务管理器)
- lsusb 查看usb设备
- lsmod 查看加载的模块(驱动)
- top 查看任务管理器

#### 归档、压缩
- zip linux.zip myfile
- unzip linux.zip
- gzip 用以压缩文件 gzip 文件名
- tar 文档进行归类
    - tar -cvf out.tar linuxcast 归档成一个文件(并没有压缩)
    - tar -xvf linuxcast.tar 释放归档的文件
    - tar -czvf back.tar.gz /etc z代表进行gzip压缩

- 经常使用的是：sudo tar -zxvf ./apache-hive-1.2.1-bin.tar.gz -C /usr/local

#### 查找
- locate kw 进行快速查找，一般使用前使用sudo updatedb
- find 查找位置 查找参数 /根目录 .当前目录
    - find / -name linuxcast
    - find / -type d 按照类型进行查找，d这里代表目录
- whereis 一般用来查找二进制文件
- which  一般用来搜寻文件安装位置


#### 网络

- 网络测试命令 ping、curl
- 查看ip: ifconfig
- 文件下载命令: wget 命令
- DNS解析: host, dig
- 路由表：iproute
- 追踪地址：traceroute
- 网络质量测试：mtr

#### 防火墙
- iptables

#### 其他
- xargs: 将上一个命令的结果作为参数传入下一个命令； 例如 cat urls.txt | xargs wget 或者 ls /etc/*.conf | xargs -i cp {} /home/likegeeks/Desktop/out  这里注意{ }的使用
- 自动回答yes或者no: yes | apt-get update
- 以根目录运行最后一个命令: sudo !!
- tee命令：将结果在控制台和log日志输出
- 重复执行一个命令，直到它运行成功使用while true进行
- [高级命令链接](https://mp.weixin.qq.com/s?__biz=MzAxODI5ODMwOA==&mid=2666541114&idx=1&sn=b2119c7dc7f94b7ba8c3f945c6c51500&chksm=80dcf491b7ab7d875ab934f45c4996491d8c7ec7d0cce21cad085887e9af4f40ba7ebfc793ab&scene=0#rd)
- ssh 登录和免密码登录？

### 文件基本结构、操作、目录


#### 文件
- linux 对大小写敏感
- . 开头的是隐藏文件  可以使用ls -a 显示
- 当前软件./pycharm.sh 这里的点代表当前目录，例如 cd .. 两个就是返回上层目录
- file 文件的类型

#### 文件操作
- 创建文件夹 `mkdir`
- 删除文件夹 rmdir
- 创建文件 touch
- 删除文件 rm -i 交互式删除 -f 强制性删除 -r 删除文件夹
- 重命名和移动文件 mv 
- 文件复制 `cp` 一般加 -r参数用来复制文件夹
- `scp` 配合公钥私钥无密码登录
- 挂载文件 mount -t vboxsf BaiduShare /mnt/bdshare/
- sudo apt-get install tree  显示文件结构 tree -L 1  显示一层

#### 文件架构
- bin：可执行的二进制文件
- sbin：只有root用户使用的二进制文件
- boot：引导文件，启动系统
- dev：硬件设备，/dev/null 表示空设备
- etc：配置文件，注意host的配置就在这个下
- usr：应用软件
- var：经常变化的文件例如log文件
- lib：库文件
- mount：挂载文件
- opt：一般用来存储大型软件
- proc: 实时信息
- tmp：临时目录

### vim

[vim插件配置](http://www.jianshu.com/p/f0513d18742a)

#### 命令模式

- 光标移动
    - 0 光标移动到行首
    - $ 光标移动到末尾
    - o 在当前行下面添加新行,此时vim自动进入插入模式
    - a 在当前光标后进行插入，此时自动进入插入模式
    - dd 删除整行
    - yy 复制当前行
    - n+yy 复制向下的n行
    - p 粘贴
    - u 撤销上一个操作
    - r 替换当前字符
    - / 查找关键字 + n (这里的n代表next)
    - 命令模式下 h左键 j下一行 k 上一行 l 右键
    - n + gg  移动到n行 (注意一定要先在 vimrc中  添加 set nu用来显示行号)
    - gg 移动到首行（在chrome vimium的插件 也是这样的）
    - G 移动到末尾
    - n + enter 向下移动n行
    - w  跳到下一个单词的开头

#### 插入模式

- 命令模式下按i 进入插入模式
- 编辑后使用shift+Z 保存退出

#### ex模式

- 命令模式下按 : 进入ex模式
- :w 保存
- :q 退出
- !系统命令，执行命令
- :sh 切换到命令行，并用ctrl+d切换
- :x 保存并退出  
- 强制退出 :q!


## 获取帮助

- 两种帮助，--help/-h  或者是 man帮助
- 帮助文档  man 可以通过/ + 关键字进行搜索

## 用户和权限基础

- 进入其他账户，不加参数进入管理员账户 su
- 赋予当前账户管理员权限 `sudo`
- chown 用户名  文件  -R 代表递归的修改目录下的所有文件  r表示读取权限，w写入权限，x代表执行 
- 权限基于UGO模型user， group， other，一共10位，第一位文件类型，后面每三个一组代表UGO
- 注：chown 为change own的简写，修改文件所属用户，r=4,w=2,x=1  则chown 777 代表UGO有所有权限或775
- 文件三种权限 r读，w写，x执行

## linux管道重定向和文本处理

### shell 数据流

| 名称     | 说明   | 编号   | 默认   |
| :----- | :--- | :--- | :--- |
| STDIN  | 标准输入 | 0    | 键盘   |
| STDOUT | 标准输出 | 1    | 终端   |
| STDERR | 标准错误 | 2    | 终端   |

### 管道和重定向

| 分类   | 关键字  | 定义                           | 例子                                       |
| :--- | :--- | :--------------------------- | :--------------------------------------- |
| 重定向  | >    | 将标准输出到文件(覆盖)                 | echo 'linux' > outfile                   |
|      | >>   | 将标准输出到文件(追加)                 | echo 'linux' >> outfile                  |
|      | 2>   | 将标准错误到文件(追加)                 | ls linux 2> outfile                      |
|      | 2>&1 | 将标准错误合并标准输出                  | ls linux 2>&1 outfile                    |
|      | <    | 将标准输入到文件                     | grep linux < infile                      |
|      | tee  | 将标准输出输出到多个文件,不加file默认console | ls \| tee \| head -10                    |
| 管道   | \|   | 将一个命令stout作为标准输入             | find / user hadoop 2> /dev/null &#124; grep video |

### 命令行文本工具
- 基于关键字的搜索(正则) grep  注意参数-i表示不区分大小写
- 基于列处理文本工具cut 常用来处理csv文件
- 文本统计 wc
- 文本排序 sort
- awk与sed工具怎样使用？

## 通配符和regex

通配符和正则表达式的区别：

- 通配符是shell内置的，常用于locate与find命令中，正则表达式是程序支持的，例如grep, sed, awk
- 通配符规则简单只有* , [ ], ? ，而regex更广泛

### 通配符[wildcard]

| 字符   | 含义        | 实例    |
| :--- | :-------- | :---- |
| \*   | 匹配0个或多个字符 | a\*b  |
| ?    | 匹配任意一个字符  | a?b   |
| []   | 匹配里面的任意字符 | [a-9] |

### 元字符(meta)

| 字符   | 说明                           |
| :--- | :--------------------------- |
| IFS  | 通常使用space                    |
| CR   | 由enter产生                     |
| =    | 设定变量                         |
| $    | 作变量或运算替换                     |
| >    | 重导向stout                     |
| <    | 重导向stdin                     |
| \|   | 命令管线                         |
| &    | 重导向file descriptor           |
| ()   | 将其内命令置于nested subshell中执行    |
| {}   | 将其内的命令置于non-named func中执行    |
| ;    | 在一个命令结束后，忽略返回值，继续执行下一个命令     |
| &&   | 在一个命令结束后，若结果为true，继续执行下一个命令  |
| \|\| | 在一个命令结束后，若结果为false，继续执行下一个命令 |
| !    | 执行history中命令                 |

## linux 软件管理工具

注意，centos使用yum工具

### 源代码编译使用

1. ./configure 检查环境
2. make 编译，生成可执行软件
3. make install 安装

### ubuntu dpkg 软件安装

- 软件安装位置whereis oracle,which mysql
- 环境变量设置：
    - 修改当前的环境变量 vim ~/.bashrc，如果需要系统变量 注意etc/profile
    - 这里的仿照bashrc文件进行修改
    - source ~/.bashrc 修改环境变量生效
    - echo $CHROME_HOME 和 直接键入chrome  检查

## 其他

- 获取当前的时间 `date +'%Y-%m-%d %H-%M-%S'`  注意一般而言英文后面都会有空格，这是应当注意的
- 定时任务  crontab -e 分时日月周 用vim进行编辑
- ! 返回一个系统命令，jupyter中也会用
- vim ~/.bashrc 和 source ~/.bashrc
- 查看环境变量`echo $ODBCINI`
- 如果是物理机是通过有线上网，那么需要使用NAT网络连接方式，如果是无线网络，那么需要使用桥接方式上网
- ldd 列出file运行所需的共享库
- ctrl+alt+T 快速调用命令窗口
- ubuntu分屏显示 ctrl + win + 上下左右
- [修改源文件为阿里云](http://blog.csdn.net/u011148119/article/details/50338355)
- [ubuntu扁平化](https://github.com/anmoljagetia/Flatabulous)

## 常见错误的解决

- sudo apt-get  install

## linux启动

- BIOS-> MBR-> GRUB-> 加载内核-> 执行init-> runlevel

# mongodb

[mongodb的安装使用](http://dblab.xmu.edu.cn/blog/mongodb/)

- mongo直接创建表
- 查询：db.集合名称.find({查询条件},[,{设置显示}]) 

常见的查询命令
- 查询总记录的条数:db.getCollection('nltk_collection').find().count()
- 查询type为C10的:db.getCollection('nltk_collection').find({type:'C10'})

mongo正则表达式查询

    db.getCollection('test_collection').find({jieba:{$regex:'食物'}})

mongo普通查询

    db.getCollection('nltk_collection').find({'type':'C10'})

# hive
## 数据的导入导出
### load 

    load data [local] inpath 'filepath' [overwrite] into table tablename

### sqoop

- oracle -> hive

       ./sqoop import  --hive-import --connect jdbc:oracle:thin:@host:端口 --username scoot --password tiger --hive-table emp1 [--columns '..']

- hive -> oracle
        ./sqoop export --conenct jdbc:oracle:thin:@..:端口 --username scoot --password tiger --table emp [--columns '..']



# git的使用

- git --help
- 自己使用：
  - git add . 
  - git  commit -m ''
  - git push origin master
- git log, git status



# chrome & google 搜索技巧

## vimium 使用

vimium应该是基于 vim的思想进行编写的，所以许多命令是通用的
- 获取帮助 shift+/ 其实就是?
- 添加例外网站，例如jupyter notebook，双方的命令模式下命令会有冲突
- 切换tab，在例外网站使用ctrl+tab，非例外网站使用大写的K，L
- [复制网页内容](https://www.douban.com/note/556628301/)
    - /搜索内容+enter, 使用右手小拇指进行按键
    - 切换到英文输入法
    - 使用v键进入视觉模式，使用shift+v 按行的视觉模式
    - 使用vim导航键选择文本:h,j,k,l (j 下翻，k上翻，h，左边，l右边)
    - 使用y复制文本 
    - ctrl+v 黏贴
- gs查看网页的源码
- x 关闭网页，左手无名指移动，直接关闭
- T 现有的标签切换。右手shift+左手t键，
- t 新建标签页
- o 键入网址，或者键入关键词使用google 搜索  右手无名指 
- gg 跳至网页的顶部
- d 向下翻半页和  u 向上翻半页
- H,L  前进 后退
- h，l向左向右，这个在分屏时有用
- /进行查找时，\I 可以按照大小写进行查找，\r  可以按照正则表达式进行查找
- 和vim类似 3K 向前切换3个tab 数字的用法,使用ctrl+F
- 使用o在当前页输入，O相当于 ctrl+T
- chrome F10 进入chrome 菜单

## google搜索技巧

- 使用搜索引擎时，一定要先分析是否有必要使用搜索引擎
- 使用关键字site，filetype，" "
- 页面进行查找ctrl+F

# 上网

- [ss搭建](https://www.rkdot.com/shadowsocks-server-setup/)，购买，服务器和本地配置
- hosts文件修改
- lantern，xx-net
- 镜像网站
