---
title: "Conditional Statements"
date: 2020-12-21T22:18:32+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
---

Conditional Statements are part of every programming language. 
They help us to decide which instruction is suppose to run when certain condition is met. 
*e.g. If I'm hungry then I'll eat else I'll wait.*
*e.g. If score is greater than 35%, you passed, else you failed.*

### If statement in Go

```
if condition/expression {
    //instruction to be performed
}
```

Condition needs to be true to perform the given set of instructions.

```
package main

import "fmt"

func main(){
  i := 10
  if i % 2 == 0 {
    fmt.Printf("%d is a even number", i)
  }
}
```

### If-Else statement in Go

```
if condition/expression {
    //instruction to be performed
} else {
    //instruction to be performed
}
```

If condition need to be false to perform instruction from else block.

```
package main

import "fmt"

func main(){
  i := 11
  if i % 2 == 0 {
    fmt.Printf("%d is a even number", i)
  } else {
    fmt.Printf("%d is a odd number", i)
  }
}
```

### if-else-if ladder

We can use multiple conditional statement at once which.

```
if i == 0 {
    fmt.Println("It's zero")
} else if i < 0 {
    fmt.Println("Negative number")
} else {
    fmt.Println("Positive number")
}
```

### If with a short statement

```
if j := 10; j%2 == 0 {
	fmt.Println("Even number")
} 
```

***You can refer <a href="https://github.com/pratikjagrut/go-tutorial/blob/master/04_if_else/main.go" style="color:DodgerBlue" target="_blank">main.go</a> file for examples***

<hr>

<a href="/blog/golang/for_loop">
  <b style="color:DodgerBlue">
    <i>🡄 Looping Construct</i>
  </b>
</a> &emsp;

<a href="/blog/golang/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/switch">
    <b style="color:DodgerBlue">
        <i>Switch Statement 🡆</i>
    </b>
</a>  &emsp;

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