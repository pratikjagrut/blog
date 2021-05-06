---
title: "Structs part-1"
date: 2021-03-04T18:02:10+05:30
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

## What is Struct?

A struct is a sequence of named elements, called fields, each of which has a name and a type. Field names may be specified explicitly (IdentifierList) or implicitly (EmbeddedField). Within a struct, non-blank field names must be unique.
***<a href="https://golang.org/ref/spec#Struct_types" style="color:DodgerBlue" target="_blank"> From golang docs.</a>***

In simple words, a struct is a user-defined type that allows the collection of different types of elements. These elements are called fields. Structs can be used to keep certain data together. A struct is a very popular and widely used user-defined type in golang.

## Struct Declaration and Initialization

A struct is defined using keyword `type` and `struct`. Type keyword is used to define user-defined data types and the struct keyword specifies that it's a struct.

```
type Person struct {
    name    string
    age     int
}
```

To use the struct we create a struct object.

`var p Person` or shorthand `p := Person{}` will create an object of struct Person and will initialize its field with zero-value of their type.

```
package main

import "fmt"

type Person struct {
    name    string
    age     int
}

func main() {
    var p Person
    fmt.Printf("%#v", p)

    p1 := Person{}
    fmt.Printf("%#v\n", p1)
}
```

```
main.Person{name:"", age:0}
main.Person{name:"", age:0}
```
`%#v` a Go-syntax representation of the value.

***<a href="https://play.golang.org/p/APy03otXxrI" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

***Struct literals***

Creating a struct object with specifying field names

```
p := Person{name: "Jon Snow", age: 24}
p1 := Person{
    name: "Jon Snow",
    age:  24,
}
```

Order of the field does not matter when specifying field names

```
p := Person{age: 24, name: "Jon Snow"}
```

Creating a struct object without specifying field names

```
p := Person{"Jon Snow", 24}
p1 := Person{
  "Jon Snow",
  24,
}
```

```
package main

import "fmt"

type Person struct {
    name string
    age  int
}

func main() {
    p := Person{name: "Jon Snow", age: 24}
    fmt.Printf("%#v\n", p)

    p1 := Person{"Jon Snow", 24}
    fmt.Printf("%#v\n", p1)

    p2 := Person{
        name: "Jon Snow",
        age:  24,
    }
    fmt.Printf("%#v\n", p2)

    p3 := Person{
        "Jon Snow",
        24,
    }
    fmt.Printf("%#v\n", p3)
}
```
***<a href="https://play.golang.org/p/Ec0BcnT7dwg" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

## Accessing struct fields

To access individual fields of the struct `.` operator is used. e.g.`struct.fieldname`.

To use the value present in a struct field.
```
value := struct.fieldname
```

To assign a new value to the struct field
```
struct.fieldname = value
```

The below example demonstrates how to access the struct fields.

```
package main

import "fmt"

type Person struct {
    name string
    age  int
}

func main() {
    p := Person{name: "Jon Snow", age: 24}
    fmt.Printf("Name of the person: %v\n", p.name)
    fmt.Printf("Age of the person: %v\n", p.age)

    p.age = 30
    fmt.Printf("Updated age of the person: %v\n", p.age)
}
```
```
Name of the person: Jon Snow
Age of the person: 24
Age of the person: 30
```
***<a href="https://play.golang.org/p/jL6nC8aoHZs" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

## Pointer to the struct

<a href="/blog/golang/series/pointers" style="color:DodgerBlue">Pointers</i></a>  are special variable that stores address of another variable. We can store address of an struct object in pointer by passing the memory address using `&` operator.

