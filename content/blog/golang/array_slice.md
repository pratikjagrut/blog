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

### Array Declarations 

An array type definition specifies length and type of element. 
The array `[n]T` is of length `n` and type `T`.

```
// This array can hold 3 integers.
var i [3]int
```

Arrays can be indexed in usual way, to access the `n<sup>th</sup>` element we can do `a[n]`.

```
i[0] = 1
i[1] = 10
i[2] = 100
```

**Array literal**

```
j := [3]string{"Go", "is", "fun"}
```

We can make compiler to compute the length of an array.

```
j := [...]string{"Go", "is", "fun"}
```

In both cases, the type of `j` is `[3]string`.

***You can refer <a href="https://github.com/pratikjagrut/go-tutorial/blob/master/06_array/main.go" style="color:DodgerBlue" target="_blank">main.go</a> file for arrays examples***


## Slices

Arrays are a bit inflexible, so slices are widely used in GO.
Slices are built on arrays giving it more flexibility, power and convenience.

The slice type is `[]T`, specified without length and `T` is the element type.
 
### Slice formation

A slice literal is like an array literal without the length.

```
i := []int{1, 2, 3, 4, 5,}
```

#### Creating a slice with make

Slices can be created with the built-in make function; this is how you create dynamically-sized arrays. 

```
func make([]T, len, cap) []T
```
Where,
- []T: Type of underlying array
- len: Length of the underlying array
- cap: Capacity of the underlying array, cap is optional


```
b := make([]int, 3, 5)
```

If the capacity argument is omitted then capacity defaults to length.

```
a := make([]int, 5)
```

##### Length and capacity

The length of a slice is the number of elements it contains.

The capacity of a slice is the number of elements in the underlying array, counting from the first element in the slice.

Length: `len(s)`

Capacity: `cap(s)`


#### Creating a slice from an array

Slice can be formed by specifying 2 indices, high bound and low bound separated by a colon, `s[low : high]`.
This selects a half-open range which includes the first element but excludes the last one.
 
```
odds := [5]int{1, 3, 5, 7, 9}

var o []int = odds[1:4]
m := odds[1:4]
```

We can skip low or high bound to use their defaults. <br> 
For low bound default is `0` and for high bound default is `length of an array`.

`a[:high]`, `a[low:]` 

To create a slice of an entire array we can omit both high bound and low bound.

```
odds := [5]int{1, 3, 5, 7, 9}
o := odds[:]
```

### Slice internals

A slice does not store any data, it just describes a section of an underlying array.

A slice consists of a pointer to the array segment, length of an array segment and its capacity (the maximum length of the segment).

<table border = "1" cellspacing="0" bordercolor="black" style="width: 15%" >
  <tr>
    <th>ptr (*Ele)</th>
  </tr>
  <tr>
    <th>Length (int)</th>
  </tr>
  <tr>
      <th>Capacity (int)</th>
  </tr>
</table>


#### Relation of array and slice

When we create a slice we create a slice variable which stores the pointer, length and capacity of the underlying array. Slicing does not copy the elements, it creates a new slice variable pointing to the original array. Hence changing element of the slice will make those changes to an underlying array and all other slices which share the same underlying array will be affected.

```
alphabet := [5]string{"A", "B", "C", "D"}

i := alphabet[0:3]
j := alphabet[1:4]

i[2] = "P" // This changes will affect alphabet, i ,j slices
```

### Append and copy functions

#### Append

```
func append(s []T, x ...T) []T
```

The append function appends the data at the end of the slice. If the destination slice has enough capacity then it is re-sliced to accommodate the new element but if capacity is not enough then new underlying array is created and allocated.

```
a := make([]int, 1)
// a == []int{0}
a = append(a, 1, 2, 3)
// a == []int{0, 1, 2, 3}
```

**Appending one slice to another**

```
a := []string{"a", "b", "c"}
b := []string{"d", "e"}
a = append(a, b...)
// a == []string{"a", "b", "c", "d", "e"}
```

#### Copy

Slice can not grow beyond the capacity of the underlying array if it tries to grow will cause runtime panic error similar to index out of bounds error.

```
nums := [3]int{1, 2, 3} // array
n := nums[:] // slicing nums array
n[3] = 4 // this will throw runtime error

panic: runtime error: index out of range [3] with length 3
```

So to achieve the dynamic array we've to create a new bigger slice and copy the content from the old slice to a new slice.

```
nums := [3]int{1, 2, 3} // array
n := nums[:] // slicing nums array

o := make([]int, len(n)+1)
copy(o, n)
o[3] = 4
```

The copy function takes destination slice and source slice as an argument and returns the number of elements copied.

```
func copy(dst, src []T) int
```

##### Examples

**Copy from one slice to another slice**

```
var odds = make([]int, 3)
n := copy(odds, []int{1, 3, 5}) // n == 3, odds == []int{1, 3, 5}
```

**Copy between same slice**

```
odds := []int{1, 3, 5}
n := copy(odds, odds[1:]) // n == 2, s == []int{3, 5, 5}
```

In this example, the values at index 0 and 1 are replaced by values at index 1 and 2.

**Copy from a string to a byte slice**

```
var s = make([]byte, 5)
copy(s, "Hello, world!") // s == []byte("Hello")
```

In this example, the slice s has a capacity of 5 elements so the only string Hello is copied to it.

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

<a href="/blog/golang/maps">
    <b style="color:DodgerBlue">
        <i>Maps 🡆</i>
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