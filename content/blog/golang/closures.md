---
title: "Closures"
date: 2021-02-07T18:23:12+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
---

Golang supports anonymous functions which are then used to form closure functions.
Anonymous functions are function without any name. Before going any further read about ***<a href="/blog/golang/anonymous_func" style="color:DodgerBlue"> anonymous function </a>***.

Closure is a special type of function value which references variable declared outside its body. The purpose of this function is to close over a variable of upper function to form a closure. The function may access and assign to the referenced variables; in this sense, the function is "bound" to the variables.

Let's see an example.
In this example we create a closure which keeps track of page hit or say counter.

```
package main

import "fmt"

func main() {
  hit := 0

  counter := func() int {
    hit += 1 
    return hit
  }

  fmt.Println(counter())
  fmt.Println(counter())
  fmt.Println(counter())
}

```

```
1
2
3
```

In above example we bound the closure to `hit` variable which is not passed to it but accessed as global variable.

The problem with above code is, `hit` is a global variable. Hence other function has access to it. So any other operation can change the value of `hit`. To avoid this closure can isolate the data.

```
package main

import "fmt"

func main() {
  counter := Counter()
  fmt.Println(counter())
  fmt.Println(counter())
  fmt.Println(counter())
}

func Counter() func() int {
  hit := 0
  return func() int {
    hit++
	return hit
  }
}
```

```
1
2
3
```

In the above example closure is bound to or references to the `hit` variable which is still can be accessed after the function call. This means closure has access to the data and no other function has access to it and hence this data can be tracked and isolated. This is one of the benefits of closure. 

***You can refer <a href="https://github.com/pratikjagrut/go-tutorial/blob/master/11_closures/main.go" style="color:DodgerBlue" target="_blank">main.go</a> file for examples***

<hr>

<a href="/blog/golang/anonymous_func">
  <b style="color:DodgerBlue">
    <i>🡄 Anonymous Function</i>
  </b>
</a> &emsp;

<a href="/blog/golang/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<!-- <a href="/blog/golang/">
    <b style="color:DodgerBlue">
        <i> 🡆</i>
    </b>
</a>  &emsp; -->

<br>

<a href="https://github.com/pratikjagrut/go-tutorial" target="_blank">
  <b style="color:DodgerBlue" class="fab fa-github">
    <i>Github Repo</i>
  </b>
</a>  &emsp;

<a href="https://github.com/pratikjagrut/go-tutorial/blob/master/REFERENCE.md" target="_blank">
  <b style="color:DodgerBlue">
    <i>&#128279; Reference</i>
  </b>
</a>