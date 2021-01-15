这个篇章我们主要学习 go语言的一些基础知识

### go数据类型概述与变量

Go 语言数据类型包含基础类型和复合类型两大类。
基础数据类型包括：布尔型、整型、浮点型、复数型、字符型、字符串型、错误类型。
复合数据类型包括：指针、数组、切片、字典、通道、结构体、接口。

#### 变量

##### 一、变量引入

如何将我们需要的数据存入计算机中，这里就引入了变量。

##### 二、变量概述(是什么)

变量几乎在所有编程语言中都存在。变量相当于是内存中的一块数据,是一块存储空间，可以通过定义一个变量来申请一块数据存储空间，之后可以通过所定义的变量名来操作我们申请的这块存储空间。可以说变量是我们编写的程序的一个最基本的组成单元或者叫组成单位。

那么每一块存储空间应该存储什么类型的变量呢？这就引出了我们的数据类型。

> 变量示意图

[![sdX7rj.png](https://s3.ax1x.com/2021/01/15/sdX7rj.png)](https://imgchr.com/i/sdX7rj)

##### 三、变量的作用与应用场景

###### 1. 作用

通过对变量的操作来实现对我们关注的数据的操作。
   
###### 2. 应用场景

在计算机中存储我们需要的数据，这时候就需要使用到变量

##### 四、变量零值

变量定义未赋值时的默认值
```
int 0
int8 0
int32 0
int64 0
rune 0 // rune 的实际类型是 int32
float32 0 // 长度为 4 byte
float64 0 // 长度为 8 byte
bool false
string “”
```

##### 五、申请变量的几个方法

我们如何在go语言当中申请变量？申请变量主要有以下几种方式：

###### 1. 不赋值有默认的零值(根据数据类型来确定零值)

```go
var variables1 int
```

###### 2. 简短声明

```go 
variables2 := "我是小杨"
```

###### 3. var variables = value 形式

```go 
var variables3 = 100 //这种情况，编译器自动做类型推导
```

###### 4. 一次赋值多个值

```go
var variables4,variables5,variables6,variables7 = 1,"我是小杨",3.14,true
fmt.Println(variables1,variables2,variables3,variables4,variables5,variables6,variables7)
```

###### 5. 简短声明,多次赋值

```go
variables4,variables5,variables6,variables7 := 1,"我是小杨",3.14,true
```

###### 6. 申请多个全局变量,在函数体外部

```go
var (
   variablesx int
   slicex []int
   interfacex interface{}
)
```

###### 7.变量的交换

```go
var i = 100
var j = 200
fmt.Println(i,j)
i,j = j,i
fmt.Println(i,j)
```

##### 六、注意事项

###### 1. 变量未必不需要添加分号;

###### 2. 变量的交换 i,j = j,i

###### 3. Go 对于已声明但未使用的变量会在编译阶段报错

```go 
var index int
//如果一个变量暂时不使用，可以赋值给他自己 
index = index
```
###### 4. `_`（下划线）是个特殊的变量名，任何赋予它的值都会被丢弃。

###### 5. 变量访问控制
`大写字母`开头的变量是可导出的，即其它包可以读取的，是公有变量（相当于传统编程语言中`class`的`public`权限修饰符）；
`小写字母`开头的就是不可导出的，是私有变量，仅本包可以使用（相当于传统编程语言中`class`的`private`权限修饰符）。

___

### 常量

##### 一、常量引入

当程序中需要引入一个在整个程序运行期，数据不发生改变时，使用常量

##### 二、常量概述（什么是常量）

就是在程序运行期不可以改变的变量

##### 三、Go 语言预定义常量

```go
true
false
iota
```

##### 四、常量的作用与应用场景

###### 1. 作用

全局唯一，编译期就已经确定的值，提高程序执行效率

###### 2. 应用场景

当程序中需要引入一个在整个程序运行期，数据不发生改变时，使用常量。

另一个就是枚举数据时使用，如下：
```go 
const (
   Monday = iota
   Tuesday
   Wednesday
   Thursday
   Friday
   Saturday
   Sunday
)
```

##### 五、申请常量的几个方法

###### 1. const constVariables 变量类型 = 变量值

```go
const constVariables1 float64 = 3.1415926 
```

###### 2. 一次申明多个值

```go 
const constVariables2,constVariables3 = 100,"小杨"
```

###### 3. const （…）

```go 
const (
   iotaVariables1 = iota  //0
   iotaVariables2 = iota  //1
   iotaVariables3 = iota  //2
)
```

###### 4. 单独赋值

```go 
const iotaVariables4 = iota //0
```

###### 5. const 指定第一个iota,其余自动递增

```go 
const (
   iotaVariables5 = iota //0
   iotaVariables6      //1
   iotaVariables7      //2
)
```

###### 6. 枚举一周的日期

```go 
const (
   Monday = iota
   Tuesday
   Wednesday
   Thursday
   Friday
   Saturday
   Sunday
)
```

###### 7. 同一行定义

```go 
const(
   iotaVariables8,iotaVariables9,iotaVariables10 = iota,iota,iota
)
```

###### 8. const中iota与iota之间跳过

```go 
const (
   iotaVariables11 = iota //0
   iotaVariables12 = "Bobo" //Bobo
   iotaVariables13 = iota //2
)
```

##### 六、注意事项

> 1.通过const关键字来申请
> 
> 2.常量是指编译期间就明确知道的值并且不可改变
> 
> 3.iota特殊，iota在每个const出现时被重置为0


___

### 数值类型

##### 一、数值引入

我们要存储一个人的年龄，就需要用到数值类型

##### 二、数值类型概述

用于定义整数类型变量的标识符

##### 三、作用与应用场景

在计算机当中存储数值类型

##### 四、申请整型变量的方法

```go
var intVariables1 = 100 //int
intVariables2 := 200 //int
var intVariables3 int32 //int32
intVariables := 126 //int

//类型转换
intVariables3 = int32(intVariables)

//指定类型
var intVariables4 int64 = 123456789
fmt.Printf("intVariables1=%T,intVariables2=%T,intVariables3=%T\n",intVariables1,intVariables2,intVariables3)

//引入unsafe包，打印占据的空间大小，即字节大小
fmt.Println(unsafe.Sizeof(intVariables4))
```

##### 五、不同数值类型与占用的空间

###### 1. 有符号位

```go  
int8 数据范围：-2^7到2^7-1
int16 数据范围：-2^15到2^15-1
int32 数据范围：-2^31到2^31-1
int64 数据范围：-2^63到2^63-1
```

###### 2. 无符号位

```go 
uint8 数据范围：0到2^8-1
uint16 数据范围：0到2^16-1
uint32 数据范围：0到2^32-1
uint64 数据范围：0到2^64-1
```

##### 六、注意事项

> 1. 默认数据类型为int
> 2. int32,int64由于占用空间大小不一样，被认为是不同的类型，所有不能相互赋值
> 3. 不同类型的转换
> 4. 占用字节 unsafe.Sizeof(intVariables)
> 5. 注意使用时数据可能溢出与损失的问题

___

