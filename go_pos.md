# Go语言实现pos协议

### Proof of Stake

+ 权益证明（PoS）是一类应用于公共区块链的共识算法，取决于验证者在网络中的经济权益

+ 在基于公共区块链的工作量证明（PoW）（如比特币和当前的以太坊用例）中，算法会奖励那些为了验证交易并创建新区块（即挖矿）解决密码难题的参与者。在基于权益证明的公共区块链（如以太坊即将实现的Casper协议）中，一组验证者轮流提议并票决下一个区块，而每位验证者的投票权重取决于其保证金额的大小（即权益）。权益证明的重要优势包括保障安全性、降低中心化危险以及提升能源效率。

+ 通常来说，权益证明算法如下所示。区块链会追踪一个验证者集，而任何持有该区块链的基础加密货币（对以太坊来说就是以太币）的人都可以通过发送一种将以太币锁定为保证金的特殊交易成为验证者。随后，创造并认可新区块的过程可通过当前所有验证者均可参与的共识算法来完成。通俗讲PoS核心概念为币龄，即持有Token的时间，持币越多并且时间越久，可能你的收益相对就会越高。


### Golang 实现 Pos demo

* 安装 go get github.com/davecgh/go-spew/spew
* 安装 go get github.com/joho/godotenv
* 如果出现 dial tcp 216.58.200.49:443: i/o timeout
* 请访问https://www.idiot6.com/2019/07/23/go-gin-golang-x/ 设置GO MODULE
* macos运行 go run main.go 然后打开新窗口输入sudo nc localhost 9000 输入token数量和BPM数量，即可等待验证Pos(不加sudo看不到输入框效果，如果是win，请安装nc客户端，并使用管理员权限打开窗口)

+ [完整源码请查看，源码下pos.go](https://github.com/chuhemiao/go-basic-example)

### 运行效果


![pos golang](https://cdn.bsatoshi.com/2020/01/01/15778570421506.jpg)


[原文作者](http://www.wuecho.com/2018/05/22/Go%E8%AF%AD%E8%A8%80%E5%AE%9E%E7%8E%B0PoS%E5%85%B1%E8%AF%86%E7%AE%97%E6%B3%95/)

[推荐阅读：权益证明 (PoS) 到底是如何运作的？](https://www.chainnews.com/articles/857317204261.htm)