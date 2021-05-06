---
title: "Interface Part-2"
date: 2021-04-25T10:46:37+05:30
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
## Type assertion

Type assertion is used to get the underlying concrete value of the interface variable.
`i.(Type)` this is the syntax of type assertion, where:

`i -> interface variable`

`Type -> type that implements interface`

Let's see an example of type assertion.

```
package main

import "fmt"

type Person interface {
    info() string
}

type Student struct {
    name string
}

func (s Student) info() string {
    return fmt.Sprintf("Student name is %s\n", s.name)
}

func main() {
    s := Student{
        name: "Barry Allen",
    }
    var p Person = s
    name := p.(Student)
    fmt.Println(name)
}
```
```
{Barry Allen}
```
***<a href="https://play.Golang.org/p/fzNWgZvcdVk" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the above example, we create a Person interface which is then implicitly implemented by the Student struct by implementing the info method.
`var p Person = s` this statement creates interface variable `p` and assign Student struct type variable `s` to it.
`name := p.(Student)` this statement extracts the concrete value of type `Student` and assign it to the `name` variable.

In the above program, type Student implements the Person interface hence `p.(Student)` can hold the concrete value of type Student.
But if `Type` from `i.(Type)` does not implement the interface then Go will throw a compilation error. Below is an illustrative example.

```
package main

import "fmt"

type Person interface {
    info() string
}

type Student struct {
    name string
}

func main() {
    var p Person
    name := p.(Student)
    fmt.Println(name)
}
```
```
./prog.go:15:11: impossible type assertion:
    Student does not implement Person (missing info method)
```
***<a href="https://play.Golang.org/p/o7rOeX5EYKa" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

If the `Type` implements the interface but the concrete value of that type is not available then Go will panic in runtime.

```
package main

import "fmt"

type Person interface {
    info() string
}

type Student struct {
    name string
}

func (s Student) info() string {
    return fmt.Sprintf("Student name is %s\n", s.name)
}

func main() {
    var p Person
    name := p.(Student)
    fmt.Println(name)
}
```
```
panic: interface conversion: main.Person is nil, not main.Student

goroutine 1 [running]:
main.main()
    /tmp/sandbox657831697/prog.go:19 +0x45
```
***<a href="https://play.Golang.org/p/yuLoDEbO3zr" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

Similarly, if the concrete type of interface variable does not match with `Type` of `i.(Type)` then Go will panic in runtime.

```
package main

import "fmt"

type Person interface {
    info() string
}

type Student struct {
    name string
}

func (s Student) info() string {
    return fmt.Sprintf("Student name is %s\n", s.name)
}

type Teacher struct {
    name string
}

func (s Teacher) info() string {
    return fmt.Sprintf("Teacher name is %s\n", s.name)
}

func main() {
    t := Teacher{
        name: "Richard Feynman",
    }
    var p Person = t
    name := p.(Student)
    fmt.Println(name)
}
```
```
panic: interface conversion: main.Person is main.Teacher, not main.Student

goroutine 1 [running]:
main.main()
    /tmp/sandbox133075599/prog.go:30 +0x45
```
***<a href="https://play.Golang.org/p/-6kfh5zgUXj" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

To avoid the above panic errors Go has another way for type assertion. 

`value, ok := i.(Type)`

In the above syntax, `Ok` is a boolean variable. It will be false if i.(Type) has no concrete value and vice versa.

```
package main

import "fmt"

type Person interface {
    info() string
}

type Student struct {
    name string
}

func (s Student) info() string {
    return fmt.Sprintf("Student name is %s\n", s.name)
}

type Teacher struct {
    name string
}

func (s Teacher) info() string {
    return fmt.Sprintf("Teacher name is %s\n", s.name)
}

func main() {
    var p Person
    name, ok := p.(Student)
    fmt.Println(name, ok)

    t := Teacher{
        name: "Richard Feynman",
    }
    var p1 Person = t
    name, ok = p1.(Student)
    fmt.Println(name, ok)
}
```
```
{} false
{} false
```
***<a href="https://play.Golang.org/p/8ox44oLj9d_4" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

