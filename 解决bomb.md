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

