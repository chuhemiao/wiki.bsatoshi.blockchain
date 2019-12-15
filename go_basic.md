# Go语言基础入门课程--Go语言介绍

### Go语言背景

![Golang基础学习](https://cdn.bsatoshi.com/2019/12/15/15763897696325.jpg)

+ Go 语言是由谷歌公司在 2007 年开始开发的一门语言，目的是能在多核心时代高效编写网络应用程序。Go 语言的创始人 Robert Griesemer、Rob Pike 和 KenThompson都是在计算机发展过程中作出过重要贡献的人。自从 2009 年 11 月正式公开发布后，Go 语言迅速席卷了整个互联网后端开发领域，其社区里不断涌现出类似 vitess、Docker、etcd、Consul 、flannel、nsq、 Kubernetes、 Anthos 、Hugo等重量级的开源项目。

+ Go语言的出身可以说非常豪华，肯·汤普逊是c语言和unix的发明者，罗伯特·格瑞史莫参与设计了Java的HotSpot虚拟机和Chrome浏览器的JavaScript V8引擎，罗博·派克在大名鼎鼎的bell lab侵淫多年，参与了Plan9操作系统、C编译器以及多种语言编译器的设计和实现。Go语言从2009年开源到现在吸引了很多开发者的注意，分别获得了2009年和2016年的TIOBE之星。Jetbrains 发布 2019 开发者生态报告：Java 最主流，Go 最有前途，Go的使用份额已从 2017 年的 8% 大幅跃升到今年的 18%，多达 13% 的开发人员愿意采用或迁移到 Go 语言。


+ Go 是一门开源的编程语言，目的在于降低构建简单、可靠、高效软件的门槛。尽管这门语言借鉴了很多其他语言的思想，但是凭借自身统一和自然的表达，Go 程序在本质上完全不同于用其他语言编写的程序。Go 平衡了底层系统语言的能力，以及在现代语言中所见到的高级特性。你可以依靠 Go 语言来构建一个非常快捷、高性能且有足够控制力的编程环境。使用 Go 语言，可以写得更少，做得更多。Go是一个高效、静态类型， 但是又具有解释语言的动态类型特征的系统级语法。


### Go语言主要发展过程

+ 2007年9月，雏形设计 ，Rob Pike（罗伯.派克） 正式命名为Go；

+ 2008年5月，Google全力支持该项目；

+ 2009年11月10日，首次公开发布，Go将代码全部开源，它获得了当年的年度语言；

+ 2011年3月16日，Go语言的第一个稳定(stable)版本r56发布。

+ 2012年3月28日，Go语言的第一个正式版本Go1发布。

+ 2013年4月04日，Go语言的第一个Go 1.1beta1测试版发布。

+ 2013年4月08日，Go语言的第二个Go 1.1beta2测试版发布。

+ 2013年5月02日，Go语言Go 1.1RC1版发布。

+ 2013年5月07日，Go语言Go 1.1RC2版发布。

+ 2013年5月09日，Go语言Go 1.1RC3版发布。

+ 2013年5月13日，Go语言Go 1.1正式版发布。

+ 2013年9月20日，Go语言Go 1.2RC1版发布。

+ 2013年12月1日，Go语言Go 1.2正式版发布。

+ 2014年6月18日，Go语言Go 1.3版发布。

+ 2014年12月10日，Go语言Go 1.4版发布。

+ 2015年8月19日，Go语言Go 1.5版发布，本次更新中移除了”最后残余的C代码”。

+ 2016年2月17日，Go语言Go 1.6版发布。

+ 2016年8月15日，Go语言Go 1.7版发布。

+ 2017年2月17日，Go语言Go 1.8版发布。

+ 2017年8月24日，Go语言Go 1.9版发布。

+ 2018年2月16日，Go语言Go 1.10版发布。

+ 2018年8月24日，Go语言Go 1.11版发布。

+ 2019年2月25日，GO语言Go1.12版发布。

+ 2019年9月4日，GO语言Go1.13版发布。

### Go是一门以软件工程为目的的语言设计

+ 快速编译
+ 严格的依赖管理
+ 代码风格的强一致性
+ 偏向组合而不是继承


### Go有两大神器来支持并发

+ goroutine：轻量的"线程"
+ channel: 带类型的，协程安全的管道，类似unix里面的pipe.


### go语言特性

+ 静态编译
+ 垃圾回收
+ 简洁的符号和语法
+ 平坦的类型系统
+ 基于CSP的并发模型
+ 高效简单的工具链
+ 支持defer延迟调用
+ 丰富的标准库
+ 面向接口的oop，没有对象与继承，强调组合，以类似于duck-typing的方式编写面向对象；


### Golang应用领域

+ 微服务
+ DevOps,docker、kubernetes
+ 高性能中间件开发，比如数据库中间件、代理服务、消息服务
+ 区块链开发，比如go-ipfs、go-ethereum等

### Golang 网页框架 + 微服务框架

+ Echo
+ Beego
+ Gin
+ Iris
+ GoKit
+ Micro


### 哪些大公司在使用Go

+ Byte Dance
+ Twitter
+ Netflix
+ TARGET
+ UBER
+ Didi
+ Tencent
+ Google
+ American Express
+ Dropbox
+ Ny Times
+ Salesforce
+ Capital One
+ Monzo
+ Twitch
+ IBM
+ Mercado Libre 
+ BiliBili

### 国内Go布道者

+ 许世伟, 以 go 为基础的 七牛云存储, go语言在中国最早最值得尊重的早期布道者
+ 达达,  以 go 为基础的游戏后端,非科班出身的著名游戏公司CTO
+ smallnest,  go 的 rpcx 远程调用中间件
+ 谢大,  beego, 很棒很全的web框架,其文档是golang 入门学习到商用的实践经典
+ 毛剑, 以 go 重构后上市的 bilibili


### 推荐入门书籍、文档和网站

+ Golang优质中文技术博客
    - [官方快速入门Golang](https://learn.go.dev/)
    - [Go夜读](https://github.com/developer-learning/night-reading-go)
    - [峰云就她了](http://xiaorui.cc/)
    - [虞双齐的博客](https://yushuangqi.com/tags/golang.html)
    - [colobu鸟窝](https://colobu.com/categories/Go/)
    - [Golang 新手需要避免踩的 50 个坑（一）](http://blueskykong.com/2019/01/23/go-mistakes-1/)
    - [飞雪无情的博客](https://www.flysnow.org/categories/Golang/)
    - [StudyGolang](https://studygolang.com/)
    - [Tony Bai](https://tonybai.com/tag/golang/)

+ 小众博客推荐

    - [Boddy](http://gopherhub.org/tags/Go/)
    - [Konica的自留地](http://www.iikira.com/tags/Golang/)
    - [面向信仰编程](https://draveness.me/tag/Golang)
    - [TY.loafer](https://tyloafer.github.io/tags/Go/)

+ 入门书籍和进阶书籍

    - [新手入门书之-Go语言圣经](https://books.studygolang.com/gopl-zh/)
    - [Go 语言之旅](https://tour.go-zh.org/welcome/1)
    - [新手入门书之-Go语言标准库](https://docs.kilvn.com/The-Golang-Standard-Library-by-Example/)
    - [进阶文档之-深入解析Go](https://tiancaiamao.gitbooks.io/go-internals/content/zh/01.0.html)
    - [进阶大神之-Go专家编程](https://rainbowmango.gitbook.io/go/chapter01/1.1-chan)

+ 源码阅读相关

    - [欧长昆：go-under-the-hood](https://github.com/changkun/go-under-the-hood/blob/master/book/zh-cn/TOC.md)

+ 英文文档和博客推荐
    - [ardanlabs](https://www.ardanlabs.com/blog/)
    - [effective go](https://golang.org/doc/effective_go.html)
    - [Go Programming Language Resources](http://go-lang.cat-v.org/)
    - [Go In Action](http://sufuq.com/books/golang/Go%20in%20Action.pdf)
    - [邮件列表](https://groups.google.com/forum/#!forum/golang-nuts)

### 推荐Golang工具

+ [检索Go 语言项目](https://gowalker.org/)
+ [Go基础代码示例](https://gobyexample.com/)
+ [最佳IDE，GoLand](https://www.jetbrains.com/go/)
+ [备用IDE，VS Code](https://code.visualstudio.com/)
+ [包管理工具](https://github.com/goproxy/goproxy.cn/blob/master/README.zh-CN.md)

### Golang脚手架

+ [go-admin](https://github.com/GoAdminGroup/go-admin) 