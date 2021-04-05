---
title: "Closures"
date: 2021-02-14T19:08:25+05:30
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

The closure is a special type of function value which references variable declared outside its body. The purpose of this function is to close over a variable of upper function to form a closure. The function may access and assign to the referenced variables; in this sense, the function is "bound" to the variables.

Let's see an example.
In this example, we create a closure which keeps track of page hit or as a counter.

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
***<a href="https://play.golang.org/p/RT9Pm82Kf3p" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

In the above example, we bound the closure to `hit` variable which is not passed to it but accessed as a global variable.

The problem with the above code is, `hit` is a global variable. Hence another function has access to it. So any other operation can change the value of `hit`. To avoid this closure can isolate the data.

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
***<a href="https://play.golang.org/p/s5THHqJzD-Y" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

In the above example closure is bound to or references to the `hit` variable which is still can be accessed after the function call. This means closure has access to the data and no other function has access to it and hence this data can be tracked and isolated. This is one of the benefits of closure.

## Some closure use cases

### Isolating the data

Suppose we want to create a function that persists data after the functional call exists. For example, we create a Fibonacci series generator where we want to keep all variables away from the user's eye, so no one can manipulate it.

```
package main

import "fmt"

func fibonacci() func() int {
	n1 := 0
	n2 := 1
	return func() int {
		n1, n2 = n2, (n1 + n2)
		return n1
	}
}

func main() {
	f := fibonacci()
	fmt.Println(0)
	for i := 0; i < 10; i++ {
		fmt.Println(f())
	}
}
```
***<a href="https://play.golang.org/p/hvidcU6RkeY" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

### Search in sorting package

A common use of Search is to find the index i for a value x in a sorted, indexable data structure such as an array or slice. In this case, the argument f, typically a closure, captures the value to be searched for, and how the data structure is indexed and ordered.

```
func Search(n int, f func(int) bool) int
```

```
package main

import (
	"fmt"
	"sort"
)

func main() {
	nums := []int{1, 3, 6, 8, 10, 15, 21, 28, 36, 45, 55}
	x := 8

	i := sort.Search(len(nums), func(i int) bool {
		return nums[i] >= x
	})
	fmt.Printf("Index of %d is %d", x, i)
}
```
***<a href="https://play.golang.org/p/FQIjK3s6whR" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

***Thank you for reading this blog please give your feedback in the comment section below.***
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

<a href="/blog/golang/pointers">
    <b style="color:DodgerBlue">
        <i>Pointers 🡆</i>
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