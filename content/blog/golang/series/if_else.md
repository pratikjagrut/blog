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
  - "2020"
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
***<a href="https://play.golang.org/p/YO_-cELIUii" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***
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
***<a href="https://play.golang.org/p/Fj2fjOaeNZy" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

### if-else-if ladder

We can use multiple conditional statement at once which.

```
package main

import "fmt"

func main(){
  i := -11
  if i == 0 {
    fmt.Println("It's zero")
} else if i < 0 {
    fmt.Println("Negative number")
} else {
    fmt.Println("Positive number")
}
}
```
***<a href="https://play.golang.org/p/kL1RyoKUzF-" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

### If with a short statement

```
package main

import "fmt"

func main() {
	if j := 10; j%2 == 0 {
		fmt.Println("Even number")
	}
} 
```
***<a href="https://play.golang.org/p/f6SyTAE1Rtz" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

***Thank you for reading this blog please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/series/for_loop">
  <b style="color:DodgerBlue">
    <i>🡄 Looping Construct</i>
  </b>
</a> &emsp;

<a href="/blog/golang/series/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/series/switch">
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