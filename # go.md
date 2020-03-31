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
# go 并发
##原理
go 搭建了一个特有的两级线程模型

### Linux 线程
Linux线程可以对其他线程进行有限的管理  ** linux中线程和进程本质上是一样的 线程是轻量级进程
**  有限管理主要有四种
1.创建线程 任何线程都可以调用系统调用pthread_creat 来创建新的线程
2.终止线程 线程可以通过多种方法终止其他线程 常用的pthread_canle 他会向目标线程发送取消线程的请求，发送请求后立即返回，不会等待目标线程做出回应。默认情况下， 目标线程总是会响应请求
3.连接已终止的线程 此操作有**系统** 调用pthread_join 该函数会一直等待目标线程终止，如果已经终止则立即返回。实际上如果一个线程能被连接，那么它终止是必须连接否则就会变成一个僵尸线程
4.分离线程 分离线程就是让一个线程变成不能被连接，分离操作另一个作用就是让系统在线程终止时自动进行清理和销毁
### Linux 线程工作流程示意图
![示意图](/home/yue/Pictures/Linux线程执行示意图.png)
### Linux  线程调度
线程的执行总是趋向于cpu受限或者io受限
一般情况下 io受限会获得更高的动态优先级
动态优先级可以实时调整，静态优先级则只能有程序指定，动态优先级就是调度器静态优先级上基础上调整而来
所有等待使用cpu的线程都会按照动态优先级排列，并按照顺序放到与该cpu对应的运行队列中，一次下一个运行的总是动态优先级最高的 
运行队列有两个 一个是等待运行的线程队列 称之为激活队列， 另一个是运行运行过但是还没有完成的队列  称为过期队列
优先级队列是若干个链表组成的数组，一个链表只会包含相同动态优先级的线程，如果有新的线程就会加到相应优先级的链表的末尾
![线程运行队列内部结构示意图](/home/yue/Pictures/线程运行队列的内部结构示意图.png)
如果调度器发现某个线程占用cpu很长时间，并且相同优先级队列有线程等待，就会执行等待线程，并把该线程放到过期队列
当激活队列线程执行完，过期队列变成激活队列，原来的激活队列就变成过期队列。保证过期队列中也会执行
线程会由于阻塞进入休眠状态，休眠状态不能够被调度执行，从运行队列中移除，进入等待队列，当事件发生或者条件满足,等待队列中的线程会进入运行队列，并调高一点优先级


## 线程模型实现
1.用户级线程模型  线程有用户级别的线程库管理，只有一个KSE对应。
2.内核级线程模型
3.两级线程模型
![线程模型示意图](/home/yue/Pictures/三种线程模型示意图.png)

## 不要用共享内存的方式来通信， 用通信来共享内存

## go 线程模型
1.M machine 代表内核线程 
2.P 上下文环境 代表Go代码片段(goroutine)的所必要的资源
3.G goroutine 一个G 代表一个Go代码片段 前者是后者的封装
G的执行需要M和P的支持 一个M和一个P关联后就形成了一个有效的G运行环境(内核线程和上下文)，每个P都会包含一个可运行的G队列(runq)该队列的G会依次传递与P关联的M并获得运行时机 
![MPG示意图](/home/yue/Pictures/MPG.png)

M 在创建的时候会加入到全局的M列表(runtime.allm)中 起始函数和预连P也会被设置，创建内核线程与之关联 M就为执行G做好了准备 M创建后会对它进行初始化，并关联P

运行时的M停止的时候会加入到空闲M列表(runtime.sched,midle)中 当需要一个新的M时会先从runtime.sched.midle获取如果获取不到才会创建

P  P是G能够在M上运行的关键，go的运行时系统会让P与不同的M建立或断开连接，让P的那些G能够及时获得运行时机

P也有P列表(runtime,allp) 和 P空闲列表(runtime.sched.pidle ) 加入到P空闲列表的条件是P的可运行G队列为空 ，一个G启用时会加入某个P的可运行队列
P与M不同 他有状态
1.Pidle 没有和M关联
2.Prunning 和一个M关联
3.Psyscall P中运行的G正在进行系统调用
4.Pgcstop 运行时系统要停止调度
5.Pdead 这个P不会在使用 列如程序中调用减少P的最大数量的函数
![P状态转换示意图](/home/yue/Pictures/p的状态转换.png)

新创建的处于Pgcstop状态，这个状态极短在进行初始化后状态变为Pidle并放入空闲P列表中，运行时系统停止调度也会处于Pgstop 状态 需要重启调度时会把状态变同意转换为pidle 他们会处于同一起跑线上 

P上有可运行G列表，和自由G列表 自由G列表包含一些运行完成的G，随着运行完成的G的增多自由G列表会很长，到达一定长度后会把一些G转移到系统调度器的自由G列表中。每当go语句中要启用一个G，会从当前P中自由G列表获取一个G来封装go语句所带的函数，如果P中没有自由G会从系统调度器中的自由G列表转移一些自由G到P中的自由G列表，如果P中的自由G列表和系统调度器中的自由G列表为空时，才会创建一个新的G，这样提高了G的复用

G 一个G就是一个goroutine   运行时系统会先检查go函数以及参数的合法性然后去P和调度器中的自由G列表获取可用的G如果没有获取到就新建一个G与M和P相同G也有一个全局的（runtime.allgs)新建的G会放入到全局列表中 然后G进行初始化，然后加入到P的下一个可执行G 如果下一个可执行G已经存在就会加入P的可运行G列表末尾，如果可运行队列已满，就只能加入到调度器的可运行G队列中












































