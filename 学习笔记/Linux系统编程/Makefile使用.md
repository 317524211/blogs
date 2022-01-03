
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

1.命令执行前，检测规则中的依赖是否存在
如果不存在，向下检查其他规则，检查有没有一个规则是用来生成这个依赖的，如果找到了，则执行该规则中的命令
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

2.检查更新，执行规则中的命令时，会比较目标和依赖文件的时间
如果依赖的时间比目标的时间晚，需要重新生成目标

## 自定义变量和预定义变量的用法

```
#定义变量
src=sub.o add.o mult.o div.o main.o
target=app
$(target):$(src)
	$(CC) $(src) -o $(target)

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
 
## 模式匹配的用法
```
#定义变量
src=sub.o add.o mult.o div.o main.o
target=app
$(target):$(src)
	$(CC) $(src) -o $(target)

%.o:%.c
	$(CC) -c $< -o $@
```

## wilecard、patsubst两个函数的使用
$(wildcard PATTERN...)  获取指定目录下指定类型的文件列表，指定目录可以是多个，用空格间隔
$(patsubst ,,)  查询符合第二个“，”后模式的单词（以空格、“TAB”、“回车”、“换行”，分隔），符合就替换
```
#定义变量
src=$(wildcard ./*.c)
objs=$(patsubst %.c, %.o, $(src))
target=app
$(target):$(objs)
	$(CC) $(objs) -o $(target)

%.o:%.c
	$(CC) -c $< -o $@

.PHONY:clean
//该目标用于删除编译完成后的.o文件,不加“.PHONY:clean”不会执行
//原因：所有规则都是为第一条规则执行，只能在vim中make clean，单独执行指定目标
//但如果在目录的vim 执行 touch clean，clean也不会执行
//原因：执行clean时，做时间检查，检查依赖和目标新旧，
//但clean没有依赖，不用更新。
//加上上一行的.PHONY:clean，表示是一个伪目标，不会做时间检查
clean:
	rm $(objs) -f
//该目标用于
```

## 单独执行makefile 指定目标的规则
在vim输入
```
make 目标名称
```
