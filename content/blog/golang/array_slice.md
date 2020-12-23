---
title: "Arrays and Slices"
date: 2020-12-22T16:08:06+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
---

## Array

The array is a collection of the same type of element in a contiguous memory location.
The array has fixed length i.e the number of elements to be stored is fixed before memory allocation.

In Go, the type `[n]T` is an array of length `n` and type `T`.

### Array Declarations 

```
// i is an array of length 3, 
// it means it can hold upto 3 int values
var i [3]int
i[0] = 1
i[1] = 10
i[2] = 100
```

**Short-hand declaration**
```
j := [3]string{"Go", "is", "fun"}
```

***You can refer <a href="https://github.com/pratikjagrut/go-tutorial/blob/master/06_array/main.go" style="color:DodgerBlue" target="_blank">main.go</a> file for arrays examples***


## Slices

Slices are a pivotal data type in Go, giving a more powerful interface to sequences than arrays. 
An array has a fixed size whereas the slice is a dynamically-sized.

The type `[]T` is a slice with elements of type `T`.

### Slice formation

#### Creating a slice with make

Slices can be created with the built-in make function; this is how you create dynamically-sized arrays. `make([]T, len, cap(optional))`

```
a := make([]int, 5)    // len(a) = 5
b := make([]int, 0, 5) // len(b) = 0, cap(b) = 5
```

#### Creating a slice from array

Slice can be formed by specifying 2 indices, high bound and low bound, `s[low : high]`. 
This selects a half-open range which includes the first element but excludes the last one.
 
```
odds := [5]int{1, 3, 5, 7, 9}

var o []int = odds[1:4]
```

We can skip low or high bound to use their defaults. For low bound default is `0` and for high bound default is `length of an array`.

`a[:high]`, `a[low:]` 

### Slice are like references to arrays

A slice does not store any data, it just describes a section of an underlying array.

Changing element of the slice will make those changes to an underlying array and all other slices which share the same underlying array.

```
alphabet := [5]string{"A", "B", "C", "D"}

i := alphabet[0:3]
j := alphabet[1:4]

i[2] = "P" // This changes will affect alphabet, i ,j slices
```

### Slice literals

A slice literal is like an array literal without the length.

```
i := []int{1, 2, 3, 4, 5,}
```

### Length and capacity

The length of a slice is the number of elements it contains.

The capacity of a slice is the number of elements in the underlying array, counting from the first element in the slice.

Length: `len(s)`

Capacity: `cap(s)`

### Appending

Slices support several operations including basic operations of arrays. One of such operation is appending.

```
z := []int{1, 2, 3, 4, 5}
z = append(z, 6, 7, 8) //1st arg is slice, and then can take any number of arg to append
```

***You can refer <a href="https://github.com/pratikjagrut/go-tutorial/blob/master/07_slice/main.go" style="color:DodgerBlue" target="_blank">main.go</a> file for slices examples***

<hr>

<a href="/blog/golang/switch">
    <b style="color:DodgerBlue">
        <i>🡄 Switch Statement</i>
    </b>
</a>  &emsp;

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