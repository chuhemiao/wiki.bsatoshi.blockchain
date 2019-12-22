# Go语言系列课程之reflect

### 反射

+ 在运行时反射是程序检查其所拥有的结构，尤其是类型的一种能力；这是元编程的一种形式。它同时也是造成混淆的重要来源。

### 特性

+ 反射可以大大提高程序的灵活性，使得interface{}有更大的发挥余地
+ 反射使用 TypeOf 和 ValueOf 函数从接口中获取目标对象信息
+ 反射会将匿名字段作为独立字段（匿名字段本质）
+ 想要利用反射修改对象状态，前提是 interface.data 是 settable,即 pointer-interface
+ 通过反射可以“动态”调用方法

### 使用

+ TypeOf 和 ValueOf 函数从接口中获取目标对象信息
+ Field过滤字段
+ Method调用反射方法


```

    type User struct {
        Id int
        Name string
        Age int
    }

    

    func main() {

        u := User{1, "ok", 18}
        Info(u)
        // 通过反射方法的调用
        uname := User{1, "ok", 18}
        v := reflect.ValueOf(uname)
        mv := v.MethodByName("HelloName")

        args := []reflect.Value{reflect.ValueOf("chuhemiao")}
        mv.Call(args)

    }

    // 通过反射调用方法
    func (u User) HelloName(name string) {
        fmt.Println("Hello", name, ", my name is", u.Name)
    }

    // 传递一个空接口
    func Info(o interface{}) {
	t := reflect.TypeOf(o)
	fmt.Println("Type:", t.Name())

	v := reflect.ValueOf(o)
	fmt.Println("Fields:", v)

	// 获取方法字段
	for i := 0; i < t.NumField(); i++ {
		f := t.Field(i)
		val := v.Field(i).Interface()
		fmt.Println("%6s: %v = %v\n", f.Name, f.Type, val)

	}

	// 获取方法
	for i := 0; i < t.NumMethod(); i++ {
		m := t.Method(i)
		fmt.Println("%s: %v\n", m.Name, m.Type)
	}


}


```