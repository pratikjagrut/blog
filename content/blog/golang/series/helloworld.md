---
title: "Classic hello world program"
date: 2020-12-19T21:48:51+05:30
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

### First thing, packages
In Go, source files are organized into system directories called packages, which enable code reusability.
When you build reusable pieces of code, you will develop a package as a shared library. But when you develop executable programs, you will use the package `main` for making the package as an executable program. The package `main` tells the Go compiler that the package should compile as an executable program instead of a shared library.

```
package main
```

### Import
The keyword `import` is used for importing a package into other packages. 
When you import packages, the Go compiler will look on the locations specified by the environment variable `ROOT` and `PATH`.

```
// Single pkg/lib import
import "fmt"
// Multiple pkg/lib import
import(
    "fmt"
    "os"
)
```

### Main function
The `main` function in the package `main` will be the entry point of our executable program. 
When you build shared libraries, you will not have any main package and main function in the package.

```
func main(){}
```
### Hello World

```
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

Save it as `main.go` or `any-name-you-prefer.go`

To run this program:
```
go run main.go

Hello, World!
```
***<a href="https://play.golang.org/p/FAszkU0xQZo" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

***Thank you for reading this blog please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/series/introduction">
  <b style="color:DodgerBlue">
    <i>🡄 Introduction and Installation</i>
  </b>
</a> &emsp;

<a href="/blog/golang/series/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/series/vdc">
  <b style="color:DodgerBlue">
    <i>Variables, data types and constants 🡆</i>
  </b>
</a>  &emsp;

<br>

<a href="https://github.com/pratikjagrut/go-tutorial/tree/master/01_helloworld" target="_blank">
  <b style="color:DodgerBlue" class="fab fa-github">
    <i>Github Repo</i>
  </b>
</a>  &emsp;

<a href="https://github.com/pratikjagrut/go-tutorial/blob/master/REFERENCE.md" target="_blank">
  <b style="color:DodgerBlue">
    <i>&#128279; Reference</i>
  </b>
</a>