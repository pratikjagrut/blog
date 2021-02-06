---
title: "Anonymous Function"
date: 2021-01-13T13:08:36+05:30
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
func() {
  fmt.Println("Golang Rocks!")
}()
```
```
Golang Rocks!
```
### Assigning anonymous function to a variable

In golang, you can assign an anonymous function to a variable. The assigned variable will be the type of function type and it can be called like a regular function.

```
v := func(){ 
  fmt.Println("Golang Rocks!") 
}
fmt.Printf("Type of variable v: %T", v)
v() 
```
```
Type of variable v: func()
Golang Rocks!
```

### Passing an argument to an anonymous function

An anonymous function can take any number of arguments similar to normal function.

```
func(i int){
  fmt.Println(i)
}(1)
```

**With any number of trailing arguments similar to Variadic functions**

```
func(i ...int){
  fmt.Println(i)
}(1, 2, 3, 4)
```

**Passing an anonymous function as an argument**

You can pass an anonymous function as an argument to a regular function or an anonymous function.

- *Anonymous function as an argument to regular function*

```
func sayHello(af func (s string) string) {
  fmt.Println(af("Jack"))
}

func main() {
  af := func(s string) string {
    return "Hello, " + s
  }

  sayHello(af)
}
```

- *Anonymous function as an argument to anonymous function*

```
func (v string) {
    fmt.Println(v)
}(func (s string) string {
    return "Hello, " + s
}("Jack"))
```

This above code looks a bit complicated and hard to fathom so another way we can achieve this is the following:

```
af := func (s string) string {
  return "Hello, " + s
}

func (af func (s string) string) {
    fmt.Println(af("Jack"))
}(af)
```

### Return an anonymous function from another function

We can return an anonymous function from another function

- *Returning from regular function*

```
func sayHello() func(s string) string {
  r := func(s string) string {
    return "Hello, " + s
  }
  return r
}

func main() {
  f := sayHello()
  fmt.Println(f("Jack"))
}
```

- *Returning from anonymous function*

```
f := func () func (s string) string {
  r := func (s string) string {
    return "Hello, " + s
  }
  return r
}

c := f()

fmt.Println(c("Jack"))
```

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