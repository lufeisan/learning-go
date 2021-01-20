我们接着学习 go语言的一些基础知识

[流程控制](#流程控制)

[函数](#函数)

[结构体](#结构体)

[方法](#方法)

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