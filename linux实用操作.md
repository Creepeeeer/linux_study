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

