# Go语言之select用法

### select的用处

+ Go的select关键字可以让你同时等待多个通道操作，

+ select 会阻塞到某个分支可以继续执行为止，这时就会执行该分支。当多个分支都准备好时会随机选择一个执行。

+ select 中的其它分支都没有准备好时，default 分支就会执行。



```

    c1 := make(chan string, 1)         //定义两个有缓冲通道，容量为1
    c2 := make(chan string, 1)

    go func() {
        time.Sleep(time.Second * 1)   //每隔1秒发送数据
        c1 <- "name: xuchao"
    }()

    go func() {
        time.Sleep(time.Second * 2)    //每隔2秒发送数据
        c2 <- "age: 25"
    }()

    for i:=0; i<2; i++ {                //使用select来等待这两个通道的值，然后输出
        select {
        case msg1 := <- c1:
            fmt.Println(msg1)
        case msg2 := <- c2:
            fmt.Println(msg2)
        }
    }


    // select默认选择
	tick := time.Tick(100 * time.Millisecond)
	boom := time.After(500 * time.Millisecond)
	for {
		select {
		case <-tick:
			fmt.Println("tick.")
		case <-boom:
			fmt.Println("BOOM!")
			return
		default:
			fmt.Println("默认情况....")
			time.Sleep(50 * time.Millisecond)
		}
	}


```