---
title: "Interface Part-1"
date: 2021-03-07T20:14:16+05:30
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
In Golang, an interface is a set of method signatures. When any type defines all the methods from an interface then that type implements the interface. So we can state that interface defines the behaviour of the object/type.

For example, an animal walks, eats and sleeps so we can have an interface `Animal` which declares the methods `walk, eat and sleep` and any animal e.g. `Tiger`, who walks, eats and sleeps so we say Tiger implements the animal interface. 

Another example could be of shapes, any shape has an area and perimeter. So the `Shape` interface can declare `area` and `perimeter` methods and any shape such as rectangle or triangle can implement a shape interface.

It is much similar to the OOP world's interface, where the interface specifies the methods and type decides how to implement them. 
In OOP programming we might have to use the `implement` keyword to explicitly implement the interface, but in Golang, if a type defines all the method from an interface then it `implicitly implements` interface.

## Declaring and Implementing Interface

To declare an interface in Golang we use the `type` and `interface` keyword. Below is a syntax:

```
type InterfaceName interface {
  // Method declaration
}
```
`Stringer` interface is declared in the `fmt` package, which has a signature of the only one method `String`.

***<a href="https://Golang.org/pkg/fmt/#Stringer" style="color:DodgerBlue" target="_blank">fmt.Stringer doc</a>***
```
type Stringer interface {
    String() string
}
```

To implement a particular interface a type needs to implement all the methods with exact name and signature defined in that interface. `Interfaces in Go are implicitly implemented.`

Below is an implementation of the `fmt.Stringer` interface from the standard library.

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
    pincode       int
}

func (p Person) String() string {
    return fmt.Sprintf("My name is '%s', I'm '%d' years old, I love in '%s', '%s'", p.name, p.age, p.address.city, p.address.country)
}

func main() {
    person := Person{
        name: "James Bond",
        age:  34,
        address: Address{
            city:    "London",
            pincode: 123456,
            country: "UK",
        },
    }

    address := Address{
        city:    "London",
        country: "UK",
        pincode: 123456,
    }

    fmt.Println(person)
    fmt.Println(address)
}
```
```
My name is 'James Bond', I'm '34' years old, I love in 'London', 'UK'
{London UK 123456}
```
***<a href="https://play.golang.org/p/0C_8uGzb04A" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the above example, we've two structs one is `Person` and the other one is `Address` and 
only the `Person` struct implements the `Stringer` interface by implementing the `String()` method because of which we could print the custom string format output.

Notice the output, the `person` variable has its custom string and the `address` variable prints output in curly braces.

Once a type implements an interface then the method implemented by that type can also be called using interface variable.

```
package main

import (
    "fmt"
)

type Shape interface {
    Area()
}

type Square struct {
    side int
}

func (s Square) Area() {
    fmt.Printf("Area of the square is %d\n", s.side*s.side)
}

func main() {
    sq := Square{
        side: 10,
    }
    var sh Shape = sq
    sq.Area()
    sh.Area()
}
```
```
Area of the square is 100
Area of the square is 100
```
***<a href="https://play.golang.org/p/cQmfCtE3GMC" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the above program, type `Square` is implementing the `Shape` interface. In the main function, we call the implemented method `Area` on variable `sq` of type `Square` and on variable `sh` of type `Shape` interface and the program still works fine.

## Interface's types and values

The variable of an interface stores, a concrete value and the type of that concrete value called concrete type. This representation can be envisaged as a tuple `(type, value)`. An interface variable can store any concrete type and value as long as that type and value implement the interface's method. The below program illustrate the type and value of the interface.

```
package main

import "fmt"

type Int int

func (i Int) String() string {
    return fmt.Sprintf("Value of Int is %d", i)
}

type Float float32

func (f Float) String() string {
    return fmt.Sprintf("Value of Float is %f", f)
}

func describe(s fmt.Stringer) {
    fmt.Printf("Concrete type of an interface is %T\n", s)
    fmt.Printf("%v\n", s)
    fmt.Println()
}

func main() {
    var s fmt.Stringer
    describe(s)

    var i Int = 10
    s = i
    describe(s)

    var f Float = 15.0005
    s = f
    describe(f)
}
```
```
Concrete type of an interface is <nil>
<nil>

Concrete type of an interface is main.Int
Value of Int is 10

Concrete type of an interface is main.Float
Value of Float is 15.000500
```
***<a href="https://play.Golang.org/p/9_yZVvc3gsa" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the above program:

We create two customs types Int and Float whose underlying types are int and float32 respectively.
Both types implement fmt.Stringer interface by implementing `String() string` function.

The statement `var s fmt.Stringer` creates variable of an interface fmt.Stringer with zero value `<nil>`.

In the main function, we assign variable of type Int and Float to the interface variable s. 
This means when a particular type implements an interface then the variable of that type can also be represented as the type of an interface.

The type and value of the interface depend on the type and which implements that interface. 
Sometimes the concrete type and value of an interface are also called dynamic type and value.
We call it dynamic because we can assign any type to the interface as long as that type implements the interface.

### Zero Value of an interface

The zero value of an interface is `<nil>`. 
A nil interface has its concrete value and concrete type nil.

```
package main

