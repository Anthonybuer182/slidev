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

# GO的特性与JAVA的差异性


---

# 目录

- 📝 **语法** - 
    - 包的导入和使用
    - 结构体,属性与修饰符
    - 函数及函数的返回值
- 🎨 **web** - 
    - api接口
- 🧑‍💻 **微服务** - 
    - 脚手架

---

# 包的导入和使用

Java是纯面向对象的使用方法和属性必须要导入类或接口，除非是lang包下的不需要导入
<br/>
Go直接导入包(路径)即可，导入后可以使用此包下面所有开放的函数和属性
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


# 结构体,属性与修饰符

Java 修饰符 变量类型 变量名
结构体通过public或protected修饰符对外暴露
<br/>
Go var 变量名 变量类型
结构体或变量名大写之后才能对外暴露  
| Java   | Go    |
|  ----  | ----  |
<div grid="~ cols-2 gap-2" m="-t-2">

```ts {all|2|1-6|9|all}
public class WQUser {
    public String name;
    public int age;
}

```

```ts {all|2|1-6|9|all}
package model

type WQuser struct {
	Name string
	Age  int16
}
```
</div>
---

# 函数的返回值和方法调用

Go 函数的返回值可以有多个 结构体和方法的关系是组合 
<br/>
Java 结构体和方法的关系是包含 
| Go 函数   | Go 方法    |
|  ----  | ----  |
<div grid="~ cols-2 gap-2" m="-t-2">

```ts {all|2|1-6|9|all}
package main

import "fmt"

func main() {
	phone, err := verify("1111111111")
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
```
```ts {all|2|1-6|9|all}
package main

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
	//  张三 今年 28
}

```
</div>
---

# 指针

Go 函数的返回值可以有多个 结构体和方法的关系是组合 
<br/>
Java 结构体和方法的关系是包含 
| Java  | Go     |
|  ----  | ----  |
<div grid="~ cols-2 gap-2" m="-t-2">

```ts {all|2|1-6|9|all}

public class Test1 {
    class User{
        String name;
    }
    public User createUser(){
        User user=new User();
        user.name="张三";
        return user;
    }
    public  User updateUser(User user){
        user.name="李四";
        return user;
    }
    public static void main(String[] args) {
        Test1 test=new Test1();
        User testUser = test.createUser();
        User updateUser = test.updateUser(testUser);
        System.out.println("地址："+testUser+" 姓名: "+testUser.name);
        System.out.println("地址："+updateUser+" 姓名: "+updateUser.name);
//        地址：Test1$User@3498ed 年龄: 李四
//        地址：Test1$User@3498ed 年龄: 李四
    }
}

```
```ts {all|2|1-6|9|all}
package main

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
	fmt.Println(p)
	fmt.Println(p1)
	// {张三 2}
	// {李四 2}
}

```
</div>
---

# 接口

Go 结构体实现的接口 需要在外面组合到结构体中
<br/>
Java 中的接口感觉就是定义了个抽象模型
| Java  | Go     |
|  ----  | ----  |
<div grid="~ cols-2 gap-2" m="-t-2">

```ts {all|2|1-6|9|all}


public class Test2 {
    void test (){
        User person=new User();
        person.say();
        person.work();
    }
    public static void main(String[] args) {
      new Test2().test();
    }

    interface Person{
        void say();
    }
    interface Worker{
        void work();
    }
    class User implements Person,Worker{
        @Override
        public void say() {
            System.out.println("说话");
        }

        @Override
        public void work() {
            System.out.println("工作");
        }
    }
}


```
```ts {all|2|1-6|9|all}
package main

import "fmt"

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
	// 说话
	// 工作
}


```
</div>

---

# Channal和协程

Go 结构体实现的接口 需要在外面组合到结构体中
<br/>
Java 中的接口感觉就是定义了个抽象模型
| Java  | Go     |
|  ----  | ----  |
<div grid="~ cols-2 gap-2" m="-t-2">

```ts {all|2|1-6|9|all}


public class Test2 {
    void test (){
        User person=new User();
        person.say();
        person.work();
    }
    public static void main(String[] args) {
      new Test2().test();
    }

    interface Person{
        void say();
    }
    interface Worker{
        void work();
    }
    class User implements Person,Worker{
        @Override
        public void say() {
            System.out.println("说话");
        }

        @Override
        public void work() {
            System.out.println("工作");
        }
    }
}


```
```ts {all|2|1-6|9|all}
package main

import "fmt"

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
	// 说话
	// 工作
}


```
</div>
---

# 闭包

Go 结构体实现的接口 需要在外面组合到结构体中
<br/>
Java 中的接口感觉就是定义了个抽象模型
| Java  | Go     |
|  ----  | ----  |
<div grid="~ cols-2 gap-2" m="-t-2">

```ts {all|2|1-6|9|all}


public class Test2 {
    void test (){
        User person=new User();
        person.say();
        person.work();
    }
    public static void main(String[] args) {
      new Test2().test();
    }

    interface Person{
        void say();
    }
    interface Worker{
        void work();
    }
    class User implements Person,Worker{
        @Override
        public void say() {
            System.out.println("说话");
        }

        @Override
        public void work() {
            System.out.println("工作");
        }
    }
}


```
```ts {all|2|1-6|9|all}
package main

import "fmt"

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
	// 说话
	// 工作
}


```
</div>

