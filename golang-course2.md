## Golang 2

[Functions, Methods, and Interfaces in Go][go2] course notes by Oliver Frolovs, 2020.

[go2]: https://www.coursera.org/learn/golang-functions-methods

Did this course in a day, speed-running videos at 1.25 to 1.5 speed. A lot of territory is familiar from general knowledge of programming. The only part which required thoughtful reading/listening was *interfaces* as they are quite peculiarly designed in Go. But I like them)

**Minor complaints re course organisation**:

* I don't like how the PowerPoint slides for each tutorial are separated into their own section with each getting "Mark as complete" button. I'd put all PPT files with slides for the week into a single (optional) item.
* Announcing the topic title in the beginning and saying 'thank you' at the end of the video also is a waste of time, and gets tiresome to watch as one speed-runs through the course.

## Using function in Go

A *function* is a set of instructions with a *name*. The name is, actually, **optional**.

All programs in Go have to have the `main()` function. When the program is run, it is automatically invoked. All other functions have to be invoked *manually*.

``` go
func main() {
    // ...
}
```

## Simplest function declaration

``` go
func HelloGruffalo() {
}
```

## Why use functions?

* Reusability
* Abstraction &ndash; the designer's friend. Not even limited to *engineering*.

* Good function naming is important for communicating the design intent.
* Good hierarchy for a *package* of many functions is also important.

## Function parameters

*Parameters* provide a way to pass the data into the function to operate on.

* *Parameters* are listed in parentheses after function name.
* *Arguments* are supplied in the call.

In this example, x and y are parameters.

``` go
func Sum(x int, y int) {
    return x + y
}
```

And here, `42` and `z` are *arguments*.

``` go
Sum(42, z)
```

Function without any parameters still requires the parentheses `()`.

``` go
func HelloGruffalo() {
    fmt.Println("Hello, Gruffalo!")
}
```

Listing arguments *of the same type*.

``` go
func Sum(x, y int) {
    // ...
}
```

## Function return value(s)

A function can *return a value* as a result.

The *type of the return value* is noted after the parameters in *function declaration*.

``` go
func Sum(x, y int) int {
    retunr x + y
}
```

Once the function is *defined*, it can be *called*.

*Calling* the `Sum` function:

``` go
z := Sum(1, 2) // z will be assigned the value of 3
```

The function can be executed, without the return value being assigned to anything. This is done for the *side effects* of the function, assuming the function has them defined.

*Calling* the function with no *side effects* and ignoring the *return value*:

``` go
Sum(1, 2) // the return value is quietly discarded
```

*Declaring* the function with *side-effects* &ndash; printing to the console:

``` go
func HelloGruffalo() {
    fmt.Println("Hello, Gruffalo!")
}
```

*Calling* the function for its *side-effects* outputs `Hello, Gruffalo!` to the console but does not return any value.

``` go
HelloGruffalo()
```

**To conclude, nothing new, this is all familiar territory!**

## Multiple return values

Like Python, in Go functions can *return multiple values*.

``` go
// Define: return two next Fibonacci values for two given Fibonacci values
func fib2(a, b int) (int, int) {
    return a+b, b+(a+b)
}
// Call: a is assigned 2, and b is assigned 3
a, b := fib2(1, 2) 
```

**FIXME** this is an awful maths example, wtf Oliver

## Call by value and call by reference

**I am aware that there is some controversy about the meaning of "passing by pointer" vs "passing by reference" in the Go community. I don't want to be part of the debate, so please don't contact me about it.** 

*Call by value* and *call by reference* describe two different ways in which the *arguments* are bound to *parameters* during the *function call*.

### Call by value

Means the argument values are *copied* into the *parameters*. Inside the functions, modifying the values of the *parameters* have no effect on the environment outside the function.

* *Data encapsulation* is a **(+)** of *call by value*
* *Copying time* is a **(-)** of *call by value*. Large objects may take a long time to copy.

## Call by reference

**Is not built into the Go language**. But it can be done *manually* by *passing a pointer as an argument* into the function. This signals that the programmer wants the original data to be altered by the function.

Then, called function has *direct access* to caller variable in memory.

