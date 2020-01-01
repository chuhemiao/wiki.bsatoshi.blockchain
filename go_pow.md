# Go语言实现pow协议


### 通俗讲解共识

+ 所谓共识，通俗来说，就是我们大家对某种事物的理解达成一致的意思。比如说日常的开会讨论问题，又比如判断一个动物是不是猫，我们肉眼看了后觉得像猫，其满足猫的特征，那么我们认为它是猫。共识，是一种规则。

###  PoW，代表者是比特币 (BTC)

+ Proof of Work 工作量证明。字面意思，就是谁做的活越多，谁话事权越大，一定层面上类似现实生活的多劳多得的概念。

### 举例说明

+ 拿比特币为例子，比特币挖矿就是通过计算符合某一个比特币区块头的哈希散列值争夺记账权。这个过程需要通过大量的计算实现，简单理解就是你进行的计算量大（工作量大），你就有大概率获得记账权，即矿工的挖出的区块并入主链。

+ 区块头，区块链中的区块的头部。你有一个饭盒，饭盒第一层，形象为动物头部，称之为头部。第一层放着米饭，米饭就是头部装载着的东西，哈希散列值，一种通过数学公式计算得出的值。
    - 哈希：数学中的散列函数
    - 散列值: 通过哈希函数得出的值
    - 例如加法公式：1 + 2 = 3。那么哈希公式：hash(1,2) = 结果

+ 区块头的哈希散列值，饭盒第一层装着的是饭。那么这里的这个值就是区块头装着的东西。记账权，话事权，谁挖出的区块是有效的。

### 缺点

+ 矿池的出现，一定程度上违背了去中心化的初衷，同时也使得51%攻击成为可能，影响其安全性。
+ 存在巨大的算力浪费，看看矿池消耗大量的电力资源，随着难度增加，挖出的不够付电费

### Golang 实现PoW协议

