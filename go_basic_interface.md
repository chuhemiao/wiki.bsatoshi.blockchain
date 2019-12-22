# Golang 基础之接口

### 接口

+ 语言提供了另外一种数据类型即接口，它把所有的具有共性的方法定义在一起，任何其他类型只要实现了这些方法就是实现了这个接口

+ 接口类型 是由一组方法签名定义的集合。接口类型的变量可以保存任何实现了这些方法的值。

+ 隐式接口从接口的实现中解耦了定义，这样接口的实现可以出现在任何包中，无需提前准备。

+ 接口值可以用作函数的参数或返回值。

+ nil 接口值既不保存值也不保存具体类型。

+ 空接口可保存任何类型的值,空接口被用来处理未知类型的值。

### 类型断言 

+ 类型断言,提供了访问接口值底层具体值的方式
    - t := i.(T)  该语句断言接口值 i 保存了具体类型 T，并将其底层类型为 T 的值赋予变量 t。


```

    var i interface{} = "hello"

	s := i.(string)
	fmt.Println(s)

	s, ok := i.(string)
	fmt.Println(s, ok)

	f, ok := i.(float64)
	fmt.Println(f, ok)

	f = i.(float64) // 报错(panic)
	fmt.Println(f)
```

### 类型选择 

+ 是一种按顺序从几个类型断言中选择分支的结构。

+ 类型选择与一般的 switch 语句相似，不过类型选择中的 case 为类型（而非值）， 它们针对给定接口值所存储的值的类型进行比较。

+ 按照接口接受的类型，然后case判断当前类型，在返回对应情况

```

func do(i interface{}) {
	switch v := i.(type) {
	case int:
		fmt.Printf("Twice %v is %v\n", v, v*2)
	case string:
		fmt.Printf("%q is %v bytes long\n", v, len(v))
	default:
		fmt.Printf("I don't know about type %T!\n", v)
	}
}

func main() {
	do(21)
	do("hello")
	do(true)
}


```

### 定义一个最常用的接口 Stringer

+ Stringer 是一个可以用字符串描述自己的类型。fmt 包（还有很多包）都通过此接口来打印值。

```

    type Person struct {
        Name string
        Age  int
    }

    func (p Person) String() string {
        return fmt.Sprintf("%v (%v years)", p.Name, p.Age)
    }

    func main() {
        a := Person{"kk", 23}
        z := Person{"chuhe miao", 22}
        fmt.Println(a, z)
    }

```


### 接口示例


```
    // 定义接口Phone，里面仅有call()一个方法
    type Phone interface {
        call()
    }

    type HwPhone struct {
    }

    func (hwPhone HwPhone) call() {
        fmt.Println("I am HwPhone, I can call you!")
    }

    type IPhone struct {
    }

    func (iPhone IPhone) call() {
        fmt.Println("I am iPhone, I can call you!")
    }


    func main() {
        // 定义一个phone的变量
        var phone Phone

        phone = new(HwPhone)
        phone.call()

        phone = new(IPhone)
        phone.call()

    }

```



### 本教程系列代码

+ [示例代码](https://github.com/chuhemiao/go-basic-example)