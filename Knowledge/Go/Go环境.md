# Go
## 安装
在网站下载
`https://studygolang.com/`
直接安装即可, mac下默认安装在`/usr/local/go`

如果下载的是压缩包, 则解压后,bin目录下的go就是执行脚本的东西

## Hello World
``` go
package main //打一个包
import "fmt" //引入一个包

func main() {
	fmt.Println("hello, world")
}
```

## 编译
如果go文件为hello.go
则在命令行可以直接`go build hello.go`
windows下会出现exe, linux,mac下会出现可执行的hello文件.

也可以使用`go run hello.go`来执行, 使用类似脚本的形式.不推荐.

## GOPATH
GOPATH是一个需要手动配置的环境变量, 用于存放外接导入的包

## VScode 配置
在mac下, 先安装VSCode