``` go
package main

import "fmt"

// s is a pointer to an integer, where the sum is stored
func Sum(x, y int, s *int) {
    *s = x+y
}

func main() {
    // Define three integers. The third one is auto-initialised to zero.
    x := 1
    y := 2
    var z int

    // Call a function which adds the values of its first two arguments,
    // and stores the result in the third argument which is passed by reference.
    Sum(x, y, &z)

    // Inspect the result
    fmt.Println(z)
}
```

The **(+)** and **(-)** of *call by reference* are the *opposite* of those by *call by value*, haha.

## Passing arrays and slices

**I am aware that there is some controversy about the meaning of "passing by pointer" vs "passing by reference" in the Go community. I don't want to be part of the debate, so please don't contact me about it.**

**Arguments are copied, even arrays.**

In the following example, *the whole array is copied*, even if only one element is used inside the function, and the array is not even altered.

``` go
package main
import "fmt"

func ShowFirst(x [3]int) {
    fmt.Println(x[0])
}

func main() {
    x := [...]int {1,2,3}
    ShowFirst(x)
}
```

Altering the array does not change anything outside the function.

``` go
package main
import "fmt"

func ShowFirst(x [3]int) {
    fmt.Println(x[0])
    x[0] = 121           // altering the argument has no effect on original array
}

func main() {
    x := [...]int {1,2,3}

    ShowFirst(x)
    ShowFirst(x)
}
```

Making `x` "global" (**FIXME** is it in *file* scope?) doesn't change the situation.

``` go
package main
import "fmt"

var x[3]int = [...]int {1,2,3}

func ShowFirst(x [3]int) {
    fmt.Println(x[0])
    x[0] = 121
}

func main() {
    ShowFirst(x)
    ShowFirst(x)
}
```

Passing the array *by reference* changes that.

``` go
package main
import "fmt"

// The function parameter now a pointer to a three element integer array.
func ShowFirst(x *[3]int) { 
    fmt.Println( (*x)[0] )         // the parens () are necessary
    (*x)[0] = 121                  // the parens () are necessary
}

func main() {
    x := [...]int {1,2,3}

    ShowFirst(&x)
    ShowFirst(&x)
}
```

This way of passing arrays by reference is doable, but messy and *isn't ideomatic in Go*. Instead, *slices* are used. In general, *slices* are used in place of arrays in Go.

**Pass slices instead!**

A *slice* is like a window on array. Slices contain a *pointer* to the array.

**Passing a slice copies the pointer.** A slice is like a structure with three elements &ndash; the pointer, the length, and the capacity. By passing the *slice*, it is passed by value, but its value include the pointer, so the underlying array can be accessed! 

Note, that when you decleare a slice you don't have to specify the size. In fact, you can't specify the size, you just give the square brackets.

``` go
package main
import "fmt"

// No array size in [] means it's a slice being passed as an argument, not array.
func IncFirst(sli []int) {
    sli[0] = sli[0] + 1
}

// The array size in [] means it's an array being passed by value
func ShowFirst(x [3]int) {
    fmt.Println(x)
}

func main() {
    x := [3]int {1,5,6}

    IncFirst(x[0:2])

    ShowFirst(x)
}
```

To reiterate, the only difference between passing in the *array* vs passing in the *slice*, is that when the slice is passed, no *size* has to be specified in the square brackets: `xs []float` or `sli []int`.

## Well-written functions

Not specific to Go. The *code* is *functions* and *data*. Focus on **understandability**: when you are asked *to find a feature*, can you find it *quickly*? It's a matter of *organisation*. Another aspect of understandability, is *finding where the data is defined and used*. Being able to trace through data is important.

A function *crashes*. Locally,

* Either the *function* is messed up; or
* Its *input*, that is *data* is messed up.

If the function is *understandable* and the data is *traceable*, it's easier to identify and fix mistakes.

*Global variables* spoil this approach, so use them sparingly, if at all.

## Guidelines for functions

* Give *functions and their parameters* good names &ndash; behaviour can be understood at a glance.

  ``` go
  func ProcessArray(a []float) float {}       // VERY GENERIC CAN MEAN ANYTHING

  func ComputeRMS(samples []float) float {}   // MUCH MORE DESCRIPTIVE
  ```

* Don't go overboard with long function names.
* Aim for *functional cohesion* &ndash; a function should perform only one "operation". What defines "one operation" is domain-dependent. *Merging behaviours* makes code complicated.

  For geometry, as an example, `PointDist()`, `DrawCircle()`, `TriangleArea()`, &hellip;

