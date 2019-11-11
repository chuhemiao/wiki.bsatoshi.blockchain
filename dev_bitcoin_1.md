# 比特币开发系列文章：虚拟机搭建比特币运行环境

# docker 安装bitcoin 并运行

mac直接下载docker 安装包，登录账号后运行，进入iTerm后运行：sudo docker pull freewil/bitcoin-testnet-box

![](https://cdn.bsatoshi.com/2019/11/09/15732875023040.jpg)

拉取到镜像后，运行 sudo docker run -t -i -p 19001:19001 -p 19011:19011 freewil/bitcoin-testnet-box  进入容器


![](https://cdn.bsatoshi.com/2019/11/09/15732876424615.jpg)


启动成功后，将在本机模拟运行两个比特币测试钱包节点，组成一个私有范围的比特币测试网络。

输入下面的命令可以查看测试网络节点状态信息:

![](https://cdn.bsatoshi.com/2019/11/09/15732877158625.jpg)

初始化和测试区块链数据

1.使用getnewaddress命令分别为两个钱包生成一个地址(或者用命令 make address1 也可以)：bitcoin-cli -datadir=1 getnewaddress

![](https://cdn.bsatoshi.com/2019/11/09/15732881021834.jpg)

2.查看地址对应的私钥：bitcoin-cli -datadir=1  dumpprivkey 2N5JfbrwupJndoTt2Ms1TN1GJbVfgbPBjbN

![](https://cdn.bsatoshi.com/2019/11/09/15732881165048.jpg)


3.生成一个区块：make generate

![](https://cdn.bsatoshi.com/2019/11/09/15732881282795.jpg)


4.生成多个区块：make generate BLOCKS=66 ， blocks后跟数字为当前要生成区块的数量

![](https://cdn.bsatoshi.com/2019/11/09/15732882151328.jpg)


继续上步骤操作继续生成新的区块，然后可以看到钱包1目前有余额，给钱包2转账，这里转100个比特币：

make sendfrom1 ADDRESS=2NAUVNvRVKn2QT2yoKYo1LXBBHES1DiiAWp AMOUNT=100