你好！
很冒昧用这样的方式来和你沟通，如有打扰请忽略我的提交哈。我是光年实验室（gnlab.com）的HR，在招Golang开发工程师，我们是一个技术型团队，技术氛围非常好。全职和兼职都可以，不过最好是全职，工作地点杭州。
我们公司是做流量增长的，Golang负责开发SAAS平台的应用，我们做的很多应用是全新的，工作非常有挑战也很有意思，是国内很多大厂的顾问。
如果有兴趣的话加我微信：13515810775  ，也可以访问 https://gnlab.com/，联系客服转发给HR。
# Aerospike Go Client

[![Aerospike Client Go](https://goreportcard.com/badge/github.com/aerospike/aerospike-client-go)](https://goreportcard.com/report/github.com/aerospike/aerospike-client-go)
[![Build Status](https://travis-ci.org/aerospike/aerospike-client-go.svg?branch=master)](https://travis-ci.org/aerospike/aerospike-client-go)
[![Godoc](https://godoc.org/github.com/aerospike/aerospike-client-go?status.svg)](http://godoc.org/github.com/aerospike/aerospike-client-go)

An Aerospike library for Go.

This library is compatible with Go 1.7+ and supports the following operating systems: Linux, Mac OS X (Windows builds are possible, but untested)

Please refer to [`CHANGELOG.md`](CHANGELOG.md) if you encounter breaking changes.

- [Usage](#Usage)
- [Prerequisites](#Prerequisites)
- [Installation](#Installation)
- [Tweaking Performance](#Performance)
- [Benchmarks](#Benchmarks)
- [API Documentaion](#API-Documentation)
- [Tests](#Tests)
- [Examples](#Examples)
  - [Tools](#Tools)


## Usage:

The following is a very simple example of CRUD operations in an Aerospike database.

```go
package main

import (
  "fmt"

  . "github.com/aerospike/aerospike-client-go"
)

func panicOnError(err error) {
  if err != nil {
    panic(err)
  }
}

func main() {
  // define a client to connect to
  client, err := NewClient("127.0.0.1", 3000)
  panicOnError(err)

  key, err := NewKey("test", "aerospike", "key")
  panicOnError(err)

  // define some bins with data
  bins := BinMap{
    "bin1": 42,
    "bin2": "An elephant is a mouse with an operating system",
    "bin3": []interface{}{"Go", 2009},
  }

  // write the bins
  err = client.Put(nil, key, bins)
  panicOnError(err)

  // read it back!
  rec, err := client.Get(nil, key)
  panicOnError(err)

  // rec may not exist - so a checking is needed.
  if rec != nil {
    fmt.Printf("%#v\n", *rec)
  }

  // delete the key, and check if key exists
  existed, err := client.Delete(nil, key)
  panicOnError(err)
  fmt.Printf("Record existed before delete? %v\n", existed)
}
```

More examples illustrating the use of the API are located in the
[`examples`](examples) directory.

Details about the API are available in the [`docs`](docs) directory.

<a name="Prerequisites"></a>
## Prerequisites

[Go](http://golang.org) version v1.7+ is required.

To install the latest stable version of Go, visit
[http://golang.org/dl/](http://golang.org/dl/)


Aerospike Go client implements the wire protocol, and does not depend on the C client.
It is goroutine friendly, and works asynchronously.

Supported operating systems:

- Major Linux distributions (Ubuntu, Debian, Red Hat)
- Mac OS X
- Windows (untested)

<a name="Installation"></a>
## Installation:

1. Install Go 1.7+ and setup your environment as [Documented](http://golang.org/doc/code.html#GOPATH) here.
2. Get the client in your ```GOPATH``` : ```go get github.com/aerospike/aerospike-client-go```
  * To update the client library: ```go get -u github.com/aerospike/aerospike-client-go```

Using [gopkg.in](https://gopkg.in/) is also supported: `go get -u gopkg.in/aerospike/aerospike-client-go.v1`

### Some Hints:

 * To run a go program directly: ```go run <filename.go>```
 * to build:  ```go build -o <output> <filename.go>```
  * example: ```go build -o benchmark tools/benchmark/benchmark.go```

<a name="Performance"></a>
## Performance Tweaking

We are bending all efforts to improve the client's performance. In our reference benchmarks, Go client performs almost as good as the C client.

To read about performance variables, please refer to [`docs/performance.md`](docs/performance.md)

<a name="Tests"></a>
## Tests

This library is packaged with a number of tests. Tests require Ginkgo and Gomega library.

Before running the tests, you need to update the dependencies:

    $ go get .

To run all the test cases with race detection:

    $ ginkgo -r -race


<a name="Examples"></a>
## Examples

A variety of example applications are provided in the [`examples`](examples) directory.

<a name="Tools"></a>
### Tools

A variety of clones of original tools are provided in the [`tools`](tools) directory.
They show how to use more advanced features of the library to reimplement the same functionality in a more concise way.

<a name="Benchmarks"></a>
## Benchmarks

Benchmark utility is provided in the [`tools/benchmark`](tools/benchmark) directory.
See the [`tools/benchmark/README.md`](tools/benchmark/README.md) for details.

<a name="API-Documentation"></a>
## API Documentation

A simple API documentation is available in the [`docs`](docs/README.md) directory. The latest up-to-date docs can be found in [![Godoc](https://godoc.org/github.com/aerospike/aerospike-client-go?status.svg)](http://godoc.org/github.com/aerospike/aerospike-client-go).

## License

The Aerospike Go Client is made available under the terms of the Apache License, Version 2, as stated in the file `LICENSE`.

Individual files may be made available under their own specific license,
all compatible with Apache License, Version 2. Please see individual files for details.

