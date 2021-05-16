---
title: "Maps"
date: 2021-01-10T16:38:32+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
  - "2021"
---

The map is a collection of key-value pairs. It is an implementation of a Hash Table, which provides Create/Add, Read, Update and Delete operations over the data. Collection of key-value pairs is unordered and each key is unique. 


## Declaration and initialization

In general GO map looks like 

```
map[KeyType]ValueType
```
The KeyType could be anything that is comparable such as string, int etc. and ValueType could be anything, even it can be another map.

```
var m map[int]string
```
The above m is a map of int keys to string values.

Maps are reference types such as slices. So uninitialized maps value is nil i.e the zero value of the map is `nil`. The nil map has no keys and we can not add any key to it because it does not point to any initialized map. Trying to add a key to nil map will throw `panic: assignment to entry in nil map` error.

```
package main

import "fmt"

func main() {
	var m map[int]string
	fmt.Printf("%T\n", m)
	fmt.Println(m)
  	m[1] = "one"
}
```
```
map[int]string
map[]
panic: assignment to entry in nil map

goroutine 1 [running]:
main.main()
	/tmp/sandbox272715404/prog.go:9 +0x107
```
***<a href="https://play.golang.org/p/V_CiNrkv9gN" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***


So to get an initialized and ready to use map use `make` function.

```
package main

import "fmt"

func main() {
	m := make(map[int]string)
	fmt.Printf("%T\n", m)
	fmt.Println(m)
	m[1] = "one"
	fmt.Println(m)
}
```
```
map[int]string
map[]
map[1:one]
```
***<a href="https://play.golang.org/p/wBiLI4qulzY" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the background make function assigns and initializes hash map data structure and returns map value which points to the hash map.

**Map literal**

```
package main

import "fmt"

func main() {
	m := map[string]int{"foo": 0, "bar": 1}
	fmt.Printf("%T\n", m)
	fmt.Println(m)
}
```
***<a href="https://play.golang.org/p/PgpzaAp2X7q" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

## Working with the maps

**Create a map using make function**

We created a map m of string keys to int values.

```
m := make(map[string]int)
```

**Add key-value pair**

The syntax is fairly similar and easy to follow. Below key `one` is set to the value `1`.

```
m["one"] = 1
```

Update operation has the same syntax

```
m["one"] = 2
```

**Read a value**

```
i := m["one"]
```

If the key is not present then we get the value of type's zero value.

```
j := m["two"] // Key not present
// j == 0
```

We can check if the key is present in map with a two-value assignment statement.

```
k, ok := m["three"]
_, ok := m["three"] // Without retrieving the value.
```

If the key is present `ok == true` if the key is not found `ok == false`.

**Delete value**

The built-in delete function will delete the values from the map. It takes the `map variable` and `key` as an argument and it does not return anything. If the given key is not found it'll not do anything.

```
delete(m, "one")
```

**Iterating over the values in maps**

We can use `range` to iterate.

```
for key, value := range m {
    fmt.Println("Key:", key, "Value:", value)
}
```

While iterating over the map the iteration order is not specific, you may get different iteration order next time you iterate.

```
package main

import "fmt"

func main() {
	// **Create a map using make function**
	m := make(map[string]int)

	// **Add key-value pair**
	m["one"] = 1
	fmt.Println("Value of m: ", m)

	// Update
	m["one"] = 2
	fmt.Println("Updated value of m: ", m)
	fmt.Println()

	// **Read a value**
	i := m["one"]
	fmt.Println("Value of i", i)

	// Key not present
	j := m["two"]
	fmt.Println("Value of j: ", j)
	fmt.Println()

	// check if the key is present
	key, ok := m["three"]
	fmt.Println(key, ok)

	// Without retrieving the value.
	_, k := m["three"]
	fmt.Println(k)
	fmt.Println()

	// **Delete value**
	delete(m, "one")
	fmt.Println("Value of m after deletion: ", m)
	fmt.Println()

	// **Iterating over the values in maps**
	m["one"] = 1
	m["two"] = 2
	m["three"] = 3
	fmt.Println("Iterate over map")
	for key, value := range m {
		fmt.Println("Key:", key, "Value:", value)
	}
}
```
***<a href="https://play.golang.org/p/rT3ajhAyenr" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

***Thank you for reading this blog, and please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/series/array_slice">
  <b style="color:DodgerBlue">
    <i>🡄 Arrays and Slices</i>
  </b>
</a> &emsp;

<a href="/blog/golang/series/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/series/range">
    <b style="color:DodgerBlue">
        <i>Range 🡆</i>
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