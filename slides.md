---
# try also 'default' to start simple
theme: seriph
# random image from a curated Unsplash collection by Anthony
# like them? see https://unsplash.com/collections/94734566/slidev
background: https://source.unsplash.com/collection/94734566/1920x1080
# apply any windi css classes to the current slide
class: 'text-center'
# https://sli.dev/custom/highlighters.html
highlighter: shiki
# show line numbers in code blocks
lineNumbers: false
# some information about the slides, markdown enabled
info: |
  ## Slidev Starter Template
  Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
# persist drawings in exports and build
drawings:
  persist: false
# page transition
transition: slide-left
# use UnoCSS
css: unocss
---
<style>
pre {
  overflow-y: auto;
  max-height: 350px;
}
</style>
# GO的特性与JAVA的差异性


---

# 目录
-  **介绍** - 
    - 背景及特性
-  **语法** - 
    - 包的导入和使用
    - 结构体与类型
    - 函数和方法
    - 匿名函数与闭包
    - 指针与值
    - 匿名字段和接口
    - goroutine与channel
-  **web** - 
    - api接口
- **微服务** - 
    - 脚手架
---

# 背景及特性

**Go语言适合用于服务端开发、分布式系统、网络编程、⼤数据开发、运维开发、区块链开发、云平台等领域**
<br/>
- Go语言实现了开发效率与执行效率的完美结合

- Go语言在多核并发上拥有原生的设计优势

- Go被描述为“C 类似语言”，从C语言中继承了很多思想

---

# 包的导入和使用

**Java是纯面向对象语言，一般需要导入相关类，才能使用此类下的方法和属性**
<br/>
**Go直接导入包(路径)即可，导入后可以使用此包下面所有开放的函数和属性**
<br/>
| Java   | Go  |
|  ----  | ----  |
<div grid="~ cols-2 gap-2" m="-t-2">

```ts {all|2|1-6|9|all}
import java.util.Date;
import java.util.ArrayList;

public class Test {
    public static void main(String[] args) {
        System.out.println(new Date());
        System.out.println(new ArrayList<String>());
    }
}
```

```ts {all|2|1-6|9|all}
package main

import (
	"fmt"
	"time"
)

func main() {
	// time/time.go/Now()
	fmt.Println(time.Now())
	// time/sleep.go/Sleep()
	time.Sleep(time.Second)
}
```
</div>

---

# 结构体与类型

**Go 结构体成员变量： 变量名 变量类型**
<br/>
**Go 定义类型与类型别名**
| Go 结构体  | Go 类型      |
|  ----  | ----  |
<div grid="~ cols-2 gap-2" m="-t-2">

```ts {all|2|1-6|9|all}
import "fmt"

type WQuser struct {
	Name   string
	Age    int16
	Gender interface{}
}

func main() {
	user1 := WQuser{Name: "张三", Age: 12, Gender: "男"}
	user2 := WQuser{"李四", 13, "女"}
	fmt.Println(user1)
	fmt.Println(user2)

}

// {张三 12 男}
// {李四 13 女}
```

```ts {all|2|1-6|9|all}
import "fmt"

// 定义类型 基于unit8生成一个新的类型
type byte uint8

//类型别名 为已存在的类型 定义一个别名
type mybyte = uint8

func main() {
	var p uint8 = 1
	var g byte = 1
	var m mybyte = 1
	fmt.Printf("p的类型：%T\ng的类型：%T\nm的类型：%T", p, g, m)

}

// p的类型：uint8
// g的类型：main.byte
// m的类型：uint8
```
</div>

---

# 函数和方法

**Go 函数的返回值可以有多个**
<br/>
**Go 方法是作用在接收者(receiver)上的一个函数，所以结构体和方法是组合关系**
| Go 函数   | Go 方法    |
|  ----  | ----  |
<div grid="~ cols-2 gap-2" m="-t-2">

```ts {all|2|1-6|9|all}
import "fmt"

func main() {
	phone, err := verify("1")
	if err != "" {
		fmt.Println(err)
	} else {
		fmt.Println(phone)
	}
}
// 校验手机号长度
func verify(phone string) (string, string) {
	var errorMsg string
	if len(phone) < 11 {
		errorMsg = "手机号长度不够"
	}
	return phone, errorMsg
}

// 手机号长度不够
```
```ts {all|2|1-6|9|all}
import "fmt"

type user struct {
	name string
	age  int8
}

func (u user) dec() {
	fmt.Println(u.name, "今年", u.age)
}
func main() {
	u := user{"张三", 28}
	u.dec()
}

//  张三 今年 28

```
</div>
---

# 匿名函数与闭包

Go 匿名函数: 不需要定义函数名的一种函数
<br/>
Go 闭包: 引用了外部自由变量的匿名函数
| Go 匿名函数  | Go 闭包     |
|  ----  | ----  |
<div grid="~ cols-2 gap-2" m="-t-2">

```ts {all|2|1-6|9|all}
import "fmt"

func main() {
	func(x, y int) {
		fmt.Println(x + y)
	}(18, 20) //函数定义完加()立即执行
}

// 38
```
```ts {all|2|1-6|9|all}
import "fmt"

func outer() func() int {
	num := 0
	inner := func() int {
		num++
		fmt.Print(num)
		return num
	}
	return inner
}

func main() {
	i := outer()
	i()
	i()
	i()
}

// 1
// 2
// 3
```
</div>

