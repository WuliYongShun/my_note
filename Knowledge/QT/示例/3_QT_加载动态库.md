# 3_QT_加载动态库
## 项目中用到的方法

```
LIBS += -L../bin -lipps
LIBS += -L../bin -lippcore

DESTDIR = ../bin
```

## 基础
带加载的动态库为:
libtest.a
test.dll
头文件为: test.h
已经放到加载者的根目录
在.pro文件中加入一行
`LIBS += -L. -ltest`
(其中-L表示目录, -l表示库的名字, 会自动寻找lib + 库名 + .a的文件)

在需要用到的地方引用头文件`test.h`即可

注意:
如果项目的构建设置中勾选了`Shadow build`, 则.目录在后面指定的文件夹中, 如果去掉了此选项, .目录在工程目录下