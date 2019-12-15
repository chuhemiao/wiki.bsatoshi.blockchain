# eos区块链环境搭建


**EOS、EOS-Mainnet、EOSIO都是什么？**

### 背景介绍

+ 2017年，一个叫Block.one的公司开发了一个叫EOSIO的软件。为了开发这个软件，Block.one进行了一个历时350天的众筹，最后募集资金超过40亿美元。

+ EOSIO这个软件是后来的EOS-Mainnet和其他区块链网络（BOS、Telos等等）构建网络的基础工具。

+ EOS-Mainnet，也就是EOS主网，是我们目前使用最广泛的基于EOSIO软件的区块链网络。网上听说的很多EOS Dapp（Decentralized Application，去中心化的app）都是运行在EOS主网上，大多数人一说EOS，基本上指的就是EOS主网。

+ EOS是EOS主网上的原生代币的符号，EOS的数量体现了你在EOS主网上可使用资源和可参与治理的多少。EOS本身具有价格，可以在各大交易所购买。

### 账户、公钥、私钥

+ 在EOS上，账户类似于用户名，所有的操作都是以账户为基础的，转账、投票、更新信息，参与Dapp等等。账户需要注册，至多12位字符。

+ 如何证明这个账户是属于你的而不是别人的呢？这个就需要用到公钥和私钥，用互联网来类比的话就是密码，不过这个密码是由公钥和私钥两部分构成的。
形象地理解，公钥和私钥就相当于锁和钥匙，私钥，也就是钥匙，掌握在你自己手里；公钥，也就是锁，和账户绑定。如果你想在账户里进行操作，就需要用你手里的私钥和公钥匹配，如果匹配上了，那么账户就认为你是所有者。

+ 实际上，EOS的账户系统还可以更加复杂，比如给予每个公钥/私钥对不同的权限（Owner和Active），对一个账户就行多人共管（Multi-sig，多签）等等，暂时先不展开了。
注意，一个公钥/私钥对可以同时控制多个账户。

（三）钱包

+ 常用的钱包，PC端和国外主要用Scatter，手机端和国内主要用TokenPocket、Meetone。这些可以通过他们的官网下载。

+ 每个EOS账户里面存在着三者资源，所有的操作都需要花费这三种资源，可以理解，这三种资源是你使用EOS网络的成本。这三种资源叫做计算（CPU）、存储（RAM）和网络（NET）。


| 项目 | 传统含义 | EOS上含义 |
| ------ | ------ | ------ |
| 计算（CPU）	 | 中央处理单元，指的是负责在计算机中执行指令和处理信息的硬件 | 一种按时间计价的资源（单位：微秒），用来衡量EOS节点应该对你帐户中的交易确认所投入的时间 |
| 网络（NET） | 互联网带宽 | 一种以空间计价的资源（单位：字节），用来衡量当在P2P层上传输数据时需要多少区块的网络描述来存储你的交易数据 |
| 存储（RAM） | 存储是用来存储云平台上的所有数据。RAM是指运行内存，速度更快，但储存是暂时的，断电后内容就会消失 | RAM不再是临时存储，而是作为主储存层，用来储存所有的数据。相当于是让储存速度更快的内存（RAM）充当了硬盘的功能。在RAM中存储数据库，可以让读取数据的速度更快 |


### EOSIO如何快速构建开发网络

+ EOSIO是由三个组件组成的。
    - nodeos:管理区块链节点的组件。
    - keosd：管理钱包的组件。
    - cleos：控制区块链和钱包CLI工具。

### Macos 安装EOSIO


+ 安装  `brew tap eosio/eosio`   `brew install eosio`

+ 卸载 `brew remove eosio`

### Ubuntu 18.04  Debian 安装 eosio

+ wget https://github.com/EOSIO/eos/releases/download/v1.8.6/eosio_1.8.6-1-ubuntu-18.04_amd64.deb

+ sudo apt install ./eosio_1.8.6-1-ubuntu-18.04_amd64.deb

### Ubuntu 16.04 Debian 安装 eosio

+ wget https://github.com/EOSIO/eos/releases/download/v1.8.6/eosio_1.8.6-1-ubuntu-16.04_amd64.deb

