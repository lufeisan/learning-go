这个篇章我们主要学习 go语言的一些基础知识

[go数据类型概述与变量](#go数据类型概述与变量)

[常量](#常量)

[数值类型](#数值类型)

[浮点类型](#浮点类型)

[字符](#字符)

[字符串](#字符串)

[布尔](#布尔)

[指针](#指针)

[数组](#数组)

[切片](#切片)

[map](#map)



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
> 
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
> 
> 2.其他类型不可以转换成布尔


### 指针

##### 一、指针概述

程序在内存中存储它的值，每个内存块都 有一个地址，而存储这个地址的变量被称为指针变量，指针。
通常用十六进制数表示，如：`0x6b0820` 或 `0xf84001d7f0`

一个指针变量可以指向任何一个值的内存地址 它指向那个值的内存地址，在 32 位机器上占用 4 个字节，在 64 位机器上占用 8 个字节，并且与它所指向的值的大小无关。
指针可以指向任何类型的值，但是使用时指定指针的类型在实际编码中具有重要意义；
在指针类型前面加上` * `号来获取指针所指向的内容。
使用一个指针引用一个值被称为间接引用。

> 1.主要用于管理内存
> 
> 2.指针是一个特殊的变量
> 
> 3.存储的是另一个变量的内存地址

[![s2lhBn.png](https://s3.ax1x.com/2021/01/19/s2lhBn.png)](https://imgchr.com/i/s2lhBn)

##### 二、指针的作用及应用场景

`作用`

节省内存空间，提高执行效率（当操作的数据量较大规模时）
访问变量的值

`应用场景`

修改变量的值
访问变量的值

##### 三、指针变量操作

先定义变量，再定义指针去取变量的地址，那么这个变量存储的就是地址，实际的值是这个地址指向的空间

```go 
//先定义变量，再定义指针去取变量的地址
var intVariables int = 100
fmt.Printf("intVariables的值=%d,地址=%v\n",intVariables,&intVariables)

//定义一个指针类型的变量，那么这个变量存储的就是地址，实际的值是这个地址指向的空间
//定义一个指针类型的变量去指向 intVariables
var pointerVariables *int = &intVariables
fmt.Printf("pointerVariables的值=%v,地址=%v\n",pointerVariables,&pointerVariables)
```

> 取地址操作符 `&`，一般在指针操作当中经常使用，`&` 取出地址
> 
> 取值操作符 `*`，一般在指针操作当中，`*` 根据地址找该地址指向空间的值。

###### 指针变量的内存分析

```go 
/*
   变量名             变量值           地址
   intVariables      100              0xc00006c008
   pointerVariables    0xc00006e008    0xc00007c020
*/
```

###### 取变量值的方式

> 1.直接通过变量名,variables
> 
> 2.通过指针间接访问(指针名),pointerVariables

##### 四、注意事项

> 1.值类型一般都有对应的指针类型，格式 数据的类型 比如int->int float64->*float64
> 
> 2.0x开头的十六进制的一组数据
> 
> 3.go语言中引用类型有哪些？指针，`slice`，`map`，`chan`,`interface`
> 
> 4.值类型：变量存储的值是值类型，通常在栈中分配
> 
> 5.引用类型：变量存储的是地址，这个地址对应的空间存储的才是实际的值，一般引用类型在堆中分配，一旦无任何变量来引用这块空间，那么会被操作系统进行垃圾回收。
> 
> 6.go语言的指针没有指针运算，因为指针的乱引用会导致的内存泄漏，以及引发一连串程序的崩溃
> 
> 7.修改指针指向变量的值,但是不会修改地址，通过指针改掉了指向变量对应的值
> 
> 8.一个指针变量可以指向任何一个值的内存地址
> 
> 9.指针也可以指向另一个指针，并且可以进行任意深度的嵌套，导致你可以有多级的间接引用，但在大多数情况这会使你的代码结构不清晰
> 
> 10.当一个指针被定义后没有分配到任何变量时，它的值为 nil。对一个空指针的反向引用是不合法的，并且会使程序崩溃

___

### 数组

##### 一、数组概述

数组是具有相同类型的一组长度固定的数据项序列。这种类型可以是整型、字符串或者自定义类型。数组长度必须是一个常量表达式，并且必须是一个非负整数。数组长度也是数组类型的一部分，所以`[5]int`和`[10]int`是属于不同类型的。

如果我们想让数组元素类型为任意类型的话可以使用空接口作为类型，当使用值时我们必须先做一个类型判断 。

数组元素可以通过 索引（位置）来读取（或者修改），索引从 0 开始，第一个元素索引为 0，第二个索引为 1，以此类推。（数组以 0 开始在所有类 C 语言中是相似的）。元素的数目，也称为长度或者数组大小必须是固定的并且在声明该数组时就给出（编译时需要知道数组长度以便分配内存）。

> 1.数组是长度固定的数据类型
> 
> 2.数据元素的类型相同

##### 二、作用及应用场景

`作用`
组在内存当中是连续的存储空间，可以有效的提升cpu的执行效率。

`应用场景`
存储多个相同类型的数据时，可以使用数组

##### 三、数组的定义

###### 一维数组的定义方式(1)

```go
//数组的定义方式1
var arrayVariables [10]int
arrayVariables[0] = 100
arrayVariables[3] = 200
//arrayVariables[10] = 100
fmt.Println(arrayVariables)
```

###### 一维数组的定义方式(2)定义并初始化

```go 
var arrayVariables2 [5]int = [5]int{1,2,3,4,5}
//在这种情况左边类型可简写
var arrayVariables3 = [5]int{1,2,3,4,5}
```

###### 数组内存分析

```go 
//遍历数组
var arrayVariables2 [5]int = [5]int{1,2,3,4,5}
var length = len(arrayVariables2)
for i :=0;i<length;i++ {
   fmt.Printf("arrayVariables2[%d]=%d,地址=%p\n",i,arrayVariables2[i],&arrayVariables2[i])
}

/*
数组在内存当中是连续的存储空间
数组的元素(下标)      元素值    元素的地址
0              1        0xc00006a060
1              2        0xc00006a068
2              3         0xc00006a070
3              4          0xc00006a078
4              5          0xc00006a080

*/
```

###### 一维数组定义方式(3) arrayVariables := […]int{1,2,3,4}

```go  
arrayVariables3 := [...]int{1,2,3,4,5}
fmt.Println(arrayVariables3,len(arrayVariables3))
```

###### 一维数组定义方式(4)，指定索引下标

```go  
arrayVariables4 := [...]int{100:200,300:500}
```

###### 二维数组,两个维度

```go 
var arrayVariables8 [4][2]int
fmt.Println(arrayVariables8)

arrayVariables9 := [4][2]int{{10,11},{3,5},{2,3},{100,88}}
fmt.Println(arrayVariables9)

arrayVariables10 := [4][2]int{1:{100,90},2:{8,9}}
fmt.Println(arrayVariables10)
```

###### 多维数组，多个维度

```go 
var arrayVariables11 [4][3][2]int = [4][3][2]int{}
fmt.Println(arrayVariables11)
```

##### 四、数组的遍历

###### 数组遍历方式一，通过for i :=0;i<length;i++ {} 形式

```go 
arrayVariables6 := [3]string{"小杨","coderyang","golang"}
arrayVariables7 := arrayVariables6
//for .. rage
for key,value := range arrayVariables6 {
   fmt.Printf("arrayVariables6[%d]=%v,地址=%p\n",key,value,&arrayVariables6[key])
}
for key,value := range arrayVariables7 {
   fmt.Printf("arrayVariables7[%d]=%v,地址=%p\n",key,value,&arrayVariables6[key])
}
```

###### 数组遍历方式二，使用 for .. range形式

```go 
arrayVariables6 := [3]string{"小杨","coderyang","golang"}
arrayVariables7 := arrayVariables6
//for .. rage
for key,value := range arrayVariables6 {
   fmt.Printf("arrayVariables6[%d]=%v,地址=%p\n",key,value,&arrayVariables6[key])
}
```

##### 五、数组注意事项

> 数组是值类型，这一点对于有c语言编程经验的同学来说需要特别的注意。
> 
> len()获取长度
> 
> 数组的长度是数组类型的组成部分,比如以下下数组为两种不同的类型

```go 
arrayVariables[10]int arrayVariables[11]int 
```

> 数组在内存当中是连续的存储空间

```go 
数组的元素(下标)          元素值            元素的地址
    0                    1            0xc00006a060
    1                    2            0xc00006a068
    2                    3            0xc00006a070
    3                    4            0xc00006a078
    4                    5            0xc00006a080
```

> 数组做为参数以引用形式传递函数，意义重大，当传递较大的数组时可以有效的提升cpu执行效率

```go 
func changeArrByPointer(arr *[10]int)  {
    (*arr)[0] = 100
}
```

> 数组做为值类型来传递函数,调用时是值拷贝，如果较大的数组传递对cpu的效能消耗是极其大的

```go 
func changeArr(arr [10]int) {
    arr[0] = 100
} 
```

___

### 切片

##### 一、切片概述

> 1.一种数据结构，便于使用与管理我们的数据集合。
> 
> 2.按需自动增长，动态数组（通过append来完成）
> 
> 3.底层指向的是数组
> 
> 4.内存当中是连续的存储空间，可以有效的提升cpu的执行效率。
> 
> 5.引用类型

##### 二、切片组成

> 指向底层数组的指针
> 
> 切片元素的长度，通过len()获取
> 
> 容量,通过cap()获取

##### 三、切片的作用与应用场景

`作用`
在函数当中传递切片时，当数据类型数据较大时，使用切片可以有效减少内存占用，提高程序执行效率

`应用场景`
从数据库表中读取商品信息时，用到map切片，每一个map看成一个整体

##### 四、切片的定义

> 定义一个数组,让切片去引用,这种方式，数组可见

```go  
arrayVariables := [...]int{12, 21, 23, 55, 98, 2}

//定义一个切片去引用数组，这种情况默认长度和容量一致
var sliceVariables []int
sliceVariables = arrayVariables[:]
```

通过以上代码，分析切片的底层情况

分别打印数组的地址与切片的地址来分析

```go  
//切片的定义
var sliceVariables []int
//定义一个数组
arrayVariables := [...]int{12,21,23,55,98,2}
for i :=0;i<len(arrayVariables);i++ {
   fmt.Printf("arrayVariables[%d]=%d,地址=%p\n",i,arrayVariables[i],&arrayVariables[i])
}

//切片去引用数组
sliceVariables = arrayVariables[:]
for i:=0;i<len(sliceVariables);i++ {
   fmt.Printf("sliceVariables[%d]=%d,地址=%p\n",i, sliceVariables[i],&sliceVariables[i])
}


var sliceVariables2 []int
sliceVariables2 = arrayVariables[1:3]
//12,21,23,55,98,2
//[21 23]
fmt.Println(sliceVariables2)
//切片指向的是底层的数组
for i :=0;i<len(sliceVariables2);i++ {
   fmt.Printf("sliceVariables2[%d]=%d,地址=%p\n",i, sliceVariables2[i],&sliceVariables2[i])
}
sliceVariables2[0] = 100

fmt.Println(arrayVariables)
fmt.Println(sliceVariables2)
```
[![sRVSjx.jpg](https://s3.ax1x.com/2021/01/19/sRVSjx.jpg)](https://imgchr.com/i/sRVSjx)


> 通过make来创建切片,这种方式可以指定切片的大小和容量，未赋值，有默认值 ，这种方式切片对应的数组不可见，由make来维护

```go  
//创建一个初始元素个数为 5 的数组切片，元素初始值为 0，并预留 6 个元素的存储空间
var sliceVariables2 []int = make([]int, 5, 6)

分析通过make方式定义切片的内存情况

var sliceVariables3 []int = make([]int,5,6)
fmt.Printf("sliceVariables3的长度=%d,容量=%d,\n切片指向的底层数组的地址=%p,切片自己的地址=%p\n",len(sliceVariables3),cap(sliceVariables3),sliceVariables3,&sliceVariables3)
```

> 通过make来创建切片的内存情况

[![sRVkUe.jpg](https://s3.ax1x.com/2021/01/19/sRVkUe.jpg)](https://imgchr.com/i/sRVkUe)

##### 五、切片的遍历

###### 1. 通过for i:=0;i<len(sliceVariables);i++ {}形式遍历

```go 
sliceVariables = arrayVariables[:]
for i:=0;i<len(sliceVariables);i++ {
   fmt.Printf("sliceVariables[%d]=%d,地址=%p\n",i, sliceVariables[i],&sliceVariables[i])
}
```

###### 2. 通过for..range形式遍历

```go  
for key,value := range sliceVariables {
   fmt.Println(key,value)
}
```

##### 六、切片的追加append

> 1.创建一个初始元素个数为 5 的数组切片，元素初始值为 0，并`预留 6 个元素`的存储空间

```go 
var sliceVariables3 []int = make([]int,5,6)

var sliceVariables3 []int = make([]int,5,6)
fmt.Printf("sliceVariables3的长度=%d,容量=%d,\n切片指向的底层数组的地址=%p,切片自己的地址=%p\n",len(sliceVariables3),cap(sliceVariables3),sliceVariables3,&sliceVariables3)
```

> 2.第一次追加切片的容量`达到预设的最大容量`

```go 
sliceVariables3 = append(sliceVariables3,7)
fmt.Printf("第一次追加sliceVariables3的长度=%d,容量=%d,\n切片指向的底层数组的地址=%p,切片自己的地址=%p\n",len(sliceVariables3),cap(sliceVariables3),sliceVariables3,&sliceVariables3)
```

> 3.第一次追加切片的容量超出了预设的最大值，go语言会新申请一块内存将原始数据拷贝到新的内存当中，切片指向新的内存空间

```go 
sliceVariables3 = append(sliceVariables3,8)
fmt.Printf("第二次追加sliceVariables3的长度=%d,容量=%d,\n切片指向的底层数组的地址=%p,切片自己的地址=%p\n",len(sliceVariables3),cap(sliceVariables3),sliceVariables3,&sliceVariables3)
```

##### 七、切片的拷贝

> 1.定义源切片

```go 
sliceVariables4 := []int{1,2,3,4,5}
```

> 2.定义目标切片

```go 
sliceVariables5 := make([]int,10)
```

> 3.目标切片，源切片，拷贝的数量以两个切片中最小切片的长度为准，copy(目标切片，源切片)

```go
copy(sliceVariables5,sliceVariables4)
fmt.Println(sliceVariables4)
fmt.Println(sliceVariables5)
```

##### 八、切片做为函数参数

###### 切片是引用类型

切片做为参数传递给函数的意义重大，同数组，当传递较大的数组切片时可以有效的提升cpu执行效率

```go 
func changeSlice(slice []int) {
   slice[0] = 100
}

//切片是引用类型
fmt.Println(sliceVariables5)
changeSlice(sliceVariables5)
fmt.Println(sliceVariables5)
```

##### 九、切片注意事项

> 1.切片是引用类型
> 
> 2.切片做为参数传递给函数的意义重大，同数组，当传递较大的数组切片时可以有效的提升cpu执行效率
> 
> 3.`new` 用于各种类型的内存分配 返回的是指针,`var variables = new(T)` 返回的是`T`，指针类型，即返回的是一个地址，默认是当前类型的零值，它返回了一个指针，指向新分配的类型` T `的零值。也就是说`new `返回指针。
> 
> 4.`make` 用来分配内存主要用来分配引用类型，比如`channel` ,`map` ,`slice`，返回一个有初始值 (非零) 的 `T `类型，不是`T`类型

___

### map

##### 一、map概述

`Map` 是一种无序的`key-value`键值对组成的集合。
通过` key `可以快速检索到我们需要的数据，这里的`key` 类似于索引，指向对应的数据值。

`Map` 是一种集合，所以我们可以像迭代数组和切片那样迭代它。不过，`Map` 是无序的，我们无法决定它的返回顺序，这是因为 `Map` 是使用 `hash` 表来实现的。

`map`无序是有原因的：主要是通过散列函数对`key`计算一个唯一值与值进行映射

通过散列函数对我们的map

0xc0001

0xc0002

0xc0003


> 1.无序的key-value键值对,每次循环出来的数据的顺序是不一致的，又称为集合
> 
> 2.引用类型
> 
> 3.类似perl当中的hash，python当中的字典，go当中被称为map
> 
> 4.通过key可快速找到value

##### 二、map的定义

> 1.使用方式 一般定义 map 的方法是：var map[key的类型]value的类型

```go
var mapVariables1 map[string]string
    //在使用map前，需要先make , make的作用就是给map分配数据空间,之后才可以进行引用
    mapVariables1 = make(map[string]string, 2)
    //需要特别说明的是，map中的键是唯一的，不可以重复，值可以重复
    mapVariables1["Monday"] = "周一"
    mapVariables1["Tuesday"] = "周二"
    mapVariables1["Wednesday"] = "周三"
    mapVariables1["Thursday"] = "周四"
```

> 2.使用方式 在申明同同时赋值

```go 
// 更常用的方法是使用map字面量。map的初始长度会根据初始化时指定的键值对的数量来确定。
    var mapVariables3 = map[string]int{
        "Monday": 1, "Tuesday": 2, "Wednesday": 3,
        "Thursday": 4, "Friday": 5, "Saturday": 6, "sunday": 7,
    }
```

> 3.通过短冒号（简短声明）直接make，当只需要声明一个 map 的时候，使用 make 的形式

```go 
mapVariables2 := make(map[string]string)

mapVariables2["Monday"] = "周一"
mapVariables2["Tuesday"] = "周二"
mapVariables2["Wednesday"] = "周三"
```

> 4.结构体和c类似 定义一个结构体，做为map的值

```go 
type course struct {
    courseName string //课程名称
    courseTime float32 //课程时长 单位分钟
    courseTeacher string //课程讲师
}
//定义一个结构体 变量并赋值
couser1 := course {
    //不指定结构体字段名的方式，严格按照定义结构体时的顺序
    "go语言体系课",300.3,"波哥",
}

courser2 := course {
    courseTeacher:"胡哥",
    courseTime:100.2,
    courseName:"如何变帅",
}

//定义map，key为string,value为结构体
courser := make(map[string]course)
courser["go"] = couser1
courser["美容"] = courser2
fmt.Println(courser)
```

> 5.map切片 map+切片

```go 
//interface{} 可以把它当作万能类型

var mapVariables6 []map[string]interface{}
mapVariables6 = make([]map[string]interface{},2)
mapVariables6[0] = make(map[string]interface{},2)
mapVariables6[0]["name"] = "小杨"
mapVariables6[0]["age"] = 18

mapVariables6[1] = make(map[string]interface{},2)
mapVariables6[1]["name"] = "coderyang"
mapVariables6[1]["age"] = 16
```

##### 三、map的遍历

```go  
for i :=0;i<len(sortKeys);i++ {
    fmt.Printf("mapVariables3[%s]=%d\n",sortKeys[i],mapVariables3[sortKeys[i]])
}

for key,value := range mapVariables3 {
    fmt.Println(key,value)
}
```

##### 四、map注意事项

> map如何判断一个key是否存在

```go 
value,ok := courser["go"]
    if ok {
        fmt.Println(value)
    } else {
        fmt.Println("no value")
    }
    //来语言特有的语法格式 
    if value,ok := courser["go"];ok {
        fmt.Println(value)
    }
```

> 只申明没有make,报错panic: assignment to entry in nil map

```go 
//var mapVariables6 map[string]string
    //mapVariables6["hello"] = "小杨"
    //nil null 空
```

> map是一个引用,函数传参，遵循引用类型规则


```go
map是无序的键值对类型，如何排序?

1.定义切片存储所有的key
2.通过排序算法（排序算法使用内置或者冒泡，选择等排序算法均可）对key进行排序
3.按照排序后的key打印map
```


