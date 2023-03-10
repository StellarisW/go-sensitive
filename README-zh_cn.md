# ð« go-sensitive

[![build](https://img.shields.io/badge/build-1.01-brightgreen)](https://github.com/StellarisW/go-sensitive)[![go-version](https://img.shields.io/badge/go-~%3D1.19-30dff3?logo=go)](https://github.com/StellarisW/go-sensitive)

[English](README.md) | ä¸­æ

> ææè¯è¿æ»¤, æ¯æå¤ç§æ°æ®æºå è½½, å¤ç§è¿æ»¤ç®æ³, å¤ç§æä½åè½

## ð Feature

- æ¯æå¤ç§æä½åè½
    - `Filter()` è¿åè¿æ»¤åçææ¬
    - `Replace()` è¿åæ¿æ¢äºææè¯åçææ¬
    - `IsSensitive()` è¿åææ¬æ¯å¦å«æææè¯
    - `FindOne()` è¿åå¹éå°çç¬¬ä¸ä¸ªææè¯
    - `FindAll()` è¿åå¹éå°çææææè¯
    - `FindAllCount()` è¿åå¹éå°çææææè¯ååºç°æ¬¡æ°
- æ¯æå¤ç§æ°æ®æºå è½½, å¨æä¿®æ¹æ°æ®æº
    - æ¯æåå­å­å¨
    - æ¯æmysqlå­å¨
    - æ¯æmongoå­å¨
    - æ¯æå¤ç§å­å¸å è½½æ¹å¼
    - æ¯æè¿è¡è¿ç¨ä¸­å¨æä¿®æ¹æ°æ®æº
- æ¯æå¤ç§è¿æ»¤ç®æ³
    - **DFA** ä½¿ç¨ `trie tree` æ°æ®ç»æå¹éææè¯

## â Usage

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
    
    // å è½½å­å¸
    
    err:=filterManager.GetStore().LoadDictPath("path-to-dict")
    if err != nil {
        fmt.Println(err)
        return
	}
    
    // å¨æå¢å è¯æ±
    
    err=filterManager.GetStore().AddWord("è¿æ¯ææè¯1", "è¿æ¯ææè¯2", "è¿æ¯ææè¯3")
    if err != nil {
        fmt.Println(err)
        return
	}
    
    fmt.Println(filterManager.GetFilter().IsSensitive("è¿æ¯ææè¯1,è¿æ¯ææè¯2,è¿æ¯ææè¯3,è¿æ¯ææè¯1,è¿éæ²¡æææè¯"))
    
    fmt.Println(filterManager.GetFilter().Filter("è¿æ¯ææè¯1,è¿æ¯ææè¯2,è¿æ¯ææè¯3,è¿æ¯ææè¯1,è¿éæ²¡æææè¯"))
    
    fmt.Println(filterManager.GetFilter().Replace("è¿æ¯ææè¯1,è¿æ¯ææè¯2,è¿æ¯ææè¯3,è¿æ¯ææè¯1,è¿éæ²¡æææè¯", '*'))
    
    fmt.Println(filterManager.GetFilter().FindOne("è¿æ¯ææè¯1,è¿æ¯ææè¯2,è¿æ¯ææè¯3,è¿æ¯ææè¯1,è¿éæ²¡æææè¯"))

    fmt.Println(filterManager.GetFilter().FindAll("è¿æ¯ææè¯1,è¿æ¯ææè¯2,è¿æ¯ææè¯3,è¿æ¯ææè¯1,è¿éæ²¡æææè¯"))

    fmt.Println(filterManager.GetFilter().FindAllCount("è¿æ¯ææè¯1,è¿æ¯ææè¯2,è¿æ¯ææè¯3,è¿æ¯ææè¯1,è¿éæ²¡æææè¯"))
}
```

## â Get

```
$ go get -u github.com/StellarisW/go-sensitive
```

## ð Import

```go
import "github.com/StellarisW/go-sensitive"
```

## 

## ð TODO

- [ ] add mongo data source support
- [ ] add  bloom algorithm