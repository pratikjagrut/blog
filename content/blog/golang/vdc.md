---
title: "Variables, data types and constants"
date: 2020-12-20T18:34:48+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
---

## Variable

Variable is a symbolic name given to the storage location which contains some value which can be changed at any time during the execution of the program. A variable must be defined with the type of data or value it is holding.

## Data types
There are several data types in Go.

```
bool        int         uint        float32     complex64
string      int8        uint8       float64     complex128
byte        int16       uint16
rune        int32       uint32
error       int64       uint64
```

## Zero value
In some programming languages variable holds a `null` or `undefined` value when not initialized, Go gives it a zero-value of its data type. A `boolean` variable if not initialized, gets the `false` value and an `integer` variable gets `0` value, `string` variable will get `nil` value.

## Declaring a variable

The `var` statement declares a list of variables. Type is at the last of the statement.

```
var varName dataType
```
E.g.:

```
var i, j, k int
var f float32
var u uint
```

**Variables with initializers**

We can initialize variable while declaring.

```
var varName dataType = value
```

```
var i int = 10
var s string = "hello"
var ok bool = true
```

*We can omit the type of variable, it will take the type of initializers*

```
var i = 42           // int
var f = 3.142        // float64
var g = "hello"      // string
```

**Short-hand declaration**

This is the most commonly used variable declaration inside functions.

```
varName := value
``` 
E.g.:
```
i := 10
s := "hello"
ok := true
```

*When declaring a variable without specifying it's type the variable's type is inferred from the value on the right-hand side.*

```
var i int
j := i            // j is an int
i := 42           // int
f := 3.142        // float64
g := 0.867 + 0.5i // complex128
```

**Assign or Re-assign**

You can assign or re-assign value to a declared variable as:
```
varName = value
```
E.g.:
```
i = 12
s = "world"
ok = false
```

**Multiple variable declarations**

Multiple variables of the same type with the single var statement 

```
var i, j, k int
var x, y, z = 0.867 + 0.5i, 4.65, true
```

Multiple variables of the different types with the single var statement 

```
var (
    i int = 10
    s string = "hello"
    ok bool = true
)
```

## Constants

Go supports constants of character, string, boolean, and numeric values. Constants are declared using `const` keyword.

E.g:
```
const str string = "constants"
```

**Untyped and Typed**

Constants can be declared with or without a type in Go. If we are declaring literal constant, then we are declaring constants that are untyped and unnamed.

E.g.:
```
const str string = "constants" //Typed constant
const i = 10 //Untyped constant, literal declaration
const f = 3.14
```
The constants on the LHS of the declaration are named constants and the literal values on the RHS are unnamed constants.

Typed constants don’t use the same type system as variables, they've their implementation for representing the values that we associate with them.

In the case of typed constant, the declared type is used to associate the type’s precision limitations or kind of constant.

In the case of untyped constant, the literal value will determine what kind/type the constant takes

Every GO compiler has the flexibility to implement constant as they wish, within the mandatory set of [requirements](http://golang.org/ref/spec#Constants).

***You can refer <a href="https://github.com/pratikjagrut/go-tutorial/blob/master/02_variables_datatypes_constants/main.go" style="color:DodgerBlue" target="_blank">main.go</a> file for examples***

<hr>

<a href="/blog/golang/helloworld">
  <b style="color:DodgerBlue">
    <i>🡄 First program in Go: Hello World</i>
  </b>
</a> &emsp;

<a href="/blog/golang/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/for_loop">
    <b style="color:DodgerBlue">
        <i>Looping Construct 🡆</i>
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