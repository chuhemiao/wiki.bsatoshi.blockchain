# Golang 基础语法

### 声明变量

+ Go中函数、变量、常量、类型、语句标签和包的名称遵循一个简单的规则：名称开头是一个字母或下划线，后面可以跟任意数量的字符、数字或下划线，并区分大小写。

+ Go和C一样也有自身的一些关键字，Go中有25个关键字，只能用在语法允许的地方，而不能用来命名。

### Go 中25个关键字简单说明

+ package: 定义包名, go中任何一个文件必须有一个package, 一般而言,package的定义和文件所属文件夹一致, 并且main函数所在文件的package必须是main

+ import: 导入包名的关键字

+ const: 声明常量的关键字

+ var: 声明变量的关键字

+ func: 定义函数关键字(结构体方法其本质也是函数)

+ defer: 延迟执行(先注册后执行)关键字(文件读写、网络连接等资源的释放). defer后面必须是函数或者方法的调用OS包中.osExit()主动调用时,defer不再执行

+ go: 并发关键字   go test() //异步执行test()函数

+ return: 函数返回

+ struct: 定义结构体

+ interface: 定义接口(所有变量都实现空接口)

+ map: 声明创建map类型关键字

+ chan: 声明创建channel类型关键字

**和控制流程的关键字**

+ if, else, for, range, break, continue

+ swich, select, case, fallthrough, default

+ type: 这个关键字非常常用, 定义结构体,类型等

+ goto: 跳转语句关键字

+ if else: 控制结构

### 声明一个变量

+ 变量声明
    - var 语句用于声明一个变量列表，跟函数的参数列表一样，类型在最后。
    - 声明多个类型时，可以使用()方式，如后续例子（声明布尔类型、uint64类型、复合类型）

```
var c, php, golang bool

func main() {
	fmt.Println( c, php, golang)
}
```

+ 变量的初始化

    - 变量声明可以包含初始值，每个变量对应一个。
    - var i, j int = 1, 2

+ 短变量声明

    - 在函数中，简洁赋值语句 := 可在类型明确的地方代替 var 声明。
    - 此方式不适合用在函数上，比如 test := main(){}  错误写法
    - k := 3
	- erlang, js, python := true, false, "no!"


Go 的数据类型分四大类型：基础类型、聚合类型、引用类型、接口类型


### 基础类型

+ 声明布尔类型、uint64类型、复合类型

```
var (
	ToBe   bool       = false
	MaxInt uint64     = 1<<64 - 1
	z      complex128 = cmplx.Sqrt(-5 + 12i)
)
```

+ 零值：没有明确初始值的变量声明会被赋予它们的 零值，其中零值有三种情况

    - 数值类型为 0，
    - 布尔类型为 false，
    - 字符串为 ""（空字符串）。

```
var i int
	var f float64
	var b bool
	var s string
	fmt.Printf("%v %v %v %q\n", i, f, b, s)

```

+ 常量声明用 const

    - const sc string = "hello chuhemiao"
    - const pi float32 = 3.1415926


+ for
    - Go 只有一种循环结构：for 循环。
    - Go 的 for 语句后面的三个构成部分外没有小括号， 大括号 { } 则是必须的。
    - for 可以直接当while使用

```
    sum := 0
	for i := 0; i < 10; i++ {
		sum += i
	}

    for ; i < 10;{
		sum += i
	}

    for sum < 1000 {
		sum += sum
	}

```

+ if
    - Go 的 if 语句与 for 循环类似，表达式外无需小括号 ( ) ，而大括号 { } 则是必须的。

```
    if x < 0 {
		return  true
	}else{
        return false
    }
```

+ switch

    - switch 是编写一连串 if - else 语句的简便方法。它运行第一个值等于条件表达式的 case 语句。

```
    // 显示当前用户的操作系统
    fmt.Print("Go runs on ")
	switch os := runtime.GOOS; os {
	case "darwin":
		fmt.Println("OS X.")
	case "linux":
		fmt.Println("Linux.")
	default:
		fmt.Printf("%s.\n", os)
	}

```


+ defer
    - defer 语句会将函数推迟到外层函数返回之后执行，延迟调用


```

    defer fmt.Println("world")

	fmt.Println("hello")

```

### 聚合类型

+ 数组
    - 类型 [n]T 表示拥有 n 个 T 类型的值的数组。
    - 表达式 var a [10]int ,变量 a 声明为拥有 10 个整数的数组。
    - 数组的长度是其类型的一部分，数组不能改变大小,声明时是多大就是多大
    - 声明的数组长度可以大于元素个数，不够的位数用0补，但是反之不成立

