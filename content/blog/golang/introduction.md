---
title: "Go Introduction and Installation"
description: ""
date: 2020-12-19T17:23:49+05:30
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

- Move that dir to `/usr/local` where all other binaries reside.

    ```
    export PATH=$PATH:/usr/local/go/bin
    ```

- Custom Installation directory

    Instead of moving dir to `/usr/local` you can choose any other dir.

    ```
    mv go $HOME/
    ```

    Then set this custom location to `GOROOT` environment variable.

    ```
    export GOROOT=$HOME/go
    ```

    To make `GOROOT` permanent add it to `.bashrc` or `.zshrc` depending on which shell you are using or else your `GOROOT` will be unset once you end your terminal session or start a new terminal session.

### MacOS X

Install GO in MacOS using Homebrew.

```
brew install go
```

### Windows

Download the Windows installer from Go’s official [download](https://golang.org/dl/) page. Open the installer and follow the on-screen instructions to install Go. 
By default, the installer installs Go in `C:\Go`.

*Once installed try `go version` to check the installation.*

## Go Code organization

<span style="color:DodgerBlue"><i>
  Note: After the introduction of <b>Go modules in Go 1.11</b>, its no longer required to store Go code in the Go workspace. You can create your Go project in any directory outside of <b>GOPATH</b>. You can refer to <b>[go docs on code organization](https://golang.org/doc/code.html)</b>. The following Go Code organization is still widely in use mostly because of its elegant organizing structure.
</i></span>

### Workspace 

Go requires you to organize your code in a specific way -

By convention, all your Go code and the code must reside in a single workspace whose path is stored in the environment variable `GOPATH`.

The `workspace` dir is supposed to contain the following sub-dir:

- `src`: contains Go source files.

    The src directory typically contains many version control repositories containing one or more Go packages. Every Go source file belongs to a package. You generally create a new subdirectory inside your repository for every separate Go package. The tree for this looks like the following:

    ```
    go
    └── src
        └── github.com
            ├── pratikjagrut
            │   └── go-tutorial
            │       └── helloworld
            │           └── main.go
            └── user
                └── project
    ```

- `bin`: contains the executable binaries.

    The `Go tool` builds and installs executable binaries to this directory.

- `pkg`: contains Go package archives.

    All the non-executable packages (shared libraries) are stored in this directory. This is typically imported and used inside other executable packages.

### Setting GOPATH

#### Linux and macOS

```
mkdir $HOME/go_workspace
export GOPATH=$HOME/go_workspace
```

*To make `GOPATH` permanent add it to `.bashrc` or `.zshrc` depending on which shell you are using or else your `GOPATH` will be unset once you end your terminal session or start a new terminal session.*

#### Windows System

- Create the workspace folder at C:\go-workspace.

- Right-click on Start → click Control Panel → Select System and Security → click on System.

- From the menu on the left, select the Advanced system's settings.

- Click the Environment Variables button at the bottom.

- Click New from the User variables section.

- Type GOPATH into the Variable name field.

- Type C:\go-workspace into the Variable value field.

- Click OK.

***Note: GOPATH must be different than the path of your Go installation.***


<a href="/blog/golang/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/helloworld">
    <b style="color:DodgerBlue">
        <i>🡆 First program in Go: Hello World</i>
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
