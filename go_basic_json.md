# Golang 基础之json

### 什么是JSON

+ JSON 是一种轻量级的数据交换格式，常用作前后端数据交换，Go 在 encoding/json 包中提供了对 JSON 的支持。
+ 好用的第三方JSON包，gjson、go-simplejson


### 序列化

+ 把 Go struct 序列化成 JSON 对象，Go 提供了 Marshal 方法，语法如下：

```
    func Marshal(v interface{}) ([]byte, error)
```

+ 并不是所有的类型都能进行序列化
    - JSON object key 只支持 string
    - Channel、complex、function 等 type 无法进行序列化
    - 数据中如果存在循环引用，则不能进行序列化，因为序列化时会进行递归
    - Pointer 序列化之后是其指向的值或者是 nil
    - 首字母大写的 field 才可以被序列化，一般使用Struct Tag 模式

### 反序列化

+ in为传入的json，out要输出的json
+ json.Unmarshal(in, &out)

```
	b := []byte(`{"Name":"Wednesday","Age":6,"Parents":["Gomez","Morticia"]}`)
	var m FamilyMember
	err := json.Unmarshal(b, &m)
	if err != nil{
		panic("反序列化失败")
	}
	fmt.Printf("%#v\n", m)

```

### 安装gjson  

+ go get github.com/tidwall/gjson



```
    const jsonExample = `{"name":{"first":"Tom","last":"Anderson"},"age":37,"children":["Sara","Alex","Jack"],"fav.movie":"Deer Hunter","friends":[{"first":"Dale","last":"Murphy","age":44},{"first":"Roger","last":"Craig","age":68},{"first":"Jane","last":"Murphy","age":47}]}`


    // 判断该json是否合法
	if !gjson.Valid(jsonExample) {
		log.Fatalf("%s", "invalid json")
	}
	// 获取Json中的age  匹配得到字段
	age := gjson.Get(jsonExample, `age`).Int()
	fmt.Printf("%T, %+v\n", age, age)
	// 获取lastname
	lastname := gjson.Get(jsonExample, `name.last`).String()
	fmt.Printf("%T, %+v\n", lastname, lastname)
	// 获取children数组
	for _, v := range gjson.Get(jsonExample, `children`).Array() {
		fmt.Printf("%q ", v.String())
	}
	fmt.Println()
	// 获取第二个孩子
	fmt.Printf("%q\n", gjson.Get(jsonExample, `children.1`).String())
	fmt.Printf("%q\n", gjson.Get(jsonExample, `children|1`).String())
	// 通配符获取第三个孩子
	fmt.Printf("%q\n", gjson.Get(jsonExample, `child*.2`).String())
	// 反转数组函数
	fmt.Printf("%q\n", gjson.Get(jsonExample, `children|@reverse`).Array())
	// 自定义函数 - 全转大写
	gjson.AddModifier("case", func(json, arg string) string {
		if arg == "upper" {
			return strings.ToUpper(json)
		}
		return json
	})
	fmt.Printf("%+v\n", gjson.Get(jsonExample, `children|@case:upper`).Array())
	// 直接解析为map
	jsonMap := gjson.Parse(jsonExample).Map()
	fmt.Printf("%+v\n", jsonMap)
	for _, v := range jsonMap {
		fmt.Printf("%T, %+v\n", v, v)
	}


```



### 推荐阅读

+ [理解 Go 中的 JSON](https://sanyuesha.com/2018/05/07/go-json/)