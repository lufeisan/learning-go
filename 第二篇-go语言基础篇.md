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

### 浮点类型

##### 一、浮点引入

当我们需要存储带有小数点的数据类型时需要使用浮点类型

##### 二、浮点概述

用于存储带有小数位的数据类型

##### 三、作用与应用场景

**作用**

当我们需要存储带有小数点的数据类型时需要使用浮点类型

**应用场景**

比如在微信小程序支付时，这里支付的金额，可能是1888.856元，这个时候就需要使用浮点类型

##### 四、主要类型

> 单精度 float32
> 双精度 float64

##### 五、申请变量的方法

###### 1. 十进制的形式来展示

```go 
var floatVariables1 float32 = 3.1415926
floatVariables2 := .1416926 //0.1416926
fmt.Printf("floatVariables1的类型=%T,占用的字节大小=%d\n",floatVariables1,unsafe.Sizeof(floatVariables1))
fmt.Printf("floatVariables2的类型=%T,占用的字节大小=%d\n",floatVariables2,unsafe.Sizeof(floatVariables2))
```

###### 2. 科学计数法来展示

```go 
floatVariables3 := 3.1415926e2 //3.1415926乘以10的2次方
floatVariables4 := 3.1415926e-2 //3.1415926除以10的2次方
fmt.Println(floatVariables3,floatVariables4)
```

###### 3. 不同精度的浮点类型的转换

```go 
var floatVariables5 float32 = 3.14
var floatVariables6 float64 = 3.14
floatVariables6 = float64(floatVariables5)
floatVariables6 = floatVariables6
```

##### 六、复数

> 实数+虚数i
> complex64(32 位实数 + 32 位虚数+i虚数单位)
> complex128（默认）(64 位实数 + 64 位虚数+i虚数单位)


###### 申请方式

```go 
var complexVariables1 complex64
complexVariables1 = 3.14+12i
complexVariables2 := complex(3.14,12)

fmt.Printf("complexVariables1的类型=%T,值=%v\n",complexVariables1,complexVariables1)
fmt.Printf("complexVariables2的类型=%T,值=%v\n",complexVariables2,complexVariables2)

//打印复数的实数部分与虚数部分
fmt.Println(real(complexVariables1),imag(complexVariables1))
```

##### 七、注意事项

> 1.默认数据类型为float64
> 
> 2.float32,float64由于占用空间大小不一样，被认为是不同的类型
> 
> 3.不同类型的转换
> 
> 4.单精度，双精度类型转换的精度损失与溢出

___

### 字符

##### 一、什么是字符

字符是电子计算机中字母、数字、符号的统称，是数据结构中最小的数据存取单位，通常由8个二进制位(一个字节)来表示一个字符。

##### 二、作用与应用场景

用于存储单个字符

##### 三、字符表示类型

> byte(uint8) byte 类型是 uint8 的别名
>
> rune 类型，代表一个 UTF-8 字符，当需要处理中文、日文或者其他复合字符时，则需要用到 rune 类型，rune 类型是 int32 类型的别名

##### 四、申请变量的方法

```go 
var charVariables1 byte = '0'
charVariables2 := '波'
//var charVariables3 byte = '波'

fmt.Printf("charVariables1 = %d,charVariables2=%d\n",charVariables1,charVariables2)
fmt.Printf("charVariables2=%c，charVariables2=%T\n",charVariables2,charVariables2)
//fmt.Printf("charVariables3=%c，charVariables3=%T\n",charVariables3,charVariables3)
variables := 'a' //对应的编码值
fmt.Printf("加和=%d,a的编码值=%d\n",100+variables,variables)
```

##### 五、注意事项

> 1.单引号括起来
> 
> 2.存储：字符-》ascii码值-》二进制
> 
> 3.读取：二进制-》ascii码值-》字符
> 
> 4.一个字符占一个字节，一个中文占3个字节
> 
> 5.字符可以与整数进行算术运算(转成ascii码值再计算)

___


### 字符串

##### 一、字符串概述

字符串是的类型标识为string, 由数字、字母、下划线组成的一串字符。 在编程语言中用于表示文本的数据类型。

##### 二、申请变量的方法

###### 1. 申明并赋值

```go 
var stringVariables1 string
stringVariables1 = "hello 小杨\n"
```

###### 2. 通过反引号定义，原样输出

```go 
var stringVariables2 = `
package main 
import (
   "fmt"
   "unsafe"
)

func main() {
   /*
   float32 4个字节
   float64 8个字节
    */
   。。。。。。。
   fmt.Println(real(complexVariables1),imag(complexVariables1))
}
   `
```

###### 3. 获取字符串长度

```go 
var stringVariables3 = "hello imooc,我是小杨"
stringVariables3Len := len(stringVariables3)
```

##### 三、字符串遍历

###### 1. 通过 for index := 0; index < stringVariables3Len;index++ {} 形式来遍历

```go 
for index := 0; index < stringVariables3Len;index++ {
   //这种情况如果是中文，则会有编码问题
   fmt.Printf("%s-编码值=%d,值=%c,类型=%T\n",stringVariables3,stringVariables3[index],stringVariables3[index],stringVariables3[index])
}
```

###### 2. 通过for..range 形式来遍历

```go 
// 通过range，在这种情况下中文就不会有问题，按照rune类型来打印
for index, val := range stringVariables3 {
   fmt.Printf("通过for index ... %s--索引:%d--字符值:%c--字符值类型;%T\n", stringVariables5, index, val, val) //val 的类型为 rune，即int32
}
```

##### 四、参照字符类型

> 1.byte(uint8) byte 类型是 uint8 的别名
> 2.rune 类型，代表一个 UTF-8 字符，当需要处理中文、日文或者其他复合字符时，则需要用到 rune 类型，rune 类型是 int32 类型的别名

##### 五、注意事项

> 1.双引号括起来
> 
> 2.`` 反引号原样输出
> 
> 3.字符串初始化之后不允许重新赋值
> 
> 4.可以以字符数组下标的形式来读取，但不能赋值
> 
> 5.len获取字符串长度
> 
> 6.字符串相加即是拼接

##### 六、面试

> 1.go语言中如何遍历字符串中有中文的情况？
> 
> for循环遍历值的类型为uint8
> 
> 2.for循环的遍历与for….range的区别
> 
> for...range遍历值的类型为int32

___

### 布尔

##### 一、布尔类型，要么为真，要么为假

> 真 true
> 假 false


##### 二、作用与应用场景

`作用`

在计算机当中，为了表示某个条件是否成立，需要使用到布尔类型

`应用场景`

在条件判断当中，条件成立或条件不成立

##### 三、申请变量的方法

```go 
var boolVaraibles1 bool
boolVaraibles1 = true
boolVaraibles2 := (true == false)

if 3 == 4 {
   fmt.Println("false")
} else {
   fmt.Println("true")
}

fmt.Println(!true,!false,!!true)
```

##### 四、注意事项

> 1.只有true和false
> 2.其他类型不可以转换成布尔

___

