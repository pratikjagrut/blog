---
title: "Go Introduction and Installation"
date: 2020-12-19T17:23:49+05:30
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

Go is an open-source, statically typed, compiled programing language built by Google.
It combines the simplest of both statically typed and dynamically typed languages and provides you with the proper mixture of efficiency and simple programming. 
It is primarily fitted to building fast, efficient, and reliable server-side or system applications.

Following are some noted features of Go -

- Safety
- Concurrency
- Efficient Garbage Collection
- High-speed compilation
- Excellent Tooling support

## Installing GO

Go binary distributions are available for all major operating systems like Linux, Windows, and macOS. 
It’s easy to install Go from the binary distributions or <a href="https://golang.org/doc/install/source" style="color:DodgerBlue" target="_blank">you can try installing Go from source.</a>


### Linux

- Download Go for Linux from Go’s official [download](https://golang.org/dl/) page.

    ```
    tar -xvf go1.15.6.linux-amd64.tar.gz
    ```

    It will create a directory named `go`.

- Move that `go` dir to `/usr/local` where all other binaries reside.

    ```
    sudo mv go /usr/local
    echo 'export PATH=$PATH:/usr/local/go/bin' >> ~/.bashrc # bashrc or zshrc depending upon your shell type
    ```

- Custom Installation directory

    Instead of moving `go` dir to `/usr/local` you can choose any other dir.

    ```
    mkdir custom_go # just for demo, you can move to any dir of your choice
    mv go custom_go
    ```

    Then set this custom location to `GOROOT` environment variable.

    ```
    export GOROOT=$HOME/go
    export PATH=$PATH:$GOROOT/bin
    ```
    and then test 

    ```
    go version
    go version go1.15.6 linux/amd64
    ```

    To make `GOROOT` and `PATH` permanent add it to `.bashrc` or `.zshrc` depending on which shell you are using or else your `GOROOT` will be unset once you end your terminal session or start a new terminal session.

### MacOS X

Install GO in MacOS using Homebrew.

```
brew install go
```

### Windows

Download the Windows installer from Go’s official [download](https://golang.org/dl/) page. Open the installer and follow the on-screen instructions to install Go. 
By default, the installer installs Go in `C:\Go` add `C:\go\bin` to your path environment variable.

***Thank you for reading this blog, and please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/series/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/series/helloworld">
    <b style="color:DodgerBlue">
        <i>🡆 First program in Go: Hello World</i>
    </b>
</a>  &emsp;

<br>

<a href="https://github.com/pratikjagrut/go-tutorial/tree/master/00_installation" target="_blank">
  <b style="color:DodgerBlue" class="fab fa-github">
    <i>Github Repo</i>
  </b>
</a>  &emsp;

<a href="https://github.com/pratikjagrut/go-tutorial/blob/master/REFERENCE.md" target="_blank">
  <b style="color:DodgerBlue">
    <i>&#128279; Reference</i>
  </b>
</a>
