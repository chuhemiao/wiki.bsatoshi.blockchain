# Go语言基础入门课程--Go语言介绍

### Go语言背景

![Golang基础学习](https://cdn.bsatoshi.com/2019/12/15/15763897696325.jpg)

+ Go 语言是由谷歌公司在 2007 年开始开发的一门语言，目的是能在多核心时代高效编写网络应用程序。Go 语言的创始人 Robert Griesemer、Rob Pike 和 KenThompson都是在计算机发展过程中作出过重要贡献的人。自从 2009 年 11 月正式公开发布后，Go 语言迅速席卷了整个互联网后端开发领域，其社区里不断涌现出类似 vitess、Docker、etcd、Consul 、flannel、nsq、 Kubernetes、 Anthos 、Hugo等重量级的开源项目。

+ Go语言的出身可以说非常豪华，肯·汤普逊是c语言和unix的发明者，罗伯特·格瑞史莫参与设计了Java的HotSpot虚拟机和Chrome浏览器的JavaScript V8引擎，罗博·派克在大名鼎鼎的bell lab侵淫多年，参与了Plan9操作系统、C编译器以及多种语言编译器的设计和实现。Go语言从2009年开源到现在吸引了很多开发者的注意，分别获得了2009年和2016年的TIOBE之星。Jetbrains 发布 2019 开发者生态报告：Java 最主流，Go 最有前途，Go的使用份额已从 2017 年的 8% 大幅跃升到今年的 18%，多达 13% 的开发人员愿意采用或迁移到 Go 语言。


+ Go 是一门开源的编程语言，目的在于降低构建简单、可靠、高效软件的门槛。尽管这门语言借鉴了很多其他语言的思想，但是凭借自身统一和自然的表达，Go 程序在本质上完全不同于用其他语言编写的程序。Go 平衡了底层系统语言的能力，以及在现代语言中所见到的高级特性。你可以依靠 Go 语言来构建一个非常快捷、高性能且有足够控制力的编程环境。使用 Go 语言，可以写得更少，做得更多。Go是一个高效、静态类型， 但是又具有解释语言的动态类型特征的系统级语法。


### Go语言主要发展过程



+ 2019 年 9 月，Go1.13 发布。增强了modules，新增了环境变量 GOPRIVATE 和 GOSUMDB, GOPROXY 支持多个，支持了 ErrorWraping；



+ 2019 年 2 月，Go1.12 发布，支持了 TLS1.3，改进了 modules，优化运行时和标准库；



+ 2018 年 8 月，Go1.11 发布，实验性支持 modules，实验性支持 WebAssembly；



+ 2018 年 2 月，Go1.10 发布，go tool 缓存编译，编译加速，很多细微的改进；



+ 2018 年 1 月，Hello, 中国! 及中国站镜像上线，大陆可以访问官网资源；



+ 2017 年 8 月，Go1.9 发布，支持 Type Alias、sync.Map，使用场景参考 slides，time 保持单增避免时间测量问题；



+ 2017 年 2 月，Go1.8 发布，显著的性能提升，GC 延迟降低到了 10us 到 100us，支持 HTTP/2 Push，HTTP Server 支持 Shutdow, sort.Slice 使排序使用更简单；



+ 2016 年 8 月，Go1.7 发布，支持了 Context，Context 在 K8s 和 Docker 中都有应用，新的编译算法减少 20%-30% 的二进制尺寸；



+ 2016 年 2 月，Go1.6发布，支持 HTTP/2，HTTPS 时会默认开启 HTTP/2，正式支持vendor；



+ 2015 年 8 月，Go1.5 发布，完全用 Go 代替了 C 代码，完全重新设计和重新实现 GC，支持 internal 的 package，实验性支持 vendor，GOMAXPROCS 默认为 CPU 个数；



+ 2014 年 12 月，Go1.4 发布，支持 Android，从 Mecurial 迁移到了 Git，从 GoogleCode 迁移到了 Github:golang/go，大部分 runtime 的代码从 C 改成了 Go，for 支持三种迭代写法；



+ 2014 年 6 月，Go1.3 发布，支持了 FreeBSD、Plan9、Solaris 等系统；



+ 2013 年 12 月，Go1.2 发布，新增收集覆盖率工具 coverage，限制了最高线程数 ThreadLimit；



+ 2013 年 5 月，Go1.1 发布，主要是包含性能优化，新增 Data Race Detector 等；



+ 2012 年 3 月，Go1.0 发布，包含了基本的语言元素比如 rune、error、map，标准库包括 bufio、crypto、flag、http、net、os、regexp、runtime、unsafe、url、encoding 等；



+ 2009 年 11 月, Google 宣布要开发一门新语言，既要开源，又有 Python 的好处，还要有 C/C++ 的性能。Go 是 BSD 的 License，大部分 Go 的项目都是 BSD 或 MIT 或 Apache 等商业友好的协议。

+ 2008年5月，Google全力支持该项目；


+ 2007年9月，雏形设计 ，Rob Pike（罗伯.派克） 正式命名为Go；



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

### 推荐阅读

+ [Go 开发关键技术指南 | 为什么你要选择 Go？](https://mp.weixin.qq.com/s/tXL_vXqIvHqafuwyGMofVw)