```
package main

import (
	"crypto/sha256"
	"encoding/hex"
	"encoding/json"
	"fmt"
	"io"
	"log"
	"net/http"
	"os"
	"strconv"
	"strings"
	"sync"
	"time"

	"github.com/davecgh/go-spew/spew"
	"github.com/gorilla/mux"
	"github.com/joho/godotenv"

)

/*
	新建 .env ，添加 ADDR=9000
	新建 main.go，引入相应的包

	go run main.go 启动当前服务 控制台打印出如下消息

	2020/01/01 14:05:28 Listening on  9000
	(main.Block) {
	 Index: (int) 0,
	 Timestamp: (string) (len=51) "2020-01-01 14:05:28.320064 +0800 CST m=+0.000794081",
	 BPM: (int) 0,
	 Hash: (string) (len=64) "f1534392279bddbf9d43dde8701cb5be14b82f76ec6607bf8d6ad557f60f304e",
	 PrevHash: (string) "",
	 Difficulty: (int) 1,
	 Nonce: (string) ""
	}
	// 使用curl 请求生成新的区块
	curl -d '{"BMP": 20}' http://localhost:9000

	53a7710028d4aee15bcf06918508aa0107387a9432018089f6c507b8e1230045  do more work!
	d19f8f83b7e315126ba341ab1cc7d1d75acbbedde48e2a619fc70958a8f1cd16  do more work!
	c5d959b91b8d62a13ff4c153ea87b150a1fa2b7df17901b3bd67bae288296fe6  do more work!
	f21e06d0c3fd40d44dc9aac5b3acbbe768b9c223233da1ca63e1ffd1cf837b26  do more work!
	b1f09c6d3853af434001755f9c51f3477ff8fb42beafe836de4f21b3e5bd804b  do more work!
	ece1a6aa8d28f08806e5452bd4a418b8517525a0f96798d87e38f3015320da0c  do more work!
	fd18e42806c63e91fc674430e3e4c9d62662630823fff6844db16ce5abcf5d53  do more work!
	19e96095db4136996e4962e68002ee1cc053771c6496c389f6337e0abd3ba826  do more work!
	...
	// 查看当前已经生成的区块
	浏览器访问：http://localhost:9000

 */
// 代表难度系数，如果赋值为 1，则需要判断生成区块时所产生的 Hash 前缀至少包含1个 0
const difficulty = 1

/*

	Block 代表区块的结构体。

	Index 是区块链中数据记录的位置

	Timestamp 是自动确定的，并且是写入数据的时间

	BPM 是每分钟跳动的次数，是你的脉率

	Hash 是代表这个数据记录的SHA256标识符

	PrevHash 是链中上一条记录的SHA256标识符

	Difficulty 是当前区块的难度系数
	Nonce 是 PoW 挖矿中符合条件的数字
	Blockchain 是存放区块数据的集合
	Message 是使用 POST 请求传递的数据
	mutex 是为了防止同一时间产生多个区块
*/

//声明区块
type Block struct {
	Index      int
	Timestamp  string
	BPM        int
	Hash       string
	PrevHash   string
	Difficulty int
	Nonce      string
}

var Blockchain []Block

type Message struct {
	BPM int
}

var mutex = &sync.Mutex{}

//生成区块
func generateBlock(oldBlock Block, BPM int) Block {
	var newBlock Block

	t := time.Now()

	newBlock.Index = oldBlock.Index + 1
	newBlock.Timestamp = t.String()
	newBlock.BPM = BPM
	newBlock.PrevHash = oldBlock.Hash
	newBlock.Difficulty = difficulty

	for i := 0; ; i++ {
		hex := fmt.Sprintf("%x", i)
		newBlock.Nonce = hex
		if !isHashValid(calculateHash(newBlock), newBlock.Difficulty) {
			fmt.Println(calculateHash(newBlock), " do more work!")
			time.Sleep(time.Second)
			continue
		} else {
			fmt.Println(calculateHash(newBlock), " work done!")
			newBlock.Hash = calculateHash(newBlock)
			break
		}

	}
	return newBlock
}
//判断产生的哈希值是否合法
func isHashValid(hash string, difficulty int) bool {
	//复制 difficulty 个0，并返回新字符串，当 difficulty 为2 ，则 prefix 为 00
	prefix := strings.Repeat("0", difficulty)
	// HasPrefix判断字符串 hash 是否包含前缀 prefix
	return strings.HasPrefix(hash, prefix)
}
// 根据设定的规则，生成 Hash 值
func calculateHash(block Block) string {
	record := strconv.Itoa(block.Index) + block.Timestamp + strconv.Itoa(block.BPM) + block.PrevHash + block.Nonce
	h := sha256.New()
	h.Write([]byte(record))
	hashed := h.Sum(nil)
	return hex.EncodeToString(hashed)
}

// 验证区块
func isBlockValid(newBlock, oldBlock Block) bool {
	if oldBlock.Index+1 != newBlock.Index {
		return false
	}

	if oldBlock.Hash != newBlock.PrevHash {
		return false
	}

	if calculateHash(newBlock) != newBlock.Hash {
		return false
	}

	return true
}

// web服务器

func run() error {
	mux := makeMuxRouter()
	httpAddr := os.Getenv("ADDR")
	log.Println("Listening on ", os.Getenv("ADDR"))
	s := &http.Server{
		Addr:           ":" + httpAddr,
		Handler:        mux,
		ReadTimeout:    10 * time.Second,
		WriteTimeout:   10 * time.Second,
		MaxHeaderBytes: 1 << 20,
	}

	if err := s.ListenAndServe(); err != nil {
		return err
	}

	return nil
}

func makeMuxRouter() http.Handler {
	muxRouter := mux.NewRouter()
	muxRouter.HandleFunc("/", handleGetBlockchain).Methods("GET")
	muxRouter.HandleFunc("/", handleWriteBlock).Methods("POST")
	return muxRouter
}

// handleGetBlockchain 获取所有区块的列表信息

func handleGetBlockchain(w http.ResponseWriter, r *http.Request) {
	bytes, err := json.MarshalIndent(Blockchain, "", "  ")
	if err != nil {
		http.Error(w, err.Error(), http.StatusInternalServerError)
		return
	}
	io.WriteString(w, string(bytes))
}

// 生成新的区块
func handleWriteBlock(w http.ResponseWriter, r *http.Request) {
	w.Header().Set("Content-Type", "application/json")
	var m Message

	decoder := json.NewDecoder(r.Body)
	if err := decoder.Decode(&m); err != nil {
		respondWithJSON(w, r, http.StatusBadRequest, r.Body)
		return
	}
	defer r.Body.Close()

	//ensure atomicity when creating new block
	mutex.Lock()
	newBlock := generateBlock(Blockchain[len(Blockchain)-1], m.BPM)
	mutex.Unlock()

	if isBlockValid(newBlock, Blockchain[len(Blockchain)-1]) {
		Blockchain = append(Blockchain, newBlock)
		spew.Dump(Blockchain)
	}

	respondWithJSON(w, r, http.StatusCreated, newBlock)

}
// 返回json格式
func respondWithJSON(w http.ResponseWriter, r *http.Request, code int, payload interface{}) {
	w.Header().Set("Content-Type", "application/json")
	response, err := json.MarshalIndent(payload, "", "  ")
	if err != nil {
		w.WriteHeader(http.StatusInternalServerError)
		w.Write([]byte("HTTP 500: Internal Server Error"))
		return
	}
	w.WriteHeader(code)
	w.Write(response)
}

func main() {
	// 根目录的文件 .env 读取相应的变量
	err := godotenv.Load()
	if err != nil {
		log.Fatal(err)
	}

	go func() {
		t := time.Now()
		// 创建初始区块
		genesisBlock := Block{}
		genesisBlock = Block{0, t.String(), 0, calculateHash(genesisBlock), "", difficulty, ""}
		spew.Dump(genesisBlock)

		mutex.Lock()
		Blockchain = append(Blockchain, genesisBlock)
		mutex.Unlock()
	}()
	// 启动web服务
	log.Fatal(run())

}
```

### 本系列教程源码

+ [完整源码请查看，源码下pow.go](https://github.com/chuhemiao/go-basic-example)