* Use *few* parameters. The fewer, the better. It improves tracing through data. Debugging is harder, when there are many parameters. Going back to *merging behaviours*, it requires having more parameters, subsets of which are *unrelated* to one another, which complicates *understanding*.
* *Group related parameters* into *structures*.

  `TriangleArea()` requires three `points`. Instead of passing *nine* different values for `x1, y1, z1`, `x2, y2, z2`, and `x3, y3, z3`, you can pass *three* points: `TriangleArea(p1, p2, p3 point)` where each `point` is a structure of three floats. We can go further, and define `TriangleArea(t triangle)`, where `triangle` is a structure of three `point`-s.

* Make function *less complex*, less *tricky*, less "clever". 

  **Make them short.** How do you write sophisticated code with simple functions? Use *function call hierarchy* &ndash; *decompose* large functions into a *hierarchy* of smaller functions.

* *Control-flow complexity* &ndash; the path from the top of the function to the bottom. How many paths are there? One, if there is no *conditional* statements, or loops (which are *implicit* conditional statements). Often, one can use *functional partitioning* (split into several functions) to reduce the *control-flow complexity*.

* **TODO** what tools in **Go** measure *control-flow complexity*?
* **TODO** what tools in **Python** measure *control-flow complexity*?

## First-class values

A concept from *functional programming* &ndash; functions can be treated like any other types:

* variables can be declared with a function type
* functions can be created *dynamically*
* functions can be *passed as arguments* and *returned as values*
* functions can be stored in the data structure, such as slices.

In many ways, Go allows to treat the functions as any other data type.

### Variables as functions

Declare a variable as a function.

``` go
package main
import "fmt"

// This function is defined statically. Its type is (int, int) -> int
func Sum(x, y int) int {
    return x + y
}

// Declare a function variable of the same type as the function above
var funcVar func(int, int) int

// Main is declared statically here, no surprises
func main() {
    // Assign a value to the function variable
    funcVar = Sum

    // Test the function by its new "name"
    fmt.Println(funcVar(1,2))

    // Can leave the type to be figured out by the compiler
    funcVarAsWell := Sum

    // Test the function by its new "name"
    fmt.Println(funcVarAsWell(2,3))
}
```

### Functions as arguments

Functions can be passed to another function as an argument.

``` go
// f is a function of type (int) -> int
// v is an integer value
func apply(f func (int) int , v int) int {
    return f(v)
}
```

### Anonymous functions

Don't need a name to a function! The concept comes from "lambda calculus". But I don't care about it. It's useful though. Using an example from the previous section, `apply`:

``` go
func main() {
    v := apply(func (x int) int { return x+1 }, 42)
}
```

The *anonymous function* definition also begins with `func`.

All in all, the *syntax is very intuitive*.

### Functions as return values

Useful to make *parameterisable* functions. The "constructor" function get the values of parameters and returns another function set up using those parameters.

This works in the same way I've parametrised Python functions in my numerical simulations. No surprises.

**TODO** maybe set up an example from schientific Python sources that I have?

Every function has an *environment*, which includes all the names defined locally in the function. But also, this includes *lexical scoping*, that is all the names available in the block in which the function was defined.

Did someone just say *closure*? ))

``` go
var x int

// The function is defined in the scope which include the variable x (above)
func Boop(y int) {
    z := 1
    // The variable x is available inside this scope as well
}
```

**FIXME** he mentioned technicality about what is the *scope* and what is the *environment*, and said people often confuse the two; check back later&hellip;

* He says "`z` is inside `Boop` *environment*", using the term *scope* would have been incorrect here.
* Variable `y` is local to `Boop()`, so it's also in `Boop()`-s *environment*.
* Variable `x` is defined in the same block as `Boop()`, so it's accessible from `Boop()`-s environment.

The *environment* goes along with the function. This is important when functions get passed around as variables.

Now we geto to... *closures*!

## Closures

A *closure* is **a *function* plus its *environment* together**. In Go, its actually implemented as a `struct`! When functions are passed/returned, their environment comes with them.

What implications does this have? 

When a function is passed as an argument, it's passed as a *closure*, that is together with its environment.