+ sudo apt install ./eosio_1.8.6-1-ubuntu-18.04_amd64.deb

### CentOS 通过RPM  安装 eosio

+ wget https://github.com/EOSIO/eos/releases/download/v1.8.6/eosio-1.8.6-1.el7.x86_64.rpm

+ sudo yum install ./eosio-1.8.6-1.el7.x86_64.rpm

### 设置一个开发目录

+ cd /data  mkdir development-eos

+ cd development-eos  进入开发目录

### 启动节点

+ keosd &

+ 如果成功则会看到如下截图：

![keosd](https://cdn.bsatoshi.com/2019/12/14/15763095080716.jpg)

### 启动nodeos


            nodeos -e -p eosio \
            --plugin eosio::producer_plugin \
            --plugin eosio::chain_api_plugin \
            --plugin eosio::http_plugin \
            --plugin eosio::history_plugin \
            --plugin eosio::history_api_plugin \
            --filter-on="*" \
            --access-control-allow-origin='*' \
            --contracts-console \
            --http-validate-host=false \
            --verbose-http-errors >> nodeos.log 2>&1 &


### 查看nodeos.log是否已经启动nodeos

+ tail -f nodeos.log

![nodeos.log](https://cdn.bsatoshi.com/2019/12/14/15763097186602.jpg)

### 查看当前已经存在的eos钱包

+ cleos wallet list

+ 不出意外应该会返回一个空的数组，当前我们并没有创建钱包

### 检查Nodeos 的端口

+ 浏览器打开：http://localhost:8888/v1/chain/get_info  当然你也可以直接使用curl的方式：curl http://localhost:8888/v1/chain/get_info

![检查Nodeos 的端口](https://cdn.bsatoshi.com/2019/12/14/15763099467987.jpg)


### Macos安装CDT

+ brew tap eosio/eosio.cdt
+ brew install eosio.cdt

+ 卸载CDT  brew remove eosio.cdt

### CentOS/Redhat内核安装CDT

+ wget https://github.com/EOSIO/eosio.cdt/releases/download/v1.6.3/eosio.cdt-1.6.3-1.el7.x86_64.rpm

+ sudo yum install ./eosio.cdt-1.6.3-1.el7.x86_64.rpm

+ 卸载CDT   sudo yum remove eosio.cdt

### 通过源码编译方式安装CDT

+ 首先克隆下源码 git clone --recursive https://github.com/eosio/eosio.cdt --branch v1.6.3 --single-branch


+ 然后执行 cd eosio.cdt   ./build.sh

+ sudo ./install.sh


### 创建一个开发模式的钱包

+ 首先执行创建钱包的命令：cleos wallet create --to-console  ， 此时cleos会返回一个密码，你可以存在任何地方，后续以备使用。

+ 打开一个eos钱包：cleos wallet open

+ 返回钱包的列表查看目前可以打开的钱包：cleos wallet list

+ 打开之前首先需要解锁：cleos wallet unlock

+ 然后在输入：cleos wallet list，会看到列表的钱包后面会增加一个*号，然后就可以在执行打开命令打开。

### 生成带有密钥的EOS钱包

+ cleos wallet create_key
+ 运行上述命令后会得到一个新的key： "EOS8PEJ5FM4LLLpHK...X6PypHu97kqGDJQY5Y"

+ 在网页https://developers.eos.io/eosio-home/docs/wallets 的第五步输入上述得到的key就可以得到一个开发的Public key

### 导出开发的密钥

+ cleos wallet import，运行命令后会得到一串字符串（private key），包存后可以用来后期的开发


### 创建eos测试账户

+ 使用命令分别创建bob和alice两个账户，YOUR_PUBLIC_KEY是之前步骤生成的key

+ cleos create account eosio bob YOUR_PUBLIC_KEY 
+ cleos create account eosio alice YOUR_PUBLIC_KEY

+ 运行命令后会反馈当前广播交易的消息

### 获取Public Key

+ cleos get account alice（当前创建的用户）

![获取Public Key](https://cdn.bsatoshi.com/2019/12/14/15763107114594.jpg)

### 参考

+ [developers eos](https://developers.eos.io/eosio-home/docs/setting-up-your-environment)