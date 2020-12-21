---
title: "Looping Construct"
description: "Looping construct is used when the same set of instructions has to be performed."
date: 2020-12-21T19:34:10+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
---

Go has only one looping construct, the `for` loop.

**Basic for loop**

The basic for loop has three components separated by semicolons:

- init statement: `i := 0` *exec before 1<sup>st</sup> iteration*
- condition expression: `i < n` *eval on every* interation
- post statement: `i++` *exec after each iteration*

*The expression is not surrounded by parentheses `( )` but the braces `{ }` around set of instructions are required.*

```
for i := 0; i < n; i++ {
    //business logic
    //set of instructions
}
```

Init and post statement are optional.

```
for ; i < n; {
    //business logic
}
```

**For is also a while() loop**

```
for i < n {
    //business logic
}
```

**Infinite loop**
```
for {
    //business logic
}
```

## Example

```
package main

import "fmt"

func main() {
	for i := 0; i < 5; i++ {fmt.Printf("Iteration number: %d\n", i)}
}
```

```
go run main.go

Iteration number: 0
Iteration number: 1
Iteration number: 2
Iteration number: 3
Iteration number: 4
```
***You can refer <a href="https://github.com/pratikjagrut/go-tutorial/tree/master/03_for_loop/main.go" style="color:DodgerBlue" target="_blank">main.go</a> file for examples***

<hr>

<a href="/blog/golang/vdc">
  <b style="color:DodgerBlue">
    <i>🡄 Variables, data types and constants</i>
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