---

# 指针与值
Go 函数和方法是值传递 但map，slice隐式指针传递
<br/>
Java 结构体和方法的关系是包含 
| Java  | Go     |
|  ----  | ----  |
<div grid="~ cols-2 gap-2" m="-t-2">

```ts {all|2|1-6|9|all}
public class Test2 {
	class User{
    	String name;
	}
    public static User updateUser(User user){
        user.name="李四";
        return user;
    }
    public static void main(String[] args) {
        User user=new User();
        user.name="张三";
        User newUser = updateUser(user);
        System.out.println("地址:"+user+" 姓名:"+user.name);
        System.out.println("地址:"+newUser+" 姓名:"+newUser.name);
    }
}
//        地址:Test1$User@3498ed 年龄:李四
//        地址:Test1$User@3498ed 年龄:李四


```
```ts {all|2|1-6|9|all}
import "fmt"

type person struct {
	name string
	age  int8
}
// func createPerson(p1 *person) *person {
func createPerson(p1 person) person {
	p1.name = "李四"
	return p1
}
func main() {
	p := person{"张三", 2}
	p1 := createPerson(p)
	fmt.Print(p)
	fmt.Println(p1)
}
// {张三 2} {李四 2}
```
</div>

---

# 匿名字段和接口

Go 匿名字段可获得和继承类似的复用能力
<br/>
Go 接口定义了一个对象的行为规范，而由具体的对象来实现规范的细节
| Go 匿名字段  | Go 接口     |
|  ----  | ----  |
<div grid="~ cols-2 gap-2" m="-t-2">

```ts {all|2|1-6|9|all}
import (
	"fmt"
)

type Worker struct {
	Name string
}
func (u Worker) work() {
	fmt.Println("work", u.Name+"工作")
}

type User struct {
	Worker
}
func (u User) say() {
	fmt.Println("user", u.Name+"说话")
}
func (u User) work() {
	fmt.Println("user", u.Name+"工作")
}

func main() {
	u := User{Worker{Name: "张三"}}
	u.say()
	u.work()
}

// user 张三说话
// user 张三工作
```
```ts {all|2|1-6|9|all}
type Person interface {
	say()
}
type Worker interface {
	work()
}
type User struct{}

func (u User) say() {
	fmt.Println("说话")
}
func (u User) work() {
	fmt.Println("工作")
}
func main() {
	u := User{}
	u.say()
	u.work()
}
// 说话
// 工作
```
</div>

---

# goroutine与channel

**Go goroutine(协程),可同时运行成千上万个并发任务，并合理地将任务分配给每一个CPU**
<br/>
**Go channel 通道（channel）是一种特殊的类型,理解为数据流管道或者消息队列**
| Go goroutine  | Go channel    |
|  ----  | ----  |
<div grid="~ cols-2 gap-2" m="-t-2">

```ts {all|2|1-6|9|all}
import (
	"fmt"
	"sync"
)

var wg sync.WaitGroup

func asyncTask() {
	fmt.Println("asyncTask groutine")
	defer wg.Done() //把计算器-1
}

func main() {
	wg.Add(1) //把计数器+1
	go asyncTask()
	fmt.Println("main groutine")
	wg.Wait() //阻塞代码的运行，直到计算器为0
	fmt.Println("程序结束")
}

// main groutine
// asyncTask groutine
// 程序结束
```
```ts {all|2|1-6|9|all}
import (
	"fmt"
	"time"
)
// goroutine耗时业务处理
func async(data int, c chan int) {
	time.Sleep(3 * time.Second)
	c <- data + 1
}

func main() {
	c := make(chan int)
	var data int = 1
	go async(data, c)
	msg := <-c
	fmt.Println(msg) 
}
// 2
```
</div>


---

# Beego

beego 是一个mvc架构，基于RESTFul框架可以快速开发API、Web、后端服务等各种应用。

<div grid="~ cols-2 gap-2" m="-t-2">

```yaml
beego web服务架构
```

```yaml
beego 脚手架生成的web项目目录结构
```

<img border="rounded" src="https://camo.githubusercontent.com/14fade415c38fccdd33c05649ad23e57c5f2f058f8b5c66fcfaf010969e2620e/68747470733a2f2f63646e2e6e6c61726b2e636f6d2f79757175652f302f323032302f706e672f3735353730302f313630373835373436323530372d38353565633534332d376365332d343032642d613063622d6232353234643561346236302e706e67">

<img border="rounded" src="https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/9abeb70c7e424ddebea2d50f4667b441~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp?">
</div>

---

# go-zero

集各种工程实践于一身的web和rpc框架。

<div grid="~ cols-2 gap-2" m="-t-2">

```yaml
go-zero 微服务架构
```

```yaml
go-zero 微服务项目目录结构
```
<img border="rounded" src="https://go-zero.dev/cn/img/pages/index/arch-cn.svg">
<img  src="https://i.postimg.cc/906HS7zm/microbg.jpg" >
<img border="rounded" src="https://user-images.githubusercontent.com/1918356/171880372-5010d846-e8b1-4942-8fe2-e2bbb584f762.png">

</div>


