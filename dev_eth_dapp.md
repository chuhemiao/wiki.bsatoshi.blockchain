# 2020年Macos最全 ETH区块链环境搭建,并使用Truffle创建第一个Dapps

### 以太坊开需要哪些工具

+ HomeBrew

+ Xcode命令行工具

+ go-ethereum

+ Ganache

+ nodejs和npm

+ Truffle

+ VsCode


### 安装HOMEBREW

+ 如果已经安装请忽略本步骤

+ 请打开https://brew.sh/，然后复制红框内内容: `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`

![homebrew](https://cdn.bsatoshi.com/2019/12/14/15763112879761.jpg)

### 安装Xcode

+ 一般电脑应该会有，没有的话，那自行谷歌把！

### 安装geth

+ brew tap ethereum/ethereum
+ brew install ethereum

+ 检测是否安装完成：输入geth -h，如果出现下图所示，则代表已经安装完成


### nodejs和npm

+ brew install node

+ node -v 检测是否已经安装成功

+ npm -v


### 安装truffle

+ npm install -g truffle

+ truffle -v 检测是否安装成功

### 安装Ganache

+ 浏览器中打开下面的链接，https://www.trufflesuite.com/ganache

+ 下载Ganache for MacOS ，然后点击下载后的dmg包，依次按步骤执行即可。

+ 然后启动此软件，就可以进行相关调试了，如下图

![安装Ganache](https://cdn.bsatoshi.com/2019/12/14/15763116506866.jpg)


### 安装VsCode

+ 打开网页：https://code.visualstudio.com/，下载后直接打开。

+ 然后安装插件，先点击步骤1，然后在步骤上直接搜索当前要安装的插件名称，然后点击install即可


![安装VsCode](https://cdn.bsatoshi.com/2019/12/14/15763119152803.jpg)

### 创建第一个dapp


+ 首先上述软件已经安装成功，然后打开Ganache客户端，可以看到已经分配的测试网账户和一些余额。

+ 然后打开终端，创建一个目录mkdir blockchain-test
+ cd blockchain-test
+ 使用前面安装的truffle创建项目，这里推荐使用truffle box 模式，它会带一些自动的事例，具体可以看文档和一些已经存在的项目：https://www.trufflesuite.com/boxes

+ 这里我们以[pet-shop](https://www.trufflesuite.com/boxes/pet-shop),首先执行：sudo truffle unbox pet-shop

![创建第一个dapp](https://cdn.bsatoshi.com/2019/12/14/15763125307985.jpg)

+ 然后得到新项目目录如下

![创建第一个dapp](https://cdn.bsatoshi.com/2019/12/14/15763126268873.jpg)

+ contracts/ : 包含所有項目中智能合約 Solidity 代码，其中有事例 Migrations.sol 智能合約，容后再介紹；

+ migrations/ : 主要是 Truffle 用与部署智能合約的一个迁移命令集；

+ test/ : 包含 JavaScript 和 Solidity 的 test cases；

+ truffle-config.js : Truffle 的一些设置，比如端口、测试网、正式网等；

+ node_modules ： 是一些安装的基础包

+ bs-config.json:是智能合约的编译鲁姆

+ src：是项目的主入口文件

+ 然后分别依次执行 ： 
    - truffle compile
    - truffle migrate
    - truffle test
    - npm run dev

+ 然后就可以看到程序已经跑起来：

![truffle创建第一个dapp](https://cdn.bsatoshi.com/2019/12/14/15763132463521.jpg)

+ 然后程序会默认打开浏览器，也可以直接访问：http://localhost:3000 查看已经得到的效果

![truffle创建第一个dapp](https://cdn.bsatoshi.com/2019/12/14/15763132695654.jpg)


+ 访问：http://localhost:3001可以看到智能合约的一些交互和当前dapp的一些运行情况，如下图：

![truffle创建第一个dapp](https://cdn.bsatoshi.com/2019/12/14/15763134408246.jpg)