## Type switch

Type switch is similar to switch case statement where type switch compares the concrete type of an interface against types specified in cases. Below is the syntax of the type switch:

```
switch i.(type) {
    case float32:
        // Something to do
    case int:
        // Logic
    default:
        // Default logic
    }
```

Here `i.(type)` syntax is fairly similar to type assertion syntax, where `i` is interface but instead of `value type` we use keyword `type`.

```
package main

import (
    "fmt"
)

func guessType(i interface{}) {
    switch i.(type) {
    case string:
        fmt.Println("It is string")
    case int:
        fmt.Println("It is Int")
    case bool:
        fmt.Println("It is boolean")
    default:
        fmt.Println("IDK")
    }
}

func main() {
    guessType(10)
    guessType("Hello")
    guessType(true)
    guessType(10.11)
}
```
```
It is Int
It is string
It is boolean
IDK
```
***<a href="https://play.Golang.org/p/Z5RM_vGPSWF" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the above example, we're passing an empty interface as an argument to function. 
The empty interface is implemented by all the type so we can pass any type of parameter while calling that function.

`i.(type)` evaluates the concrete type of an interface and then a matching case is executed if none of the cases is matched then the default case is executed.

## Implementing interfaces using pointer receivers vs value receivers

In Golang methods can have both pointer or value as a receiver which restricts the accessibility of methods only to the type of its receiver.
Methods from an interface can also pointer or value as a receiver in their implementation.

***Implementing interface with value receiver***

```
package main

import (
    "fmt"
)

type Car interface {
    information()
}

type Ferrari struct {
    name   string
    colour string
}

func (f Ferrari) information() {
    fmt.Printf("Name of the car: %s\n", f.name)
    fmt.Printf("Colour of the car: %s\n", f.colour)
    fmt.Println()
}

func main() {
    var c1 Car

    f := Ferrari{
        name:   "SF90 STRADALE",
        colour: "ROSSO CORSA",
    }
    c1 = f
    c1.information()

}
```
```
Name of the car: SF90 STRADALE
Colour of the car: ROSSO CORSA
```
***<a href="https://play.Golang.org/p/D0hHbX-1g90" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the above code, type `Ferrari` is implementing method `information` from an interface `Car` with a value receiver and in the main function, we're assigning variable `f` of struct `Ferrari` to variable `c1` of an interface `Car` and then calling `information` method using interface variable.

***Implementing interface with pointer receiver***

```
package main

import (
    "fmt"
)

type Car interface {
    information()
}
type Porsche struct {
    name   string
    colour string
}

func (p *Porsche) information() {
    fmt.Printf("Name of the car: %s\n", p.name)
    fmt.Printf("Colour of the car: %s\n", p.colour)
    fmt.Println()
}

func main() {

    p := &Porsche{
        name:   "718 SPYDER",
        colour: "BLACK",
    }
    var c2 Car = p
    c2.information()
}
```
```
Name of the car: 718 SPYDER
Colour of the car: BLACK
```
***<a href="https://play.Golang.org/p/fGVGiYL3qrJ" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the above code, type `Porsche` is implementing method `information` from an interface `Car` with a pointer receiver and in the main function we're assigning variable pointer `p` of struct `Porsche` to variable `c2` of an interface `Car` and then calling `information` method using interface variable.

In Golang, a method with value receiver or pointer receiver can be called on either value or pointer.
It means if you're implementing a method with a value receiver then you can use a value or pointer of that type to call that method.

**But in the case of an interface does this phenomenon work?**

***Calling method with value receiver on pointer type***

In the below code, we implement the method `information` with value receiver and call it on pointer type.

