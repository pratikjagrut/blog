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

The pointer is a special variable in Golang that stores the memory address of other variables. 

Variables are used to store some type of data. All variables are assigned a particular memory where they store data and this memory has a memory address that is in hexadecimal format. The number that starts with `0x` is hexadecimal like (`0x14` which is equivalent to 20 in decimal). Golang allows us to store this memory address in variables but only pointers will understand that the stored value is pointing to some memory whereas other variables will treat it just as a value.

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

***<a href="https://play.golang.org/p/DRmvVzN-gFK" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***
### Shorthand declaration

In Golang shorthand declaration(:=) is used to narrow down the variable declaration. The Golang compiler will decide if the RHS variable is a pointer variable if we're assigning the memory address of the LHS variable using `&`.

```
i := 42
p := &i
```
### Declaring pointer with the new function

Golang has a built-in allocating primitive function called `new`. The `new(T)` allocates memory, initializes it with zero-value of type T and returns the pointer to that memory. In Go terminology, it returns a pointer to a newly allocated zero value of type T.

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
***<a href="https://play.golang.org/p/C8gmExWxJ5B" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***
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

***<a href="https://play.golang.org/p/gz-qxg5IT3Q" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

## Pass-by-value vs Pass-by-pointer

When we write a function we decide parameters to be passed `by-value` or `by-pointer`.

**Pass by value**

Every time variable is passed as a parameter the new copy of that variable is created and passed to the function. This copy has a different memory location hence any changed to this copy will not affect the original variable. 

In the below example we pass the parameter by value.

```
package main

import "fmt"

func add(i int) {
  i = i + 10
  fmt.Println("Variable copy from add function:", i)
}

func main() {
  i := 10
  fmt.Println("Original variable:", i)
  add(i)
  fmt.Println("Original variable:", i)
}
```

```
Original variable: 10
Variable copy from add function: 20
Original variable: 10
```
***<a href="https://play.golang.org/p/uSHAuPe4dEn" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

**Pass by Pointer**

When we pass parameter by-pointer Go makes the copy of that pointer to the new location. This pointer copy has the same memory address stored in it hence it is pointing to the original variable and any changes done using this pointer will change the value of the original variable.

```
package main

import "fmt"

func add(i *int) {
  *i = *i + 10
  fmt.Println("Variable copy from add function:", *i)
}

func main() {
  i := 10
  fmt.Println("Original variable:", i)
  add(&i)
  fmt.Println("Original variable:", i)
}
```

```
Original variable: 10
Variable copy from add function: 20
Original variable: 20
```
***<a href="https://play.golang.org/p/ojMMRRkIeo3" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

*In some way we can say pass-by-pointer is an implementation of pass-by-value.*

## Container types(slices, maps etc) and pointers

```
package main

import (
	"fmt"
)

func modify(h map[int]int) {
	h[1] = 5
	fmt.Println("Modified map: ", h)

}

func main() {
	m := make(map[int]int)
	m[1] = 1
	m[2] = 2
	m[3] = 3
	fmt.Println("Original map: ", m)
	modify(m)
	fmt.Println("Original map: ", m)
}
```

In the above example, we're creating a map and passing it to the modify function. With the general look, it seems like we're passing an argument by-value because we're not passing the address of map m using &. So this means the copy of map m should be created and the original map is untouched. But if we run this we get an output as follows.

```
Original map:  map[1:1 2:2 3:3]
Modified map:  map[1:5 2:2 3:3]
Original map:  map[1:5 2:2 3:3]
```

***We passed an argument by-value then why did the original map was updated?***

When we create a map using `m := make(map[int]int)` the compiler makes call to the `runtime.makemap` function whose signature is as 
`func makemap(t *maptype, hint int, h *hmap) *hmap`.

So as we see, the return type of runtime.makemap is a pointer to the `runtime.hmap structure`. So when we passed a map to the function we actually passed a pointer to the runtime.hmap structure of map m and hence the original map was modified.

Instead of map if we try above program using slice we will get the similar output because slice variable stores the pointer to underlying array. ***<a href="/blog/golang/array_slice" style="color:DodgerBlue" target="_blank">Read more about Arrays and Slices here.</a>***

***<a href="https://play.golang.org/p/ORs5UkdECmS" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

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