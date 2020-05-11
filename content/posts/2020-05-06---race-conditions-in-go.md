---
title: Race conditions in GO
date: "2020-05-10T22:40:32.169Z"
template: "post"
draft: false
slug: "race-conditions-in-go"
category: "Golang"
tags:
  - "Golang"
  - "Go routines"
  - "Web Development"
description: "When two Goroutines share the same resources and try to read/write that resource at the same time then there might be non deterministic output for the program and this situation is said to be Race condition. 
."
socialImage: "/media/42-line-bible.jpg"
---


Goroutines are the methods which run concurrently with other methods of the Go Program. All Goroutines run in the same address space. The execution of the different gorountine depends upon the interleaving among the Goroutines. Interleavings are the execution of order of tasks of different Goroutines, and while writing the code this order is always non deterministic. Hence go routines can execute their corresponding tasks in different manners. Thus can produce different output every time for the same input.

For example in below program  

```go
package main
 
import (
   "time"
   "fmt"
)
 
func evenNumbers() {
    for i:=0; i < 5;i++ {
    fmt.Println(i+ i)
     time.Sleep(150 * time.Millisecond)
  }
}
 
func oddNumbers() {
  for i:=0; i < 5;i++ {
    fmt.Println(i+ i+1)
     time.Sleep(200 * time.Millisecond)
  }
}
 
func main() {
  go oddNumbers()
  go evenNumbers()
  time.Sleep(2000 * time.Millisecond)
}

```
 
Above program when compiled and run results in following output 

```
0 // output from function evenNumbers
1 // output from function oddNumbers
2 // output from function oddNumbers
3 // output from function oddNumbers
4 // output from function evenNumbers
5 // output from function oddNumbers
6 // output from function evenNumbers
8 // output from function evenNumbers
7 // output from function oddNumbers
9 // output from function oddNumbers

```

The above output is independent of order of code written and called, while both thee functions has been executed concurrently, some of the code from function1 has executed, while some of the code from function 2 has been executed. There is no deterministic order for the execution. 





## The-syntactical-sugar

Race Condition 

When two Goroutines share the same resources and try to read/write that resource at the same time then there might be non deterministic output for the program and this situation is said to be Race condition. 

In the Below program the `add` and `mul` are two goroutines which are executed together.
Now both of them try to add and multiply with 2 for the given x. 

Now if we are taking x = 2 in the program, then there might be two conditions for the same,  

If 
x =( x * 2) + 2 				for x =2 , the output would be 6
x = 2  * (x +2)				for x = 2 output would be 8

The output depends upon the execution order of the both Goroutines. Now in the below case since we have called add first then output should be 8. 

But surprisingly the output returned to be 6 or sometimes 8, which satisfies the race condition. 

```go

package main
 
import (
  "time"
  "fmt"
)
 
var x int
 
func add() {
   x = x+2
}
 
func mul()  {
  x = x*2
 
}
 
func main() {
  x = 2
  go add()
  go mul()
  time.Sleep(1000 * time.Millisecond)
  fmt.Println(x)
}

```