This may be important for figuring out where the variable values are coming from. Remember, that Go is *lexically scoped*.

## Variadic functions

One useful tool is to be able to pass a *variable number of arguments* into the function. Think `fmt.Printf` as an example.

Functions can take a variable number of arguments. 

* Use an *ellipsis* &hellip; to specify.
* Treated as a slice inside the function.

``` go
func Max(vs ...int) {
    maxV := -1 // FIXME valid integer, but cannot use nil here "untyped nil"
    for _, v := range vs {
        if v > maxV {
            maxV = v
        }
    }

    return maxV
}
```

* Treated as a slice inside the function&hellip; but if the data *already is in a slice*, can pass it in as such:

``` go
vsli := []int {1,3,6,9}
Max(vsli...)              // Note the ellipsis in the suffix!
```

Thus, in Go one *can pass a slice to a variadic function* and it will be "unpacked" into variable arguments.

## Deferred function calls

* They don't get executed until the surrounding function completes. 
* Typically used for *cleanup* activities.
* Use the keyword `defer` to&hellip;defer the call))

``` go
func main() {
    defer fmt.Println("Bye!")

    fmt.Println("Hello, Gruffalo!")
}
```

The `defer`-red call is not executed until `main` is complete.

* The *arguments* **are not** evaluated in a deferred way. The arguments are evaluated immediately.

**Arguments of a deferred call are evaluated immediately!**

## Revision example

``` go
// The function fA is (statically) defined here. 
// It takes no arguments. 
// It returns a function.
// The returned function takes no arguments.
// The returned function returns an integer.
//
// Note, that fA forms a closure. 
// That is, the returned function keeps the environment in which it was defined.
// That environment includes the local (to fA) variable i.
// This variable is inaccessible directly from outside the returned function.
func fA() func() int {
    i := 0
    return func() int {
        i++
        return i
    }
}
```

Onto *object-orientation* in Golang now.

## OOP in Golang

Go doesn't have classes *exactly*. But it has something similar. 

Traditionally, *classes* are a collection of *data fields* and *functions* that share a well-defined responsibility. A class is a *template*, it contains the data field, but not data. An *object* is an instance of a class that contains actual data. Blah blah blah, let's leave all that to the purists.

*Encapsulation* is hiding the data and implementation details behind the *interface*. It is associated with *abstraction* in general. It helps with keeping the data (internal state) *consistent*.

So, Go doesn't have a "class" keyword and all that. But&hellip; there are different ways of associating data with methods in Go!

## Associating methods with data in Go

### Receiver type

It's done using a *receiver type*. A method (function) has a *receiver type* that it is associated with. Use *dot notation* to call the method. 

The type has to be defined in the same package as the method that it is associated with. So, can't "monkey-patch" the built-in types.

``` go
type MyInt int

func (mi MyInt) Double() int {
    return int(mi*2)
}

func main() {
    v := MyInt(3)
    fmt.Println(v.Double())
}
```

Hmm... now that's new. So, as defined above, `MyInt` is the *receiver type* for the function `Double()`. By listing a *receiver type* in the function definition, we let the compiler know that when a function `Double` is invoked using dot notation and the &hellip; entity of type `MyType`, this is the right function to invoke.

### Implicit method arguments

It looks as if `Double()` has no arguments, but there is an *implicit* argument. So, this is similar to Python's `self`, I suppose. 

Every time there is a *receiver type* specified in function definition, it creates an *implicit* parameter of that type, which does not have to be listed in parentheses `()` with other parameters. It is *implied*.

Using *dot notation*, object `v` is an *implicit* argument to the method `Double`. Like other arguments in Go, it is *passed by value*. So, a copy gets passed. Interesting.

Weird, but let's hold onto this notion. I hope the benefits of this approach will become obvious soon enough?

To build useful data types, it's common to use `struct`-s as a *receiver type*.

``` go
type Point struct {
    x float64
    y float64
}
```

### Structs with methods

Now, we can define a type using a `struct`, just like in the previous section. And we can use this type as a receiver type with methods to get something similar to classes in other languages. 

Structs and methods together allow arbitrary data and functions to be **composed**.

