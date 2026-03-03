### 快捷键

- ctrl+c 强制停止，如某些程序的运行要强制停止，或者命令输入错误

- ctrl+d 退出账户的登录，或者退出某些程序的界面（比如python退出要按ctrl+d）

  #### 历史命令搜索

- history 会输入所有输入过的命令，序号越大越近
- !命令前缀，自动执行上一次匹配前缀的命令
- ctrl+r 输入内容去匹配历史命令

​       如果搜索到的内容是你需要的，那么回车键直接执行，键盘左右键得到此命令（不执行）

####       光标移动快捷键

- ctrl+a 跳到命令开头
- ctrl+e 跳到命令结尾
- ctrl+键盘左键 向左跳一个单词
- ctrl+键盘右键 向右跳一个单词

​	

- ctrl +l /clear 清屏





### 软件安装

linux命令行的应用商店  软件安装需要root权限

centos yum，ubuntu apt

```c++
apt [-y] [install| remove | search] 软件名称
```

- -y 自动确认 无需手动确认安装或卸载
- install 安装
- remove 卸载
- search 搜索



### systemctl

**控制软件的启动停止开机自启**

能被systemctl管理的软件被称之为服务

```c++
systemctl start |stop |status |enable |disable 服务名
```

- start启动
- stop停止
- status查看状态
- enable开启开机自启
- disable 关闭开机自启

系统内置的服务常见的有：

- NetworkManager 主网络服务
- network 副网络服务
- firewalld 防火墙服务
- sshd ssh服务



除了内置的服务以外 部分第三方软件安装以后也可以用systemctl来控制





### 软链接

类似于windows里的快捷方式

```c++
ls -s 参数1 参数2
```

- -s选项，创建软链接
- 参数1：被链接的文件或文件夹
- 参数2：要链接去的目的地

```c++
lrwxrwxrwx 1 creep creep    5 Jan 27 20:12 11.txt -> 1.txt
```

这里的l指明了是软链接



### date

在命令行中查看系统的时间

```c++
date [-d] [+格式化字符串]
```

- 格式化字符串：通过特定的字符串来标记，控制显示的日期格式

- %Y 年

- %y 年份后两位

- %m 月份

- %d 日

- %H 小时

- %M 分钟

- %S 秒

- %s 自1970-01-01 00:00:00到现在的秒数

- ```c++
  creep@LAPTOP-395G2AEK:~/2$ date +%Y-%m-%d
  2026-01-27
  creep@LAPTOP-395G2AEK:~/2$ date "+%Y-%m-%d %H:%M:%S"
  2026-01-27 20:37:47
  ```

- -d 用于日期的计算

- ```c++
  date -d "+1 day" +%Y%m%d #显示后一天的日期
  date -d "-1 day" +%Y%m%d #显示前一天的日期
  ```

  支持的时间标记

  ```c++
  year 年
  month 月
  day 天
  hour 小时
  minute 分钟
  second 秒
  ```





### 修改时区

**root权限**

```c++
rm -f /etc/localtime
ln -s /usr/share/zoneinfo/Asia/Shanghai /etc/localtime
```





### ip地址

每一台联网的电脑都有一个地址，用于和其他计算机通讯，ip地址主要有两个版本V4和V6(V6很少用)

**Ipv4地址格式为：a.b.c.d,其中abcd表示0~255的数字** e.g 192.168.88.101

```c++
ifconfig 查看本机的ip地址
```

#### 特殊的ip地址

- 127.0.0.1 ip指代本机
- 0.0.0.0 特殊的ip 可以指代本机，可以在端口绑定中用来确定绑定关系



### 主机名

每一台电脑除了对外联络地址（ip地址）以外，也可以有个名字称为主机名

```c++
hostname #查看主机名
hostnamectl set-hostname 主机名 #修改主机名
```





### 域名解析

通过主机名和字符地址去代替数字化的ip地址，**这称之为域名**

访问一个网站的流程：

- 先看本机的记录(私人地址本)
- linux：   /etc/hosts
- windows C:\windows\system32\drivers\etc\hosts





### 固定ip

虚拟机的ip地址是通过dhcp服务获取的

dhcp：动态获取ip地址，每次重启都会重新获得ip地址



### ping

**检查指定网络服务器是否是可联通状态**

```c++
ping [-c num] ip/主机名
```

- -c 检查的次数 num 如果不使用-c 将无数次持续检查
- 参数 被检查的ip或主机名地址



### wget

非交互式的文件下载器，在命令行中下载网络文件

```c++
wget [-b] url
```

- -b  可选，后台下载，会将日志写入当前工作目录的wget-log文件
- url 下载链接



### curl

发送http网络请求，可用于下载文件，获取信息

```c++
curl [-O] url
```

- -O 用于下载文件，当url是下载链接时，可以使用此选项保存文件





### 端口

是设备与外界通讯交流的出入口，可分为物理端口和虚拟端口

