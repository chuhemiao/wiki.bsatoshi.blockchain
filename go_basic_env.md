# macos 下快速搭建 Golang 开发环境


### 首先选择适合自己系统的安装包

+ 打开Golang下载地址，[download](https://golang.org/dl/)，然后选择下载稳定版本。

+ 此处以macos为例，选择下图红框内的pkg地址下载

![Golang 1.13.5](https://cdn.bsatoshi.com/2019/12/15/15763927564453.jpg)


+ 安装完之后，打开终端，输入go version，会显示当前已经安装的版本

![go version](https://cdn.bsatoshi.com/2019/12/15/15763950799140.jpg)

+ Notice：如果已经安装了旧版本，可以删除：/usr/local/go 和/etc/paths.d/go ，然后在下载新版本安装即可

### 直接使用Vim运行第一个Go程序

+ 使用Vim编写第一个程序，首先创建一个目录 sudo mkdir go-basic-example

+ cd  go-basic-example

+ 创建第一个go程序：sudo touch main.go

+ 使用vim 编辑并输出hello world  ，sudo vim main.go

+ 在文件内写入：

```
package main

import "fmt"

func main() {
	fmt.Printf("hello, world\n")
}
```

+ 然后保存，并修改文件权限为644，sudo chmod -R 644 main.go

+ 最后运行 go run main.go 结果输出如下图所示

![显示效果](https://cdn.bsatoshi.com/2019/12/15/15763955569723.jpg)

### 下载Goland，并运行第一个Go程序

+ 打开连接，[最佳IDE，GoLand](https://www.jetbrains.com/go/)，并下载Goland，下载后依次执行安装即可。

+ 作者使用的是教育版，当然更支持使用正版，如果你囊中羞涩，可以使用下面的方式使用破解版本。

+ Goland 破解方式：[GoLand的永久破解和配置](https://juejin.im/post/5d25e6cef265da1b71531dba)

+ 打开已经安装好的Goland，如下图：

![goland](https://cdn.bsatoshi.com/2019/12/15/15763959754403.jpg)

+ 点击New Project

![新建go项目](https://cdn.bsatoshi.com/2019/12/15/15763961081931.jpg)

+ 第一步选择Go Modules模式，然后修改项目名称，最后点击create，即可创建一个项目为go-basic-example的新项目，提示：由于1.13之后版本默认proxy开启，所以GOROOT已经帮我们自动选择了当前的SDK，也就是上述步骤安装的Golang包。

+ 新建项目之后go-basic-example目录下只有一个go.mod文件，这个是用来后期安装go语言的包所使用，也就是包管理工具，很简单粗暴，所有包都使用语义化版本模式。

+ 然后在go-basic-example下建一个main.go文件，新建完之后修改package 上的包名为main，然后写入：

![go-basic-example](https://cdn.bsatoshi.com/2019/12/15/15763965195989.jpg)

```
func main(){
    fmt.Println("Hello World\n")
}
```

+ Goland Ide 会自动提示和引入已经使用的包，因此在截图中输入fmt.pln，然后直接回车会把当前fmt这个包引入。

+ 输入代码后，点击左侧的小绿三角（也可以使用go run main.go运行），即可运行当前的Hello World 程序，如下图所示

![go hello world](https://cdn.bsatoshi.com/2019/12/15/15763967682338.jpg)