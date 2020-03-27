# **go语言中只有slice map 和channel是引用类型其它都是值类型包括结构体**

# 变量

变量必须先声明在使用
**声明后必须使用**

## 变量声明方式

	1 var 变量名 变量类型
## 声明多个变量

var (
	变量名 变量类型
	变量名 变量类型
)
	

```go
var s1 string
```
```go
var (
   	s1 string
	age int
)
```



## 驼峰命名

## 声明变量同时并命名
```go
    `var s1 string = "jack"`
```
## 类型推导	
```go
var name ="jack" 
```
## 简短声明

**简短声明不能声明全局变量**
	

```go
name := "jack"
```



## 匿名变量

	匿名变量不占空间 不会分配内存 所以不存在重复命名
	`_ , x := foo()`

## 注意事项
**函数外的每个语句必须以关键字开始(var func const)**
**简短声明不能使用在函数外**
**_多用于占位表示忽略**
# 常量

## 声明
const 常量名 = 值
**常量声明时必须赋值**
```go
const pi = 3.1415926
```
**批量声明常量时，如果某一行没有赋值 默认和上一行一致**
```go
const (
	n1 = 100
	n2
	n3
)
```
## iota
**iota在const关键字出现的时候被重置为0**
**const中没新增一行 iota+1**
```go
const (
	n1 = iota
	n2   
	n3
)
```
n2默认和上一行一样n2=2 同理 n3=3
定义数量级
```go
const(
	_ = iota
	kb = 1 << (10 * iota)
	mb = 1 << (10 * iota)
	gb = 1 << (10 * iota)
	tb = 1 << (10 * iota)
)
```
## 整形 浮点型 （略）
## bool
默认false
** go 语言中不允许 讲bool 型转换成整形**
bool 类型无法参与运算也无法与其他类型进行转换
bool 只有true 和false
```go
b1 := true
var b2 bool
```
## 字符串
go 语言中 字符串是原声类型 与int float一样
内部使用utf-8
```go
s1 := "hhaha"
```
**字符串类型必须使用双引号**
转义 使用\
`` 里面的内容原样输出
```go
s1 := `http://www.baidu.com`
```
### 字符串的常用操作
方法 | 介绍
--|--:
len(str)|求长度
+或fmt.Sprintf|拼接字符串
split|分割
contains|判断是否包含
HasPrefix/HasSuffix|前缀后缀判断
Index()/LastIndex()|字符出现的位置
strings.join(a[]string,sep string)|join操作
## 修改字符串
**需要将字符串转换成[]byte 或者[]rune都将重新分配内存并复**
## 类型转换
T(表达式)
```go
s1 := "hello"
s2 := []rune(s1)
s2[0] = '语'
s1 = string(s2)
```
# 流程控制

## if else
	if 表达式 {
		代码块
	}else{
		代码块
	}
```go
if age > 18{
	fmt.Println("age > 18")
}else{
	fmt.Println("age <= 18")
}
```
## if else if 
if 表达式 {
    
}else if 表达式{
    
}else if 表达式{
    
}else{
    
}
# for 循环

## 基本格式
	for 初始语句;条件表达式;结束语句 {
		循环体语句
	}
```go
for i := 0;i <= 12;i++{
	
}
```
## for range
可以遍历数组切片字符串map 通道
数组 切片 字符串 返回索引和值
map 返回键和值
通道只返回值

for i,v := range s{
	循环体语句
}
break continue 和其他语言类似
# switch case
	switch expr {
		case expr 
	}
```go
switch n {
	case 1:
		fmt.Println("1")
	case 2:
		fmt.Println("2")
	case 3:
		fmt.Println("3")
	case 4:
		fmt.Println("4")
	default:
		fmt.Println("exit")
	}