```
package main

import (
    "fmt"
)

type Car interface {
    information()
}

type Ferrari struct {
    name   string
    colour string
}

func (f Ferrari) information() {
    fmt.Printf("Name of the car: %s\n", f.name)
    fmt.Printf("Colour of the car: %s\n", f.colour)
    fmt.Println()
}

func main() {
    var c Car
    f1 := &Ferrari{
        name:   "SF90 STRADALE",
        colour: "ROSSO CORSA",
    }
    c = f1
    c.information()
}
```
```
Name of the car: SF90 STRADALE
Colour of the car: ROSSO CORSA
```
***<a href="https://play.Golang.org/p/6OS8urGqkA5" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the above code, the pointer to value conversion is done by Golang implicitly.
It is valid to call a method with value type on any value or anything whose value can be dereferenced.

***Calling method with pointer receiver on value type***

In the below code, we implement the method `information` with pointer receiver and call it on the value type.

```
package main

import (
    "fmt"
)

type Car interface {
    information()
}

type Porsche struct {
    name   string
    colour string
}

func (p *Porsche) information() {
    fmt.Printf("Name of the car: %s\n", p.name)
    fmt.Printf("Colour of the car: %s\n", p.colour)
    fmt.Println()
}

func main() {
    var c Car

    p := Porsche{
        name:   "718 SPYDER",
        colour: "BLACK",
    }
    c = p
    c.information()

}
```
```
./prog.go:29:4: cannot use p (type Porsche) as type Car in assignment:
    Porsche does not implement Car (information method has pointer receiver)
```
***<a href="https://play.Golang.org/p/cP0WQqvbQbr" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

In the above code, we're implementing the `information` method using pointer receiver and then calling it on value type instead of a pointer, and we're getting compilation error.
*So what's happening?*

If we look at the implementation of the `information` method it has a pointer receiver and we're calling it on `p` which is a value type and does not implement the `Car` interface.
Hence we see the compilation error.

But in Golang, the method with value receiver or pointer receiver can be called on either value or pointer then why is this failing here?

This is because: it is completely valid to call the pointer receiver method on a pointer or on anything value whose address can be acquired that value which is addressable. 
In this case, the value type is assigned to the interface variable which is now a concrete value of the interface whose address can not be obtained and hence we get that compilation error. 

***Note: If we call a method directly with struct variable then this issue will not occur.***

## Comparing interface's variables

The two interface variables are comparable only if the `concrete value and concrete type` are comparable.
Interface variables can be compared with `==` and `!=` operators.

If the concrete types or concrete values are not the same then the interface variables are not equal.
If the concrete types or concrete values are the same then the interface variables are equal.
Variables of an empty interface are always equal. 
***<a href="https://Golang.org/ref/spec#Comparison_operators" style="color:DodgerBlue" target="_blank">Read more on Golang comparison operators.</a>***

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

func main() {
    var i Int = 10
    var f Float = 5.5

    var v1 fmt.Stringer = i
    var v2 fmt.Stringer = f

    fmt.Println(v1 == v2) // false, because concrete types are not same

    var i1 Int = 6
    var v3 fmt.Stringer = i1

    fmt.Println(v1 == v3) // false, because concrete values are not same

    var f2 Float = 5.5
    var v4 fmt.Stringer = f2

    fmt.Println(v2 == v4) // true

    var m, n interface{}
    fmt.Println(m == n) // true
}
```
***<a href="https://play.Golang.org/p/crqoWj9PbmQ" style="color:DodgerBlue" target="_blank">Run this code in Go Playground</a>***

### Some good resources to read

***<a href="https://research.swtch.com/interfaces" style="color:#2eb8ac" target="_blank">Go Data Structures: Interfaces by Russ Cox</a>***

***<a href="https://blog.golang.org/laws-of-reflection" style="color:#2eb8ac" target="_blank">The Laws of Reflection by Rob Pike</a>***

***Thank you for reading this blog please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/series/interface_part_1">
  <b style="color:DodgerBlue">
    <i>🡄 Interface Part-1</i>
  </b>
</a> &emsp;

<a href="/blog/golang/series/contents">
  <b style="color:DodgerBlue">
    <i>• Contents</i>
  </b>
</a>  &emsp;

<!-- <a href="/blog/golang/series/">
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