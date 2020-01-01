# Go语言实现Dpos协议

### Dpos概念

+ DPOS全称Delegated proof of Stake，中文是委托权益证明，DPOS共识机制是基于POW及POS的基础上，出现的一种基于投票选举的共识算法。

### Dpos规则

+ 可以生产区块，如果不称职就会被踢出代表列表重新选举。这里的选举最少需要整个网络一半的节点通过则证明去中心化的有效投票。

+ DPOS算法要求随机指定代表列表的顺序，不按照顺序生成区块的是无效的，每个周期会重新洗牌一次，打乱原有顺序。代表之间不存在争夺情况，不会遗漏区块，定时会出现一个区块，这就使共识达成的时间周期大大缩短，这也是相对于POS,POW的优点所在。

### Dpos奖励机制

+ DPOS因为每秒可以处理确认比POW和POS大上几个数量级的交易量，会将一部分交易作为奖励给网络维护节点和投票者，作为代表选举维护的奖励，让更多的节点参与进来。

### Dpos优势

+ DPOS的优势就在于能将维系网络运行的能源消耗降到最低，以一种低成本的方式来管理整个链上的运行，这就很大程度上解决了POW的能源耗损问题。同时，更加“去中心化”的管理方式，将区块链网络运行的决定权分散到全网的各个节点手中，这就很大程度上避免了POS容易出现的被庄家操纵的“控股”现象。DPOS共识机制的出现，将通过实施区块链上的“民主”来对抗“中心化”所产生的负面效应，用被公选的“弱中心化”的方式来提高全网运维的效率。


### Pow Pos Dpos 三种共识机制具备以下特点：

+ POW（工作量证明）：安全、去中心化，去信任化；但速度低，共识时间长，耗能大；

+ POS（权益证明）：共识时间短，耗能小；但效率低下，易产生马太效应，带来中心化；

+ DPOS（委托权益证明）：出块时间很短，效率相对更高。

### Golang实现Dpos算法

```

package main

import (
	"crypto/sha256"
	"encoding/hex"
	"fmt"
	"math/rand"
	"strconv"
	"time"
)

var blockChain []Block

//存放代理人的地址
var delegate = [] string{"aaa","bbb","ccc","ddd"}

// 声明区块的结构体

type Block struct {
	BMP int

	PrefHash string

	HashCode string

	TimeStamp string

	Index int

	//区块验证者
	Validator string
}


func main(){
	var firstBlock Block

	blockChain = append(blockChain,firstBlock)

	//通过变量n按顺序让代理人作为矿工
	var n  = 0

	var temp = 0

	for {

		randeDelegate()
		//每隔5秒产生一个新区快
		time.Sleep(5 * time.Second)

		var nextBlock = GenerateNextBlock(temp,blockChain[temp],delegate[n])

		blockChain = append(blockChain,nextBlock)

		n ++

		temp ++

		n = n %len(delegate)

		fmt.Println(blockChain)
	}
}


//随机调换
func randeDelegate() {
	rand.Seed(time.Now().Unix())
	index := rand.Intn(len(delegate))
	index1 := rand.Intn(len(delegate))

	if index1 == index {
	Label :
		index1 = rand.Intn(len(delegate))
		if index1 == index{
			goto Label
		}
	}

	tempDelegate := delegate[index]
	delegate[index] = delegate[index1]
	delegate[index1] = tempDelegate
}

// 声明产生新区快的方法
func GenerateNextBlock(bmp int,oldBlock Block,validator string) Block {

	var newBlock Block
	newBlock.PrefHash = oldBlock.HashCode
	newBlock.TimeStamp = time.Now().String()
	newBlock.Index = oldBlock.Index + 1
	newBlock.Validator = validator
	newBlock.BMP = bmp
	newBlock.HashCode = SetHash(newBlock)
	return newBlock
}

// 产生区块哈希的方法
func SetHash(b Block) string {

	hashCode := []byte(b.Validator+strconv.Itoa(b.Index)+b.TimeStamp+b.PrefHash+strconv.Itoa(b.BMP))

	sha := sha256.New()

	sha.Write(hashCode)

	hash := sha.Sum(nil)

	return hex.EncodeToString(hash)
}

```

+ 运行结果，每5秒生成一个新的区块链

```

[{0    0 } {0  98b05fa476e91a956f8460204cd528588ca06fe4b3a9e292f3e7d2b116fe24a4 2020-01-01 14:35:22.869545 +0800 CST m=+5.000842331 1 aaa}]
[{0    0 } {0  98b05fa476e91a956f8460204cd528588ca06fe4b3a9e292f3e7d2b116fe24a4 2020-01-01 14:35:22.869545 +0800 CST m=+5.000842331 1 aaa} {1 98b05fa476e91a956f8460204cd528588ca06fe4b3a9e292f3e7d2b116fe24a4 19e5781899bfdbd3919ffb17494a375fd84838269fc7103205d3b8317614be03 2020-01-01 14:35:27.875648 +0800 CST m=+10.006794579 2 bbb}]
[{0    0 } {0  98b05fa476e91a956f8460204cd528588ca06fe4b3a9e292f3e7d2b116fe24a4 2020-01-01 14:35:22.869545 +0800 CST m=+5.000842331 1 aaa} {1 98b05fa476e91a956f8460204cd528588ca06fe4b3a9e292f3e7d2b116fe24a4 19e5781899bfdbd3919ffb17494a375fd84838269fc7103205d3b8317614be03 2020-01-01 14:35:27.875648 +0800 CST m=+10.006794579 2 bbb} {2 19e5781899bfdbd3919ffb17494a375fd84838269fc7103205d3b8317614be03 d4129578e3bfa88f3d73418a86e9f0bc1c10e57e7a6ded7c75e7278b70a9bcf1 2020-01-01 14:35:32.877303 +0800 CST m=+15.008299445 3 aaa}]
[{0    0 } {0  98b05fa476e91a956f8460204cd528588ca06fe4b3a9e292f3e7d2b116fe24a4 2020-01-01 14:35:22.869545 +0800 CST m=+5.000842331 1 aaa} {1 98b05fa476e91a956f8460204cd528588ca06fe4b3a9e292f3e7d2b116fe24a4 19e5781899bfdbd3919ffb17494a375fd84838269fc7103205d3b8317614be03 2020-01-01 14:35:27.875648 +0800 CST m=+10.006794579 2 bbb} {2 19e5781899bfdbd3919ffb17494a375fd84838269fc7103205d3b8317614be03 d4129578e3bfa88f3d73418a86e9f0bc1c10e57e7a6ded7c75e7278b70a9bcf1 2020-01-01 14:35:32.877303 +0800 CST m=+15.008299445 3 aaa} {3 d4129578e3bfa88f3d73418a86e9f0bc1c10e57e7a6ded7c75e7278b70a9bcf1 33eca22906ae2462f6549382d5a84d34842472339c9f12712e6159daa3d7cdbf 2020-01-01 14:35:37.882827 +0800 CST m=+20.013673930 4 ddd}]

```

### 本系列教程源码

+ [完整源码请查看，源码下dpos.go](https://github.com/chuhemiao/go-basic-example)