``` go
// Using the Point struct defined in the previous section...

// Note that the receiver type is Point, 
// and the method gets an implicit parameter named p
func (p Point) DistToOrigin() {
    t := math.Pow(p.x, 2) + math.Pow(p.y, 2)
    return math.Sqrt(t)
}

// Example of using the method...
func main() {
    p1 := Point(3,4)
    fmt.Println(p1.DistToOrigin())
}
```

It looks a bit flimsy so far... but holding on to the idea for now...

## Encapsulation

### Controlling access

Can define *public functions* to allow *controlled access* to hidden data.

``` go
package data
var x int = 100
func PrintX() {fmt.Println(x)}
```

To access it from `main` package:

``` go
package main
import "data"
func main() {
    data.PrintX()
}
```

We can also define a function which would modify the private variable. We can do this with structures too!

## Controlling access to structs

* Hide fields of structs by starting field name with a lower-case letter.
* Define public methods which access hidden data.

``` go
package data

type Point struct {
    x float64
    y float64
}

func (p *Point) InitMe(xn, yn float64) {
    p.x = xn
    p.y = yn
}
```

Here, using the function `InitMe`, we can modify `x` and `y` values of the struct, *without having direct access* to them.

Another example of altering the hidden members of the structure:

``` go
func (p *Point) Scale(v float64) {
    p.x = p.x * v
    p.y = p.y * v
}

func (p *Point) PrintMe() {
    fmt.Println(p.x, p.y)
}
```

Revision: *Point (pointer to Point type) is a *receiver type* for these functions.

The methods have names starting with a *capital letter* so they are *public*.

**FIXME** is this a convention or is it actually enforced by the compiler?

Using the above examples from `main`:

``` go
package main
import "data"


// Access to hidden fields using only public methods.
func main() {
    var p data.Point
    p.InitMe(3, 4)
    p.Scale(2)
    p.PrintMe()
}
```

Hmm... how would you *chain* the method calls?!

**FIXME** yes, actually, how would you *chain* the method calls?

## Limitations of methods in Go

* Receiver is passed implicitly as an argument to the method. Passed *by value*.
* Method cannot modify the data inside the receiver. **FIXME** immutability?

In the following example, a copy of `p1` is passed into `OffsetX()` method as an explicit parameter. Thus, the method *cannot change* the value of `x` inside `p1`!

``` go
func main() {
    p1 := Point(3,4)
    p1.OffsetX(5)     // cannot alter p1
}
```

* Large receiver objects are a problem, because they get copied onto the stack!

  Imagine an `Image` type:

  ``` go
  type Image [100][100]int

  func main() {
      i1 := GrabImage()
      // Before BlurImage() is invoked, 10000 ints get copied...
      i1.BlurImage()      // how would you actually alter the i1?!
  }
  ```

We do what we did before. Need to *call by reference*. Instead of passing in the value of a type, pass a pointer.

### Pointer receivers

When declaring a function, set the *receiver type* to a *pointer*. This achieves *call by reference*.

``` go
// Note the star which tells it's passed by reference
func (p *Point) OffsetX(v float 64) {
    p.x = p.x + v  // FIXME how come we don't need to dereference?
}
```

* Receiver can be a *pointer to a type*.

**There is no need to dereference the pointer inside the method!?**

This is because the technique is common enough for the compiler *to do that for you*. The compiler dereferences it automatically. Likewise, there is no need to reference manually either:

``` go
func main() {
    p := Point(3,4)
    p.OffsetX(5)      // but OffsetX expects pointer receiver, so (&p)
}
```

**FIXME** so is this basically syntactic sugar?

### Using pointer receivers

When using *pointer receivers*, it's a good programming practice to:

* either all methods for a type have *pointer receivers*; or
* all of the methods for a type have *non-pointer receivers*.

## Revision point

* To *associate a method with an arbitrary data type* in Go, *define the method so that its **receiver type** is the data type of interest*.
* To *hide variables or functions in a package*, so that functions outside of the package cannot access them, *give the variable/function a name which starts with a lower-case letter*.

## Polymorphism

Is an ability of an "object" to have many different forms depending on the context.

Polymorphism:

* *identical* at a high level of abstraction
* *different* at a lower level (of implementation)

**FIXME** was Perl's scalar and vector context for a variable... polymorphism?

**Go does not have inheritance!** Which I suppose is fine, because *composition* is so much more useful than *inheritance*.

