# Golang 基础之错误处理


### 错误处理机制

+ Go 语言通过内置的错误接口提供了非常简单的错误处理机制
+ 一般使用 error 值来表示错误状态,使用errors.New 可返回一个错误信息

+ error 类型是一个内建接口：

```

    type error interface {
        Error() string
    }

```

+ 通常函数会返回一个 error 值，调用的它的代码应当判断这个错误是否等于 nil 来进行错误处理。

```

    open,err := os.OpenFile("./opentest.txt",os.O_RDONLY,0644)

	if err != nil{
		errors.New("math: square root of negative number")
	}

	fmt.Println("函数之方法：",open)

```

### 本教程系列代码

+ [示例代码](https://github.com/chuhemiao/go-basic-example)