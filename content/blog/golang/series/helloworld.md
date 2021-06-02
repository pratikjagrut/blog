---
title: "Classic hello world program"
date: 2020-12-19T17:23:49+05:32
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
## Source code organization

Since GO1.11 we've two ways of organizing go code: one is, using `GOPATH` and the second one is using `go mod`.
`GOPATH` structure was widely in use and kind of only way to structure your go code before GO1.11.
In this blog, we'll use `go mod` since it provides more features and flexibility over GOPATH.

***[To know more about writing code with GOPATH read this blog.](https://golang.org/doc/gopath_code)***

Go programs are organized into packages, which enable code reusability. A package is a collection of source files in the same directory that are compiled together. Functions, types, variables, and constants defined in one source file are visible to all other source files within the same package.

The collection of packages that are bundled and release together is known as modules. These modules are stored in a repository.
A repository may contain one or more modules but a Go repository typically contains only one module, located at the root of the repository.

It is recommended to use a remote repository path to organize Go code even though we're not going to publish it at the remote repository.
For example, our hello world module name will be `github.com/pratikjagrut/helloworld`.
A module can be defined locally without belonging to a repository. 
This module's path serves as an import prefix for its package. An import path is a string used to import a package.

## Writing our first program

To start a new project, we'll first choose the module's pathname and then initialize it using `go mod init`.
I'm choosing `github.com/pratikjagrut/helloworld` path, but you can choose a different one.

Create project/module directory.
```
mkdir helloworld 
cd helloworld
go mod init github.com/pratikjagrut/helloworld
go: creating new go.mod: module github.com/pratikjagrut/helloworld

cat go.mod
module github.com/pratikjagrut/helloworld

go 1.16
```
*While using repository pathname, make sure to change pratikjagrut to your username.*

Now let's create a file `main.go` (any name will work followed by extension .go).

```
package main

import "fmt"

func main() {
  fmt.Println("Hello, world!")
}
```
In this code:
- Declare the main package using the keyword `package`.
- Import the popular fmt package using the keyword `import`.
- Implement the main function to print a message to the console.

While developing the executable command, we use the `main` package. 
The main package tells the Go compiler that this package should compile as an executable program instead of a shared library.

Run the code.
```
go run .

Hello, world!
```
***<a href="https://play.golang.org/p/FAszkU0xQZo" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

As this is the main package, we can install the code as a command using `go install`.

`go install` is controlled by `GOPATH` and `GOBIN` environment variables.
If the GOBIN environment variable is set, then binary will install at the GOBIN location, else it will install at the `$GOPATH/bin` location. The default GOPATH ($HOME/go or %USERPROFILE%\go).
To use the installed binary as a command, make sure the binary installation path is added to the $PATH variable.

```
go install .
helloworld

Hello, world!
```
We can make use of any command to install the bin.
```
go install
go install .
go install github.com/pratikjagrut/helloworld
```

## Create and import package from the same module

Here we'll create a `utils` package that will have only one function `SwapStrings`.
`SwapStrings` starts with capital because we need to ***[export](https://golang.org/ref/spec#Exported_identifiers)*** it, so that it could be used outside of the package utils.

```
mkdir utils # inside helloworld dir
```
Create a file `utils.go` in utils dir with the following code.

```
package utils

func SwapStrings(a, b string) (string, string) {
  return b, a
}
```

We can build it to check if it compiles successfully.

```
go build
```
If it outputs nothing, then it means compilation successful.
`go build` will also add this package to the local cache.

Now let's use this package in our executable program.
```
package main

import (
  "fmt"
  "github.com/pratikjagrut/helloworld/utils"
)

func main() {
  fmt.Println("Hello, world!")
  fmt.Println(utils.SwapStrings("Hello,", "world!"))
}
```

```
go run .

Hello, world!
world! Hello,
```

***Thank you for reading this blog, and please give your feedback in the comment section below.***
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