*Overriding* is another concept traditionally associated with OOP. 

In traditional OOP, *inheritance* and *overriding* (methods) is used to implement the polymorphism. Remember *superclasses*? Bleurgh!

The methods would have same signatures (in terms of superclasses) and this is how polymorphism would be implemented. Traditionally.

Enough, please. No more "traditional" OOP for me.

## Interfaces in Go

Since Go does not have inheritance (thanks!), it uses *interfaces* to implement *polymorphism*. I am familiar with the concept from Objective-C and I like it. I agree with I an that this is a clean approach.

* An *interface* is a *set of method signatures*. 
* It's not a type, it's less than that.
* It's used to model *conceptual similarity* between the types.

Example: `Shape2D` interface, providing `Area()` and `Perimeter()` methods.

* The *interface* does not implement the method, it only provides the signatures.
* Any data type that *implements* the interface, *satisfies* the interface and within the context where the interface is used, these data types can be used interchangeably, thus satisfying the definition of *polymorphism*.

### How to define an interface in go

An interface is defined&hellip; using the `interface` keyword.

``` go
type Shape2D interface {
    Area() float64
    Perimeter() float64
}

// The Triangle data type SATISFIES the Shape2D interface.
type Triangle {...}
func (t Triangle) Area() float64 {...}
func (t Triangle) Perimeter() float64 {...}
```

**NO NEED TO STATE IT XPLICITLY**, unlike in other languages.

## Interface types and concrete types

The *interface types* and *concrete types* are fundamentally different.

### Concrete types

* Specify the *exact representations* of the data and methods.
* *Complete method implementation* is included.

### Interface types

* Specifies *some* method signatures. No data is specified.
* Implementations are abstracted. As in *not provided*.
* But remember that an interface gets *mapped* to a concrete type!

When you create the interface, you declare an *interface type*. But then you *can make values of that type*! You *can declare variables of that type*. You can pass and return the values of that type. In the example given in previous sections, a variable of type `Shape2D` can be declared. 

Now, the *interface value*, that is the value of the *interface type* has two components:

* there is a *dynamic **type*** &ndash; a *concrete type*, that is assigned to;
* there is a *dynamic **value***, is actually the value of that *dynamic type*.

In the `Shape2D` example, the *dynamic type* could be a `Triangle` or a `Rectangle`. The *dynamic value* would be a value of type `Triangle`, instantiated in a program.

Subtle, but understandable so far&hellip;

So, and *interface value* **is actually a pair**, the *dynamic type* together with the *dynamic value*.

**TODO** read this again later haha

## Example of the shenanigans above

``` go
// An interface type is defined. It contains a single method (void) -> (void).
// It's a very simple interface, indeed.
type Speaker interface {
    Speak()
}

// A (concrete) type Dog, representing... a dog is defined.
// It contains only a single field of type string, which is the dog's name.
// It's a very simple data type, indeed.
type Dog struct {
    name string
}

// A method (!!!) with the "receiving type" Dog is defined.
// The method name and signature match those declared in the Speaker interface.
// Thus, this definition makes the Dog data type SATISFY the Speaker interface.
func (d Dog) Speak() {
    fmt.Println(d.name)
}

func main() {

    // A variable of the interface type is declared. It has no value assgned yet.
    // But it is going to have an value of interface type Speaker assigned later.
    var s1 Speaker

    // A variable of (concrete) type and a value of that type is assigned to it.
    var d1 Dog{"Brian"} 

    // Since the (concrete) type Dog implements the interface Speaker,
    // this assignment is legal. Now, the dynamic type of s1 is Dog, 
    // and the dynamic value is that value of (concrete) type Dog which has
    // the name "Brian".
    s1 = d1

    // So, s1 is a PAIR: a "dynamic type" together with a "dynamic value".
    s1.Speak()
}
```
Now, the interface can have a `nil` *dynamic value*, meaning no dynamic value. It can have a *dynamic type* but not a *dynamic value*:

``` go
func main() {
    var s1 Speaker
    var d1 *Dog       // FIXME why a pointer though?

    // d1 has no concrete VALUE yet
    s1 = d1
    // s1 now has a dynamic type, but no dynamic VALUE
}
```

How do you like that, Elon Musk?

## `nil` dynamic value

* Can still call the `Speak()` method of `s1`

