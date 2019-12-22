# Go语言基础常用包

### 基础包之文本操作


+ strings — 字符串操作
    - 字符串长度；
    - 求子串；
    - 是否存在某个字符或子串；
    - 子串出现的次数（字符串匹配）；
    - 字符串分割（切分）为[]string；
    - 字符串是否有某个前缀或后缀；
    - 字符或子串在字符串中首次出现的位置或最后一次出现的位置；
    - 通过某个字符串将[]string连接起来；
    - 字符串重复几次；
    - 字符串中子串替换；
    - 大小写转换；
    - Trim操作；

```

    str := "ssssppllssdsdljjklljsd"
	// 字符串长度
	l1:=len([]rune(str))
	l2:=bytes.Count([]byte(str),nil)-1
	l3:=strings.Count(str,"")-1
	l4:=utf8.RuneCountInString(str)
	fmt.Println(l1)
	fmt.Println(l2)
	fmt.Println(l3)
	fmt.Println(l4)

	// 字符串中是否存在某个字符  返回值 true或false
	fmt.Println(strings.ContainsAny(str, "i"))
	// 字符串出现的次数
	fmt.Println(strings.Count(str, "ss"))
	// 字符串分割
	fmt.Printf("%q\n", strings.Split("a,b,c", ","))

	fmt.Printf("%q\n", strings.SplitN("foo,bar,baz", ",", 2))
	// 字符串以某某开头
	sstr := strings.HasPrefix(str,"ss")
	fmt.Println(sstr)
	// 字符串以某某结尾
	send := strings.HasSuffix(str,"dddd")
	fmt.Println(send)


```

### 本教程系列代码

+ [示例代码](https://github.com/chuhemiao/go-basic-example)
