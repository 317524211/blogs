
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