**FIXME** but to what end?!

* The compiler doesn't need a dynamic value to call

  It would be *wise* to check inside `Speak()` if there is a dynamic value assigned, indeed!

**FIXME** I'm still puzzled as to why that is beneficial?

Yes, you *can* (or rather *could*) make the call, but why would you want this to be *legal*?

``` go
func (d *Dog) Speak() {
    if d == nil {
        fmt.Println("<noise>")
    } else {
        fmt.Println(d.name)
    }
}
func main() {
    var s1 Speaker
    var d1 *Dog

    s1 = d1
    s1.Speak()
}
```

**FIXME** is this some kind of "superclass" "overrideable" behaviour example?

For now, the point is that

> It is legal to have an interface with a *dynamic type* but without a *dynamic value*.

There is also another concept, *nil dynamic type*, which describes an interface with a&hellip; `nil` *dynamic type*. And that's a different situation &ndash; then you cannot call the methods on that interface. 

Because without the *dynamic type* you **don't know which method you are referring to**!

``` go
var s1 Speaker
// Cannot call a method s1.Speak(), 
// that would result in a runtime error
```

Hmm&hellip; ok, I understand *how* it works, but still don't get *why* you'd want that "feature" to be legal? 

**TODO** check back later in the course

## Why interfaces?

* Function overloading: take `int` or `float`. Take interface `z` instead.

This is a common way to use an interface. Hides the details between the types, emphasises important common features between the types.

## Empty interface

An *empty interface* specifies **no methods**.

* *All types* satisfy the empty interface.
* Use it **to have a function accept any type as an argument**.

``` go
// Here, val can be ANY type.
func PrintMe(val interface{}) {
    fmt.Println(val)
}
```

This is how you specify an empty interface: `interface{}`.

## Type assertions

A lot of use for *interfaces* is to conceal the difference between the types. But *sometimes* one needs to *differentiate based on a type*. In some cases, *concrete types* matter. In those cases, you have to *expose type differences*.

How do you peel off the interface to look at the concrete types?

Example: graphics interface, for `DrawShape(s Shape2D)` any shape will do, but for **implementation** of the interface, I might want to know the *concrete type* of `s`, perhaps to map them to native graphics API.

In this case, *type assertions* can be used to **determine and extract** the underlying *concrete type*:

``` go
func DrawShape(s Shape2D) bool {

    rect, ok := s.(Rectangle)         // Concrete type in parentheses ()
    if ok {
        DrawRect(rect)
    }

    tri, ok := s.(Triangle)           // Concrete type in parentheses ()
    if ok {
        DrawTriangle(tri)
    }
}
```

* If interface contains concrete type: `rect == concreteType, ok == true`
* Otherwise, `rect == zero, ok == false`

Because there can be *many* different types to disambiguate, there is a `switch` construct which is meant precisely for that!

### Type switch

Switch statement used with a *type assertion*.

``` go
func DrawShape(s Shape2D) bool {
    switch sh := s.(type) {
        case Rectangle:
            DrawRectangle(sh)
        case Triangle:
            DrawTriangle(sh)
        default:
            fmt.Fprintf(os.Stderr, "unknown type\n")
    }
}
```
The *type assertion* part here is `s.(type)`. The generic word `type` is used. Then, `sh` will be whatever the *concrete type* `s` represents.

## Handling errors

The *error interface*.

Many Go programs (packages) return *error interface* objects to indicate errors.

``` go
type error interface {
    Error() string
}
```

**Wow so sophistication much error handling wow haha**

* Under correct operation, `error == nil` is returned.
* On error, `Error()` prints error message.

Lots of Go functions return `error` as a *second return value*.

``` go
f, err := os.Open("/etc/issue")
if err != nil {
    fmt.Println(err)
    os.Exit(1)
}
```

The `fmt` package calls `error()` method to generate string to print. Handy!

The pattern is:

1. check whether error is nil
2. if it is not nil, handle it

## Revision points

* Type assertions return *two* values:

  ``` go
  rect, ok := s.(Rectangle)
  ```
* From a quiz: *an interface always has a dynamic type*. 

  I suppose they mean that in the worst case, the dynamic type is the the *interface type*, such as `Shape2D` in the examples.

  ## End of course

  And this concludes the second course in series)
  