**cd —换个目录（change directory）**

```bash
cd / #切换到根目录
cd ~ #切换到家目录 默认路径
cd #等效上面
cd home/creep#也等效上面
cd .. #回到上一级目录

```



**ls —— 这里有什么？**

**作用：** 列出当前目录下的文件和文件夹（list）

```bash
ls
ls -l       # 详细信息（权限、大小、时间）
ls -a       # 显示隐藏文件（以 . 开头的）
ls -la      # 详细 + 隐藏，都显示
```



**pwd—— 我在哪？**

**作用：** 显示你当前所在目录（print working directory）

```
pwd
```

可能输出：

```
/home/creep/csapp/bomb
```

这就是你现在的位置。



**mkdir 新建文件夹**

```bash
mkdir 1#在此时的路径下建一个文件夹
cd 1
```



**rm 删除文件**（此时rm'删除的文件不会到回收站会直接删掉）

```bash
rm a.txt #删除当前路径的a.txt文件
rm -r 1 #删除当前路径的1文件夹

```



**cp 复制文件**

```bash
cp 1.cpp 2.cpp #将1.cpp的文本复制到2.cpp 如果2.cpp没有就会新建一个2.cpp
cp -r 1 2#将1目录复制到2目录
#在2前也可以加路径
```



**mv移动和重命名**

```bash
mv 1.cpp 2.cpp#重命名
mv 1.cpp 1/1.cpp #移动
mv 1.cpp 1/2.cpp #移动加重命名
```



**cat 看文件里的所有内容**

```bash
cat 1.cpp 
```



**less 分页看文件内容**

**作用：** 一页一页看，大文件很方便。

```bash
less bomb.c
```

在 `less` 里面常用操作：

空格：下一页

`b`：上一页

上下方向键：一行一行移动

`/字符串`：向下搜索

`q`：退出



**`head` / `tail` —— 看前几行 / 后几行**

```bash
head bomb.c       # 默认前 10 行
head -20 bomb.c   # 前 20 行

tail bomb.c       # 后 10 行
tail -20 bomb.c   # 后 20 行
```







**./bomb **

在当前目录运行一个叫 `bomb` 的可执行文件：

```
./bomb
```

- `.` 表示当前目录
- `./bomb` 就是「当前目录下的 bomb 这个文件」

**5.2 如果提示「Permission denied」**

说明文件没有执行权限。加权限：

```
chmod +x bomb
./bomb
```

`chmod`：change mode，修改文件权限。
 `+x`：给文件添加可执行权限。





**重定向，管道**

**输出重定向 `>`,`>>`**

```c++
./1 > out.txt #将输出内容输出到out.txt覆盖之前的内容
./1 >>out.txt #追加到之前的内容后面
```



**输入重定向 `<`**

```c++
./1 < in.txt #将in作为输入
```



**管道`|`**

把前一个的命令的输入作为后一个命令的输入

```c++
objdump -d bomb | less
```



**`objdump`-将二进制文件反汇编为汇编代码**

```c++
objdump -d bomb | less #将整个bomb的内容反汇编出来
objdump grep phase #搜索出只包含关键字的行
```



