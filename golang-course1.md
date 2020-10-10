
# Golang

[Getting Started with Go](https://www.coursera.org/learn/golang-getting-started) course notes by Oliver Frolovs, 2020.

* **Not a beginner's course!** It assumes a good understanding of basic principles of programming.
* I watched the videos at 1.25 speed and skipped some parts, skim-reading the transcripts instead.
* Good choice of topics and level of depth. *Pointers* covered before more pedestrian data types.
* The *scope of variables* (W2) is explained with the right balance of formalism and accessibility. And very concisely.

## Setting up the environment

I use [Ubuntu 20.04 LTS][ubuntu] under [WSL][wsl] and the Go version in Ubuntu `apt` repo was too old for my liking.

### Installing Go

I followed the [Download and Install][go] instructions on the Go website to install a more recent version.

``` shell
$ curl -O https://dl.google.com/go/go1.15.2.linux-amd64.tar.gz
$ sudo tar -C /usr/local -xzf go1.15.2.linux-amd64.tar.gz
$ export PATH=$PATH:/usr/local/go/bin
```

I made a Go *workspace* (`$GOPATH`), although see the note below on *modules*.

``` shell
$ mkdir ~/go
```

I've also updated my interactive shell configuration file `.bashrc`:

``` bash
# Go as installed using official installation method
if [ -x /usr/local/go/bin/go ]; then
    # Go binaries
    export PATH=$PATH:/usr/local/go/bin

    # Go workspace
    export GOPATH=~/go
fi
```

Some points for further investigation:
* **FIXME** `curl`ing the download URL from the webpage returned a piece of HTML with the a different download URL&hellip; weird!
* **FIXME** shouldn't `/usr/local/` be writeable without `sudo`?
* **TODO** there is a way to `dpkg` the `tar ...` part and make it a proper (local) package in Ubuntu
* **TODO** modules made `$GOPATH` somewhat irrelevant: [Using Go modules][modules]

[go]: https://golang.org/doc/install
[ubuntu]: https://releases.ubuntu.com/20.04/
[wsl]: https://docs.microsoft.com/en-us/windows/wsl/about
[modules]: https://blog.golang.org/using-go-modules

### Setting up Visual Studio Code

I've added [VSCode Go extension](https://code.visualstudio.com/docs/languages/go) to my [WSL Remote Target][vscode-wsl]. I would like to use *modules*, so following the  advice given during installation, I've enabled `Go Language Server` option by setting `go.useLanguageServer` to `true` in *Go extension* settings. 
This has prompted to install `gopls` to which I have agreed.

Once I opened some `.go` file, VSCode has asked me to install the missing modules. I responded with `Install All`.

I was able to `run test` in one of the [REDACTED] unit tests, which I accept as a sign of success in setting up the environment.

[vscode-wsl]: https://code.visualstudio.com/docs/remote/wsl

### Code organisation

I started out using Go *workspace* with the intention to move to module-based workflow later.

My Go workspace (`$GOPATH`) is set to `~/go` and structured according to the official convention into:

* `$GOPATH/bin`
* `$GOPATH/pkg`
* `$GOPATH/src`

Say, I wanted to have a Go "project" for experimentation. I name it `go-study` and place it in `$GOPATH/src/go-study/`. There is a file `main.go` there, with the following code.

``` go
package main

import (
	"fmt"
	"math"
)

func main() {
	fmt.Println("Hello, Gruffalo!")
	fmt.Printf("%f", math.Trunc(1.98))
}
```

This way, when I add a new entry to `import`, VSCode does not complain about missing libraries, so I guess it's OK?

*Update*: actually, I don't even need to add anything to `import` because IntelliSense manages the import based on what's actually used in the `.go` file. The `import` statement gets updated on file save. Neat.

## Test Go installation

Separately from VSCode, I test if Go runs from the WSL [Windows Terminal][winterm].

``` shell
$ go version
go version go1.15.2 linux/amd64
```

[winterm]: https://github.com/microsoft/terminal

## Liftoff!

This concludes the *yak shaving* part and I can finally begin the course.

---

## Why Go

* Fast
* Garbage collection (gc code gets compiled together with your code)
* Simpler objects (unlike C++, Go is *weakly* object-oriented)
* Concurrency built-in
* Extensive standard library

## User-defined types

Group together *data* and *code*. **Go** does not use the term **class**. Instead, it has **struct**. 

* It doesn't have *inheritance*.
* It doesn't have *constructors*.
* It doesn't have *generics*.

Hmm...

## Concurrency

Most, but not all, motivation stems from **performance limits**.

Moore's Law doesn't work anymore. Can't crank up the clock anymore &mdash; power constraints are real. *We are at the limits of air cooling.* 
Solution? **Increase the number of cores**.

*Concurrent programming* enables *parallelism*.

## Concurrency in Go

Go has a lot of concurrency primitives built into the language.

* *routines* represent concurrent tasks, basically a *thread*
* *channels* are used for communication between concurrent tasks (*routines*?)

These are the *high level yet basic keywords* in the language. The concurrency is *built into the language*.

## Code organisation in Go

### Workspaces

A *workspace* is a directory. There is typically a hierarchy of directories inside the workspace.

Recommended to have inside the *workspace* directory:

* `src` contains source code files.
* `pkg` contains *packages* (libraries).
* `bin` contains *executables* (compiled programs).

* A programmer typically has *one workspace for many projects*.
* The directory hierarchy is *recommended* but *not enforced*.  Common organisation is good for sharing.
* The workspace directory is defined by `$GOPATH` *environment variable*.

The `$GOPATH` *may be* defined by the Go *installer*, but don't rely on it. The recommended installation method on Linux un-`tar`-ring into `/usr/local/` certainly cannot do that.

### Packages

A *package* is a group of related source code files. Each package can be imported by other packages.

The `import` keyword is used to access other packages. The standard library include many packages. The `$GOROOT` and `$GOPATH` directories are searched for packages.

``` go
import "fmt"
```

``` go
import (
    "cobra"
    "fmt"
    "math"
)
```

There **must** be one package named `main`. When it's build (compiled), an *executable is made*. When other packages are built, an executable is not made.

``` go
package main
import "fmt"
func main() {
    fmt.Printf("Hello, Gruffalo!\n")
}
```

**FIXME** I suspect that packages are searched differently in the context of *using  modules*.

## The `go` tool

The tool can do many different things.

* `go build` compiles the program. Arguments can be a list of packages or a list of `.go` files.
* `go doc` prints documentation for a package.
* `go fmt` formats the code in the canonical way.
* `go get` downloads and installs packages.
* `go list` lists all installed packages.
* `go run` compiles **and** runs the executable. *Update*: I <3 it!
* `go test` runs tests saved in files ending in `_test.go`

## Variable declarations

Follow the format: **var** *name* *type*

``` go
var x int
var s string
```

Basic types: integers, floats, strings.

## Type declarations

*Aliases* can be defined for type names. Useful for writing self-documenting code.

``` go
type Celsius float64
type IDNum int
```

Then variables can be declared using these aliases.

``` go
var growboxTemp Celsius
var pid IDNum
```

Go *linters* don't like underscores ( `_` ) in variable names. Use capitalisation instead: `tempDiff`, not `temp_diff`.

## Variable initialisation in Go

**Initialise after declaration**

We've seen that many times before in C.

``` go
var x int
x = 100
```

**Initialise in declaration**

The literal constant `100` is an integer, so the *type is inferred* as integer.

``` go
var x = 100
```

Type inference is optional. The type can be specified as well.

``` go
var x int32 = 100
```

Uninitialised variables have a *zero value*. I suppose the zero value is different for each type.

``` go
var x int    // x == 0
var s string // s == ""
```

**TODO** what's the *zero value* of a custom type?

**Short variable declaration**

Declare and initialise in one line using the `:=` operator.

``` go
x := 100
```

The *variable type* is inferred from the expression on the right hand side. Can do this *only inside a function.* 

## Pointers in Go

A *pointer* value is an address in memory. So, a pointer *points* to some data in memory.

Operations on pointers:

* The `&` operator returns the address of a *variable* or a *function*.
* The `*` operator returns data at an address. This is known as *dereferencing*.

They are the opposites of one another.

``` go
var x int = 1
var y int

var ip *int   // ip is a pointer to int

ip = &x       // ip now points to x
y  = *ip      // y is now 1
```

Now `y` has value `1`. 

**FIXME** What if `x` is assigned a different value now?

## Creating variables with `new()`

The `new()` function creates a variable and returns a *pointer* to it. The variable is initialised to zero by default.

``` go
ptr := new(int)
*ptr = 42
```

A variable of type `int` is created and the pointer to it is returned. The pointer is then dereferenced, that is the value `42` is put into the memory location pointed to by `ptr`.

## Variable scoping

In Go, variable scoping is done using *blocks* &mdash; they are a sequence of declarations and statements within matching brackets, `{}`

``` go
{
    // scope A
    {
        // scope B
        // variables declared in scope A are also accessible
    }
    // scope A only
}
```

There is also a hierarchy of **implicit blocks**:

* *Universe block* &ndash; all Go source code, the biggest block.
* *Package block* &ndash; all source code in a particular package. The *package* can be composed of many files. This block is a *subset* of the *Universe block*. 
* *File block* &ndash; all source code in the current file. This block is a *subset* of the *Package block*.
* `if`, `for`, and `switch` define implicit blocks as well.
* individual clauses in `switch` or `select` each get a block.

The main point is that there is a *hierarchy of blocks*. At each level the block can have its own environment of variables associated with it.

Using the set notation, {clauses in `switch` or `select`} &sube; {`if`, `for`, `switch`} &sube; File &sube; Package &sube; Universe.

## Lexical scoping

This defines how variables references are resolved. Go is *lexically scoped* using *blocks*.

I'll just say that it's "intuitive" based on the model I learned from C <3 &ndash; go to the greater including scope, until the variable definition is found.

## Traditional view on memory management

### Stack vs heap

*Traditionally*, the *stack* is where the function local variables are allocated. They are deallocated once the function completes (returns).

The *heap* is a persistent area of memory which does not get deallocated automatically. Memory on the heap must be allocated and deallocated manually when it's no longer needed.

In C <3:

``` c
x = malloc(32);
// the variable x has a life 
// full of adventure and suffering...
free(x);
```
It's *error-prone* but *fast*.

Go does things differently. It has *garbage collection*.

## Garbage collection

When using pointers, it's *very hard* to figure out when a variable is no longer in use so it can be deallocated *safely*.

Example in Go, returning the pointer to a *local* variable. This is not legal in C, but **Go can do it**:

``` go

func foo() *int {
    x := 1
    return &x
}

func main() {
    var y *int
    y = foo()
    fmt.Printf("%d", *y)
}
```

This is possible thanks to *garbage collection*. 

**Go is a compiled language which enables garbage collection!**

* Implementation is *fast*
* Compiler determines *stack* vs *heap*
* Garbage collection in the background

**FIXME** Does GC **pause** the program?! I remember Azul Java GC does not, so it's possible.

## Comments in Go

Like in C <3

### Single-line comments

``` go
// Mamka Tvoya
var x int // Боже Праведный!
```

### Block comments

``` go
/* 
  Mamka Tvoya
  Иисус Христос был русским и родился в Твери.
  2020 (с) Православная Тверь
*/

var x int
```

## Output

Using `fmt` package:

* `fmt.Printf()`
* `fmt.Println()`

### String concatenation

``` go
x := "Gruffalo"
fmt.Printf("Hello, " + x)
```

### Format strings

Very similar to C <3 Use a *conversion character* for each argument.

``` go
x := "Gruffalo"
fmt.Printf("Hello, %s", x)
```

## Integers in Go

Generic integer declaration is `int`:

```Go
var x int
```

But there is a wide variety of integer types, based on width in bits and sign: 

* `int8`, `int16`, `int32`, `int64`
* `uint8`, `uint16`, `uint32`, `uint64` &mdash; unsigned

Finally (!) some sensible names, no more `short`, and `long long`, haha.

Usually it's best to declare as `int` and leave it to the compiler to figure out, unless there is a reason to control the size manually.

### Operations on integers

As one would expect in C <3

## Type conversions in Go

Type conversions are not always possible. The following would *fail* (thankfully).

``` go
var x int32 = 1
var y int16 = 2

x = y
```

The compiler views `int32` and `int16` as *different types* so the *assignment would fail*.

### `T()` operator

Convert type with `T()` operator.

``` go
var x int32
var y int16 = 2
x = int32(y)
```

Converting `int16` to `int32` is always possible &mdash; it *sign-extends* the value in `y`.

Not all conversions are this easy. **FIXME** more information?

## Floating point numbers

* `float32`  &ensp;~6 decimal digits of precision
* `float64` ~15 decimal digits of precision

Floating-point numbers can be expressed as *decimals* or using *scientific notation*.

``` go
var g float64 = 9.81           // acceleration of free fall on Earth [m/s^2]
var h float64 = 6.62607e-34    // Plank's constant [J.s]
```

## Complex numbers in Go

Rejoice, mortals! Natively supported, the *complex numbers* are.

``` go
var z complex128 = complex(2,3)
```

**FIXME** is this some kind of *constructor*? But Go doesn't have them, right?!

## ASCII and Unicode

*Characters* are not the same as *bytes* (and they haven't been for a long time).

* In ASCII, 7 or 8-bit code represents a character, so each character *can be* packed into a byte. But that covers only `2^8 = 256` characters, so not a lot.

Unicode characters are 32-bit, so *can represent a lot more characters*.

*UTF-8* is a variable Unicode encoding which matches ASCII for lower 2^8 *code points*. It is the default encoding in go.

*Code point* is the Unicode term for a character. There can be `2^32` code points. In Go, the code point is called a *rune*.

## Strings in Go

* Strings are an arbitrary sequence of *bytes*.
* Strings are *read-only*.
* Strings are in *UTF-8*, so at higher level they are made of *runes*.
* Strings are often meant to be printed.

### String literals

Are notated by double quotes.

``` go
x := "Gruffalo"
```

**Bytes are not runes!**

The string in the following example is made of Cyrillic runes. Each of these runes takes more than a single byte. Thus, byte-addressing the string prints rubbish and not the corresponding runes.

``` go
x := "Православная Тверь!\n"
fmt.Printf("%c", x[0])
fmt.Printf("%c", x[3])
```

Outputs ASCII symbols `Ð`, instead of runes `П` and `в`.

## String packages in Go

### Working at individual rune level

Given that bytes are not equivalent to runes, for working at the *runes* level (of abstraction), the `Unicode` package treats strings as "arrays of runes".

* Runes are divided into many different categories.
* The package provides a set of *predicates* to test categories of runes

  - `IsDigit(r rune)`
  - `IsSpace(r rune)`
  - `IsLetter(r rune)`
  - `IsLower(r rune)`
  - `IsPunct(r rune)`
  - &hellip;

* The package provides functions for *conversions*

  - `ToUpper(r rune)`
  - `ToLower(r rune)`
  - &hellip;

### Working at the whole string level

There is also the `strings` package. It provides functions to manipulate UTF-8 encoded strings. It does not look at individual runes, but at the whole string instead.

* Search 
* Compare
* Contains
* Has prefix
* Index
* &hellip;

**String manipulation**

Strings are *immutable*, but the `strings` package provides some functions to create new strings based on some existing string.

* Replace
* *To lower* and *to upper*
* Trim spaces

Another useful package is `strconv` containing conversions to and from other *basic datatypes*.

* `Atoi(s)` converts string to an integer
* `Itoa(i)` converts integer to a string
* `FormatFloat(f, fmt, prec, bitSize)` converts fp number to a string representation of that number
* `ParseFloat(s, bitSize)` does the opposite &mdash; converts a string to a floating point number
* &hellip;

## Constants in Go

A *constant* is an expression whose value is known at compile time. A *type* is inferred from the right-hand side of the assignment: boolean, string, number.

``` go
const x = 1.3
const (
    y = 4
    z = "Gruffalo"
)
```

### Enumerations in Go

* `iota` generates a set of related but distinct constants.
* Often represents a property which has several distinct possible values.
  
  - days of the week
  - months of the year
* the *key* thing is: constants must be different, but the *actual value is not important*

> Just like an *enumerated* type in other languages, like in C <3

**FIXME** Why did they pick up an unfamiliar name?!

``` go
type Grades int

const (
    A Grades = iota
    B
    C
    D
    F
)
```

In these example, we want five different grades, represented by integers, but we don't care what actual value each grade has, we just want something different.

We don't have to repeat the type and `iota`, it is implied! Each constant is assigned to a unique integer.

## Control flow in Go

The *control flow* describes the order in which the statements are executed inside a program.

### The most basic control flow

Is executing one statement at a time, one after another, top to bottom in terms of mapping it to the source code file.

Control flow might change from the basic one because the programmer inserted statements which alter the control flow.

### Conditional statement

``` go
if <condition> {
    <consequent>
}
```

Unlike C <3, the brackets `{}` are a must. There is also an optional `else` clause, as one would expect.

### Iteration

* `for` loops iterate while a condition is true.
* *May* have an *initialisation* and *update* operations.

``` go
for <init>; <cond>; <update> {
    <stmts>
}
```

There are several forms of `for` statements. The three most common ones are:

``` go
// Traditional form, seen before
for i:=0; i<10; i++ {
    fmt.Printf(".")
}

// The for loop itself has no initialisation and no update, only the condition
i = 0
for i < 10 {
    fmt.Printf(".")
    i++
}

// Infinite loop, maybe for an embedded system?
for {
    fmt.Printf(".")
}
```

**Switch/case statement**

* `switch` is a multi-way if statement.
* it may contain a `tag` which is a variable to be checked.
* only one `case` is going to be executed. This is a deviation from C <3.

```Go
switch x {
    case 1:
        // ...
    case 2:
        // ...
    default:
        // optional part if no other case match
}
```

Note, that `break` is not necessary to skip other cases, this is not C <3.

**Tagless switch**

Sometimes one does not want a *tag* for each case, but an *expression* instead. The first case for which the expression evaluates to `true` is executed.

The case contains a boolean expression to evaluate.

``` go
switch {
    case x > 1:
        // ...
    case x < -1:
        // ...
    default:
        // optional
}
```

A *tagless switch* can be used in place of a sequence of chained `if else` statements. And this looks good, I must add! Chained if-else never looked right.

**Break and continue**

* `break` exits the containing loop, as one would expect in C <3.
* `continue` skips the rest of the current iteration to the next iteration.

## Reading user input in Go

**Most trivial way**

The `scan` function is the most basic way for reading user input. It is in `fmt` package.

* takes a pointer as an argument
* typed data is written to pointer
* returns the number of scanned items and the error code, or `nil` if all is well

```Go
var appleNum int

fmt.Printf("Number of apples?")

num, err := fmt.Scan(&appleNum)
fmt.Printf(appleNum)
```

Note the *multiple assignment*!

**More sophisticated: handling whole lines**

If the input is supposed to have whitespace, best to use `bufio`.

```go
package main

import (
    "bufio"
    "fmt"
    "log"
    "os"
)

func main() {
    file, err := os.Open("/path/to/file.txt")
    if err != nil {
        log.Fatal(err)
    }
    defer file.Close()

    scanner := bufio.NewScanner(file)
    for scanner.Scan() {
        fmt.Println(scanner.Text())
    }

    if err := scanner.Err(); err != nil {
        log.Fatal(err)
    }
}
```

From [StackOverflow][1]

[1]: https://stackoverflow.com/questions/8757389/reading-a-file-line-by-line-in-go/16615559#16615559

I also liked [another answer][2], with different options considered.

[2]: https://stackoverflow.com/a/41741702

## Composite datatypes in Go

Aggregate data types we'll look at: arrays, slices, maps, and *structs*.

## Arrays in Go

*Fixed-length* sequence of elements of a *chosen type*.

Key points:

* The size of the sequence is *fixed*.
* The elements are all of the *same type*.

As in C, *indixing* starts at 0. Elements are accessed using *subscript notation* `[]`. Unlike C, the arrays are *initialised to zero* by default.

```Go
var x [5]int

x[0] = 2
fmt.Printf(x[1])  // is going to be zero
```

**Array literals in Go**

Is a sequence of pre-defined values that make up an array.

```Go
var x [5]int = [5]{1, 2, 3, 4, 5}
```

The left-hand side declaration is familiar. The right-hand side syntax is new. This is how you describe *array literals*. I note that the *size* of the literal is explicitly provided, which is great. Length of the literal must be length of array.

The size of the array can be *inferred* from the size of array literal using &`hellip;` *keyword*

```Go
x := [...]int {1, 2, 3, 4}
```

**Iterating through array in Go**

Using `for` loop.

```Go
x := [3]int {1, 2, 3}

for i, v range x {
    fmt.Printf("index %d, value %d \n", i, v)
}
```

`range` is a keyword. It returns two values: index and element value at that index.

## Slices in Go

A *slice* is a *window* on an underlying (possibly larger) array. They can be variable size, up to a the size of the whole array. A slice has three main properties:

* a *pointer* indicating the start of the slice
* the *length*, which is the number of elements in the slice
* the *capacity*, which is the *maximum* number of elements in the slice &mdash; from start of slice to end of array.

```Go
arr := [...]string {"a", "b", "c", "d", "e", "f", "g"}

s1 := arr[1:3] // includes elements 1 and 2: [b,c]
s2 := arr[2:5] // includes elements 2,3, and 4: [c,d,e]
```

Note, that slices can overlap. We use *bracket and colon notation* with slices. Similar to Python's slices so far.

**Length and capacity**

For *slices*,

* `len()` returns the *length*, aka *size*
* `cap()` returns the *capacity* (of an underlying array)

**FIXME** I got into the habit of always adding *of an underlying array* when I say *capacity*, at least until I remember the Go terminology.

**Referring to slices**

When writing to a slice, you are writing into the underlying array. Note, that different slices can be overlapping on the underlying array.

**Slice literals**

* Can be used to initialise the slice.
* Creates the underlying array and creates a slice to reference it.
* Slice points to the start of the array, length is capacity.

Note, that there is nothing in the brackets `[]`, so the compiler infers that this is a *slice*. It creates the array and it makes the slice point to the beginning of that array.

```Go
sli := []int {1, 2, 3}
```

**FIXME** This looks like rather technical shenanigans which have to do with the language being a compiled one? Would like to see some uses of this which is not just like what you do with Python slices (with added technical complexity).

**Creating slices**

There is a function `make()` which can be used to create *slices* (and an underlying array).

The use case for it is when you want to make a slice because you have some data to store and you want to initialise the slice to a particular size *in the beginning*.

Two argument version: specify *type* and *length* or *capacity*:

```Go
// Initialise a slice to zero. Length == capacity == 10.
sli = make([]int, 10) 
```

Three argument version: specify *length* and *capacity* separately. So, the *underlying array* is bigger than the *slice*:

```Go
// Initialise a slice to zero. Length is 10, but capacity is 15.
sli = make([]int, 10, 15)
```

**Increasing the size of a slice**

Use `append()` to increase the size (*length*) of *slice*. It adds element to the end of the slice. 

If the size of the underlying array is reached, *it will make a new array*. There is a time penalty for that.

```Go
sli = make([int, 0, 3]) // slice length is zero, but underlying array is size 3
sli = append(sli, 100)  // the underlying array is increased to size 100
```

## Hash tables

Allow fast access to large bodies of data. Contains key/value pairs. Each value is associated with unique key. *Hash function* is used to compute the slot for a key. All of this is familiar territory.

**Tradeoffs of hash tables**

Advantages of hash tables over lists:

* Faster lookups than lists (O(1) rather than O(n), I must add)
* Arbitrary keys, not just integers (but key must be *immutable*, I must add). Those keys may have some meaning to them, unlike simple integers.

Disadvantages of hash tables over lists:

* May have *collisions*, when two keys hash to same slot. *Unlikely*, and handled by Go.
* I would add, that classic hash tables *are not ordered*, while the lists are. This may be a disadvantage in many scenarios.

## Maps in Go

A *map* is a Golang's implementation of a *hash table*.

**Creating maps**

* Use `make()` to create a map. The following example declares, and then creates a map.

```go
var idMap map[string]int   // [key type]value type
idMap = make(map[string]int)  
```

* Use a *map literal* to create a map.

```go
idMap := map[string]int {
    "joe": 123
}
```

**Accessing maps**

Reference a value with `[key]`. Returns zero if key is not present.

**FIXME** i don't like this, zero is a valid integer value, wtf?

```go
fmt.Println(idMap["joe"])
```

**Adding a key/value pair**

```go
idMap["mouse"] = 456
```

**Deleting a key/value pair**

```go
delete(idMap, "joe")
```

**Key existence test**

Two-value assignment *tests for existence of the key*:

```go
id, p := idMap["joe"]
```

A *boolean* `p` would indicate if the key `"joe"` is in the map.

**Number of values in the map**

The `len` function returns the number of key/value pairs in the map.

```go
fmt.Println(len(idMap))
```

**Iterating through a map**

Use two-value assignment with a `range` keyword.

```go
for key, val := range idMap {
    fmt.Println(key, val)
}
```

No surprises here.

## Structs in Go

A `struct` is short for *structure* and it comes from C <3. It's an aggregate data type, grouping together values of arbitrary data types.

Example: `Person struct`. Each `person` has name, address, and a phone no.

* Have three separate variables, `name`, `address`, `phone`; or
* Make a single `struct` with three fields.

Can define a `struct` *type*, analogous to `type Celsius int` seen before.

```go
type struct Person {
    name string
    addr string
    phone string
}

var p1 Person // contains data one person
var p2 Person // contains data for another person
```

**Accessing `struct` fields**

Use *dot notation*.

```go
p1.name = "Gruffalo"
x := p1.addr
```

**Initialising `struct`**

Use `new()`:

```go
p1 := new(Person)
```

**FIXME** Why not `make()`?

Or use a *struct literal*:

```go
p1 := Person(name: "Gruffalo", addr: "Deep Dark Wood", phone: "123")
```

## **TODO** Revision examples

* The *capacity* is from the *pointer* to the slice **to the end of an underlying array**!
* `append(xs, 42)` **adds the value 42 to the slice**, expanding the underlying array, if the need be, so `cap(xs)` increases.

**Syntax**

This example puts together quite a few concepts from Go *syntax*.

**TODO** annotate with comments

```go
type P struct {
    x string
    y int
}

func main() {
  b := P{"x", -1}
  a := [...]P{
        P{"a", 10}, 
        P{"b", 2},
        P{"c", 3}
    }
    
  for _, z := range a {
    if z.y > b.y {
      b = z
    }
  }
  fmt.Println(b.x)
}
```

**Length and capacity**

The following prints `0 3`.

`append` puts the item into the slice, or expands the slice if the need be.

```go
func main() {
  s := make([]int, 0, 3)
  s = append(s, 100)
  fmt.Println(len(s), cap(s))
}
```

## Protocols and formats in Go

Golang has packages to handle lots of different protocols and data formats.

**RFC**

Not news, just not something I check out a lot in the recent years))

