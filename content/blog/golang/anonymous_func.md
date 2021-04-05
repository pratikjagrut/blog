---
title: "Anonymous Function"
date: 2021-02-14T19:07:57+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
---

The anonymous function is a feature in Golang which let us define a function without a name. This feature is also called a function literal. This is useful when you want an inline function or to form a closure.

### Declaring the anonymous function

The syntax is pretty straight forward and much similar to normal function.

```
func(parameter_list)(return_type){
  return
}()
```
`Parameter list` and `return type` are optional.

`()` this will invoke the function as soon as it is defined.

```
package main

import "fmt"

func main() {
	func() {
		fmt.Println("Golang Rocks!")
	}()
}
```
***<a href="https://play.golang.org/p/Kpnl__MXw7V" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

### Assigning anonymous function to a variable

In golang, you can assign an anonymous function to a variable. The assigned variable will be the type of function type and it can be called like a regular function.

```
package main

import "fmt"

func main() {
	v := func() {
		fmt.Println("Golang Rocks!")
	}
	fmt.Printf("Type of variable v: %T\n", v)
	v()
} 
```
```
Type of variable v: func()
Golang Rocks!
```
***<a href="https://play.golang.org/p/Ebz_b0v-AX-" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

### Passing an argument to an anonymous function

An anonymous function can take any number of arguments similar to normal function.

```
package main

import "fmt"

func main() {
	func(name string) {
		fmt.Println("Hello, ", name)
	}("Jack")
}
```
***<a href="https://play.golang.org/p/oSsoVNXmNwX" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

**With any number of trailing arguments similar to Variadic functions**

```
package main

import "fmt"

func main() {
	func(i ...int) {
		fmt.Println(i)
	}(1, 2, 3, 4)
}
```
***<a href="https://play.golang.org/p/vMjTAcWpKec" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

**Passing an anonymous function as an argument**

You can pass an anonymous function as an argument to a regular function or an anonymous function.

- *Anonymous function as an argument to regular function*

```
package main

import "fmt"

func sayHello(af func(s string) string) {
	fmt.Println(af("Jack"))
}

func main() {

	sayHello(func(s string) string {
		return "Hello, " + s
	})
}
```
***<a href="https://play.golang.org/p/UKJB3fh9DaA" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***


- *Anonymous function as an argument to anonymous function*

```
package main

import "fmt"

func main() {
	func(v string) {
		fmt.Println(v)
	}(func(s string) string {
		return "Hello, " + s
	}("Jack"))
}
```
***<a href="https://play.golang.org/p/d8dprfgLXgF" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

This above code looks a bit complicated and hard to fathom so another way we can achieve this is the following:

```
package main

import "fmt"

func main() {
	af := func(s string) string {
		return "Hello, " + s
	}

	func(af func(s string) string) {
		fmt.Println(af("Jack"))
	}(af)
}
```
***<a href="https://play.golang.org/p/l7sP7Nz8qpw" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

### Return an anonymous function from another function

We can return an anonymous function from another function

- *Returning from regular function*

```
package main

import "fmt"

func sayHello() func(s string) string {
	r := func(s string) string {
		return "Hello, " + s
	}
	return r
}

func main() {
	f := sayHello()
	fmt.Printf("Type of variable f: %T\n", f)
	fmt.Println(f("Jack"))
}
```
***<a href="https://play.golang.org/p/NY3YiPG4N9h" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

- *Returning from anonymous function*

```
package main

import "fmt"

func main() {
	f := func() func(s string) string {
		r := func(s string) string {
			return "Hello, " + s
		}
		return r
	}

	fmt.Printf("Type of variable f: %T\n", f)
	c := f()

	fmt.Printf("Type of variable c: %T\n", c)
	fmt.Println(c("Jack"))
}
```
***<a href="https://play.golang.org/p/jwfmOnhyOGh" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

***Thank you for reading this blog please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/functions">
  <b style="color:DodgerBlue">
    <i>🡄 Functions</i>
  </b>
</a> &emsp;

<a href="/blog/golang/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/closures">
    <b style="color:DodgerBlue">
        <i>Closures 🡆</i>
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