- 物理端口，usb接口，rj45接口等
- 虚拟端口，计算机内部的端口，不可见的，用来操作系统与外部进行交互使用的

计算机程序之间的通讯，通过ip只能锁定计算机，无法锁定具体的程序，通过端口可以锁定计算机上具体的程序，确保程序之间的沟通

linux系统支持65535个端口

- 公认端口：1-1023 通常用于一些系统内置或知名程序的预留使用，如ssh的22端口，https服务的443端口，非特殊处理，不占用这个范围的端口
- 注册端口：1024-49151，通常可以随意使用，用于松散的绑定一些程序、服务
- 动态端口：49152-65535，通常不会固定绑定程序，用于临时使用



#### nmap

**查看端口的占用情况**

如果没有使用apt安装

```c++
nmap +被查看的ip地址（本机127.0.0.1)
```



#### netstat

**查看指定端口的占用情况**

```c++
netstat - anp |grep 端口号
```





### 进程

每一个程序运行的时候，都被操作系统注册为系统中的一个：进程

并会为每一个进程分配一个：**进程号**



#### ps 

**查看linux系统的进程信息**

```c++
ps [-e -f]
```

- -e,显示出全部的进程
- -f ，以完全格式化的形式展示信息

```c++
UID          PID    PPID  C STIME TTY          TIME CMD
UID：进程所属用户ID
PID：进程的进程号ID
PPID:进程的父亲ID
C：cpu占用率
STIME：进程的启动时间
TTY：启动此进程的终端序号 ？表示非终端启动
TIME：进程占用cpu的时间
CMD：进程对应的启动路径
```



#### kill

**结束进程**

```c++
kill [-9] 进程ID
```

- -9 表示强制关闭进程，不使用此选项会向进程发送信号要求其关闭，但是否关闭看进程自身的处理机制





### 环境变量

**操作系统在运行的时候记录的一些关键信息，用以辅助系统运行**



```c++
env #查看当前系统中记录的环境变量
```



**环境变量是一种key value型结构，并且可以有多个Value**

无论当前目录是什么都能执行/usr/bin/cd 这个程序，就是借助环境变量PATH这个值做到的

```c++
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/usr/games:/usr/local/games:/snap/bin
```

当执行任何命令，都会按照顺序，从PATH路径中搜索要执行的程序的本体 

比如执行cd命令，就从/usr/bin中搜索到了cd命令并执行



#### $ 

**取变量的值**，取得环境变量的值就可以通过语法$环境变量名来取得

e.g 

```c++
echo $PATH 取得PATH这个环境变量的值并且输出
```

如果和其他内容混在一起可以通过{}来标注取的变量是谁

```c++
echo${PATH}ABC
```

#### 自行设计环境变量

- 临时设置

  ```c++
  export 变量名=变量值
  ```

- 永久生效

针对当前用户生效，配置在当前用户的 ~/.bashrc文件中

针对所有用户生效，配置在系统的 /etc/profile文件中

source 配置文件 进行立刻生效



### 压缩

linux常用压缩格式：tar和gzip，zip

linux常用压缩格式：.tar .gz

- tar：简单的将文件组装到一个.tar的文件内，并没有太多的文件体积的减少
- gzip：使用gzip压缩算法将文件压缩到一个文件内，可以极大的减少压缩后的体积



#### tar

```c++
tar [-c -v -x -f -z -C] 参数1 餐数2 ......参数n
```

- -c 创建压缩文件，用于压缩模式
- -v 显示压缩进度
- -x解压模式
- -f要创建的文件，或要解压的文件，-f选项必须位于所有选项的最后一个
- -z gzip模式，不使用-z就是普通的tarball模式（无论是解压还是压缩）,-z选项如果使用的话，一般处于选项的第一个
- -C，选择解压的目的地，用于解压模式(需要单独使用，和解压所需其他参数分开)

**常用压缩组合**

```c++
tar -cvf test.tar 1.txt 2.txt #将1.txt 2.txt 压缩到test.tar文件内
tar -zcvf test.gz 1.txt 2.txt #将1.txt 2.txt 压缩到test.gz文件内，使用gzip模式
```

**常见解压组合**

```c++
tar -xvf test.tar 解压test.tar至当前目录
tar -xvf test.tar -C /home/creep 解压test.tar 将文件解压至指定目录
tar -zxvf test.gz -C /home/creep 解压test.gz 将文件解压至指定目录
```



#### zip

**压缩文件为zip压缩包**

```c++
zip [-r] 参数1 参数2 ....参数N
```

-r 被压缩的包含文件夹的时候，需要使用

```c++
e.g zip test.zip a.txt b.txt c.txt
    zip -r test.zip test creep a.txt
```



#### unzip

**解压zip压缩包**

```c++
unzip [-d] zip压缩包文件
```

- -d 指定要解压去的地方 同tar的-C

```c++
e.g unzip test.zip 
    unzip test.zip -d /home/creep
```

