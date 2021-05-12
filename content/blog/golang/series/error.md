---
title: "Error"
date: 2021-05-08T18:54:08+05:30
draft: true
author: "Pratik Jagrut"
layout: "blog"
categories:
  - "golang"
tags:
  - "golang"
  - "programming"
---
`Error` is an unexpected result of an unexpected circumstances or of an abnormal behavior of program.
`Error Handling` is a process of knowing where error could occur and if it occurs then having a mechanism to handle that error.
***So what could be these, unexpected circumstances or abnormal behavior?***
For example, Network connection error, user entering wrong data, function invoked with wrong values or file not found and many other scenarios.

In Golang, `an error is a value type whose zero value is nil` i.e error is a built-in type.
This makes developers to treat error as a ***[first class citizen](https://en.wikipedia.org/wiki/First-class_citizen)***.
Errors are treated in the similar way as int, string, bool etc.
Errors can be returned from any function, they can be passed as parameters and they can be stored into variables.

Golang has errors but not exceptions. Golang's way to handle exception is not to have an exception at first place.
Please read Dave Cheney's blog about ***[Why Go gets exceptions right](https://dave.cheney.net/2012/01/18/why-go-gets-exceptions-right)***.

Golang has a support for multiple return values by function. This feature is primarily used for returning a result and an error.
Below is a signature of a Read method from ***[bufio package.](https://golang.org/src/bufio/bufio.go?s=4875:4925#L188)***
```
func (b *Reader) Read(p []byte) (n int, err error)
```
`Read` method returns the number of bytes read into p and returns variable `err` of type `error`.
So if for some reason this function fails then caller will be apprised by returning custom defined error.
Caller should have mechanism to inspect the returned error and take action on it i.e log error.
An error is a value type and its zero value is nil, caller should check against nil to determine if error has ocurred or not and then only should deal with the result returned from function.
Below is an idiomatic way of handling error in Golang.
```
if err != nil {
  // handle error
}
```
Almost every project written in Golang you'll find the above block of code.
This explicit way handling error gives us more control over error handling.
We can decorate the error in human readable format and make it more informative.
Below is an example of error handling.
```
package main

import (
  "fmt"
  "os"
)

func main() {
  f, err := os.Open("README.md")
  if err != nil {
    fmt.Println(err)
    os.Exit(1)
  }
  fmt.Println(f.Name(), "opened successfully")
}
```
```
open README.md: no such file or directory
Program exited: status 1.
```
***<a href="https://play.golang.org/p/m6f5_P8Brqz" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

In above program, we're trying to open README.md file which is not present so os.Open function returns an error which we're inspecting and handling. 

## Error under the hood

In Golang, error is built-in type, but actually error is an `interface type made available globally`.
***[It is a single method interface.](https://golang.org/ref/spec#Errors)*** 
Please read this ***[blog on interface](/blog/golang/series/interface_part_1)***, if you don't know what interface is?
```
type error interface {
  Error() string
}
```
Any type implements the error interface is a valid error. 
To create a custom error any type just need to provide definition to `Error() string` method.
For example, in above example of opening file, the error returned was actually of type ***[*pathError](https://github.com/golang/go/blob/master/src/os/file.go#L316)***. `pathError` is a custom error which ***[implements the error interface](https://golang.org/pkg/io/fs/#PathError)***.

## Let's create an error

From above section we know that error is an interface and any type which implements that interface is an error.
Let's try to create a custom error.
```
package main

import "fmt"

type httpError struct {
  code   int
  method string
  fn     string
}

func (h *httpError) Error() string {
  return fmt.Sprintf("ERROR:%d:%s:%s", h.code, h.method, h.fn)
}

//Mock function to demo some operation
func getUser(uid int) (interface{}, error) {
  // some business logic
  authorized := false
  if authorized {
    //find user logic
    return "User found", nil
  }
  return "", &httpError{code: 401, method: "GET", fn: "getUser"}
}

func main() {
  _, err := getUser(1)
  if err != nil {
    fmt.Println(err)
  }

  // Inline variant
  // if _, err = getUser(2); err != nil {
  // 	fmt.Println(err)
  // }
}

```
```
ERROR:401:GET:getUser
```
***<a href="https://play.golang.org/p/dFSDoh2fBjz" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

In above example, `httpError` struct implements `error` interface by providing definition to `Error` method.
`getUser` is a mock function which mocks the getUser operation.

Here main function is the caller for the methods. So main function is suppose to handle the returned errors.
In main function, this statement `_, err := getUser(1)` executes the getUser function and stores the error in `err` variable and ignores the result using `_`.

After the function call, caller is checking if the function is returning an error or not using if-else statement.

If you notice the return type of an error in `getUser` function is `error interface type` and while returning actual value it is returning pointer `&httpError{code: 401, method: "GET", fn: "getUser"}` that is pointer to the `httpError` struct.

***If the return type of an function and type of actual return value are different then how this function is able to return the value?***
This is because type `httpError` implements the `error interface`.
Under the hood interface variable will hold the value and type of the type that implements it.
Read more about interface types and values in ***[interface blog post.](/blog/golang/series/interface_part_1)***

Another thing to notice is the output.
```
ERROR:401:GET:getUser
```
We're passing variable `err` of type `httpError struct` to the `fmt.Println` function and it is printing nicely documented output, instead of messy struct variable.

***How?***
This is happening because we've defined `Error` method which returns custom error message string.
So under the hood `fmt.Println` function is calling `Error` method and printing the string returned.
So we never have to explicitly call Error method to get custom error message.

## Handling error using type assertion

In above example the variable `err` is of type interface. This err variable will not have access to fields of httpError.
But err being variable of error interface and that interface is implemented by type httpError we can use type assertion to extract underlying concrete value of interface variable.

In ***[interfaces](/blog/golang/series/interface_part_2/)*** blog we've seen how type assertion is performed.
By extracting this underlying value we can gain more control over the error value and we can decide how to return this information to caller.
Below is an illustrative example:

```
package main

import "fmt"

type httpError struct {
  code   int
  method string
  fn     string
}

func (h *httpError) Error() string {
  return fmt.Sprintf("ERROR: %d:%s:%s\n", h.code, h.method, h.fn)
}

//Mock function to demo some operation
func getUser(uid int) (interface{}, error) {
  // some business logic
  authorized := false
  if authorized {
  //find user logic
  return "User found", nil
  }
  return "", &httpError{code: 401, method: "GET", fn: "getUser"}
}

func main() {
  _, err := getUser(1)
  if err != nil {
    if errVal, ok := err.(*httpError); ok {
      fmt.Printf("Status Code: %d\n", errVal.code)
      fmt.Printf("Method: %s\n", errVal.method)
      fmt.Printf("function returned error: %s\n", errVal.fn)
    }
  }
}
```
```
Status Code: 401
Method: GET
function returned error: getUser
```
***<a href="https://play.golang.org/p/cVIHQEKs1a5" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

This is a same example as previous with small tweak. Instead of printing `err` variable we're performing type assertion over it.
Here `errVal, ok := err.(*httpError)` will return a pointer to the instance of the `httpError`.
Now we can access the fields of `httpError` struct using `errVal`.

In case the underlying error is not of type `*httpError` the `ok` variable will be set to false returning control outside the if block.

## Handling error using type switch

Using type switch we can check the type of an error and handle it accordingly.
Read more about type switch in ***[interfaces blog.](/blog/golang/series/interface_part_2/)***
Below is an illustrative example:

```
package main

import "fmt"

type fooError struct {
  msg string
}

func (f *fooError) Error() string {
  return fmt.Sprintf("Error: %s", f.msg)

}

type barError struct {
  msg string
}

func (b *barError) Error() string {
  return fmt.Sprintf("Error: %s", b.msg)
}

func doSomething() error {
  return &fooError{"Something is wrong with foo!"}
}

func main() {
  err := doSomething()

  switch err.(type) {
  case nil:
    fmt.Println("Everything is fine.")
  case *fooError:
    fmt.Println("Foo: ", err)
  case *barError:
    fmt.Println("Bar: ", err)
  }
}
```
```
Foo:  Error: Something is wrong with foo!
```
***<a href="https://play.golang.org/p/7tbNi8TmkBg" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

In above example, we're have a type switch is analogous to regular switch case statement.
Here `switch err.(type)` we're discerning the underlying type of err variable and then it will be compared with all the cases,
whichever case is matched the error will be handled accordingly.

***<a href="" style="color:DodgerBlue" target="_blank">Run the code in Go Playground</a>***

***Thank you for reading this blog please give your feedback in the comment section below.***
<hr>

<a href="/blog/golang/">
  <b style="color:DodgerBlue">
    <i>🡄 </i>
  </b>
</a> &emsp;

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