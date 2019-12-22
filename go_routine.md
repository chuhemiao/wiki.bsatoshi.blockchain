# 细说Go语言之Goroutine


### 什么是Goroutine

+ Go的CSP并发模型，是通过goroutine和channel来实现的。

+ goroutine 是Go语言中并发的执行单位。有点抽象，其实就是和传统概念上的”线程“类似，可以理解为”线程“。

+ channel是Go语言中各个并发结构体(goroutine)之前的通信机制。 通俗的讲，就是各个goroutine之间通信的”管道“，有点类似于Linux中的管道。

+ 线程（Thread）：有时被称为轻量级进程(Lightweight Process，LWP），是程序执行流的最小单元。一个标准的线程由线程ID，当前指令指针(PC），寄存器集合和堆栈组成。另外，线程是进程中的一个实体，是被系统独立调度和分派的基本单位，线程自己不拥有系统资源，只拥有一点儿在运行中必不可少的资源，但它可与同属一个进程的其它线程共享进程所拥有的全部资源。

+ 线程拥有自己独立的栈和共享的堆，共享堆，不共享栈，线程的切换一般也由操作系统调度。

+ 协程（coroutine）：又称微线程与子例程（或者称为函数）一样，协程（coroutine）也是一种程序组件。相对子例程而言，协程更为一般和灵活，但在实践中使用没有子例程那样广泛。


### 示例

```

    func main() {
        messages := make(chan string)

        go func() { messages <- "ping" }()

        msg := <-messages
        fmt.Println(msg)
    }

```

### 推荐阅读

+ [Go goroutine理解](https://segmentfault.com/a/1190000018150987)