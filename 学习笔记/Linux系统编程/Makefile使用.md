
## Linux目录的操作

```
mkdir 01_gcc //创建01_gcc文件夹
mv test* 01_gcc //将当前所有test放入01_gcc
mv MakeFile1 MakeFile
```

## makefile编译多个文件
```
//MakeFile文件夹输入
app:sub.c add.c mult.c div.c main.c
	gcc sub.c add.c mult.c div.c main.c -o app
```

```
//VIM执行
make
```

## makefile基本原理
```
//1.命令执行前，检测规则中的依赖是否存在
//如果不存在，向下检查其他规则，检查有没有一个规则是用来生成这个依赖的，如果找到了，则执行该规则中的命令
app:sub.o add.o mult.o div.o main.o
	gcc sub.o add.o mult.o div.o main.o -o app

sub.o:sub.c
	gcc -c sub.c -o sub.o

add.o:add.c
	gcc -c add.c -o add.o

mult.o:mult.c
	gcc -c mult.c -o mult.o

div.o:div.c
	gcc -c div.c -o div.o

main.o:main.c
	gcc -c main.c -o main.o
```
