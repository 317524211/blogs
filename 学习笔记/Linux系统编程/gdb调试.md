## gdb调试的基本命令
```
gcc 源文件名.c -o 源文件名 -g //-o，关闭优化选项，-g，打开调试选项，-wall打开所有的warining
gdb 源文件名 //进入调试

set args 10 20 //给程序设置参数
show args //获取设置参数

l //查看当前文件代码（默认显示10行），可在后面加上行号/函数名。
set list 行数 //设置行数

l 文件名:行号 //查看非当前文件代码
l 文件名:函数名 //查看非当前文件代码
```

## 对于.cpp文件，尽量用g++编译
```
g++ bubble.cpp seletc.cpp main.cpp -o app -g
```

## gdb调试打断点
```
b 8 //当前文件第8行
i break //断点信息
b select.cpp:8 //在其他文件第8行打断点
```

## gdb运行
```
start //程序在第一行运行
run //遇到断点停

c //继续运行，到下一个断点停
n //执行下一行代码，不进入函数体

p 变量名 //打印变量值
ptype //变量名 （打印变量类型）

```
