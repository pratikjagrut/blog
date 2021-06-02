---
title: "Go code organization using GOPATH"
date: 2020-12-19T17:23:49+05:31
draft: true
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
  - "2020"
---
Go programs are organized into packages. A package is a collection of source files in the same directory that are compiled together. Functions, types, variables, and constants defined in one source file are visible to all other source files within the same package.

Since GO 1.11 we've two ways of organizing Go project. One is using `GOPATH` and second is using `go mod or modules`.

### Using GOPATH

By convention, all your Go code must reside in a single workspace whose path is stored in the environment variable `GOPATH`.

Here we use `workspace` dir, whose structure looks like below. In this case workspace directory is go.

```
go
├── bin
├── pkg
└── src
    └── github.com
        └── pratikjagrut
            └── go-tutorial
                └── helloworld
                    └── main.go
```
- `src`: contains Go source files.

    The src directory typically contains many version control repositories containing one or more Go packages. Every Go source file belongs to a package. You generally create a new subdirectory inside your repository for every separate Go package. The tree for this looks like the following:


- `bin`: contains the executable binaries.

    The `Go tool` builds and installs executable binaries to this directory.

- `pkg`: contains Go package archives.

    All the non-executable packages (shared libraries) are stored in this directory. This is typically imported and used inside other executable packages.

Here we'll also need to set `GOPATH` environment variable to the workspace directory we're using.

```
export GOPATH=$HOME/go
```

*To make `GOPATH` permanent add it to `.bashrc` or `.zshrc` depending on which shell you are using or else your `GOPATH` will be unset once you end your terminal session or start a new terminal session.*

***[To know more about writing code with GOPATH read this blog.](https://golang.org/doc/gopath_code)***

***Thank you for reading this blog please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/series/introduction">
  <b style="color:DodgerBlue">
    <i>🡄 Introduction</i>
  </b>
</a> &emsp;

<a href="/blog/golang/series/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/series/code_organization_go_mod">
    <b style="color:DodgerBlue">
        <i>Code organization using go mod 🡆</i>
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