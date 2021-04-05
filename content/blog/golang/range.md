---
title: "Range"
date: 2021-01-11T23:41:28+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
---

The range keyword is used to iterate over various data types. It is used in for loops and its return values are dependent on the data types over which we're using range keyword.

### Range over slice/array

Range on **Array and Slice** returns the first value as an index and second value as an element located at that index.
```
package main

import "fmt"

func main() {
	nums := []int{1, 2, 3, 4, 5}
	for i, v := range nums {
		fmt.Printf("Index :%d, value: %d\n", i, v)
	}
}
```
Output:
```
Index :0, value: 1
Index :1, value: 2
Index :2, value: 3
Index :3, value: 4
Index :4, value: 5
```
***<a href="https://play.golang.org/p/WwdJkWeMfpA" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

### Range over maps

Range on **Map** returns the first value as a key and second value is a value associated with that key.

```
package main

import "fmt"

func main() {
	m := map[string]int{"foo": 0, "bar": 1}
	for k, v := range m {
		fmt.Printf("Key :%s, value: %d\n", k, v)
	}
}
```
Output:
```
Key :foo, value: 0
Key :bar, value: 1
```
***<a href="https://play.golang.org/p/DA_QyJzPFB7" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

### Range over a string

Range on **String** returns the first value as an index and second value is rune int.

```
package main

import "fmt"

func main() {
	str := "golang"
	for i, s := range str {
		fmt.Printf("Index :%d, Rune value: %d\n", i, s)
	}
}
```
Output:
```
Index :0, Rune value: 103
Index :1, Rune value: 111
Index :2, Rune value: 108
Index :3, Rune value: 97
Index :4, Rune value: 110
Index :5, Rune value: 103
```
***<a href="https://play.golang.org/p/lRFYbsOObFc" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

*Rune int value can be type cast string using string() method. e.g. string(103) == g*

### Range over a channel

Range on **Channel** returns only one value that is the value received from the channel.

```
package main

import "fmt"

func main() {
	channel := make(chan string, 2)
	channel <- "Hello"
	channel <- "World"
	close(channel)

	for v := range channel {
		fmt.Println(v)
	}
}
```
***<a href="https://play.golang.org/p/YPHa5RvPGbP" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***


***\*KEEP IN MIND\****

You can not update the value in the range loop.

```
package main

import "fmt"

func main() {
	nums := []int{1, 2, 3, 4, 5}
	fmt.Println("Slice before range: ", nums)

	for _, v := range nums {
		v += 1
	}

	fmt.Println("Slice after range: ", nums)
}
```
Output:
```
Slice before range:  [1 2 3 4 5]
Slice after range:  [1 2 3 4 5]
```
***<a href="https://play.golang.org/p/iGimIFCgcL_J" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

In the above example, I try to increment all the values of the slice by 1 but the slice is unaffected. This is because the range loop copies the value from slice to local variable. So to update the slice we'll need to use traditional way `nums[i] += 1`.

***Thank you for reading this blog please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/maps">
  <b style="color:DodgerBlue">
    <i>🡄 Maps</i>
  </b>
</a> &emsp;

<a href="/blog/golang/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/functions">
    <b style="color:DodgerBlue">
        <i>Functions 🡆</i>
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