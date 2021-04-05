---
title: "Functions"
date: 2021-01-12T12:36:48+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
---

A function is a block of statements which performs a specific task. Functions is a well organized and reusable code. It improves the code readability, maintainability and testability. The general function is: 

```
func function_name( [parameter list] ) [return_types]
{
  body of the function
}
```

### Declaring and calling functions

The function is declared using `func` keyword.

```
func sayCheeze() {
  fmt.Println("Cheeeeeeeeeeeeze")
}
```
Calling the function is pretty easy.

```
sayCheeze()
```

```
package main

import "fmt"

func sayCheeze() {
	fmt.Println("Cheeeeeeeeeeeeze")
}

func main() {
	sayCheeze()
}
```
***<a href="https://play.golang.org/p/sz4RmqzeqZZ" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

### You may pass input parameters

```
func addition(i int, j int) {
  fmt.Println(i + j)
}
```

We need to pass the declared number of parameters while calling the function.

```
addition(1, 2)
```

When two or more consecutive parameters have the same type we can omit the type from all but last.

```
package main

import "fmt"

func addition(i, j, k int) {
	fmt.Println(i + j + k)
}

func main() {
	addition(10, 20, 30)
}
```
***<a href="https://play.golang.org/p/Hd3WlDtdSbI" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

### You may define the return type of function

```
func addition(i, j, k int) int {
   return i + j + k
}
```
```
sum := addition(1, 2, 3)
```

A function can return any number of results.

```
package main

import "fmt"

func addition(i, j int) (int, int, int) {
	return i, j, i + j
}

func main() {
	a, b, sum := addition(1, 2)
	fmt.Println(a, b, sum)
}
```
***<a href="https://play.golang.org/p/hqkVQEkp_Ik" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

### Named return values

Go's return values may be named. The named return values are treated as locally defined variables in the function.

```
package main

import "fmt"

func division(i int) (quotient, remainder int) {
	quotient = i / 10
	remainder = i % 10
	return
}
func main() {
	quotient, remainder := division(125)
	fmt.Printf("Quotient: %d and Remainder: %d", quotient, remainder)
}
```
***<a href="https://play.golang.org/p/4mOb0aPX7B2" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

### Variadic functions

Variadic functions can be called with any number of trailing arguments. 
For example, `fmt.Println` is a common variadic function.

```
package main

import "fmt"

func total(nums ...int) (total int) {
	for _, i := range nums {
		total += i
	}
	return total
}

func main() {
	fmt.Println(total(1, 2, 3, 4, 5))
	fmt.Println(total(1, 2, 3, 4, 5, 6, 7, 8, 9, 10))
}
```
***<a href="https://play.golang.org/p/g0EkydaW9k2" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

***Thank you for reading this blog please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/range">
  <b style="color:DodgerBlue">
    <i>🡄 Range</i>
  </b>
</a> &emsp;

<a href="/blog/golang/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/anonymous_func">
    <b style="color:DodgerBlue">
        <i>Anonymous Function 🡆</i>
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