```
    var a [2]string
	a[0] = "Hello"
	a[1] = "Chuhemiao"
	fmt.Println(a[0], a[1])
	fmt.Println(a)

	primes := [6]int{2, 3, 5, 7, 11, 13,15,17,19,21}
    // 如果位数不够则补0
	prime := [10]int{2, 3, 5, 7, 11, 13}
    //array index 5 out of bounds [0:5] 超过了会报错
	primeNum := [5]int{2, 3, 5, 7, 11, 13}
	fmt.Println(primes)
```

+ 结构体

    - 结构体（struct）就是一组字段，使用关键字struct声明
    - 如果内部字段为大写则可外部使用
    - 结构体字段使用点号来访问
    - 结构体字段可以通过结构体指针来访问,访问形式可以是(*p).X，也可以直接p.X

+ 映射（map）
    - 映射将键映射到值。
    - 映射的零值为 nil 。nil 映射既没有键，也不能添加键。
    - make 函数会返回给定类型的映射，并将其初始化备用。
    - 映射的文法与结构体相似，使用时必须有键名。
    - 修改映射，直接赋值即可
    - 删除映射，使用delete(m, key)，删除对应的key即可
    - elem, ok = m[key]，检测某个键是否存在，如果ok为true则存在，否则不存在
```
    type Sex struct {
        X int
        Y int
    }

    v := Sex{18, 20}
    v.X = 4
    p1 := &v
    p1.X = 1e9
    fmt.Println(v.X)
    // 映射
    type Vertex struct {
        Lat, Long float64
    }

    var m map[string]Vertex
    // make 函数会返回给定类型的映射，并将其初始化备用。
    m = make(map[string]Vertex)
	m["Bell Labs"] = Vertex{
		40.68433, -74.39967,
	}
	fmt.Println(m["Bell Labs"])

    // 映射的操作  赋值，删除，检测key是否存在
	mdk := make(map[string]int)

	mdk["Answer"] = 42
	fmt.Println("The value:", mdk["Answer"])

	mdk["Answer"] = 48
	fmt.Println("The value:", mdk["Answer"])

	delete(mdk, "Answer")
	fmt.Println("The value:", mdk["Answer"])

	vmdk, ok := mdk["Answer"]
	fmt.Println("The value:", vmdk, "Present?", ok)


```


### 引用类型

+ 指针
    - Go 拥有指针。指针保存了值的内存地址。

    - 类型 *T 是指向 T 类型值的指针。其零值为 nil。

    - var p *int 声明一个指针类型的p



+ 切片slice
    - 每个数组的大小都是固定的。而切片则为数组元素提供动态大小的、灵活的视角。
    - 类型 []T 表示一个元素类型为 T 的切片
    - 切片通过两个下标来界定，即一个上界和一个下界，二者以冒号分隔：a[low : high]
    - 切片下界的默认值为 0，上界则是该切片的长度。
    - 切片 a 的长度和容量可通过表达式 len(a) 和 cap(a) 来获取。
    - 切片也是从下标0开始，切出的数据遵从：包括第一个元素，但排除最后一个元素。
    - 切片并不存储任何数据，它只是描述了底层数组中的一段。
    - 更改切片的元素会修改其底层数组中对应的元素。
    - 与它共享底层数组的切片都会观测到这些修改。
    - 切片的零值是 nil,nil 切片的长度和容量为 0 且没有底层数组
    - 切片可以用内建函数 make 来创建，创建动态数组,make可以接受三个参数
        + b := make([]int,5) // len(b)=5, cap(b)=5 长度为5，容量为5的切片
        + b := make([]int,0,5) // len(b)=0, cap(b)=5 长度为0，容量为5的切片
    - 切片可包含任何类型，甚至包括其它的切片。
    - 为切片追加新的元素是种常用的操作，Go了内建的 append 函数。
        + func append(s []T, vs ...T) []T，append 的第一个参数 s 是一个元素类型为 T 的切片，其余类型为 T 的值将会追加到该切片的末尾。
        + append 返回值是一个包含原切片所有元素加上新添加元素的切片。
        + 底层数组太小，不足以容纳所有给定的值时，它就会分配一个更大的数组
    - 切片中取元素可使用 for 循环的 range 形式可遍历切片或映射。
        + for 循环遍历切片时，每次迭代都会返回两个值。第一个值为当前元素的下标，第二个值为该下标所对应元素的一份副本。
        + 如果不需要取下标，则可使用 _ 下划线直接过滤
        + 若只需要索引，忽略第二个变量即可。
    
