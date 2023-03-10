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

# 函数及函数的返回值

Go 函数的返回值可以有多个

<div grid="~ cols-1 gap-2" m="-t-2">

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
</div>
