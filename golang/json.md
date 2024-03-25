# Working with json in golang
<!-- table of contents -->
## Table of contents
1. [Introduction](#introduction)
1. [Field tags](#field-tags)
    1. [Omitting fields](#omitting-fields)
    1. [Renaming fields](#renaming-fields)
    1. [Ignoring fields](#ignoring-fields)
    1. [Custom encoding](#custom-encoding)
    1. [Custom decoding](#custom-decoding)
    1. [DynamoDB tags](#dynamodb-tags)
1. [Encoding](#encoding)
1. [Decoding](#decoding)
1. [Unmarshalling](#unmarshalling)
1. [Marshalling](#marshalling)
1. [References](#references)

## Introduction
Go has a built-in package for encoding and decoding JSON data. The package is called `encoding/json`. The package provides functions for encoding and decoding JSON data. The package also provides functions for marshalling and unmarshalling JSON data.

## Field tags
The `encoding/json` package provides a way to control how fields are encoded and decoded. The package provides a way to specify field tags. Field tags are used to specify how fields are encoded and decoded.

### Omitting fields
Fields can be omitted from the JSON output by using the `json:"-"` tag. The `json:"-"` tag tells the encoder to omit the field from the JSON output.

```go
type Person struct {
    Name string `json:"name"`
    Age  int    `json:"-"`
}
```

In the example above, the `Age` field will be omitted from the JSON output.

### Renaming fields
Fields can be renamed in the JSON output by using the `json:"name"` tag. The `json:"name"` tag tells the encoder to use the specified name in the JSON output.

```go
type Person struct {
    Name string `json:"name"`
    Age  int    `json:"age"`
}
```

In the example above, the `Name` field will be renamed to `name` in the JSON output.

### Ignoring fields
Fields can be ignored in the JSON output by using the `json:"-"` tag. The `json:"-"` tag tells the encoder to ignore the field.

```go
type Person struct {
    Name string `json:"name"`
    Age  int    `json:"-"`
}
```

In the example above, the `Age` field will be ignored in the JSON output.

### Custom encoding
Fields can be encoded using a custom function by using the `json:",omitempty"` tag. The `json:",omitempty"` tag tells the encoder to use the custom function to encode the field.

```go
type Person struct {
    Name string `json:"name"`
    Age  int    `json:",omitempty"`
}
```

In the example above, the `Age` field will be encoded using a custom function.

### Custom decoding
Fields can be decoded using a custom function by using the `json:",string"` tag. The `json:",string"` tag tells the decoder to use the custom function to decode the field.

```go
type Person struct {
    Name string `json:"name"`
    Age  int    `json:",string"`
}
```

In the example above, the `Age` field will be decoded using a custom function.

### DynamoDB tags
The `encoding/json` package provides tags for encoding and decoding DynamoDB data. The package provides tags for encoding and decoding DynamoDB data.

```go
type Person struct {
    Name string `json:"name"`
    Age  int    `json:"age" dynamodbav:"age"`
}
```

In the example above, the `Age` field will be encoded and decoded using the DynamoDB tags.

## Encoding
The `encoding/json` package provides functions for encoding JSON data. The package provides functions for encoding JSON data.

```go
package main

import (
    "encoding/json"
    "fmt"
)

type Person struct {
    Name string `json:"name"`
    Age  int    `json:"age"`
}

func main() {
    p := Person{Name: "Alice", Age: 30}
    b, err := json.Marshal(p)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(string(b))
}
```

In the example above, the `json.Marshal` function is used to encode the `Person` struct.

## Decoding
The `encoding/json` package provides functions for decoding JSON data. The package provides functions for decoding JSON data.

```go
package main

import (
    "encoding/json"
    "fmt"
)

type Person struct {
    Name string `json:"name"`
    Age  int    `json:"age"`
}

func main() {
    b := []byte(`{"name":"Alice","age":30}`)
    var p Person
    err := json.Unmarshal(b, &p)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(p)
}
```

In the example above, the `json.Unmarshal` function is used to decode the JSON data into the `Person` struct.

## Unmarshalling
The `encoding/json` package provides functions for unmarshalling JSON data. The package provides functions for unmarshalling JSON data.

```go
package main

import (
    "encoding/json"
    "fmt"
)

type Person struct {
    Name string `json:"name"`
    Age  int    `json:"age"`
}

func main() {
    b := []byte(`{"name":"Alice","age":30}`)
    var p Person
    err := json.Unmarshal(b, &p)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(p)
}
```

In the example above, the `json.Unmarshal` function is used to unmarshal the JSON data into the `Person` struct.

## Marshalling
The `encoding/json` package provides functions for marshalling JSON data. The package provides functions for marshalling JSON data.

```go
package main

import (
    "encoding/json"
    "fmt"
)

type Person struct {
    Name string `json:"name"`
    Age  int    `json:"age"`
}

func main() {
    p := Person{Name: "Alice", Age: 30}
    b, err := json.Marshal(p)
    if err != nil {
        fmt.Println(err)
        return
    }
    fmt.Println(string(b))
}
```

In the example above, the `json.Marshal` function is used to marshal the `Person` struct into JSON data.

## References
- [https://golang.org/pkg/encoding/json/](https://golang.org/pkg/encoding/json/)
- [https://gobyexample.com/json](https://gobyexample.com/json)
- [https://www.sohamkamani.com/blog/2017/10/18/parsing-json-in-golang/](https://www.sohamkamani.com/blog/2017/10/18/parsing-json-in-golang/)
- [https://tutorialedge.net/golang/parsing-json-with-golang/](https://tutorialedge.net/golang/parsing-json-with-golang/)
- [https://www.calhoun.io/working-with-json-in-go/](https://www.calhoun.io/working-with-json-in-go/)
- [https://www.sohamkamani.com/blog/2017/10/18/parsing-json-in-golang/](https://www.sohamkamani.com/blog/2017/10/18/parsing-json-in-golang/)
- [https://tutorialedge.net/golang/parsing-json-with-golang/](https://tutorialedge.net/golang/parsing-json-with-golang/)
- [https://www.calhoun.io/working-with-json-in-go/](https://www.calhoun.io/working-with-json-in-go/)
- [https://www.sohamkamani.com/blog/2017/10/18/parsing-json-in-golang/](https://www.sohamkamani.com/blog/2017/10/18/parsing-json-in-golang/)
- [https://tutorialedge.net/golang/parsing-json-with-golang/](https://tutorialedge.net/golang/parsing-json-with-golang/)

```

