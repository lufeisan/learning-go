我们接着学习 go语言的一些基础知识

[流程控制](#流程控制)

[函数](#函数)

[结构体](#结构体)

[方法](#方法)

[面向对象概述](#面向对象概述)

[面向对象封装](#面向对象封装)

[面向对象继承](#面向对象继承)

[面向对象多态](#面向对象多态)

### 流程控制

##### 一、流程控制是什么

程序的执行顺序

##### 二、条件控制：if eles else if

```go  
if true {
       fmt.Println("true")
   } else if false {
       fmt.Println("false")
   } else {
       fmt.Println("other")
   }
```

> 左大括号放在同一行

```go 
//if的另一种使用方法，判断类型
//if value,ok := courser["go"];ok {
//    fmt.Println(value)
//}
```

> 打开某一个文件不存在或者由于权限的问题无法操作，这种使用方式，在go语言普遍存在，我们也推荐以这种方式来书写。

```go 
if fileHandle,err := os.Open("hello.txt");err != nil {
        //null
        fmt.Println(fileHandle)
        fmt.Println(err.Error())
    } else {
        fmt.Println("获取文件成功")
    }
```


##### 三、选择控制 switch case select  

```go 
switch switchVariables := 100; {
    case switchVariables >90:
        fmt.Println("成绩优秀")
        fallthrough
    case switchVariables>80:
        fmt.Println("成绩良好")
        fallthrough
    case switchVariables >=60:
        fmt.Println("成绩合格")
    default:
        fmt.Println("成绩不及格")
    }
```

```go
//if eles
var switchVariables int = 100
//if switchVariables > 100 {
//
//} else {
//
//}
```

```go  
//使用switch模拟if else
switch {
    case switchVariables > 90:
        fmt.Println("成绩优秀")
    case switchVariables > 80:
        fmt.Println("成绩良好")
    case switchVariables >=60:
        fmt.Println("成绩合格")
    default:
        fmt.Println("成绩不及格")
    }
```

```go 
//switch判断类型，类型断言(后面还会详细讲解) 
switch typeVariables := interfaceVariables.(type) {
case float32:
    fmt.Println("float32",typeVariables)
case float64:
    fmt.Println("float64",typeVariables)
case int8:
    fmt.Println("int8",typeVariables)
default:
    fmt.Println("未知的类型",typeVariables)
}

//类型断言，这种方式在go语言中称为类型断言
var category = "笔记本"
switch category  {
//一个case中判断多个满足条件
case "电脑", "笔记本", "手机":
    fmt.Println("数码产品")
case "T恤", "背心":
    fmt.Println("服饰产品")
case "饼干", "巧克力", "苏打":
    fmt.Println("零食产品")
default:
    fmt.Println("其他产品")
}
```

##### 四、循环控制

###### for

```go 
- //循环控制 for e
  //for 初始化条件;循环的条件;变化的条件 {
  //
  //}
    
    
- for i :=0;i<10;i++ {
        fmt.Println(i)
    }
- initVariables := 1
    for initVariables < 10 {
        fmt.Print(initVariables)
        initVariables++
    }
- 条件语句是可以被省略的，如 i:=0; ; i++ 或 for { } 或 for ;; { }（;; 会在使用 gofmt 时被移除）：这些循环的本质就是无限循环。最后一个形式也可以被改写为 for true { }，但一般情况下都会直接写 for { }//死循环
    //for {
    //    fmt.Println(1)
    //}
```

###### for…range…

```go 
  var stringVariables = "慕课，go语言体系课"
    for key,value := range stringVariables {
        //fmt.Println(key,value)
        fmt.Printf("key=%d,value=%c,类型=%T\n",key,value,value)
    }
 //只打印key,不打印value
    for key := range stringVariables {
        fmt.Printf("key=%d\n",key)
    }
// value遍历数据中对应索引的值拷贝，所以对它所做的任何修改都不会影响到数据中原有的值（但如果value 为指针，则会产生指针的拷贝，就会修改数据的原值）。一个字符串是 Unicode 编码的字符（或称之为 rune）集合，for...rage可以用来遍历字符串：每个 rune 字符和索引在 for-range 循环中是一一对应的。它能够自动根据 UTF-8 规则识别 Unicode 编码的字符。
```

##### 五、跳转控制

###### goto

跳转到某个标签

```go 
func gotoFunc() {
    variables := 0
GOTO:
    fmt.Println(variables)
    variables++
    goto GOTO
}
```

###### break
```go 
 //break退出当前循环
    for outerIndex :=0;outerIndex<10;outerIndex ++ {
        for innerIndex :=0 ;innerIndex<6;innerIndex ++ {
            fmt.Println(outerIndex,innerIndex)
            break
        }
    }
 //break+退出标签
FORBREAK:    for outerIndex :=0;outerIndex<10;outerIndex ++ {
                for innerIndex :=0 ;innerIndex<6;innerIndex ++ {
                    fmt.Println(outerIndex,innerIndex)
                    break FORBREAK
                }
            }
```

###### continue

```go 
//continue 忽略当前循环剩余的代码
        for outerIndex :=0;outerIndex<3;outerIndex ++ {
            for innerIndex :=0 ;innerIndex<2;innerIndex ++ {
                fmt.Println(outerIndex,innerIndex)
                continue
                fmt.Println("这里是内层循环剩余的代码")
            }
        }

 //continue+标签，忽略当前循环剩余的代码，跳转转到某个标签
FORCONTINUE:for outerIndex :=0;outerIndex<3;outerIndex ++ {
                for innerIndex :=0 ;innerIndex<2;innerIndex ++ {
                    fmt.Println(outerIndex,innerIndex)
                    continue FORCONTINUE
                    fmt.Println("这里是内层循环剩余的代码")
                }
            } 
```

___

### 函数

##### 一、函数的概述

函数是什么，在其他编程语言都有函数 为了完成某个具体功能封装起来的功能的集合

##### 二、函数的定义

```go 
//函数定义格式
func 函数名(参数) (返回值) {
    //函数体
    return xxx
}

func funcName(input1 type1, input2 type2) (output1 type1, output2 type2) {
    // 这里是处理逻辑代码
    // 返回多个值
    return value1, value2
 }
```

> 1.函数的定义及左大括号放在同一行
> 
> 2.多返回值
> 
> 3.忽略函数返回值 `_`


##### 三、多返回实例演示

> 实例: 定义一个函数[actionVariables]，返回2个返回值，加和，相减，测试多返回值

```go
func actionVariables(var1 int,var2 int)(int,int) {

    return var1 + var2,var1-var2
}
```

函数的参数如果一致，则可在最后一个参数中书写类型

函数返回值名称可指定，可忽略

指定函数返回值名称时，可直接return


> 如果2个参数或多个参数的类型一致，可把类型写在最后

```go 
func actionVariables(var1,var2 int)(int,int) {
    return var1 + var2,var1-var2
}
```

> 函数调用

```go  
var sum int
var minus int

sum,minus = actionVariables(1,2)
fmt.Println(sum,minus)
```

> 实例: 定义一个函数[actionVariables2]，测试函数多返回值时，设置有名与无名

```go 
func actionVariables2(var1,var2 int) (sum int,minus int) {
    sum = var1 + var2
    minus = var1 - var2
    //return sum,minus
    return
}
```

> 函数调用

```go  
sum,minus = actionVariables2(1,2)
fmt.Println(sum,minus)
```

##### 三、不定参数

> 可变参数…interface{}做为函数参数的使用,通过分析go系统自带的fmt.println讲解可变参数

```go 
// 1. 定义函数[actionVariables3]，可变参数，测试

func actionVariables3(args ...interface{}) {
    for _,value := range args {
        fmt.Println(key,value)
    }
}

// 2. 调用

actionVariables3(1,"我是小杨",3.14,true)
```

> 可变参数，类似于切片，go语言里有很多，可变参数是go语言的特性

```go 
//可变参数...interface{}做为函数参数的类型判断
//1.在函数[actionVariables3],增加功能，判断可变参数的类型

func actionVariables3(args ...interface{}) {
    for _,value := range args {
        switch value.(type) {
        case int:
            fmt.Println(value,"int")
        case string:
            fmt.Println(value,"string")
        case float64:
            fmt.Println(value,"float64")
        case bool:
            fmt.Println(value,"bool")
        default:
            fmt.Println(value,"unknow")
        }
    }
}

//2.调用
actionVariables3(1,"我是小杨",3.14,true)
```

##### 四、函数的作用域

函数体内部定义的变量称为局部变量，作用域只在函数体当中有效，函数调用完成之后，为这些变量定义的内存空间就会被释放

```go  
//1.定义函数[testScope],分析函数的作用域

func testScope(args int) {
    args = 100
    fmt.Println(args)
}

//2.调用

var args int
testScope(args)
fmt.Println(args)
```

> `_` 在函数中的使用，用于忽略返回值

```go  
sum, _ = actionVariables(3,5)
```

##### 五、递归函数

什么是递归函数 在一个循环体当中执行，必须有一个条件可以在满足某个条件时终止当前的循环，否则为死循环

> 递归函数举例: 
> 一般以斐波那契数列举例

斐波那契数列 特点 1 2 3 ...

```go 
/*
    位置        值
    1        1
    2        1
    3        2
    4        3
    ..        ..
    n        func(n-1) + func(n-2)
    */
```

传递一个位置，返回当前位置的值

```go
- 1.定义函数[fibonaci]实现

func fibonaci(index int64) int64 {
    if index == 1 || index == 2 {
        return 1
    } else {
        return fibonaci(index-1) + fibonaci(index-2)
    }
}

- 2.调用

//第20位置对应的值
fmt.Println(fibonaci(2))
```

##### 六、匿名函数与闭包

什么是匿名函数 没有名字的函数称为匿名函数

`应用场景`

当一个函数仅使用一次的时候，可定义为匿名函数

###### 匿名函数的使用方式

> 使用方式一:  定义一个匿名函数实现两个数的加和，定义的时候并调用

```go 
sumVariables := func(var1,var2 int) int {
        return var1 + var2
    }(1,2)
    
fmt.Println(sumVariables)
```

> 使用方式二: 定义一个变量，将匿名函数赋值给该变量，则变量具体匿名函数的功能

```go  
- //将一个匿名函数赋值给一个变量，这个变量存储的是这个匿名的地址

func1 := func(var1,var2 int) int{
    return var1 - var2
}
fmt.Printf("func1调用的值=%d,func1=%p\n",func1(1,2),&func1)

// func1存储的是函数的地址
// 输出 func1调用的值=-1,func1=0xc000130018
```

`匿名函数是不能独立存在的`

```go
//报错
func(var1,var2 int)int{return 1} 

//或者我们直接调用 
func(var1,var2 int)int{return 1}(1,2)
```


###### 闭包

首先他是一个函数，是函数与函数外部数据的引用（在函数体内部引用到了函数体外部的数据）

> 实例演示 以一个例子来定义一个闭包，该闭包函数每调用一次，让值加1

```go  
func clousure() func(int64) int64 {
     var step int64 = 0
     return func(_step int64) int64 {
          //函数内部引用函数外部的数据
       step +=  _step
       return step
     }
}

func2 := clousure()

fmt.Println(func2(1))
fmt.Println(func2(2))
fmt.Println(func2(3))
```

`分析执行结果`

闭包函数每次调用，均保留上次的执行结果，并参与下一次调用时候的运算

> 同一个包中，函数不支持重载即不能有相同的函数名

##### 七、defer

在我们实际的开发过程中，我们经常去连接一个远程的数据库，或者说连接本地的数据库，在我们连接数据库之后呢，就会返回连接的句柄，这种情况我们就占用了这个资源，假如我们程序执行的时候还没来得及关键关闭这些资源的时候，我们的程序就崩溃了，但是对这个资源的占用还一种存在着，我们如何解决，以此我们引出defer关键字
`defer` 关键字允许我们将业务逻辑延迟到函数返回之前才执行某个语句或函数
关键字` defer` 的用法类似于面向对象编程语言` Java` 和` C# `的` finally `语句块，它一般用于释放某些已分配的资源。

`使用场景`

常用于资源的回收

> 定义一个函数来演示defer的使用，该功能用于模拟打开一个文件

```go 
func deferAction() {
    handle,err := os.Open("hello.txt")
    //这里是一大堆的文件操作程序...
    //fmt.Println(5/0)
    err = err
    handle.close()
}
```

由于程序的错误，导致后面的代码无法执行，导致打开的资源一直被占用着，则其他程序无法使用

> 对代码优化

```go 
func deferAction() {
    handle,err := os.Open("hello.txt")
    defer handle.Close()

    //这里是一大堆的文件操作程序...
    //fmt.Println(5/0)
    err = err 
}
```

> 先进后出原则

```go
func deferAction2(var1,var2 int) int {
     defer fmt.Println(var1)     //1
     defer fmt.Println(var2)    //2

     sum := var1 + var2
     defer fmt.Println(sum)    //3

     return sum
} 

//defer
deferAction2(1,2)
```

##### 八、函数的高级用法

> 函数做为一种类型，在函数参数中使用

```go 
func actionVariables4(var1,var2 int) (sum int,minus int) {
    sum = var1 + var2
    minus = var1 - var2
    //return sum,minus
    return
}

//第一个参数为函数类型
func funcAsArgs(funcName func(int,int)(int,int),var1,var2 int)(int,int) {
    return funcName(var1,var2)
}


//函数可以做为一种类型
sum,minus = funcAsArgs(actionVariables4,1,2)
fmt.Println(sum,minus)
```

go语言官方推荐函数返回值命名

> 函数做为值在函数参数中使用

定义一个切片，判断哪个是偶数，哪个是奇数
以此，我们引出 函数做为值在函数参数中使用的例子
定义2个函数判断是否为奇数，偶数，来演示如何将函数做为值来使用

```go 
type Boolean func(int)bool

//是否为偶数
func isEven(integer int) bool {
    if integer % 2 == 0 {
        return true
    }

    return false
}

//是否为奇数
func isOdd(integer int)bool {
    if integer % 2 == 0 {
        return false
    }

    return true
}

func judgeSlice(slice []int,boolean Boolean) (result []int) {

    for _,value := range slice {
        if boolean(value) {
            result = append(result,value)
        }
    }

    return result
}


slice := []int{1,2,3,4,5,6,7}

evenSlice := judgeSlice(slice,isEven)
oddSlice := judgeSlice(slice,isOdd)
fmt.Println("偶数：",evenSlice)
fmt.Println("奇数：",oddSlice)
```

##### 九、init()/main()，go语言保留函数

> go语言编译器会自动调用
> 
> 在定义的时候不能有任何的参数与返回值
> 
> init()一般存在于所有的包中

> 在一个包中可以有多个init()函数
> 
> 但是我们建议只写一个init()函数
> 
> 一般用于初始化工具，比如连接数据库
> 
> main()只能在main包中使用

`执行顺序`

> -当前包引入其他包，优先调用其他包的全局变量，init()函数（如果其他包也调用 了init()函数，则继续向上调用），再调用本包的init()函数
> 
> -全局变量
> 
> -init()先执行
> 
> -main()后执行
> 
> -执行顺序:全局变量-> init() -> main()

##### 十、值类型、引用类型做为参数调用

> 1.数组，值类型
> 
> 2.切片/map，引用类型
> 
> 3.以值类型传递参数，是对应值的拷贝，不会改变实参的值
> 
> 4.以引用类型传递参数，传递的是对应的地址，这个地址占用的空间是轻量级的，对内存占用是极少的，可以通过指针传递的方式，传递一个何种较大的数据，会改变实参的值

___

### 结构体

##### 一、结构体概述

结构体是值类型，用于自定义数据类型与实现面向对象

##### 二、作用与应用场景

`作用`

用于定义自定义类型

`应用场景`

自定义数据类型
面向对象

##### 三、定义自定义类型与使用

###### 定义自定义类型的方式1

```go 
type structVariables struct{}


type integer int
var intVariables int
var integerVariables integer
intVariables = integerVariables

//基于一种类型去创建另一种类型，被认为是两种不同的类型
fmt.Println(intVariables,integerVariables)

//无法相互赋值,如何赋值？类型转换
intVariables = int(integerVariables)
```

###### 定义自定义类型的方式2 结构体

> 结构体字段可以是任何类型，以及结构体本身，函数，接口等等
> 
> 结构体类型是某一类具体事物的抽象
> 
> 以中秋节的月饼举例，月饼的模板，做出月饼
> 
> 通过组合一定数据的字段来完成

```go  
type 结构体名 struct {
    field1 type1
    field2 type2
    ....
} 
```

**结构体的使用方式1**

```go 
type userinfo struct {
    name string
    age int
    height float32
    eduschool string
    hobby []string
    moreinfo map[string]interface{}
}

//使用
var bobo userinfo
bobo.name = "小杨"
bobo.age = 18
bobo.height = 181
bobo.eduschool = "庞各庄大学"
bobo.hobby = []string{"coding","运动","旅行"}
bobo.moreinfo = map[string]interface{}{
    "work":"福报厂",
    "duty":"产品狗",
}
```

**结构体的使用方式2 :=简短声明来实现一个结构变量**

第二种形式没有字段名，只声明对应的值，每个值也可以分别占一行，不过习惯上这种形式会写在一行里，结尾不需要逗号。这种形式下，值的顺序很重要，必须要和结构声明中字段的顺序一致，同时在我们不指定字段名称的时候，结构体当中的所有字段必须全部赋值

```go
// 1.声明变量
// 2.初始化
var liuge = userinfo{
    name:      "",
    age:       0,
    height:    0,
    eduschool: "",
    hobby:     nil,
    moreinfo:  nil,
}

huge := userinfo{
        eduschool: "庞各庄大学",
        hobby:     []string{"拍电影","唱歌","旅行"},
        moreinfo: map[string]interface{}{
            "role":"演员",
            "earnmoney":300000,
        },
        name:      "小杨",
        age:       28,
        height:    188,
    }
```

> 不指定字段名的时候，需要严格的按照定义结构体时候的顺序赋值
> 
> 指定字段名的时候，可以不按定义结构体时候的顺序赋值
> 
> 对结构体赋值时，如果各个字段不在一行，最后一个字段必须添加逗号
> 
> 对结构体赋值时，如果各个字段在同一行，则最后的一个字段可以不添加逗 号

```go  
xiaoge := userinfo{"小哥",12,120,"小学",[]string{"学习","玩","打游戏"}, map[string]interface{}{"年级":"六年级"}}
fmt.Printf("xiaoge=%v\n",xiaoge)
```

对结构体赋值时，如果各个字段在同一行，则最后的一个字段可以不添加逗号

**结构体的使用方式3 new**

使用`new` `new(int)`,`new(string)`,`new(T)` 返回结构体指针

```go 
//var t *T
//t = new(T)
var xiaoming *userinfo
xiaoming = new(userinfo)
(*xiaoming).name = "小明"
(*xiaoming).age = 12
(*xiaoming).eduschool = "北京小学"
//xiaoming->(*xiaoming) go语言编译器自动转换
xiaoming.hobby = []string{"学习","玩","打游戏"}
fmt.Println(xiaoming)
```

**结构体的使用方式4 &地址符，同样是返回的结构体指针**

```go 
var xiaohong *userinfo = &userinfo{
    "小红",12,120,"小学",[]string{"学习","玩","打游戏"}, map[string]interface{}{"年级":"五年级"},
}
```

##### 四、结构体注意事项

> 不指定字段名的时候，需要严格的按照定义结构体时候的顺序赋值
> 
> 1.结构体是值类型
> 
> 2.结构体之间是否可以相互转换？可以转换，前提条件：具有相同的字段（个数，类型，名称)
> 
> 3.结构体可以做为另一个结构体字段的类型
> 
> 4.结构体变量赋值，各字段不在同一行时，最后一个字段必须加逗号
> 
> 5.结构体变量赋值，各字段在同一行时，最后一个字段的逗号可加，可不加

```go 
//1.结构体是值类型
    user1 := userinfo{
        name:      "user1",
        age:       0,
        height:    0,
        eduschool: "",
        hobby:     nil,
        moreinfo:  nil,
    }
    user2 := user1
    fmt.Printf("user1 = %p,user2 = %p\n",&user1,&user2)


//2.结构体之间是否可以相互转换？可以转换，前提条件：具有相同的字段（个数，类型，名称)
user3 := userinfo{
    name:      "user3",
    age:       0,
    height:    0,
    eduschool: "",
    hobby:     nil,
    moreinfo:  nil,
}

user4 := peopleinfo{
    name:      "user4",
    age:       0,
    height:    0,
    eduschool: "",
    hobby:     nil,
    moreinfo:  nil,
    //pmoreinfo:nil,
}

user3 = userinfo(user4)
//user3 = user4
fmt.Println(user3)
```

##### 五、自定义类型做为结构体字段的类型与最佳实践

###### 结构体可以做为另一个结构体字段的类型

> 后台管理系统中，不同权限分配的问题

```go 
//后台管理系统中，权限问题，这里涉及了角色，超级管理员，管理员，普通用户
type role struct {
    user userinfo 
    authorization Integer  //1=超级管理员，2=管理员，3=普通用户
}


superadmin := role{
    user:          userinfo{
        name:      "超级管理员",
        age:       0,
        height:    0,
        eduschool: "",
        hobby:     nil,
        moreinfo:  nil,
    },
    authorization: 1,
}
admin := role{
    user:          userinfo{
        name:      "管理员",
        age:       0,
        height:    0,
        eduschool: "",
        hobby:     nil,
        moreinfo:  nil,
    },
    authorization: 2,
}
fmt.Println(superadmin,admin)
```

##### 六、结构体在内存中的布局

结构体在内存中的布局是连续的存储空间

```go 
type Rectange struct {
	x int
	y int
	z int
}

r := Rectange{
	x: 1,
	y: 11,
	z: 11,
}

fmt.Printf("x=%p,y=%p,z=%p\n",&r.x,&r.y,&r.z)

// 输出
x=0xc000138000,y=0xc000138008,z=0xc000138010
```

___

### 方法

##### 一、方法的概述

方法是什么 实际上也是函数，声明时，在关键字func 和函数名之间增加了一个参数,这个参数被称作接收者,将函数与接收者的类型绑在一起。如果一个函数有接收者，这个函数就被称为方法。

> Go 语言里有两种类型的接收者：值接收者，指针接收者

##### 二、方法作用

方法有哪些作用呢?

给用户定义的类型添加新的行为

##### 三、方法定义与使用

我们一起来看一看方法的声明定义方式

定义格式

```go 
func (var vartype)funcname(参数列表) (返回值列表) {
       函数体
   }
```

##### 方法演示

为我们自定义的类型增加方法
```go 
- 1.定义结构体
type miniaction struct {
    name string //接口名称 热销商品，某一个分类下的商品列表
    router string //路由地址 https://api.imooc.com/hotproduct
    action string //路由对应的方法名 func hotproduct() {}
}
- 2.1.为结构体增加方法
func (mini miniaction)getMiniInfo() {
    fmt.Printf("mini.name=%s,mini.router=%s,mini.action=%s\n",mini.name,mini.router,mini.action)
}

- 2.2.为结构体增加方法
func (this *miniaction)miniInfo()  {
    fmt.Printf("mini.name=%s,mini.router=%s,mini.action=%s\n",this.name,this.router,this.action)
}
- 3.1.实例化结构体

mini1 := miniaction{
        name:   "获取商品列表",
        router: "productList",
        action: "productList()",
    }
    //调用
//接收者有两种，一种是值类型，一种是指针类型
    //接收者是值类型的时候，调用者可以是值类型，也可以是引用类型
    mini1.getMiniInfo()
- 3.2.实例化结构体

mini2 := &miniaction{
        name:   "获取分类下的商品列表",
        router: "productListByCategory",
        action: "productListByCategory()",
    }
mini2.getMiniInfo()
- //接收者是一个指针类型,调用者可以是值类型，也可以指针类型
    mini2.miniInfo()
    (*mini2).miniInfo()
    mini1.miniInfo()
```

##### 四、方法注意事项

> 1.接收者是值类型的时候，调用者可以是值类型，也可以是引用类型
> 
> 2.接收者是一个指针类型,调用者可以是值类型，也可以指针类型
> 
> 3.定义的方法只能通过指定的类型来调用，不能像函数一样来调用
> 
> 4.方法的接收者对应的变量名，习惯使用this,self

```go 
//比如传统编程语言当中的Person类
class Person{
    public name
    function info(){
        this.name
    }
}

p = new Person()
p.info()
```

> 自定义类型也可以做为方法的接收者

```go 
- 1.自定义类型
type float float32

- 2.为自定义类型定义方法

func (radius float)getCircleAround() float {
    return radius*3.14*2
}

- 3.定义一个自定义的类型并调用方法
var radius float = 2
fmt.Println(radius.getCircleAround())
```

`接收者类型限定`
> 接收者不能是接口,因为接口是一类事物的抽象，而方法是某个具体事物的实现，所以不能把一个接口类型的变量做为接收者

##### 五、方法和函数的区别

> 值类型，引用类型都可做为参数使用
> 
> 做为参数时遵循函数当中的值传递与引用传递规则
>
> 如果想要方法改变接收者的数据，就在接收者的指针类型上定义该方法。否则，就在普通的值类型上定义方法。
> 
> 方法调用:调用者.方法名（参数）
> 
> 函数调用：函数名（参数列表）
> 
> 首字母大小写，遵循包的规则

___

### 面向对象概述

##### 一、什么是面向对象

###### 权威的定义

面向对象`(Object Oriented,OO)`是软件开发方法。

泛指现实中一切事物，每种事物都具备自己的属性和行为。面向对象思想就是在计算机程序设计过程中，参照现实中事物，将事物的属性特征、行为特征抽象出来，描述成计算 机事件的设计思想。

###### 通俗的定义

月饼的比喻：

几个概念: `类` `对象` `属性` `方法`

月饼有各种各样的形状（模板，软件工程当中的”类”），中秋节商场里买月饼，商场里有各个不同形状的月饼(软件工程当中的”对象”),月饼的重量，颜色，形状，尺寸等这些类比软件工程当中的”属性”,月饼的生产方法，将面粉放到不同模板当中就可做出各种不同形状的月饼(软件工程当中的”方法”)

###### 二、面向对象在实际工作中的作用

> 1.有利于团队合作,分工、分模块开发
> 
> 2.提高工作效率

###### 三、面向对象的几个概念

###### 1. 类

> 定义:具有同种属性的对象称为类，是个抽象的概念。
> 
> 它定义了所包含的全体对象的公共特征和功能。
> 
> 举例：“人”就是一类，比如小杨、coderyang 等等这些都是对象，类就相当于一个模具，对象就是类的一个实例化，小杨就是人的一个实例化！我们在做程序的时候，经常要将一个变量实例化，就是这个原理！
>
> 一般情况下，在调用类时不直接调用类，而是通过类的对象来操作，比如我们问小杨的时候，不会喊“人，你干嘛呢！” 相反我们会问“小杨，你在干嘛呢！”
> 

###### 2. 对象

> 定义：某个抽象类的实例化

###### 3. 属性

> 定义：属性用来描述具体某个对象的特征，属性属于对象`静态`的一面，用来形容对象的一些特性
> 
> 举例：小杨身高181CM，体重80KG，这里身高、体重都是属性。

###### 4. 行为或方法

> 定义：方法属于对象动态的一面.
> 
> 举例：猴子会跑，会学人说话，跑、学人说话这些行为就是对象的方法！表现为动态的一面

##### 5. 面向对象三大特征

**1). 封装**

> 隐藏隐私数据，对外暴露公开的接口，增强安全，简化编程
> 
> 通过引入外部包小写字母开头的私有的结构体来实现封装,我们引入了`工厂方法`来实现
> 
> 通过引入外部包结构体中小写字母开头的私有字段来实现封装，我们引入`gettter`和`setter`来实现


**2). 继承**

> 子类继承父类，子类自动拥有父类的属性和方法
> 
> 这里我们通过封装一个公共的支付结构体，把它做为父类，同时实现4个不同支付平台的结构体，把这4个不同支付平台的结构体做为子类，来实现继承的功能
> 
> 详细的分析了在多个继承关系当中，如果有相同的数据字段，他们的访问顺序
> 
> 方法的继承与重载
> 
> 多重继承作业，实现多重继承当中接口的所有方法

**3). 多态**

> 同一种类型在不同场景下表现为不同的行为，我们举了生活中的饮用水，在不同的温度下水的三种形态，分别为冰，水，蒸汽
> 
> 多态的定义格式与实现方式
> 
> 结构体与自定义类型都可以实现接口中的方法
> 
> 接口的多重继承实现方式

___

### 面向对象封装

##### 什么是封装

> 隐藏隐私数据，对外暴露公开的接口，增强安全，简化编程

封装就是隐藏对象的属性和实现细节，仅对外公开接口，控制对数据的读写操作，也就是将数据也就是对象属性与操作数据的方法进行有机的结合，形成“类”，封装的目的是为了增强安全性和简化编程，使用者不必了解具体的实现细节，而只是要通过外部接口，以特定的访问权限来使用类的成员

封装，就是把客观事物封装成抽象的类，并且类可以把自己的数据和方法只让可信的类或者对象操作，对不可信的进行信息隐藏。一个类就是一个封装了数据以及操作这些数据的代码的逻辑实体。在一个对象内部，某些代码或某些数据可以是私有的，不能被外界访问。通过这种方式，对象对内部数据提供了不同级别的保护，以防止程序中无关的部分意外的改变或错误的使用了对象的私有部分。

通过引入外部包小写字母开头的私有的结构体来实现封装,我们引入了工厂方法来实现

通过引入外部包结构体中小写字母开头的私有字段来实现封装，我们引入`gettter`和`setter`来实现

##### 封装的作用

比如某位漂亮小姐姐可能年龄已经不小了，但是这位漂亮小姐姐会保养，可能已经30多岁了，看起来像个18岁的小姑娘，别人问她年龄时，她不愿意说，这是她的隐私。

在软件工程当中，如果包中的结构体中某些变量，我们不希望外部实体直接访问，因为这些数据比较重要，也就是说对外部的包来说他是一个私有的，对数据起到保护的作用。

##### 封装的使用

###### 1. 外部包中的结构体首字母小写

引入前面包的知识，定义一个`model`包，新建`userinfo.go`文件，这里我们将结构体`userInfo`首字母小写

```go 
package model

//class UserInfo{
//
//}
type userInfo struct {
    Name string
    Age int
    Height float32
    Eduschool string
    Hobby []string
    MoreInfo map[string]interface{}
} 
```

在我们的`main.go`文件中执行如下代码即会报错

```go 
//这种情况下是无法调用的，首字母小写它是非导出的，即外部的包无法访问。
boge := model.userInfo{
    Name:      "波哥",
    Age:       18,
    Height:    181,
    Eduschool: "北京邮电大学",
    Hobby:     []string{"coding","运动"},
    MoreInfo:  nil,
}
```

那如果外部包想访问这个结构体，如何来操作，这里就需要引入软件编程设计模式中的工厂模式了，工厂就如同现实中的工厂用于生产产品，在软件工程当中，工厂模式就是用于生成对象。这里建立工厂函数`NewUserInfo`，习惯以`New`开头

```go 
//工厂模式：生成对象
func NewUserInfo(name string,age int,height float32,eduschool string,hobby []string,moreinfo map[string]interface{}) *userInfo {
    return &userInfo{
        Name:      name,
        Age:       age,
        Height:    height,
        Eduschool: eduschool,
        Hobby:     hobby,
        MoreInfo:  moreinfo,
    }
}
```

在我们的main.go文件中执行如下代码正确

```go 
//这种情况下即可以访问了。
boge := model.NewUserInfo("小杨",18, 181,"北京邮电大学",[]string{"coding","运动"},nil)
fmt.Printf("coderyang的信息=%v\n",boge)
```

###### 2. 外部包中的结构体字段首字母小写

引入前面包的知识，定义一个`model`包，新建`product.go`文件，这里我们将结构体`Product`中的两个字段首字母小写

```go 
package model

type Product struct {
    productName string
    productPrice float32
}
```

这种情况下同样是无法调用的，首字母小写它是非导出的，即外部的包无法访问。

如果包中的结构体中某些变量，我们不希望外部实体直接访问，也就是说对外部的包来说他是一个私有的， 可是我们又想获取或者设置对应的数据，如何操作？
前面我们讲解方法接收者时有讲解过，我们可以从面向对象语言特性中得到启发，也就是面向对象中提供的 `getter` 和 `setter` 方法。对于 `setter` 方法使用 `Set` 前缀，对于` getter `方法只使用成员名，这样就形成了对我们数据的保护，称为对数据的封装。

> 工作中的应用
> 
> 比如产品的价格，我们不希望外部数据直接进行修改，因为这些数据很重要，但是我们可以提供一个接口告知使用者，你想修改我商品的价格，可以，但是必须按我的规定来，比如商品的价格必须在某个范围之内，这些是在接口中事先封装好的，不在这个范围，则拒绝修改。
> 

我们增加如下方法：

```go 
//getter setter
func (this *Product)SetProductName(_productName string )  {
    this.productName = _productName
}

func (this *Product)GetProductName() string  {
    return this.productName
}

func (this *Product)SetProductPrice(_productPrice float32)  {
    this.productPrice = _productPrice
}

func (this *Product)GetProductPrice() float32  {
    return this.productPrice
}
```

在我们的main.go文件中执行如下代码正确

```go 
product := &model.Product{}
product.SetProductName("慕课网go语言体系课")
fmt.Println(product.GetProductName())
```

___

### 面向对象继承

##### 什么是继承

继承是面向对象的基本特征之一，继承就是子类继承父类的特征和行为，使得子类对象（实例）自动就拥有了父类的属性和方法，

当多个子类拥有父类相同的方法与属性时，就可以抽取共有特征和方法形成一个父级类，形成了父子类之间关系。

继承机制可以很好的提高了代码复用率，比如在Java中的Object类，就是所有类的超类。

继承，指可以让某个类型的对象获得另一个类型的对象的属性的方法。

它支持按级分类的概念。继承是指这样一种能力：它可以使用现有类的所有功能，并在无需重新编写原来的类的情况下对这些功能进行扩展。 通过继承创建的新类称为“子类”或“派生类”，被继承的类称为“基类”、“父类”或“超类”。

继承的过程，就是从一般到特殊的过程。要实现继承，可以通过 “继承”（`Inheritance`）和“组合”（`Composition`）来实现。继承概念的实现方式有二类：实现继承与接口继承。实现继承是指直接使用 基类的属性和方法而无需额外编码的能力；接口继承是指仅使用属性和方法的名称、但是子类必须提供实现的能力。

在go语言当中继承：主要是通过类型组合的方式来实现：内嵌一个（或多个）包含想要的行为（字段和方法）的类型；多重继承可以通过内嵌多个类型实现

##### 继承的作用

支付是一个企业项目变现的重要手段，做为企业应用必不可少的功能，支付系统包括微信支付，支付宝，银联，京东等等，在开发中如何避免重复代码来实现类似的支付功能？由此引出继承

##### 继承的使用

###### 1. 结构体嵌套

> 继承在go语言中主要通过在一个结构体中嵌套另一个结构体，那么这个结构体自动拥有另一个结构体的字段与方法，实现了继承

引入前面包的知识，定义一个`mode`l包，新建`payment.go`文件，这里我们将结构体`PaymentArgs`

```go
package model

import "fmt"
//微信支付
//支付宝
//银联
//银行卡
type PaymentArgs struct {
    AppID string
    MchID string
    Key string
    CallbackUrl string
}
```

同时在`model`包，新建`Alipay.go`文件，这里我们让结构体`Alipay` 继承 `PaymentArgs`

```go 
package model

import "fmt"

type Alipay struct {
    PaymentArgs 
    AlipayOpenID string
    string
}
```

这样`Alipay`结构体就自动拥有`PaymentArgs`的信息

在我们的`main.go`文件中这样来实现结构体变量

```go 
alipay := &model.Alipay{
        PaymentArgs:  model.PaymentArgs{
            AppID:"alipay123",
            MchID:"alipaymchid",
            Key:"alipayfjkadsfjkasfjas",
            CallbackUrl:"https://api.imooc.com/alipay",
        },
        AlipayOpenID: "alipayopenid",
    }
```

当然如果想再为`微信支付`增加一个类似的结构体，也可以同时在`model`包，新建`payment_weixin.go`文件，这里我们让结构体`WeixinPay` 继承 `PaymentArgs`，访问方式同`Alipay`

我们在`main.go`中来打印他们的信息

```go 
fmt.Println(alipay.PaymentArgs.AppID)
fmt.Println(weixinpay.WeixinOpenID)
```

###### 2. 同一个结构体继承了多个不同的结构体

> 多个不同结构体有相同字段时，如何使用?

在`mode`l包，新建`payment_other.go`文件，这里我们将结构体`PaymentOther` ，结构体内容同`PaymentArgs`相同,`payment_other.go`的内容

```go 
package model

//微信支付
//支付宝
//银联
//银行卡
type PaymentOther struct {
    AppID string
    MchID string
    Key string
    CallbackUrl string
}
```

这里我们让`Alipay`这个结构体同时继承`PaymentArgs`和`PaymentOther`,`Alipay.go`的内容

```go
package model

import "fmt"

type Alipay struct {
    PaymentArgs //匿名结构体
    PaymentOther PaymentOther //有名结构体
    AlipayOpenID string
    string
}
```

这里`Alipay`结构体想访问`AppID`字段就必须指定结构体名，这里有两个概念`匿名结构体`和`有名结构体`

`匿名结构体` 在嵌套结构体时没有指定结构体变量名，例如上面`Alipay`结构体中的`PaymentArgs`
`有名结构体` 在嵌套结构体时没有指定结构体变量名，例如上面`Alipay`结构体中的`PaymentOther`
因为他们具有相同的字段，如果想访问`Alipay`结构体中的`AppID`就必须指定结构体变量名或者匿名结构体名

在`main.g`o中，如下的访问

```go 
fmt.Println(alipay.PaymentOther.AppID)
fmt.Println(alipay.PaymentArgs.AppID)
```

###### 3. 方法的继承与重载

我们为`payment.go`文件中`PaymentArgs`结构体增加方法

```go 
func (this *PaymentArgs)Info() {
    fmt.Printf("Info = %v\n",this)
}
```

这样我们定义的`Alipay`结构体与`WeixinPay`结构体自动就继承了`PaymentArgs`的方法

我们在`main.go`中调用

```go 
paymentArgs := model.PaymentArgs{
    AppID:       "superAppid",
    MchID:       "superMchid",
    Key:         "superKey",
    CallbackUrl: "https://api.imooc.com/super",
}
paymentArgs.Info()
```

同样的我们可以对继承的方法进行重定义

在我们的`Alipay.go`中为`Alipay`结构体增加方法

```go  
func (this *Alipay)Info()  {
    fmt.Printf("alipay = %v\n",this)
}
```

此时`Alipay`结构体重写了`Info()`方法，在`main.go`中调用

```go  
alipay := &model.Alipay{
    PaymentArgs:  model.PaymentArgs{
        AppID:"alipay123",
        MchID:"alipaymchid",
        Key:"alipayfjkadsfjkasfjas",
        CallbackUrl:"https://api.imooc.com/alipay",
    },
    AlipayOpenID: "alipayopenid",
}
alipay.Info()
```

##### 结构体继承访问流程

> 这里以上面`Alipay`结构体当中访问`AppID`为例
> 
> 1.先判断`AppID`是否属于`Alipay`,如果有就访问
> 
> 2.如果没有，继续去找他继承的结构体`PaymentArgs`，如果有就访问
> 
> 3.如果没有继续去找`PaymentArgs`这个结构的所继承的结构体，如果有就访问，没有就报错,因为`PaymentArgs`结构体没有再继承别的结构体
> 

##### 结构体注意事项

> 1.如果一个结构中继承了多个结构体，而这些多个结构体当中有相同的字段，那么我们就需要使用 结构体名来访问

如上面我们所演示的访问Alipay结构体中的AppID就必须指定结构体变量名或者匿名结构体名

> 2.一个内置类型可以做为结构体的匿名字段，这种方式只能在本包访问

```go  
//定义一个结构体，字段为一个内置string类型
type StringStruct struct {
    string
}

ss := StringStruct{"hello"}
//这种方式只能在本包中访问
fmt.Println(ss.string)
```

##### 继承有什么优点

> 1.提高代码的复用率
> 
> 2.提高代码的扩展性与维护性


___

###  面向对象多态

##### 什么是多态

> 多态同一个行为具有多个不同表现形式。也就是说一个类实例（对象）的相同方法在不同场景下有不同表现形式。多态机制使内部结构不同的对象可以共享相同的外部接口。
> 
> 这意味着，虽然针对不同对象的具体操作不同，但通过一个公共的类，它们（那些操作）可以通过相同的方式予以调用。最大的优点就是说可以降低类型之间的耦合度，对吧
> 

在go语言当中多态：用接口实现：某个类型的实例可以赋给它所实现的任意接口类型的变量。类型和接口是松耦合的，并且多重继承可以通过实现多个接口实现。

多态，是指一个类实例的相同方法在不同情形有不同表现形式。

多态机制使具有不同内部结构的对象可以共享相同的外部接口。这意味着，虽然针对不同对象的具体操作不同，但通过一个公共的类，它们（那些操作）可以通过相同的方式予以调用。

##### 多态的作用

张三的儿子娶媳妇，通知李五去他家`喝喜酒`（这里就是一个`方法`），但是李五有事不能来，李五就让他的三个儿子其中一个代表他老爹李五去`喝喜酒`（这里就是一个`方法`），使用的是他们老爹的`喝喜酒`方法,就像他老爹本人一样。

不必编写每一子类的功能调用，可以直接把不同子类当父类看，屏蔽子类间的差异，提高代码的通用率/复用率

父类引用可以调用不同子类的功能，提高了代码的扩充性和可维护性

##### 多态的使用

###### 1. 定义接口与类型，让类型去实现接口中的方法

> 1.定义接口时，方法不能实现
> 
> 2.一个类型如果实现了接口中的所有方法，我们就说这种类型实现接口，不仅仅结构体，也可以是内置类型
> 
> 3.自定义类型可以实现多个接口

`定义格式`

```go  
type 接口名 interface {
    方法名1（参数列表）（返回值）
    方法名2（参数列表）（返回值）
    方法名3（参数列表）（返回值）
    。。。
}
通过自定义类型来实现接口中的所有方法
//定义类型
type T struct {
}
type TT string

//方法接收者
func (this *T)方法名1()（返回值）{}
func (this *T)方法名2()（返回值）{}
func (this *T)方法名3()（返回值）{} 
```

在`main.go`中定义一个结构体一个接口`pay`，增加两个方法`topay()`，`info()`

```go 
type pay interface {
    topay()
    info()
}
```

同时我们来定义一个结构体`payment`

```go 
type payment struct {
    paymentmethod string
}
```

让这个结构体去实现接口`pay`中的所有方法

```go 
func (this *payment)topay()  {
    fmt.Println("topay:",this.paymentmethod)
}

func (this *payment)info()  {
    fmt.Println("info:",this.paymentmethod)
}
```

我们来定义`payment`类型的变量`_payment`

```go  
_payment := &payment{paymentmethod:"alipay"}
```

这要我们就可以通过这个变量去调用接口中的方法了，因为我们的结构体`payment`实现了接口中所有的方法

```go 
_payment.info()
_payment.topay()
```

> 注意点
> 
> 一个变量实现了接口当中所有方法，接口就可以指向这个变量
> 
> 接口内的方法不能实现，体现了程序的多态与低偶合高内聚

```go 
var _pay pay
//一个变量实现了接口当中所有方法，接口就可以指向这个变量
_pay = _payment
_pay.info()
_pay.topay()
```

不过一般不这样使用

###### 2. 自定义类型也可以实现接口

在`main.go`文件中,定义两个接口

```go 
type write interface {
    echo()
    out()
}

type read interface {
    scan()
    input()
}
```

我们来基于内置类型创建自定义类型

```go 
//自定义类型，基于内置类型
type readwrite string
```

让自定义类型来实现上面定义的两个接口中的所有该当

```go 
//自定义类型`readwrite`实现`write`接口中的`echo()`方法
func (this *readwrite)echo()  {
    fmt.Println("readwrite:echo()")
}

//自定义类型`readwrite`实现`write`接口中的`out()`方法
func (this *readwrite)out()  {
    fmt.Println("readwrite:out()")
}

//自定义类型`readwrite`实现`read`接口中的`scan()`方法
func (this *readwrite)scan()  {
    fmt.Println("readwrite:scan()")
}

//自定义类型`readwrite`实现`read`接口中的`input()`方法
func (this *readwrite)input()  {
    fmt.Println("readwrite:input()")
}
```

这样我们自定义的类型`readwrite`就实现了两个接口中的所有方法，在`main.go`文件中调用

```go 
var _readwrite readwrite
_readwrite.echo()
```

> 多重继承接口，所有的方法都要实现

```go 
//多重继承格式
type InterfaceAA interface {
    InterfaceA
    InterfaceB
}
```

##### 综合案例

为了巩固面向对象知识点，通过结合面向对象三大特征，综合的对面向对象的知识进行进阶

> 企业项目中经常涉及到与日志存储的业务，比如针对web项目的日志存储

> 比如磁盘IO操作的日志:磁盘进行数据拷贝读取一般会有读写日志,记录读取到的位置，即当前数据在磁盘的哪个碰头哪个扇区上

> 比如网络请求的日志:去访问某个网站一般会有请求日志的记录，用于分析来访客户，刻画出用户的区域，访问兴趣爱好（网购时的一个典型例子,用户浏览记录写cookie）

这里我们模拟一个`网络`读写日志与`磁盘`读写日志的例子

定义写操作接口`write`

```go 
type write interface {
    echo()
    out()
}
```

定义公共日志结构体`Log`，做为父类,并为其增加方法`writeLog()`，传递一个`write`接口类型的变量

```go 
//日志结构体
type Log struct {
    name string
    content string
    addtime int64
}

func (this *Log)writeLog(_write write)  {
    fmt.Println(this.name+"---"+this.content)
    _write.echo()
    _write.out()
}
```

定义`网络`读写结构体与`磁盘`读写结构体，继承自父类`Log`

```go 
type NetLog struct {
    Log
}

type IOLog struct {
    Log
}
```

定义自定义类型，`iowrite`与`netwrite`，分别实现`write`接口中的所有方法

```go 
type iowrite string
func (this *iowrite)echo()  {
    fmt.Println("iowrite:echo()")
}
func (this *iowrite)out()  {
    fmt.Println("iowrite:out()")
}

type netwrite string
func (this *netwrite)echo()  {
    fmt.Println("netwrite:echo()")
}
func (this *netwrite)out()  {
    fmt.Println("netwrite:out()")
}
```

`main.go`文件中

```go 
//父类引用指向子类对象
//一个变量实现了接口当中所有方法，接口就可以指向这个变量
log := &Log{
    name:    "微信小程序支付日志",
    content: "微信小程序支付日志内容",
    addtime: 0,
}

var _iowrite *iowrite
var _netwrite *netwrite 
//writeLog的参数是一个write类型，我们这里的iowrite实现了write接口中的所有方法，所以可以传递iowrite
//相当于write （指向）-> iowrite
log.writeLog(_iowrite)

//writeLog的参数是一个write类型，我们这里的netwrite实现了write接口中的所有方法，所以可以传递netwrite
//相当于write （指向）-> netwrite
log.writeLog(_netwrite)
```

> 调用者多态的一面

```go 

netlog := &NetLog{Log{
    name:    "微信小程序网络支付日志",
    content: "微信小程序网络支付日志内容",
    addtime: 0,
}}
//writeLog的调用者是Log,我们的NetLog继承自Log，所以可直接调用
netlog.writeLog(_netwrite)

filelog := &IOLog{Log{
    name:    "微信小程序文件支付日志",
    content: "微信小程序文件支付日志内容",
    addtime: 0,
}}
//writeLog的调用者是Log,我们的IOLog继承自Log，所以可直接调用
filelog.writeLog(_iowrite)
```