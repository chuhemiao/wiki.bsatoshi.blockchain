# Golang 基础之如何使用Go Module和Go proxy

### 最佳解决方案

+ 从 Go 1.11 版本开始已经开始支持Go Mod ，并且提供了包下载的解决方案，就是使用 国内大厂的第三方代理比如：`https://goproxy.cn/` 、`https://athens.azurefd.net` 直接代理下载，官方设置方法：

+ macos/linux

    - `export GO111MODULE=on `
    - `export GOPROXY=https://goproxy.io`

+ Wins 使用PowerShell 设置（这里输入是去当前设置的GOPATH）
    - `$env:GO111MODULE="on"`
    - `$env:GOPROXY="https://goproxy.cn"`


+ Go version 》=1.13 请使用
    - `go env -w GOPROXY=https://goproxy.io,direct`
    - `go env -w GOPRIVATE=*.corp.example.com`



### 推荐阅读

+ [Goproxy 中国](https://github.com/goproxy/goproxy.cn/blob/master/README.zh-CN.md)
+ [Go 语言解决不能Go get安装Gin问题解决方案](https://www.idiot6.com/2019/07/23/go-gin-golang-x/)