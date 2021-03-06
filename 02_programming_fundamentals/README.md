# Programming Fundamentals

*************************************************************************

## Bool Type

*************************************************************************

Exploring types in more detail - starting with the bool type. Booleans are binary variables representing true/false values.

Important to understand how the people who built this language are talking about the language.

From the [language spec](https://golang.org/ref/spec#Boolean_types):

>"A boolean type represents the set of Boolean truth values denoted by the predeclared constants true and false. The predeclared boolean type is bool."

Booleans are important in programming as they allow us to evaluate an expression down to T/F values.

```go
package main

import (
    "fmt"
)

var d bool

func main() {
    fmt.Println(d)
    d = true
    fmt.Println(d)
    a := 7
    b := 42
    fmt.Println(a == b)
}

```

Declaring d as type 'bool'. If we do not declare a value, the default/zero value of bool is false.

*Note: Go is all about ease of programming and efficient execution.*

We can use comparison operators along with our evaluation. See above for the "is equal to" operation where we evaluate an expression. There is no triple equal operator in Go vs JavaScript.

```
==    equal
!=    not equal
<     less
<=    less or equal
>     greater
>=    greater or equal
```

Single equal is assignment, double equal is comparison.

## How Computers Work

*************************************************************************

### Overview & Takeaways

* Circuits/Switches
* Coding Schemes
* Binary Digits
* 2^n
* 5 generations of computers
* Moore's Law
* Bits
* Bits, Bytes, KB, MB, GB, TB
* Machine Language

Computers run on electricity - electricity has two discrete states: on or off.

We can take these states and assign coding schemes based on whether the state is on/off. *Ex: A Porch light on Halloween.*

If we take the simplicity of circuits/transistors, in a state of on/off and scale that up, we have the processing system of a computer.

Coding Schemes

    * Assign meaning to ON/OFF state
    * Porch Light on Halloween
        * 1 porch light = 2 messages
        * 2 porch lights = 4 messages
        * 3 porch lights = 8 messages
        * 4 porch lights = 16 messages
        * 5 porch lights = 32 messages
        * 6 porch lights = 64 messages
        * 7 porch lights = 128 messages
        * 8 porch lights = 258 messages
    * The formula for finding out how many "states" we can have is 2^n.

Instead of writing on/off, we can abbreviate these states with 0 = off, 1 = on.

#### Coding Schemes - Example

|	States	|	Action		|
|-----------|---------------|
|	1.1		|	Let's Party!|
|	1.0		|	Movie Night	|
|   0.1		|	Studying	|
|	0.0		|	Sleeping	|

These are called binary digits (0/1, on/off) - aka Bits, Machine Language.

Circuits/switches/transistors, all of these are relating to the core fact that there are states in a computer that can be seen as on/off. It's a gate that can either be opened/closed.

##### ASCII

* A coding scheme that has been widely used for text.
* Letters, symbols, and characters of the alphabet are represented in on/off states.

##### UTF-8

* World's largest coding scheme
* First part of UTF-8 is ASCII

##### Measuring Bits

* 1 bit
* 8 bits = byte
* 1000 bytes = KB
* 1000 KB = MB
* 1000 MB = GB
* 1000 GB = TB

##### History of Computers

First computer was the Eniac - came about in the 1940s. Had 16,000 porch lights. Instead of using lightbulbs they were using vacuum tubes to represent on/off states.

Problem - these vacuum tubes were hot and ran/off off.

![computer-bug](https://static.businessinsider.com/image/5593f5cc6bb3f7ac51d8d3cf/image.jpg)

Second generation of computers ran on transitors. Third generator of computers using silicon wafers/chips.

![silicon-wafer](https://techcet.com/wp-content/uploads/2014/09/LLxNk.jpg)

Since the beginning of computers, we've ramped up to 2.6 Billion circuits the size of your thumbnail. Intel - integrated electronics. Fourth generation: Microprocessors.

Moore's Law: Moore's law is the observation that the number of transistors in a dense integrated circuit doubles approximately every two years.

##### Numeral Systems

Will speak about this later, but think about hexadecimal, etc.

## Numeric Types

*************************************************************************

First - Integers do not have decimals (whole numbers), floating point numbers have decimals (real numbers).

Second - in the language spec we have numeric types. Do you have to use all of these data types? No. But we can be very specific with the size of ints. In general, we can typically use ```int``` and ```float64```.

[Caleb Doxsey's Book](https://www.golang-book.com/books/intro/3)

```go

package main

import (
    "fmt"
)

var x int8 = -129 //Will not run!
var y int8 = -128
var z uint8 = -128 //Will not run!

func main() {
    fmt.Println(x)  // tmp/sandbox148150758/main.go:7: constant -129 overflows int8
    fmt.Printf("%T\n", x)
    fmt.Println(y)
    fmt.Printf("%T\n", y)
}
```

### Uint vs int

```uint8``` stands for unsigned - if it is signed, it goes from negative to postive. If it's unsigned, it only goes from 0 upwards.

The Language Spec on [Numberic Types](https://golang.org/ref/spec#Numeric_types):

```plaintext

uint8       the set of all unsigned  8-bit integers (0 to 255)
uint16      the set of all unsigned 16-bit integers (0 to 65535)
uint32      the set of all unsigned 32-bit integers (0 to 4294967295)
uint64      the set of all unsigned 64-bit integers (0 to 18446744073709551615)

int8        the set of all signed  8-bit integers (-128 to 127)
int16       the set of all signed 16-bit integers (-32768 to 32767)
int32       the set of all signed 32-bit integers (-2147483648 to 2147483647)
int64       the set of all signed 64-bit integers (-9223372036854775808 to 9223372036854775807)

float32     the set of all IEEE-754 32-bit floating-point numbers
float64     the set of all IEEE-754 64-bit floating-point numbers

complex64   the set of all complex numbers with float32 real and imaginary parts
complex128  the set of all complex numbers with float64 real and imaginary parts

byte        alias for uint8
rune        alias for int32

```

We also have implementation specific sizes. For example, ```int``` and ```uint``` can store either 32 or 64 bits. And the compiled will determined whether it'll be 32 or 64 - mechanical sympathy.

All numeric types are distinct except for bytes and runes.

* ```byte``` - alias for uint8 (byte is 8 bits)
* ```rune``` - alias for int32 (32 0s and 1s - runes are characters. Go uses the UTF-8 coding scheme, and runes are representations of that.)

#### Runtime

Runtime packages has GOARCH, GOOS.

>"Package runtime contains operations that interact with Go's runtime system, such as functions to control goroutines. It also includes the low-level type information used by the reflect package; see documentation for the programmable interface to the run-time type system."

```go

package main

import (
    "fmt"
    "runtime"
)

func main() {
    fmt.Println(runtime.GOOS)
    fmt.Println(runtime.GOARCH)
}

//nacl
//amd64p32
```

[Go Playground Example](https://play.golang.org/p/1vp5DImIMM)

## String Type

*************************************************************************

[Go Blog Post on Strings](https://blog.golang.org/strings)

Remember, Go is all about ease of programming. A string type represents a set of string values. A string value is a (possibly empty) sequence of bytes. Strings are immutable: once created, it is impossible to change the contents of a string.

A string is a sequence of bytes. Underlying, a string is a slice of bytes. Recall, a byte is an alias from int8.

```go

package main

import "fmt"

func main() {
s := "Hello, 世界"
    fmt.Printf("%s\n", s) //plain string
    fmt.Printf("%q\n", s) //quoted string
    fmt.Printf("%x\n", s) //hexidecimal = base 16 lower case letters
    fmt.Printf("---%x\n", "世")
    for i :=0; i < len(s); i++ {
        fmt.Printf("%x ", s[i])
    }
    fmt.Println("")
    for i, v := range s {
        fmt.Printf("%#U \t %d", v, i) //Unicode, base 10
    }

}

// 6U+4E16 '世' - Crazy!

```

Note: ```%x```. It just dumps out the sequential bytes of the string as hexadecimal digits, two per byte.

[Playground Example](https://play.golang.org/p/dqC4SVP3pyp)

## Numeral Systems

*************************************************************************

A numeral system is a system we use to keep track of numbers. One system we use is called base10. A base10 numeral system allows us to count in increments of tens. It goes from 0-9.

Base 10 - you can put one digit in each of these spots. Base 10 to the power of 0. Anything to the power of 0 is one.

### Decimal

| ten millions	| millions 	| hundred thousands	| ten thousands	| thousands	| hundreds	| tens	| ones	|
|---------------|-----------|-------------------|---------------| ------------|-----------|-------|-------|
| 10^7			| 10^6	 	| 10^5			| 10^4				| 10^3		| 10^2		| 10^1	| 10^0	|

![example](https://docs.google.com/document/d/1GOVlFLkV0TQ49NGgX5_77JJZwJXdLgVb1sGSPk0jsAg/edit)

### Binary

Base2 - We have 0s and 1s. Ones, twos, fours, eights, sixteens, thirty-twos, sixty-fours, one-twenty-eights.

Ex: 42 in Binary

thirty-two	| sixteen	| eights	| fours	| twos	| ones	|
|-----------|-----------|-----------|-------|-------|-------|
|	2^5		| 2^4		| 2^3		| 2^2	| 2^1	| 2^0	|
|	1		| 0			| 1			| 0		| 1		| 0		|

There are 10 types of people in the world. Those who understand binary and those who don't.

### Hexadecimal

Also known as base16. For 16, we do 0-9, and then letters a-f to represent 10-15.

```go

package main

import (
    "fmt"
)

func main() {
    s := "V"
    fmt.Println(s)
    bs := []byte(s)
    fmt.Println(bs)

    b := bs[0]
    fmt.Println(b)
    fmt.Printf("%T\n", b)
    fmt.Printf("%b\n", b)
    fmt.Printf("%#X\n", b)
}

```

Output:
V
[86]
86
uint8
1010110
0X56

## Constants

*************************************************************************

Constants are a single, unchanging value - that only exists at the time of compilation. Const is reserved keyword.

There are typed are untyped constants.
* const dog = "Toby"
* const dog string = "Toby"

```go

package main

import (
    "fmt"
)

const (
    a int     = 42
    b float64 = 42.78
    c string  = "James Bond"
)

func main() {
    fmt.Println(a)
    fmt.Println(b)
    fmt.Println(c)
    fmt.Printf("%T\n", a)
    fmt.Printf("%T\n", b)
    fmt.Printf("%T\n", c)
}

```

## Iota

*************************************************************************

The pre-declared identifier iota denotes an integer constant. It is reset to 0 whenever the reserved word const appears in the source.

```go

package main

import (
    "fmt"
)

// 0, 1, 2, 3, 4, 5
const (
    a = iota
    b
    c
    d
    e
    f
)

// reset - 0, 1, 2
const (
    h = iota
    i
    j
)

func main() {
    fmt.Println(a)
    fmt.Println(b)
    fmt.Println(c)
    fmt.Println(d)
    fmt.Println(e)
    fmt.Println(f)
    fmt.Println(h)
    fmt.Println(i)
    fmt.Println(j)
}

```

## Bit Shifting

*************************************************************************

Recall the binary system is 0s and 1s. Bit shifting is when you shift binary digits to the left or right. Two operators:

>>
<<

Are for shifting bits.

%d = decimal
%b = binary.

```go

package main

import (
    "fmt"
)

func main() {
    x := 4
    fmt.Printf("%d\t\t%b\n", x, x)
    // 4, 100

    y := x << 1
    fmt.Printf("%d\t\t%b", y, y)
    //8, 1000
    z := y << 1
    fmt.Printf("%d\t\t%b", z, z)
    //16, 10000
}

```
[Playground Link](https://play.golang.org/p/SBr7s4AgUo)

Another example - notice that the binary digits shift up by 10 each time.

```go

package main

import (
    "fmt"
)

const (
    _  = iota
    kb = 1 << (iota * 10)
    mb = 1 << (iota * 10)
    gb = 1 << (iota * 10)
)

func main() {
    fmt.Printf("%d\t\t\t%b\n", kb, kb)
    fmt.Printf("%d\t\t\t%b\n", mb, mb)
    fmt.Printf("%d\t\t%b\n", gb, gb)
}

```

[Playground Link](https://play.golang.org/p/IwNVlOcrLG)


Quiz Results: [link](https://docs.google.com/forms/d/e/1FAIpQLSfjhxXjo0r_OsVys58B1lVs35CLPpneVcjiEKTPsLuQs4mftA/viewscore?viewscore=AE0zAgBhX75E9cVoJ9gL26H06XASuFQOQrIvbYX5S2IOA3RwBpkfpImukKOUfQ)

21/21 - nice! Though I 1000% guessed on that eneiac question :)