```
# 运算符

# Array
存放像**相同类型**元素的容器，必须指定长度
**长度是数组的一部分**
## 声明
var    数组名   [长度] 类型
```go
var array1 [10]int32
```
## 初始化
如果不初始化数组有默认值
1.先声明 在初始化   变量名=[长度]类型{value1,value2.....}
```go 
var b1 [3]bool
b1=[3]bool{true,true,true}
```
2.根据初始值自动判断数组的长度
```go
b2 := [...]bool{true,false,true}
```
3.根据索引来初始化
```go
b3 := [5]int{0:1,1:3}
```
## 数组的遍历
1.根据索引遍历
```go
citys := [...]string{"上海","北京","杭州"}
for i := 0;i < len(city);i++{
	fmt.Println(city[i])
}
```
2. for range遍历
```go
citys := [...]string{"上海","北京","杭州"}
for i,v := range citys{
	fmt.Println(i,v)
}
```
## 多维数组

## 数组是值类型
**数组是值类型，赋值和传参会复制整个数组，因此改变副本的值，本身的值不变**
```go
array1 := [...]int {1,2,3}
array2 := array1
array2[0] = 100
fmt.Println(array1,array2)
```
# 切片 slice
拥有相同元素的可变 长度的数列，基于数组的封装，可以自动扩容非常灵活，是一个引用类型 
包含长度 地址 容量
## 声明
var 变量名 [ ]T
```go
var arr []int
```
## 初始化
```go
arr = []int{1,2,3}
```
## 长度和容量
len(), cap()
## 基于数组/切片得到切片
arr[number1:number2] 包含number1，不包含number2 ,number，number2可缺省 arr是原数组或切片
```go
arr1 := arr[1:3]
arr2 := arr[2:]
arr3 := arr[:3]
```
**切片指向体层数组**
**切片的长度等于元素的个数**
**切片的容量等于从切片的第一个元素到*原数组或切片*的最后一个元素**
## make
make([]T,len,cap) cap 可缺省
```go
arr := make([]int,3,5)
arr := make([]int,3) cap==len
```
## 切片的赋值拷贝
切片是一个引用了类型
## 切片的遍历

[TOC]



```go
for i := 0;i < len(arr);i++{
	fmt.Println(i,arr[i])
}
for i,v := range arr{
		fmt.Println(i,arr[i])
}
```
## make 和new 的区别
1.make new 都是分配内存
2.make 只能用于 slice map channel
3.new 返回的是一个指针类型 make 返回的是本身类型的一个引用
[make和new](https://sanyuesha.com/2017/07/26/go-make-and-new/)

#map

## 声明
map[T]T   key value
**引用类型必须初始化*map slice channel* **
## 遍历
for range
```go
var m1 map[int]int
m1 = make(map[int]int, 10)
for i := 0; i < 10; i++ {
  	m1[i] = i
}
for k, v := range m1 {
	fmt.Println(k, v)
}
```
## 删除
delete(map,key)
```go
delete(m1,1)
```
#函数
go 可以返回多个返回值

## defer
当有多个defer按声明的逆序执行
### defer执行时机
![defer执行时机](/home/yue/Pictures/defer执行时机.png)
## 函数作为参数和返回值
```go
func f1(x, y int) int {
	return x + y
}
func f2(f func(int,int) int ){
	f(6,7)
}
```
**函数内不能有声明的函数可以有匿名函数**
```go
func f3() {
	total := func(x, y int) int {
		return x + y
	}(6,7)
	fmt.Println(total)
}
```
## 闭包
[闭包详解](https://zhuanlan.zhihu.com/p/92634505)

# 结构体

**结构体是值类型**
## 声明
type 类型名 struct{
	字段名 字段类型
	字段名 字段类型
	字段名 字段类型
}

## 匿名结构体
多用于一些临时情况
### 匿名结构体声明
var 类型名 struct{
	字段名 字段类型
	字段名 字段类型
	字段名 字段类型	
}
```go
func main(){
	var person struct{
		name string
		age int
	}
	person.name = "jetty"
	person.age = 12
	fmt.Println(person)
}
```

## 创建指针类型的结构体
可以通过new对结构体进行实例化得到的是结构体的指针
```go
var p = new(person)
*p.name = "jetty"
*p.age =12
```
也可以是用&取地址
```go
p := &person{}
```
## 结构体初始化
### 键值对初始化
```go
p := person{
	name : "jetty",
	age : 12,
}
//也可以对结构体的指针初始化
p1 := &person{
	name : "jetty1",
	age :12,
}
```
*结构体的字段不写就是默认值*
## 结构体的内存布局
**结构体占用一块连续的内存**
[在 Go 中恰到好处的内存对齐](https://zhuanlan.zhihu.com/p/53413177)

## 方法和接收者
*方法是作用于特定类型的函数*
*接收者是表示调用该方法的具体类型变量*
func (接收者名 T) 方法名(参数列表) (返回列表){}
```go
func (d dog) say{
	fmt.Println(d.name)
}
```
**结构体变量名如果大写表示公有**
**标识符如果大写表示公有**
**标识符 变量名 类型名 函数名 方法名**

#接口
**接口是一种类型，是一个特殊类型了它规定了实现街口的变量有的方法**
*只要实现了接口的方法就实现了接口*
## 接口的定义
```go
type 接口名 interface{
	方法名1(参数列表)(返回值列表)
	方法名1(参数列表)(返回值列表)
} 
```
## 接口的实现
一个变量实现了接口**所有**的方法就说这个变量实现了接口
## 值接收者实现接口与指针接收者实现接口的区别
值接收者实现接口 值类型和指针类型都能保存
指针类型实现接口只能保存指针类型

```go
type animal interface {
       eat()
       move()
 }
 func (d dog) eat(){
 	fmt.Println("dog")
 }
 
 
 func main(){
 	d := newDog("jetty",12)//自己定义的构造函数
 	d1 := d
    d1.eat()   
 }
```











































