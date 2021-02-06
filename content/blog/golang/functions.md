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
func addition(i, j, k int) {
  fmt.Println(i + j + k)
}
```

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
func addition(i, j int) (int, int, int) {
   return i, j, i + j
}
```
```
a, b, sum := addition(1, 2)
```

### Named return values

Go's return values may be named. The named return values are treated as locally defined variables in the function.

```
func calc(i int) (x, y int) {
    x = i / 10
    y = i % 10
    return
}
```

### Variadic functions

Variadic functions can be called with any number of trailing arguments. 
For example, `fmt.Println` is a common variadic function.

```
func total(nums ...int) (total int) {
    for _, i := range nums {
        total += i
    }
    return total
}
```
Function call
```
total := total(1, 2, 3, 4, 5)
total = total(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
```

***You can refer <a href="https://github.com/pratikjagrut/go-tutorial/blob/master/10_functions/main.go" style="color:DodgerBlue" target="_blank">main.go</a> file for examples***

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