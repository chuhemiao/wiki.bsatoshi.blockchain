# Go语言之channel


### 什么是Channel

+ 通道（channel），就像一个可以用于发送类型化数据的管道，由其负责协程之间的通信，从而避开所有由共享内存导致的陷阱；这种通过通道进行通信的方式保证了同步性。数据在通道中进行传递：在任何给定时间，一个数据被设计为只有一个协程可以对其访问，所以不会发生数据竞争。

+ channel是带有类型的管道，你可以通过它用信道操作符 <- 来发送或者接收值，“箭头”就是数据流的方向
    - ch <- v    // 将 v 发送至信道 ch。
    - v := <-ch  // 从 ch 接收值并赋予 v。
    - 默认情况下，发送和接收操作在另一端准备好之前都会阻塞

+ 和映射与切片一样，信道在使用前必须创建：ch := make(chan int)

+ channel可以是 带缓冲的。将缓冲长度作为第二个参数提供给 make 来初始化一个带缓冲的信道:
    - 方式一：  var ch1 chan int  ch1 = make(chan int)
    - 方式二：  ch := make(chan int, 100),通道只能传递100个数据(buf 是通道可以同时容纳的元素个数)
    - 仅当信道的缓冲区填满后，向其发送数据时才会阻塞。当缓冲区为空时，接受方会阻塞。(fatal error: all goroutines are asleep - deadlock!)

### 例子

```

    func sum(s []int, c chan int) {
        sum := 0
        for _, v := range s {
            sum += v
        }
        c <- sum // 将和送入 c
    }


    func main() {
        s := []int{7, 2, 8, -9, 4, 0}

        c := make(chan int)
        go sum(s[:len(s)/2], c)
        go sum(s[len(s)/2:], c)
        x, y := <-c, <-c // 从 c 中接收

        fmt.Println(x, y, x+y)
    }

```

### 关闭channel

+ 发送者可通过 close 关闭一个信道来表示没有需要发送的值了。
+ 接收者可以通过为接收表达式分配第二个参数来测试信道是否被关闭：若没有值可以接收且信道已被关闭，那么在执行完之后 ok 会被设置为 false。
    -  v, ok := <-ch

```

    func fibonacci(n int, c chan int) {
        x, y := 0, 1
        for i := 0; i < n; i++ {
            c <- x
            x, y = y, x+y
        }
        close(c)
    }


    c := make(chan int, 10)
	go fibonacci(cap(c), c)
	for i := range c {
		fmt.Println(i)
	}
```

### 通道的同步

+ 使用通道来同步协程之间的执行

```

    // 这个worker函数将以协程的方式运行
    // 通道`done`被用来通知另外一个协程这个worker函数已经执行完成
    func worker(done chan bool) {
        fmt.Print("working...")
        time.Sleep(time.Second)
        fmt.Println("done")
        // 向通道发送一个数据，表示worker函数已经执行完成
        done <- true
    }
    // 使用协程来调用worker函数，同时将通道`done`传递给协程
    // 以使得协程可以通知别的协程自己已经执行完成
    done := make(chan bool, 1)
    go worker(done)
    // 一直阻塞，直到从worker所在协程获得一个worker执行完成的数据
    <-done

```

### 解决阻塞的2种办法

+ 使用select的default语句，在channel不可读写时，即可返回
+ 使用select+定时器，在超时时间内，channel不可读写，则返回（推荐方式）


### 本教程系列代码

+ [示例代码](https://github.com/chuhemiao/go-basic-example)

### 推荐阅读

+ [理解 Go 中的 JSON](https://sanyuesha.com/2018/05/07/go-json/)