```
package main

import "fmt"

type Person struct {
    name string
    age  int
}

func main() {
    // First way of creating pointer to struct
    personPtr := &Person{name: "James Bond", age: 32}
    fmt.Println(personPtr)
    fmt.Println(*personPtr) // Dereferencing the struct pointer

    fmt.Printf("Age of \"%v\" is \"%v\" \n", (*personPtr).name, (*personPtr).age)

    fmt.Println()
    // Second way of creating pointer to struct
    person := Person{name: "Jon Snow", age: 24}
    ptr := &person
    fmt.Println(ptr)
    fmt.Println(*ptr) // Dereferencing the struct pointer

    fmt.Printf("Age of \"%v\" is \"%v\" \n", (*ptr).name, (*ptr).age)
}
```
```
&{James Bond 32}
{James Bond 32}
Age of "James Bond" is "32" 

&{Jon Snow 24}
{Jon Snow 24}
Age of "Jon Snow" is "24" 
```
***<a href="https://play.golang.org/p/lJYO7n5moq5" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the above program, we're accessing the struct field by dereferencing the pointer `(*ptr).name, (*ptr).age` which reduces the readability and makes a program a little unkempt. The Golang also allow us to access fields of the struct without dereferencing the pointer as shown in the below example.

```
package main

import "fmt"

type Person struct {
    name string
    age  int
}

func main() {
    // First way of creating pointer to struct
    person := &Person{name: "James Bond", age: 32}
    fmt.Println(person)
    fmt.Printf("Age of \"%v\" is \"%v\" \n", person.name, person.age)
}
```
```
&{James Bond 32}
Age of "James Bond" is "32" 
```
***<a href="https://play.golang.org/p/nYCTG9in-ws" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the above program, we're accessing the field using `person.name, person.age`.
## Anonymous Struct and anonymous fields

### Anonymous Struct 

In Golang we're allowed to create a struct without a name such a struct is called an anonymous struct. This kind of struct is useful if we want to use the struct only once in the program. We can create a struct using the following syntax:

```
variable := struct{
    // field
}{
    // field value
}

// OR

PtrVariable := &struct{
    // field
}{
    // field value
}
```
Below is an example of an anonymous struct.
```
package main

import "fmt"

func main() {
    person := struct {
        name string
        age  int
    }{
        name: "James Bond",
        age:  32,
    }
    fmt.Println(person)

    ptrPerson := &struct {
        name string
        age  int
    }{
        name: "Jon Snow",
        age:  24,
    }
    fmt.Println(ptrPerson)
}
```
```
{James Bond 32}
&{Jon Snow 24}
```
***<a href="https://play.golang.org/p/1FQzainnKVs" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

### Anonymous fields

In Golang we're allowed to define anonymous fields in a struct. Anonymous fields are fields without a name. We just need to define the type of the field and GO will use that type as the name of that field. Below is the syntax of anonymous fields

```
type structName struct{
    // value type
    string
    int
    bool
}
```

```
package main

import "fmt"

type Person struct {
    string
    int
}

func main() {
    person := &Person{
        "James Bond", 
        32,
    }
    fmt.Println(person)

    fmt.Printf("Age of \"%v\" is \"%v\" \n", person.string, person.int)
}
```
```
&{James Bond 32}
Age of "James Bond" is "32"
```
***<a href="https://play.golang.org/p/r5kNOoc1Xb5" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In above example we access the anonymous fields by using value type as name of the field `person.string, person.int`.

***It is not allowed to define anonymous fields of the same type more than once.***

If we try to define struct as following golang will throw an error. 
```
type Person struct {
    string
    int
    string
}
```
```
./prog.go:8:2: duplicate field string
```

If we name one of the string fields then this error will not occur.
```
package main

import "fmt"

type Person struct {
    name string
    int
    string
    
}

func main() {
    person := &Person{
        "James Bond", 
        32,
        "Say Hello",
    }
    fmt.Println(person)
}
```
```
&{James Bond 32 Say Hello}
```
***<a href="https://play.golang.org/p/v8qcTOiZVCN" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

***Thank you for reading this blog please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/series/pointers">
  <b style="color:DodgerBlue">
    <i>🡄 Pointers</i>
  </b>
</a> &emsp;

<a href="/blog/golang/series/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/series/structs_part_2">
    <b style="color:DodgerBlue">
        <i>Structs part-2 🡆</i>
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