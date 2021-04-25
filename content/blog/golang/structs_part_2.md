---
title: "Structs part-2"
date: 2021-03-04T21:53:38+05:30
draft: false
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
---
## Nested Structs

Golang allows us to use struct as a field of another struct, this pattern is called nesting. A nested struct can be defined using the following syntax.

```
type struct1 struct{
    // fields
}

type struct2 struct{
    // fields
    s struct1
}
```

Suppose we need to collect the data of a person, person's name, age and address. In address, we need to collect the city and country of that person. So we can do this using nested structs as shown below:

```
package main

import "fmt"

type Person struct {
    name    string
    age     int
    address Address
}

type Address struct {
    city, country string
}

func main() {
    person := &Person{
        name: "James Bond",
        age:  34,
        address: Address{
            city:    "London",
            country: "UK",
        },
    }

    fmt.Printf("%#v", person)
}
```
```
&main.Person{name:"James Bond", age:34, address:main.Address{city:"London", country:"UK"}}
```
***<a href="https://play.golang.org/p/e4A9YhIirqW" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

### Accessing fields of nested struct

To access the fields of nested struct we can do `structObj1.structObj2.structObj3........fieldName`.

Below is an example:

```
package main

import "fmt"

type Person struct {
    name    string
    age     int
    address Address
}

type Address struct {
    city, country string
}

func main() {
    person := &Person{
        name: "James Bond",
        age:  34,
        address: Address{
            city:    "London",
            country: "UK",
        },
    }

    fmt.Printf("Name: %v\n", person.name)
    fmt.Printf("Age: %v\n", person.age)
    fmt.Printf("City: %v\n", person.address.city)
    fmt.Printf("Country: %v\n", person.address.country)
}
```
```
Name: James Bond
Age: 34
City: London
Country: UK
```
***<a href="https://play.golang.org/p/OTkVLWQRf3Q" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

### Promoted fields

When the struct has another struct as an anonymous field then fields of anonymous structs are called promoted fields. This means we can access the fields of the nested struct without using the object of the nested struct, we can access them just by using the parent struct.

For example:

```
package main

import "fmt"

type Person struct {
    name string
    age  int
    Address
}

type Address struct {
    city, country string
}

func main() {
    person := &Person{
        name: "James Bond",
        age:  34,
        Address: Address{
            city:    "London",
            country: "UK",
        },
    }

    fmt.Printf("Name: %v\n", person.name)
    fmt.Printf("Age: %v\n", person.age)
    fmt.Printf("City: %v\n", person.city) // Instead of person.address.city we used person.city
    fmt.Printf("Country: %v\n", person.country) // Instead of person.address.country we used person.country
}
```
```
Name: James Bond
Age: 34
City: London
Country: UK
```
***<a href="https://play.golang.org/p/wkxWR0u6zoT" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

***Only unique fields of nested anonymous struct gets promoted.*** 

If the parent struct and nested anonymous struct has the same name field then that field will not be promoted.

```
package main

import "fmt"

type Person struct {
    name string
    age  int
    City
}

type City struct {
    name, country string
}

func main() {
    person := &Person{
        name: "James Bond",
        age:  34,
        City: City{
            name:    "London",
            country: "UK",
        },
    }

    fmt.Printf("Name: %v\n", person.name)
    fmt.Printf("Age: %v\n", person.age)
    fmt.Printf("City: %v\n", person.City.name)
    fmt.Printf("Country: %v\n", person.country)
}
```
***<a href="https://play.golang.org/p/gklcUfcRJV9" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

In this example, we have `City` a nested anonymous struct, whose fields are `name` and `country`. The `name` field is also available in `Person` struct. So when we try `person.name` then the compiler will give us access to Person's name field by default hence to access the name field from City struct we've to do `person.City.name`. The country field from City struct is unique here so we can just access it by using `person.country`.

## Comparing struct

Structs in golang are value type and so they can be compared.


Two struct values may be equal if:
- They're of the same type.
- Their corresponding fields are equal.
- Their corresponding fields should be comparable.

For example:

```
package main

import "fmt"

type Person struct {
    name string
    age  int
}

func main() {
    p1 := Person{
        name: "James Bond",
        age:  34,
    }

    p2 := Person{
        name: "James Bond",
        age:  34,
    }

    fmt.Println(p1 == p2) // true
}
```
***<a href="https://play.golang.org/p/KZrnjv-8qC1" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

***Comparing pointers to the struct will always be false, we need to compare dereferenced pointer values.***

```
package main

import "fmt"

type Person struct {
    name string
    age  int
}

func main() {
    p1 := &Person{
        name: "James Bond",
        age:  34,
    }

    p2 := &Person{
        name: "James Bond",
        age:  34,
    }
    fmt.Println(p1 == p2) // false
    fmt.Println(*p1 == *p2) // true
}
```
***<a href="https://play.golang.org/p/qcQYTF_BUcP" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

If structs contain incomparable values then struct values can not be compared using `==` operator, it will throw an error.

```
package main

import "fmt"

type Person struct {
    name     string
    age      int
    measures map[string]float32
}

func main() {
    p1 := Person{
        name: "James Bond",
        age:  34,
        measures: map[string]float32{
            "Height": 183,
            "Weight": 76,
        },
    }

    p2 := Person{
        name: "James Bond",
        age:  34,
        measures: map[string]float32{
            "Height": 183,
            "Weight": 76,
        },
    }
    fmt.Println(p1 == p2)
}
```
```
./prog.go:30:18: invalid operation: p1 == p2 (struct containing map[string]float32 cannot be compared)
```

