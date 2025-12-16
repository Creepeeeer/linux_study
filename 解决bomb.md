反汇编bomb成bomb.s

```c++
objdump -d bomb >bomb.s
```



第0关

在bomb.s里找到phase_0

<img src="C:\Users\LENOVO\AppData\Roaming\Typora\typora-user-images\image-20251203111453458.png" alt="image-20251203111453458" style="zoom: 50%;" />

把第五行push的地址粘下来

0x8049764

```c++
gdb ./bomb
break phase_0
run
随便输
x/s 刚才复制的
输出的就是第一题答案
```



第1关

```c++
creep@creep-virtual-machine:~/Desktop/task1$ gdb bomb
(gdb) break phase_1
Breakpoint 1 at 0x8048a09
(gdb) run 
Starting program: /home/creep/Desktop/task1/bomb 
[Thread debugging using libthread_db enabled]
Using host libthread_db library "/lib/x86_64-linux-gnu/libthread_db.so.1".
Welcome to my fiendish little bomb. You have 7 phases with
which to blow yourself up. Have a nice day!
1

BOOM!!!
The bomb has blown up.
1

Breakpoint 1, 0x08048a09 in phase_1 ()
(gdb) ni 10
0x08048a2b in phase_1 ()
(gdb) x/dw $ebp-0x18+4
0xffffcf74:     1101933764 #第一个答案
(gdb) x/dw $ebp-0x18
0xffffcf70:     -2046820352 #第二个答案
```

