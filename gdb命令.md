[(16 封私信) gdb/cgdb常见调试命令详细总结 - 知乎](https://zhuanlan.zhihu.com/p/655719314)

### 启动与执行程序

```bash
gdb ./1
```

进入调试环境后会看到 `(gdb)` 提示符。

**已经在gdb里想打开另外一个文件**

```c++
kill #先杀死现在进程
file ./bomb #再进入另外一个文件
```

**终止输入**

```c++
ctrl +C
```



### **运行gdb**

```c++
run
run in.txt #读入in.txt作为输入
#如果上次用了 in.txt下次输入还是in.txt
#下次使用前如果要清空输入
set args
run in.txt 是读取in.txt有的作为输入 剩下的在键盘输入
run <in.txt 是直接重定向到in.txt 所有读入都在in.txt
```



### **list a,b**

查看第a行到第b行的代码

如果想看全部可以 

```c++
list 1,500#右边可以设置成一个比较大的值
```

### 单步调试

#### **break 打断点**

**在某个位置设“停下来”的点**

位置可以是：

- 函数名：`break phase_1`
- 行号：`break 42`
- 源文件+行号：`break bomb.c:100`
- 地址：`break *0x401234`

**查看所有端点信息**

```c++
info breakpoints
```

**delete**

```c++
delete#删除所有断点
delete 1 #删除在info break 里符号为1的断点
```



#### next / step：源码级单步（写 C++ 时用得多）

你现在调 C++（`cin >> n;` 那些）会用到：

```
(gdb) next      # 执行下一行源码，不会进入函数内部
(gdb) n

(gdb) step      # 执行下一行源码，如果是函数调用就进入函数体
(gdb) s
```

bomb lab 更多是看汇编，用 `si/ni`，但你以后写 C++ 调 bug 就会用 `n/s`。

------

####  si / ni：指令级单步（bomb lab 主力）

```
(gdb) stepi     # 单步执行一条机器指令，会进入 call
(gdb) si

(gdb) nexti     # 单步执行一条机器指令，不进入 call 里
(gdb) ni
```

配合 `layout asm`，你可以一条条往下走，看寄存器变化。

------

#### finish：跑到当前函数返回

```
(gdb) finish
```

当前在函数里面，`finish` 会跑到这个函数 return 的那一行并停下。

在你不想在某个小函数里面一步步时很好用。



### 寄存器

**查看寄存器内容**

```c++
info registers
```

**查看单个寄存器**

```c++
(gdb) print/x $rax      # 16 进制
(gdb) p/x $rax

(gdb) print/d $rax      # 10 进制
(gdb) p/d $rax

(gdb) p/t $rax          # 二进制
```

 **修改寄存器**（不一定在作业里用，但很有用）

```
(gdb) set $rax = 0
(gdb) set $rdi = 0x401500
```

可以手动改寄存器，模拟不同情况。



### 查看内存

```c++
x/<数量><格式><单位> 地址
```

常用格式：

- `x`：十六进制
- `d`：十进制
- `s`：字符串
- `i`：指令（反汇编）
- `c`：字符

单位：

- `b`：1 字节（byte）
- `h`：2 字节（halfword）
- `w`：4 字节（word）
- `g`：8 字节（giant word，64-bit）

```
(gdb) x/s 0x8049764
# = 查看从 0x8049764 开始的字符串
```



### 查看栈帧

**backtrace / frame**

**backtrace：查看调用栈**

```
(gdb) backtrace
(gdb) bt
```

例子：

```
#0  phase_3 () at bomb.c:120
#1  phase_defused () at bomb.c:250
#2  main () at bomb.c:50
```

你就知道当前是在 `phase_3` 里面，是 `main` 调它的。

------

**切换到某一层函数栈帧**

```
(gdb) frame 0
(gdb) frame 1
(gdb) f 2
```

`frame 0` 是当前函数，`frame 1` 是调用者。

------





### **查看符号 / 函数列表**

### **列出所有函数名**

```
(gdb) info functions
(gdb) i func
```

太长可以加过滤：

```
(gdb) info functions phase
# 只列出和 phase 有关的函数
```





### display：每步都自动显示某个值

例如你每条指令之后都想看 `$rax`：

```
(gdb) display/x $rax
(gdb) display/x $rdi
```

之后每次 `si`，gdb 会自动打印这些值。

取消：

```
(gdb) undisplay 1      # 删除编号 1 的自动显示
(gdb) info display     # 查看当前自动显示的列表
```
