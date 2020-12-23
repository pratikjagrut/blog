---
title: "Switch"
date: 2020-12-22T14:35:42+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
---

A switch statement is another way to write a sequence of if - else statements.

Go's switch is like the one in C and C++ except that `it only runs the selected case, not all the cases that follows` so we don't need break statement here.

```
switch expression {
    case exp1:
        //Executes if expression matches exp1
    case exp2:
        //Executes if expression matches exp2
    default:
        //Executes if expression does not matches with any case
}
```

### Switch evaluation order

Switch cases evaluate cases from top to bottom and stops when a case succeeds. 

In below example, it checks `case "Linux":` if os matches with `Linux` then it stops at that case else go to the next case.

```
//Prints which OS you're using
switch os := runtime.GOOS; os {
case "linux":
    fmt.Println("Linux.")
case "darwin":
    fmt.Println("OS X.")
default:
    fmt.Printf("%s.\n", os)
}
```

### Switch with NO condition

Switch with no condition is like `switch true`. It is useful for writing log if-else-if ladder.
```
t := time.Now()
switch {
case t.Hour() < 12:
    fmt.Println("Good morning!")
case t.Hour() < 17:
    fmt.Println("Good afternoon.")
default:
    fmt.Println("Good evening.")
}
```

***You can refer <a href="https://github.com/pratikjagrut/go-tutorial/blob/master/05_switch/main.go" style="color:DodgerBlue" target="_blank">main.go</a> file for examples***

<hr>

<a href="/blog/golang/if_else">
  <b style="color:DodgerBlue">
    <i>🡄 Conditional Statements</i>
  </b>
</a> &emsp;

<a href="/blog/golang/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/array_slice">
    <b style="color:DodgerBlue">
        <i>Arrays and Slices 🡆</i>
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