# 基本类型

## 数字

* Double   64Bit
* Float    32Bit
* Long     64Bit
* Int      32Bit
* Short    16Bit
* Byte     8Bit

### 字面常量

十进制：123，123L

十六进制： 0x0F

二进制： 0b0010101

> Kotlin不支持八进制

double： 12.5
float: 12.5f,12.5F

### 数字字面值中的下划线

val oneMillion = 1_000_000  
val creditCardNumber = 1234_5678_9012_3456L  
val socialSecurityNumber = 999_99_9999L  
val hexBytes = 0xFF_EC_DE_5E  
val bytes = 0b11010010_01101001_10010100_10010010  

### 显示转换

每个数字类型支持如下的转换:

toByte(): Byte  
toShort(): Short  
toInt(): Int  
toLong(): Long  
toFloat(): Float  
toDouble(): Double  
toChar(): Char  

## 字符

Char
> 不能当数字使用，但是可以显示转换：val c:Char = '1'  val i: Int = c.toInt()

## 布尔
Boolean:只有两个值：true和false

### 布尔运算
* ||  或
* &&  与
* ！  非

## 数组

数组在 Kotlin 中使用 Array 类来表示  

## 字符串

String 

> 转义采用传统的反斜杠方式

>原生字符串 使用三个引号（"""）分界符括起来，内部没有转义并且可以包含换行和任何其他字符:
```
val text = """
    for (c in "foo")
        print(c)
