---
title: "Hello World"
description: "Write our first program in Go"
date: 2020-12-19T21:48:51+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
  - "tech"
---

# Classic hello world program

## First thing, packages
In Go, source files are organized into system directories called packages, which enable code reusability.
When you build reusable pieces of code, you will develop a package as a shared library. But when you develop executable programs, you will use the package `main` for making the package as an executable program. The package `main` tells the Go compiler that the package should compile as an executable program instead of a shared library.

```go
package main
```

## Import
The keyword `import` is used for importing a package into other packages. 
When you import packages, the Go compiler will look on the locations specified by the environment variable `GOROOT` and `GOPATH`.

```go
// Single pkg/lib import
import "fmt"
// Multiple pkg/lib import
import(
    "fmt"
    "os"
)
```

## Main function
The `main` function in the package `main` will be the entry point of our executable program. 
When you build shared libraries, you will not have any main package and main function in the package.

```go
func main(){}
```
## Hello World

```go
package main

import "fmt"

func main() {
    fmt.Println("Hello, World!")
}
```

Save it as `main.go` or `any-name-you-prefer.go`

To run this program:
```shell
go run main.go

Hello, World!
```

<a href="/blog/golang/introduction">
  <b style="color:DodgerBlue">
    <i>🡄 Introduction and Installation</i>
  </b>
</a> &emsp;

<a href="/blog/golang/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<!-- <a href="/blog/golang/">
    <b style="color:DodgerBlue">
        <i>🡆</i>
    </b>
</a>  &emsp; -->
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
