---
title: Understand goroutines

---
<!--Understand goroutines-->

Let’s start with a reallife example of concurrency.

Assume you are writing an email on your computer and a call comes through. You stop writing the email to first take the call and then get back to writing your email. Another call comes through before you are done so you pause from writing and answer the second call.

Now that’s concurrency. You are writing an email (an independent function) and answering calls (another independent function).

Goroutines are functions (or methods) that run concurrently with other functions (or methods), it is what allow us to run concurrent functions.

To understand goroutines, we’ll two programs that perform the same task - one with a goroutine and the other without.

Add the code below to create the first program (without goroutine).

{{copy filename='code.go'}}
```go
package main

import (
	"fmt"
	"time"
)

func say(s string) {
	for j := 0; j < 4; j++ {
		fmt.Println(s)
		time.Sleep(time.Millisecond * 1000)
	}
}

func main() {
	say("Email")
	say("sent")
}
```
{{ /copy }}

From the code above, the function `say()` takes a string and prints it out 4 times. There is a 1 second (1000 millisecond) delay after each string is printed out.

Run the program to view the output:

{{ execute }}
```
go run code.go
```
{{ /execute }}

Next, we’ll create a goroutine.