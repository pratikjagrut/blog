---
title: "Pointers"
date: 2021-02-21T18:28:54+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
---

The pointer is a special variable in Go that stores the memory address of other variables. 

Variables are used to store some type of data. All variables are assigned a particular memory where they store data and this memory has a memory address that is in hexadecimal format. The number that starts with `0x` is hexadecimal like (`0x14` which is equivalent to 20 in decimal). Go allows us to store this memory address in variables but only pointers will understand that the stored value is pointing to some memory whereas other variables will treat it just as a value.

## Declaring Pointer

The type `*T` is a pointer to a `T` value. It's zero value is `<nil>`.

```
var pointer_name *Data_Type
var p *int = &variable
```

In the above snippet, you can see two symbols `*` and `&`, which are two operators.

`* Operator` is also called dereferencing operator which is used to declare an operator and also to access the value stored at the memory address pointer pointing to.

`& Operator` this operator is used to access the memory address of a variable.

Below is an example demoing the use of * and &.

```
package main

import "fmt"

func main() {
  i := 42
  
  var p *int = &i
  
  fmt.Println("The value of i is: ", *p)
  fmt.Println("The memory address of i is", p)
}
```

```
The value of i is:  42
The memory address of i is 0xc00002c008
```

### Shorthand declaration

```
i := 42
p := &i
```

### Declaring pointer with the new function

Golang has a built-in allocating primitive function called `new`. The `new` allocates memory but does not initialize memory it only zeros it(zero-value). The `new` function returns a pointer to the memory location. The `new(T)` allocates zeroed storage to T and returns the memory address as `*T`. In Go terminology, it returns a pointer to a newly allocated zero value of type T.

**What is the difference between `var p *int` and `p := new(int)`?**

The expression `var p *int` only declares the pointer and does not initialize it with any memory address, i.e pointer does not point to any memory location. Whereas in `new(T)` function returns the pointer pointing to the memory location in the system. 
```
package main

import "fmt"

func main() {
  var p *int
  fmt.Println("The value of p", p)
  
    p1 := new(int)
  fmt.Println("The value of *p1 is: ", *p1)
  fmt.Println("The value of p1", p1)
}
```
```
The value of p <nil>
The value of *p1 is:  0
The value of p1 0xc00002c008
```
In the above example, we can not dereference pointer `p` because it has `<nil>` value. Trying to dereference it will throw an error.
```
panic: runtime error: invalid memory address or nil pointer dereference
```

## Passing pointer to the function

We can pass a pointer to the function as we pass other variables. We can create a pointer to the variable and then pass it to the function or we can just pass an address of that variable using `&`.

In the below example we initialize a variable i with the value 10. We've function `addTen(i *int)` which takes a pointer as an argument and then it adds 10 by dereferencing the pointer hence mutating the original value. Below are shown both the ways of passing pointer the function.

```
package main

import "fmt"

func addTen(i *int) {
  *i = *i + 10
}

func main() {
  i := 10
  p := &i
  fmt.Println(i)
  addTen(p) // Pass by pointer
  fmt.Println(i)
  addTen(&i) // Pass by address
  fmt.Println(i)
}

```

```
10
20
30
```

<hr>

<a href="/blog/golang/closures">
  <b style="color:DodgerBlue">
    <i>🡄 Closures</i>
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