 First steps wit golang, how to install and run a simple program.
 - [Install](#install)
 - [Run](#run)
 - [Hello World](#hello-world)
- [Variables](#variables)
- [Constants](#constants)
- [Data Types](#data-types)
- [Operators](#operators)
- [Control Structures](#control-structures)
- [Functions](#functions)
- [Pointers](#pointers)
- [Structs](#structs)
- [Interfaces](#interfaces)
- [Errors](#errors)
- [Concurrency](#concurrency)
- [Channels](#channels)
- [Select](#select)
- [Timeouts](#timeouts)
- [Non-Blocking Channel Operations](#non-blocking-channel-operations)
- [Closing Channels](#closing-channels)
- [Range over Channels](#range-over-channels)

 ## Install
 Download the latest version of Go from the [official website](https://golang.org/dl/).

 ## Run
 To run a Go program, you need to compile it first. You can do this by running the `go run` command followed by the name of the file you want to run. 

 ```bash
 go run hello.go
 ```
 This will compile and run the `hello.go` file.

 ## Hello World
 Here is a simple Go program that prints "Hello, World!" to the console.

 ```go
 package main

 import "fmt"

 func main() {
  // 	fmt.Println("Hello, World!")
 }
 ```
 You can run this program by saving it to a file named `hello.go` and running the `go run` command as shown above.

 ## Variables
 In Go, you can declare variables using the `var` keyword followed by the variable name and type.

 ```go
 package main

 import "fmt"

 func main() {
 	var x int
 	var y string
 	var z bool

 	x = 5
 	y = "Hello"
 	z = true

 	fmt.Println(x, y, z)
 }
 ```
 This program declares three variables `x`, `y`, and `z` of type `int`, `string`, and `bool` respectively, and assigns them values. It then prints the values of these variables to the console.

 ## Constants
 In Go, you can declare constants using the `const` keyword followed by the constant name and value.

 ```go
 package main

 import "fmt"

 const Pi = 3.14

 func main() {
 	fmt.Println(Pi)
 }
 ```
 This program declares a constant `Pi` with the value `3.14` and prints it to the console.

 ## Data Types
 Go has several built-in data types such as `int`, `string`, `bool`, `float32`, and `float64`. You can also create your own data types using the `type` keyword.

 ```go
 package main

 import "fmt"

 type Celsius float64

 func main() {
 	var temperature Celsius
 	temperature = 22.5

 	fmt.Println(temperature)
 }
 ```
 This program declares a new data type `Celsius` and uses it to create a variable `temperature` of type `Celsius`. It then assigns a value to `temperature` and prints it to the console.

 ## Operators
 Go supports several operators such as `+`, `-`, `*`, `/`, `%`, `&&`, `||`, `!`, `==`, `!=`, `<`, `>`, `<=`, `>=`, `++`, and `--`.

 ```go
 package main

 import "fmt"

 func main() {
 	x := 5
 	y := 3

 	fmt.Println(x + y)
 	fmt.Println(x - y)
 	fmt.Println(x * y)
 	fmt.Println(x / y)
 	fmt.Println(x % y)
 	fmt.Println(x == y)
 	fmt.Println(x != y)
 	fmt.Println(x < y)
 	fmt.Println(x > y)
 	fmt.Println(x <= y)
 	fmt.Println(x >= y)
 }
 ```
This program demonstrates the use of various operators in Go.

## Control Structures
Go has several control structures such as `if`, `else`, `for`, `switch`, and `defer`.

```go
package main

import "fmt"

func main() {
    x := 5

    if x > 0 {
        fmt.Println("Positive")
    } else if x < 0 {
        fmt.Println("Negative")
    } else {
        fmt.Println("Zero")
    }

    for i := 0; i < 5; i++ {
        fmt.Println(i)
    }

    switch x {
    case 1:
        fmt.Println("One")
    case 2:
        fmt.Println("Two")
    default:
        fmt.Println("Other")
    }
}
```
This program demonstrates the use of various control structures in Go.

## Functions
In Go, you can define functions using the `func` keyword followed by the function name, parameters, return type, and body.

```go
package main

import "fmt"

func add(x, y int) int {
    return x + y
}

func main() {
    sum := add(3, 5)
    fmt.Println(sum)
}
```
This program defines a function `add` that takes two integers as parameters and returns their sum. It then calls this function and prints the result to the console.

## Pointers
Go supports pointers, which are variables that store the memory address of another variable.

```go
package main

import "fmt"

func main() {
    x := 5
    p := &x

    fmt.Println(x)
    fmt.Println(p)
    fmt.Println(*p)
}
```
This program demonstrates the use of pointers in Go.

## Structs
Go supports structs, which are user-defined data types that group together variables of different types.

```go
package main

import "fmt"

type Person struct {
    Name string
    Age  int
}

func main() {
    p := Person{Name: "Alice", Age: 30}

    fmt.Println(p)
}
```
This program defines a struct `Person` with two fields `Name` and `Age`, creates a variable `p` of type `Person`, and prints it to the console.

## Interfaces

Go supports interfaces, which are collections of method signatures that define the behavior of objects.

```go
package main

import "fmt"

type Shape interface {
    Area() float64
}

type Circle struct {
    Radius float64
}


func (c Circle) Area() float64 {
    return 3.14 * c.Radius * c.Radius
}

func PrintArea(s Shape) {
    fmt.Println(s.Area())
}

func main() {
    c := Circle{Radius: 5}
    PrintArea(c)
}
```

This program defines an interface `Shape` with a method `Area`, a struct `Circle` with a field `Radius`, and a method `Area` that calculates the area of the circle. It then defines a function `PrintArea` that takes a `Shape` as a parameter and prints its area. Finally, it creates a `Circle` and calls `PrintArea` with it.

## Errors

Go uses the `error` interface to represent errors. You can create custom error types by implementing the `Error()` method.

```go
package main

import (
    "errors"
    "fmt"
)


type MyError struct {
    Message string
}

func (e MyError) Error() string {
    return e.Message
}

func Divide(x, y int) (int, error) {
    if y == 0 {
        return 0, MyError{Message: "division by zero"}
    }
    return x / y, nil
}

func main() {
    result, err := Divide(6, 3)
    if err != nil {
        fmt.Println("Error:", err)
    } else {
        fmt.Println("Result:", result)
    }
}
```

This program defines a custom error type `MyError` that implements the `Error()` method, a function `Divide` that divides two integers and returns an error if the second integer is zero, and a `main` function that calls `Divide` and handles the error.

## Concurrency

Go has built-in support for concurrency using goroutines. You can create a new goroutine by using the `go` keyword followed by a function call.

```go
package main

import (
    "fmt"
    "time"
)

func PrintNumbers() {
    for i := 0; i < 5; i++ {
        fmt.Println(i)
        time.Sleep(1 * time.Second)
    }
}

func main() {
    go PrintNumbers()
    time.Sleep(5 * time.Second)
}
```

This program creates a new goroutine that prints numbers from 0 to 4 with a delay of 1 second between each number. The `main` function then waits for 5 seconds to allow the goroutine to finish.

## Channels

Go has built-in support for channels, which are used to communicate between goroutines. You can create a new channel using the `make` function.

```go
package main

import (
    "fmt"
)

func PrintNumbers(ch chan int) {
    for i := 0; i < 5; i++ {
        ch <- i
    }
    close(ch)
}

func main() {
    ch := make(chan int)
    go PrintNumbers(ch)
    for n := range ch {
        fmt.Println(n)
    }
}
```

This program creates a new channel `ch`, creates a goroutine that sends numbers from 0 to 4 to the channel, and then reads the numbers from the channel in the `main` function.

## Select

Go has a `select` statement that allows you to wait on multiple channel operations.

```go
package main

import (
    "fmt"
    "time"
)

func PrintNumbers(ch1, ch2 chan int) {
    for i := 0; i < 5; i++ {
        select {
        case ch1 <- i:
        case ch2 <- i:
        }
    }
    close(ch1)
    close(ch2)
}

func main() {
    ch1 := make(chan int)
    ch2 := make(chan int)
    go PrintNumbers(ch1, ch2)
    for {
        select {
        case n, ok := <-ch1:
            if !ok {
                ch1 = nil
            } else {
                fmt.Println("ch1:", n)
            }
        case n, ok := <-ch2:
            if !ok {
                ch2 = nil
            } else {
                fmt.Println("ch2:", n)
            }
        }
        if ch1 == nil && ch2 == nil {
            break
        }
    }
}
```

This program creates two channels `ch1` and `ch2`, creates a goroutine that sends numbers from 0 to 4 to either channel, and then reads the numbers from the channels using a `select` statement in the `main` function.

## Timeouts

Go has built-in support for timeouts using the `time.After` function.

```go
package main

import (
    "fmt"
    "time"
)

func PrintNumbers(ch chan int) {
    for i := 0; i < 5; i++ {
        ch <- i
    }
    close(ch)
}

func main() {
    ch := make(chan int)
    go PrintNumbers(ch)
    timeout := time.After(3 * time.Second)
    for {
        select {
        case n, ok := <-ch:
            if !ok {
                ch = nil
            } else {
                fmt.Println(n)
            }
        case <-timeout:
            fmt.Println("Timeout")
            return
        }
        if ch == nil {
            break
        }
    }
}
```

This program creates a new channel `ch`, creates a goroutine that sends numbers from 0 to 4 to the channel, and then reads the numbers from the channel in the `main` function. It also creates a timeout of 3 seconds using the `time.After` function.

## Non-Blocking Channel Operations

Go has built-in support for non-blocking channel operations using the `select` statement with a `default` case.

```go
package main

import (
    "fmt"
)

func main() {
    ch := make(chan int)
    select {
    case ch <- 1:
        fmt.Println("Sent")
    default:
        fmt.Println("Not Sent")
    }
}
```

This program creates a new channel `ch` and tries to send a value to the channel using a `select` statement with a `default` case.

## Closing Channels

Go has built-in support for closing channels using the `close` function.

```go
package main

import (
    "fmt"
)

func main() {
    ch := make(chan int)
    go func() {
        for i := 0; i < 5; i++ {
            ch <- i
        }
        close(ch)
    }()
    for n := range ch {
        fmt.Println(n)
    }
}
```

This program creates a new channel `ch`, creates a goroutine that sends numbers from 0 to 4 to the channel, and then reads the numbers from the channel in the `main` function. The goroutine closes the channel after sending all the numbers.

## Range over Channels

Go has built-in support for iterating over channels using the `range` keyword.

```go
package main

import (
    "fmt"
)

func main() {
    ch := make(chan int)
    go func() {
        for i := 0; i < 5; i++ {
            ch <- i
        }
        close(ch)
    }()
    for n := range ch {
        fmt.Println(n)
    }
}
```

This program creates a new channel `ch`, creates a goroutine that sends numbers from 0 to 4 to the channel, and then reads the numbers from the channel in the `main` function using the `range` keyword.

