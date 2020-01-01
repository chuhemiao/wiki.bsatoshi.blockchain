# Go语言实现raft协议

### Raft算法概述

+ Raft算法由leader节点来处理一致性问题。leader节点接收来自客户端的请求日志数据，然后同步到集群中其它节点进行复制，当日志已经同步到超过半数以上节点的时候，leader节点再通知集群中其它节点哪些日志已经被复制成功，可以提交到raft状态机中执行。Raft 提供了一种在计算系统集群中分布状态机的通用方法，确保集群中的每个节点都同意一系列相同的状态转换。

+ 通过以上方式，Raft算法将要解决的一致性问题分为了以下几个子问题。

    - leader选举：集群中必须存在一个leader节点。
    - 日志复制：leader节点接收来自客户端的请求然后将这些请求序列化成日志数据再同步到集群中其它节点。
    - 安全性：如果某个节点已经将一条提交过的数据输入raft状态机执行了，那么其它节点不可能再将相同索引 的另一条日志数据输入到raft状态机中执行。


###  Raft 协议将整个过程分为主要3个步骤：

+ 领导者：和其他一致性算法相比，Raft 使用一种更强的领导能力形式。比如，日志条目只从领导者发送给其他的服务器。这种方式简化了对复制日志的管理并且使得 Raft 算法更加易于理解。

+ 领导选举：Raft 算法使用一个随机计时器来选举领导者。这种方式只是在任何一致性算法都必须实现的心跳机制上增加了一点机制。在解决冲突的时候会更加简单快捷。

+ 关系调整：Raft 使用一种共同一致的方法来处理集群成员变换的问题，在这种方法中，两种不同的配置都要求的大多数机器会重叠。这就使得集群在成员变换的时候依然可以继续工作。


### Raft算法基础

+ 一个典型的 Raft 集群包含多个节点。在任意时刻，每个节点都将处于以下三个状态之一：

    - leader：处理所有来自客户端的请求，封装为可重入的日志记录（log entry），并将其复制给其他 follower 节点，并在收到超过半数的确认后将日志提交。
    - follower：follower 是被动的，他们自己不产生请求，只处理 leaders 和 candidates 的请求并回应。
    - candidate：follower 被选举成为 leader 之前的状态。

+ Raft 集群的节点之间只存在两种 RPC 调用：

    - RequestVote RPC：发起于 candidate 节点，作用于其他节点，用于收集选票，只有当 candidate 当前日志的 term 和 index 都比当前节点
    - AppendEntries RPC：发起于 leader 节点，作用于 follower 节点，用于将 leader 的 log entries 复制给 follower。当 AppendEntries RPC 不包含 log entry 时，则其作为心跳（heartbeat）告知所有 follower 节点 leader 的存活。


+ 所有节点启动时都是 follower 状态，当一个 follower 在一段时间内没有收到来自其他节点的请求或心跳，其超时并转化为一个 candidate 并发起选举。

+ 当收到大多数节点的同意后，candidate 转化为 leader，并开始处理其任期内的一切操作，直到其发现了集群中处于更高 term 的节点，则再次转化为 follower 接受其他请求。

** 待更新更多内容 **

### 推荐阅读

+ [Raft算法分析与实现](https://juejin.im/entry/5b74e1f0f265da283479709f)
+ [ETCD 原理分析（一）- Raft 算法原理](https://blog.didiyun.com/index.php/2019/02/27/etcd-raft/)
+ [Raft算法原理](https://www.codedump.info/post/20180921-raft/)
+ [etcd Raft库解析](https://www.codedump.info/post/20180922-etcd-raft/)