```

	primeSlice := [6]int{2, 3, 5, 7, 11, 13}

	var sslice []int = primeSlice[1:4]
	var slicestart []int = primeSlice[:4]
	var sliceend []int = primeSlice[1:]
    // [3,5,7]
	fmt.Println(sslice)
	fmt.Println(slicestart)
	fmt.Println(sliceend)

    // 切片为nil 的情况
	var snil []int
	fmt.Println(s, len(s), cap(snil))
	if snil == nil {
		fmt.Println("nil!")
	}
    // 创建一个可变长度的切片使用内置函数make
    amake := make([]int, 5)
	printSlice("amake", amake)
    // 给切片添加元素

    var sappend []int
	
	printSlice(sappend)

	// 添加一个空切片
	sappend = append(sappend, 0)
	printSlice(sappend)

	// 这个切片会按需增长
	sappend = append(sappend, 1)
	printSlice(sappend)

	// 可以一次性添加多个元素
	sappend = append(sappend, 2, 3, 4)
	printSlice(sappend)

    //  循环切片中的值 ，如果不需要取下标，则可使用 _ 下划线直接过滤
	for i, v := range sappend {
		fmt.Printf("2**%d = %d\n", i, v)
	}

```


+ Go的函数
    - Go是编译型语言，所以函数编写的顺序是无关紧要的；鉴于可读性的需求，最好把 main() 函数写在文件的前面，其他函数按照一定逻辑顺序进行编写
    - 编写多个函数的主要目的是将一个需要很多行代码的复杂问题分解为一系列简单的任务（那就是函数）来解决。同一个函数可以被调用多次
    - 函数的类型
        + 普通的带有名字的函数
        + 匿名函数或者lambda函数
        + 方法，方法就是一类带特殊的 接收者 参数的函数。方法接收者在它自己的参数列表内，位于 func 关键字和方法名之间。
    - 函数也可以以声明的方式被使用，作为一个函数类型
    - 函数的最后一个参数是采用 ...type 的形式，那么这个函数就可以处理一个变长的参数，这个长度可以为 0，这样的函数称为变参函数。
        + func myFunc(a, b, arg ...int) {}
    - 函数实现斐波那契数列
    


```

// 实现一个加法函数
// 函数的定义
/*
	1.必须以func 开头，然后是函数名（传入值类型）返回类型{
		函数体，必须有返回值
	}
 */

func add(a int, b int) int {
    return a+b
}

// 以声明的方式被使用，作为一个函数类型,此时不需要函数体，函数可以直接赋值给变量

type addPlus func(int, int) int

addNum := addPlus


// 实现一个方法


type VertexFunc struct {
	Xv, Yv float64
}

func (vv VertexFunc) Abs() float64 {
	return math.Sqrt(vv.Xv*vv.Xv + vv.Yv*vv.Yv)
}

vv := Vertex{3, 4}
fmt.Println(vv.Abs())

// 函数之变长参数

	xargs := min(1, 3, 2, 0)
	fmt.Printf("The minimum is: %d\n", xargs)
	slice := []int{7,9,3,5,1}
	xargs = min(slice...)
	fmt.Printf("The minimum in the slice is: %d", xargs)


    func min(s ...int) int {
        if len(s)==0 {
            return 0
        }
        min := s[0]
        for _, v := range s {
            if v < min {
                min = v
            }
        }
        return min
    }


// 递归实现斐波那契数列


    var i int
    for i = 0; i < 10; i++ {
       fmt.Printf("%d\t", fibonacci(i))
    }

    func fibonacci(n int) int {
        if n < 2 {
            return n
        }
        return fibonacci(n-2) + fibonacci(n-1)
    }



```
+ 类型转换
    - 类型转换用于将一种数据类型的变量转换为另外一种类型的变量。
    - 如果计算过程中，没有转换类型，Go语言会报错，必须是同类型的才可以相互计算、赋值等

```
    var sumType int = 17
	var count int = 5
	var mean float32

	mean = float32(sumType)/float32(count)
	fmt.Printf("mean 的值为: %f\n",mean)

```


### 本教程系列代码

+ [本教程例子代码](https://github.com/chuhemiao/go-basic-example)