* A bit of history: [RFC1866 HTML2.0](https://www.ietf.org/rfc/rfc1866.txt)
* URI
* HTTP

**Network protocols packages**

* `net/http`, for *HTTP*, such as `http.Get("www.cloud84.dev")
* `net` for *TCP/IP* and *sockets* programming

```go
net.Dial("tcp", "uci.edu:80")
```

It's **very** useful to have these packages ready for use.

## JSON

* JavaScript Object Notation
* RFC7159
* Format to represent structured information
* Human-readable
* All Unicode
* Fairly compact representation (for a human-readable format)
* Attribute-value pairs correlate to `struct` or `map` in Golang
* Basic value types: bool, number, string, array, object
* Types can be combined recursively:
  - array of struct
  - struct in struct
  - and more...

A `struct` in Go:

```go
p1 := Person(name: "Gruffalo", addr: "Deep Dark Wood", phone: "123")
```

As a *JSON* object:

```json
{
    "name": "Gruffalo",
    "addr": "Deep Dark Wood",
    "phone": "123"
}
```

**JSON marshalling**

Generating JSON representation from an object.

I remember, that *marshalling* and *serialisation* aren't exactly the same thing!

A type definition in Go:

```go
type struct Person {
    name string
    addr string
    phone string
}
```

Define a value of that type:

```go
p1 := Person(name: "Gruffalo", addr: "Deep Dark Wood", phone: "123")
```

Marshall into JSON format:

```go
barr, err := json.Marshall(p1)
```

`json.Marshall()` returns JSON representation as `[]byte`.

* `barr` is data as `[]byte`, so `barr` stands for *byte array*
* `err` is `nil` if there is no conversion error

JSON *unmarshalling*:

Converting a JSON `[]byte` into a Go object.

```go
var p2 Person
err := json.Unmarshall(barr, &p2)
```

* as before, `err == nil` if there is no conversion error

Constraint: `p2` must "fit" the JSON `[]byte`, that is must have the same attributes/fields.

## File access in Go

*Files* are still commondly used to trade data between the programmes. File access is *linear access* (not *random access*), because originally they come from *tapes*. 

(What a crap abstraction! Obsolete af.)

Basic operations:

* Open
* Read bytes into `[]byte`
* Write `[]byte` into file
* Seek moves read/write *head* (eek! obsolete)

Go has `ioutil` package for basic file-related operations.

**Reading files in Go**

To read, use `ioutil.ReadFile(fname)`. 
* Don't need to open/close, as the whole file is read at once.
* **Will not work with large files** if cannot fit them in memory.

**Writing files in Go**

```go
dat = "Hello, Gruffalo!"

err := ioutil.WriteFile("outfile.txt", dat, 0777)
```

* Writes `[]byte to file`
* Creates a file
* Uses UNIX-style access permission
* Cannot append to an existing file

## `os` package file access

So, `ioutil` gives some very basic file-related functions. For more granular control, the `os` package has file-related functions.

* `os.Open()` opens a file and returns a descriptor `File`
* `os.Close()` closes a file descriptor
* `os.Read()` reads from a file into a `[]byte`, controls the amount read

**Opening and reading example**

Using the `os` package for opening and reading files.

```go
f, err := os.Open("dt.txt")
barr := make([]byte, 10)
nb, err := f.Read(barr)
f.Close()
```

* Reads and fills `barr`
* `Read` returns # of bytes read
* May be less than `[]byte` length

**Writing a file example**

Using the `os` package for creating the file and writing data into it.

```go
f, err := os.Create("outfile.txt")

barr := []byte {1,2,3}
nb,err := f.Write(barr)
nb,err := f.WriteString("Hello, Gruffalo!")  // it has to be Unicode sequence
```

We could have appended the data to an existing file as well, `os` has functions for that.

---

## The end

This concludes the course!