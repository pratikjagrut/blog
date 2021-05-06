---
title: "Looping Construct"
date: 2020-12-21T19:34:10+05:30
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

Go has only one looping construct, the `for` loop.

### Basic for loop

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

### For is also a while() loop

```
for i < n {
    //business logic
}
```

### Infinite loop

```
for {
    //business logic
}
```

### Example

```
package main

import "fmt"

func main() {
	for i := 0; i < 5; i++ {fmt.Printf("Iteration number: %d\n", i)}
}
```
***<a href="https://play.golang.org/p/OysJvNK3rNz" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***
```
Iteration number: 0
Iteration number: 1
Iteration number: 2
Iteration number: 3
Iteration number: 4
```

***Thank you for reading this blog please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/series/vdc">
  <b style="color:DodgerBlue">
    <i>🡄 Variables, data types and constants</i>
  </b>
</a> &emsp;

<a href="/blog/golang/series/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/series/if_else">
    <b style="color:DodgerBlue">
        <i>Conditional Statements 🡆</i>
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