import "fmt"

func main() {
    var s fmt.Stringer
    fmt.Printf("The concrete type of a nil interface is %T\n", s)
    fmt.Printf("The concrete value of a nil interface is %v", s)
}
```
```
The concrete type of a nil interface is <nil>
The concrete value of a nil interface is <nil>
```
***<a href="https://play.golang.org/p/8GKGXSwOEOw" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

If we try to call a method on a nil interface, the program will panic.

```
package main

import "fmt"

type Day string

func (day Day) String() string {
    return string(day)
}

func main() {
    var s fmt.Stringer
    fmt.Println("The day is ", s.String())
}
```
```
panic: runtime error: invalid memory address or nil pointer dereference
[signal SIGSEGV: segmentation violation code=0x1 addr=0x0 pc=0x497683]

goroutine 1 [running]:
main.main()
    /tmp/sandbox117008893/prog.go:13 +0x23
```
***<a href="https://play.golang.org/p/9KwItPMGxWD" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

The error pretty much is self-explanatory. The underlying concrete value and type are nil so the method can not be called on that object.

## Empty Interface

An interface with zero methods is called an empty interface.
The empty interface is represented by `interface{}`. 

Since an empty interface has no methods it is implemented by all the types.
Let's dive into an example:

```
package main

import "fmt"

func getType(s interface{}) {
    fmt.Printf("%T\n", s)
}

func main() {
    i := 10
    getType(i)

    s := "Hola"
    getType(s)

    f := 12.24
    getType(f)

    b := true
    getType(b)
}
```
```
int
string
float64
bool
```
***<a href="https://play.Golang.org/p/m6GMNMIBAUo" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

The function `getType(s interface{})` accepts an empty interface as an argument hence we were able to pass any type of variable to the function.

Have you ever wondered how the `Println` function can accept any number of values of different different types and print it? 
The answer is `interface{}`. 

This is the signature of Println function `func Println(a ...interface{}) (n int, err error)`. 
The Println function is a `variadic function` which can take arguments of type `interface{}`.

## Implementing multiple interfaces

 A type can implement more than one interface. Let's see how it is done.

 ```
 package main

import (
    "fmt"
)

type Shape interface {
    Area()
}

type Quadrilateral interface {
    isQuadrilateral() bool
}

type square struct {
    noOfSides int
    side      int
}

func (s square) Area() {
    fmt.Printf("Area of the square is %d\n", s.side*s.side)
}

func (s square) isQuadrilateral() bool {
    if s.noOfSides == 4 {
        return true
    }
    return false
}

func main() {
    s := square{
        noOfSides: 4,
        side:      10,
    }

    var sh Shape = s
    sh.Area()

    var q Quadrilateral = s
    fmt.Println(q.isQuadrilateral())
}
```
```
Area of the square is 100
true
```
***<a href="https://play.Golang.org/p/1alfdI_h-DW" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the above example, we've two interfaces `Shape` and `Quadrilateral`. Type `square` implements both interfaces. The program is easy and self-explanatory.

## Embedding interfaces

In Golang, one interface can embed any other interface.
Golang does not support inheritance but this embedding of interfaces can give a sense of inheritance.
Below is an illustrative example:

```
package main

import (
    "fmt"
)

type Shape interface {
    Area()
}

type Quadrilateral interface {
    Shape
    fmt.Stringer
    isQuadrilateral() bool
}

type square struct {
    noOfSides int
    side      int
}

func (s square) Area() {
    fmt.Printf("Area of the square is %d\n", s.side*s.side)
}

func (s square) isQuadrilateral() bool {
    if s.noOfSides == 4 {
        return true
    }
    return false
}

func (s square) String() string {
    return fmt.Sprintf("Number of sides are %d and dimension of side is %d", s.noOfSides, s.side)
}

func main() {
    s := square{
        noOfSides: 4,
        side:      10,
    }
    var q Quadrilateral = s
    fmt.Println(s.String())
    s.Area()
    fmt.Println(q.isQuadrilateral())
}
```
```
Number of sides are 4 and dimension of side is 10
Area of the square is 100
true
```
***<a href="https://play.Golang.org/p/UOQv16mFLn7" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the above example, we have `Shape` and `fmt.Stringer` interfaces which are embedded in the `Quadrilateral` interface.
The type `square` implements method from `Shape`, `fmt.Stringer` and `Quadrilateral` interfaces.
In the main function, we're creating a variable of type `square` and assigning it to the variable of the `Quadrilateral` interface.
After that, we're calling all the method implemented by type `square` using only the variable of the `Quadrilateral` interface.

***Thank you for reading this blog please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/series/structs_part_2">
  <b style="color:DodgerBlue">
    <i>🡄 Structs Part-2</i>
  </b>
</a> &emsp;

<a href="/blog/golang/series/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<a href="/blog/golang/series/interface_part_2">
    <b style="color:DodgerBlue">
        <i>Interface Part-2 🡆</i>
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