In the above code, a map is used as a field in a struct and a map is an incomparable type. To compare such structs we can use `reflect.DeepEqual()` function.

```
package main

import (
    "fmt"
    "reflect"
)

type Person struct {
    name     string
    age      int
    measures map[string]float32
}

func main() {
    p1 := Person{
        name: "James Bond",
        age:  34,
        measures: map[string]float32{
            "Height": 183,
            "Weight": 76,
        },
    }

    p2 := Person{
        name: "James Bond",
        age:  34,
        measures: map[string]float32{
            "Height": 183,
            "Weight": 76,
        },
    }
    fmt.Println(reflect.DeepEqual(p1, p2)) // true
}
```
***<a href="https://play.golang.org/p/R1nK7gPUcrt" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***
## Structs and methods/receiver function

Golang supports both function and method. A method is a function that is defined for a particular type or with a receiver. A method in Golang also called a receiver function. Following is the example.

```
package main

import "fmt"

type Person struct {
    name string
    age  int
}

func (p Person) GetInfo() string {
    return fmt.Sprintf("\"%v\" is \"%v\" years old.", p.name, p.age)
}

func main() {
    p := Person{
        name: "James Bond",
        age:  34,
    }

    fmt.Println(p.GetInfo())
}
```
```
"James Bond" is "34" years old.
```
***<a href="https://play.golang.org/p/NnCg1hi-t2d" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

We can also use a pointer as the receiver of the method. The difference between value as receiver and pointer as a receiver is, golang passes everything as value and hence in value receiver the function will get a copy of struct and function will not touch original struct whereas in pointer as a receiver function will get a copy of a pointer which will be pointing to an original struct.

The below examples illustrates the difference between pointer and value as a receiver.

```
package main

import "fmt"

type Person struct {
    name string
    age  int
}

// Value as receiver
func (p Person) UpdateAge(age int) {
    p.age = age
}

// Pointer as receiver
func (p *Person) UpdateName(name string) {
    p.name = name
}

func main() {
    p := Person{
        name: "James Bond",
        age:  34,
    }

    // Value as receiver example
    fmt.Println("Age before update: ", p.age)
    p.UpdateAge(24)
    fmt.Println("Age after update: ", p.age)

    fmt.Println()

    // Pointer as receiver
    fmt.Println("Name before update: ", p.name)
    p.UpdateName("Jon Snow")
    fmt.Println("Name after update: ", p.name)
}
```
In above example `UpdateAge()` is using value as receiver and `UpdateName()` is using pointer as a receiver.
```
Age before update:  34
Age after update:  34

Name before update:  James Bond
Name after update:  Jon Snow
```
***<a href="https://play.golang.org/p/gvDMobx70PK" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***
## Empty Struct

In GOlang, we can have an empty struct. A struct without any field is called an empty struct. Below is the signature of an empty struct.
```
type T struct{}
var s struct{}
```

Empty struct does not have any field so it does not occupy any memory i.e it occupies `zero bytes` of storage.
```
var s struct{}
fmt.Println(unsafe.Sizeof(s)) // prints 0
```

We can create an array of the empty struct and still it occupies zero bytes.
```
var arr [100000]struct{}
fmt.Println(unsafe.Sizeof(arr)) // prints 0
```

The slice of structs will consume some byte just to store pointer, length and capacity of an underlying array but structs still will be of zero bytes.

```
sls := make([]struct{}, 100000)
fmt.Println(unsafe.Sizeof(sls)) // prints 24
```

```
package main

import (
    "fmt"
    "unsafe"
)

func main() {
    var s struct{}
    fmt.Println("Size of an empty struct: ", unsafe.Sizeof(s)) // prints 0

    var arr [100000]struct{}
    fmt.Println("Size of an array of an empty struct: ", unsafe.Sizeof(arr)) // prints 0

    sls := make([]struct{}, 100000)
    fmt.Println("Size of a slice of an empty struct: ", unsafe.Sizeof(sls)) // prints 24
}
```
```
Size of an empty struct:  0
Size of an array of an empty struct:  0
Size of a slice of an empty struct:  24
```
***<a href="https://play.golang.org/p/SB9x1tSICW1" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

Read more about the empty struct and its use cases at ***<a href="https://dave.cheney.net/2014/03/25/the-empty-struct" style="color:DodgerBlue" target="_blank">Dave Cheney's blog.</a>***

## Array/Slice of structs

The ***<a href="/blog/golang/array_slice" style="color:DodgerBlue" target="_blank">Array/Slice</a>*** is a collection of the same type of element in a contiguous memory location. We can create an array/slice of structs.

```
package main

import "fmt"

type Person struct {
    name string
    age  int
}

func newPerson(name string, age int) *Person {
    return &Person{
        name: name,
        age:  age,
    }
}

func main() {
    people := make([]*Person, 0) // slice of a struct Person with initial length 0

    people = append(people, newPerson("James Bond", 34))
    people = append(people, newPerson("Jon Snow", 24))
    people = append(people, newPerson("Joey Tribbiani", 32))

    for _, person := range people {
        fmt.Println(person)
    }

    fmt.Println("Name of friends character: ", people[2].name)
}
```
```
&{James Bond 34}
&{Jon Snow 24}
&{Joey Tribbiani 32}
Name of friends character:  Joey Tribbiani
```
***<a href="https://play.golang.org/p/g9-754U92un" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

***Thank you for reading this blog please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/structs_part_1">
  <b style="color:DodgerBlue">
    <i>🡄 Structs part-1</i>
  </b>
</a> &emsp;

<a href="/blog/golang/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/interface_part_1">
    <b style="color:DodgerBlue">
        <i>Interface Part-1 🡆</i>
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