"""
```
### 字符串模板

字符串可以包含模板表达式 ，即一些小段代码，会求值并把结果合并到字符串中。 模板表达式以美元符（$）开头，由一个简单的名字构成:
```
val i = 10
val s = "i = $i" // 求值结果为 "i = 10"
```
或者用花括号括起来的任意表达式:
```
val s = "abc"
val str = "$s.length is ${s.length}" // 求值结果为 "abc.length is 3"
```
原生字符串和转义字符串内部都支持模板。 如果你需要在原生字符串中表示字面值 $ 字符（它不支持反斜杠转义），你可以用下列语法：
```
val price = """
${'$'}9.99
"""
```



# 语句

## in关键字的使用

判断一个对象是否在某一个区间内  

//判断x在[1,10]之间  

`  if(x in 1..10) `    



//判断想不在[1,10]之间  

`if(x !in 1..10)`    

//遍历集合  

`for(name in names)`

## 控制流

### if表达式

```
// 传统用法
var max = a 
if (a < b) max = b

// With else 
var max: Int
if (a > b) {
    max = a
} else {
    max = b
}
 
// 作为表达式
val max = if (a > b) a else b
```

if的分支可以是代码块，最后的表达式作为该块的值：

```
val max = if (a > b) {
    print("Choose a")
    a
} else {
    print("Choose b")
    b
}
```
> 如果你使用 if 作为表达式而不是语句（例如：返回它的值或者把它赋给变量），该表达式需要有 else 分支。

### When 表达式

when 取代了类 Java 语言的 switch 操作符。其最简单的形式如下：

```
when (x) {
    1 -> print("x == 1")
    2 -> print("x == 2")
    else -> { // 注意这个块
        print("x is neither 1 nor 2")
    }
}
```

when 将它的参数和所有的分支条件顺序比较，直到某个分支满足条件。 when 既可以被当做表达式使用也可以被当做语句使用。如果它被当做表达式， 符合条件的分支的值就是整个表达式的值，如果当做语句使用， 则忽略个别分支的值。（像 if 一样，每一个分支可以是一个代码块，它的值是块中最后的表达式的值。）

如果其他分支都不满足条件将会求值 else 分支。 如果 when 作为一个表达式使用，则必须有 else 分支， 除非编译器能够检测出所有的可能情况都已经覆盖了。

如果很多分支需要用相同的方式处理，则可以把多个分支条件放在一起，用逗号分隔：

```
when (x) {
    0, 1 -> print("x == 0 or x == 1")
    else -> print("otherwise")
}
```

我们可以用任意表达式（而不只是常量）作为分支条件

```
when (x) {
    parseInt(s) -> print("s encodes x")
    else -> print("s does not encode x")
}
```
我们也可以检测一个值在（in）或者不在（!in）一个区间或者集合中：

```
when (x) {
    in 1..10 -> print("x is in the range")
    in validNumbers -> print("x is valid")
    !in 10..20 -> print("x is outside the range")
    else -> print("none of the above")
}
```
另一种可能性是检测一个值是（is）或者不是（!is）一个特定类型的值。注意： 由于智能转换，你可以访问该类型的方法和属性而无需任何额外的检测。

```
fun hasPrefix(x: Any) = when(x) {
    is String -> x.startsWith("prefix")
    else -> false
}
```
when 也可以用来取代 if-else if链。 如果不提供参数，所有的分支条件都是简单的布尔表达式，而当一个分支的条件为真时则执行该分支：

```
when {
    x.isOdd() -> print("x is odd")
    x.isEven() -> print("x is even")
    else -> print("x is funny")
}
```

### For 循环

for 循环可以对任何提供迭代器（iterator）的对象进行遍历，这相当于像 C# 这样的语言中的 foreach 循环。语法如下：

`for (item in collection) print(item)`

循环体可以是一个代码块。  
```
for (item: Int in ints) {
    // ……
}
```

如上所述，for 可以循环遍历任何提供了迭代器的对象。即：

* 有一个成员函数或者扩展函数 iterator()，它的返回类型
* 有一个成员函数或者扩展函数 next()，并且
* 有一个成员函数或者扩展函数 hasNext() 返回 Boolean。
* 这三个函数都需要标记为 operator。

对数组的 for 循环会被编译为并不创建迭代器的基于索引的循环。

如果你想要通过索引遍历一个数组或者一个 list，你可以这么做：

```
for (i in array.indices) {
    print(array[i])
}
```
注意这种“在区间上遍历”会编译成优化的实现而不会创建额外对象。

或者你可以用库函数 withIndex：
```
for ((index, value) in array.withIndex()) {
    println("the element at $index is $value")
}
```

### While 循环

while 和 do..while 照常使用  
```
while (x > 0) {
    x--
}

do {
  val y = retrieveData()
} while (y != null) // y 在此处可见
```
# 返回和跳转

Kotlin 有三种结构化跳转表达式：

* return。默认从最直接包围它的函数或者匿名函数返回。
* break。终止最直接包围它的循环。
* continue。继续下一次最直接包围它的循环。

## Break 与 Continue 标签

```
loop@ for (i in 1..10) {
            for (j in 4..10) {
                if (i==j) break@loop else println("$i====>>>>>>>$j")
            }
        }
跳出第一个for循环
		 for (i in 1..10) {
            loop@ for (j in 4..10) {
                if (i==j) break@loop else println("$i====>>>>>>>$j")
            }
        }
跳出里边的for循环
```

> 标签限制的 break 跳转到刚好位于该标签指定的循环后面的执行点。 continue 继续标签指定的循环的下一次迭代。

## 标签处返回

```
fun foo() {
    listOf(1, 2, 3, 4, 5).forEach {
        if (it == 3) return // 非局部直接返回到 foo() 的调用者
        print(it)
    }
    println("this point is unreachable")
}
```
这个 return 表达式从最直接包围它的函数即 foo 中返回。不会打印“this point is unreachable”

```
fun foo() {
    listOf(1, 2, 3, 4, 5).forEach lit@{
        if (it == 3) return@lit // 局部返回到该 lambda 表达式的调用者，即 forEach 循环
        print(it)
    }
    print(" done with explicit label")
}
}
```
结束forEach循环，继续执行foo下边的方法，会打印“done with explicit label”



# 函数

## 函数的声明

函数使用`fun`声明，返回值位于参数括号之后`:Type`，如果返回值为空可以省略或者使用`:Unit`代替

```kotlin
fun functionName(param1: Int,param2: String):Unit{
    
}
```

如果函数只有一行表达式，可以简写：

`fun add(a: Int,b: Int) = a + b`

### 默认参数

```kotlin
fun say(firstName: String = "Jack"): String = firstName
```

调用的时候可以直接调用`say()`即可，会使用默认参数Jack，也可以传入参数`say("Tom")`

### 变参函数

在Kotlin中使用`vararg`关键字来表示变长参数

```kotlin
fun strAppend(vararg strArr: String): String{
    for (str in strArr){
        return ...
    }
}
```

### 扩展函数

普通的函数名前添加被扩展的类名，为类扩展新的函数

```kotlin
fun Activity.toast(msg: CharSwquence, duration: Int = Toast.LENGTH_SHORT){
	Toast.makeText(this,msg,dutation).show()    
}
```

