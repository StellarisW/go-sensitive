# π« go-sensitive

[![build](https://img.shields.io/badge/build-1.01-brightgreen)](https://github.com/StellarisW/go-sensitive)[![go-version](https://img.shields.io/badge/go-~%3D1.19-30dff3?logo=go)](https://github.com/StellarisW/go-sensitive)

English | [δΈ­ζ](README-zh_cn.md)

> Filter sensitive words, support multiple data sources, filter algorithms and functions

## π Feature

- support multiple functions
    - `Filter()` return filtered text
    - `Replace()` return text which sensitive words that is been replaced
    - `IsSensitive()` Check whether the text has sensitive word
    - `FindOne()` return first sensitive word that has been found in the text
    - `FindAll()` return all sensitive word that has been found in the text
    - `FindAllCount()` return all sensitive word with its count that has been found in the text
- support multiple data sources with dynamic modification
    - support memory storage
    - support mysql storage
    - support mongo storage
    - support multiple ways of add dict
    - support dynamic add/del sensitive word while running
- support multiple filter algorithms
    - **DFA** use `trie tree`  to filter sensitive words

## β Usage

```go
package main

import (
	"fmt"
	"github.com/StellarisW/go-sensitive"
)

func main() {
    filterManager := sensitive.NewFilter(
        sensitive.StoreOption{
            Type: sensitive.StoreMemory
        },
        sensitive.FilterOption{
            Type: sensitive.FilterDfa
        }
    )
    
    // load dict
    
    err:=filterManager.GetStore().LoadDictPath("path-to-dict")
    if err != nil {
        fmt.Println(err)
        return
	}
    
    // dynamic add sensitive words
    
    err=filterManager.GetStore().AddWord("θΏζ―ζζθ―1", "θΏζ―ζζθ―2", "θΏζ―ζζθ―3")
    if err != nil {
        fmt.Println(err)
        return
	}
    
    fmt.Println(filterManager.GetFilter().IsSensitive("θΏζ―ζζθ―1,θΏζ―ζζθ―2,θΏζ―ζζθ―3,θΏζ―ζζθ―1,θΏιζ²‘ζζζθ―"))
    
    fmt.Println(filterManager.GetFilter().Filter("θΏζ―ζζθ―1,θΏζ―ζζθ―2,θΏζ―ζζθ―3,θΏζ―ζζθ―1,θΏιζ²‘ζζζθ―"))
    
    fmt.Println(filterManager.GetFilter().Replace("θΏζ―ζζθ―1,θΏζ―ζζθ―2,θΏζ―ζζθ―3,θΏζ―ζζθ―1,θΏιζ²‘ζζζθ―", '*'))
    
    fmt.Println(filterManager.GetFilter().FindOne("θΏζ―ζζθ―1,θΏζ―ζζθ―2,θΏζ―ζζθ―3,θΏζ―ζζθ―1,θΏιζ²‘ζζζθ―"))

    fmt.Println(filterManager.GetFilter().FindAll("θΏζ―ζζθ―1,θΏζ―ζζθ―2,θΏζ―ζζθ―3,θΏζ―ζζθ―1,θΏιζ²‘ζζζθ―"))

    fmt.Println(filterManager.GetFilter().FindAllCount("θΏζ―ζζθ―1,θΏζ―ζζθ―2,θΏζ―ζζθ―3,θΏζ―ζζθ―1,θΏιζ²‘ζζζθ―"))
}
```

## β Get

```
$ go get -u github.com/StellairsW/go-sensitive
```

## π Import

```go
import "github.com/StellairsW/go-sensitive"
```

## 

## π TODO

- [ ] add redis data source support
- [ ] add bloom algorithm
