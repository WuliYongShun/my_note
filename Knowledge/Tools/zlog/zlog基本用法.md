# zlog基本用法

## 下载
在http://hardysimpson.github.io/zlog/ 下载最新的zlog源码包。

## 解压
`tar -zxvf zlog-1.2.12.tar.gz`

## 编译
`make`

如果是交叉编译, 个人理解应该把src里面的makefile中, CC变量修改为交叉编译器的地址就行

编译完成后, 在src中会生成
`libzlog.a`和`libzlog.so`

## 使用demo
```
#include <stdio.h>
#include "zlog.h"

int main(int argc, char** argv)
{
    int rc;
    zlog_category_t *c;

    rc = dzlog_init("zlog.conf", "cxy_rules");
    if (rc)
    {
        printf("init failed\n");
        zlog_fini();
        return -1;
    }
    char test_str[32] = "this is a zlog test";
    dzlog_debug("hello, zlog: %s", test_str);
    dzlog_debug("hello, zlog debug");
    zlog_fini();

    return 0;
}
```

编译命令
```
gcc -o zlog_demo zlog_demo.cpp -L./ -Wl,-rpath,./ -lzlog
```

## 自己写的工具类
```
#include "zlog_utils.h"

int g_isLogOpen = 0;

#define dbout(arg...) do { if (g_isLogOpen) dzlog_debug(arg);} while(0)

int ZlogInit(const char* config_path, const char* rules)
{
    int ret = -1;
    if (rules == NULL || config_path == NULL)
    {
        printf("ZlogUtils: input param error");
        return -1;
    }
    int rc = dzlog_init("zlog.conf", rules);
    if (rc)
    {
        printf("ZlogUtils: init failed, rules = %s\n", rules);
        zlog_fini();
    }
    else
    {
        printf("ZlogUtils: init success\n");
        g_isLogOpen = 1;
        ret = 0;
    }
    return ret;
}

void ZlogDestroy(void)
{
    g_isLogOpen = 0;
    zlog_fini();
}
```

## 配置文件示例
```
[formats]
simple = "%m%n"
cxy_formats = "%d|%U|%L|%V --- %m%n"
[rules]
my_cat.DEBUG >stdout;simple

client_rules.DEBUG "/work/share/client_log_%d(%F).log";cxy_formats
server_rules.DEBUG "/work/share/server_log_%d(%F).log";cxy_formats
```

