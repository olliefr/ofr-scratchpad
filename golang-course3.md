# Golang 3

[Concurrency in Go](https://www.coursera.org/learn/golang-concurrency/) course notes by Oliver Frolovs, 2020.

**This is different from other two sets of notes in that I had recorded only the concepts or facts that were truly new to me... so the notes are very short))**

## Moore's law and other animals

* *Dennard scaling* (1974) &ndash; an observation stating that *as the transistors get smaller their power density stays constant. Not true anymore.

## Concurrent and parallel

*Concurrent* means that task start and end times overlap, so that their execution *may* happen in parallel.

True *parallel* execution requires having more than one instance of hardware to run several sets of instructions *at the same time*.

*Concurrent execution* is very likely to still offer advantage over *sequential execution* because often the tasks have to wait on IO (incl. memory access).

*Parallel compilers* are hard and they don't work (yet).

## Processes

On Linux, the scheduler gives every process a 20 ms time slice.

## Goroutines

* *Goroutines* are a *thread* but in Go.
* Many *goroutines* execute within a single OS thread.
* From OS point of view, it schedules the "main thread", but inside it Go switches its *goroutines*.
* Go Runtime Scheduling does switching.
* Go coroutines mapped to a *logical processor* which is tied to the *main thread*. There is no opportunity for the *parallelism* in this scheme of things, but then you can add cores, hence add *logical processors*, and then Go runtime can do *parallel scheduling*.

*Interleavings* are instructions in two different tasks. The *order of execution* between concurrent tasks is not deterministic. A *race condition* is a problem that might happen as a result of interleaving. It happens when the outcome of a program depends on interleaving order. *Race conditions* happen due to *communication* between tasks. 

**A *goroutine* is a lightweight thread managed by the Go runtime.**

``` go
go f(x, y, z) // starts a new coroutine running f(x,y,z)
```

The evaluation of `f`, `x`, `y`, and `z` happens in the current goroutine and the execution of `f` happens in the new goroutine.

Goroutines run in the same address space, so access to shared memory must be synchronised. The `sync` package provides useful primitives, although you won't need them much as there are other *primitives*. (???)

## Synchronisation

By using *synchronisation* we restrict the scheduling. Every time we use synchronisation, we reduce performance, but this is *necessary evil*. 

``` go
// GOROUTINE 1:

x = 0
x = x + 1

// MAKE GLOBAL EVENT HAPPEN
```

``` go
if <GLOBAL EVENT HAPPENED> {
    fmt.Printf("x = %d", x)
}
```

## Wait groups

The `sync` package contains functions to synchronise between Goroutines. It includes `WaitGroup`s. 

* `sync.WaitGroup` forces a goroutine to wait for other goroutines. The goroutine would not continue until all goroutines in a waiting group have finished. 
* A `WaitGroup` is a general type with a lot of methods defined for it.
* The `WaitGroup` object internally contains a *counting semaphore*. The counter is increment for each goroutine added to the group, and decremented when a  goroutine from the group is completed.

**FIXME** is this implemented using `defer`?

``` go
// Main Thread:

var wg sync.WaitGroup

wg.Add(1)
go MouseDoTheJob(&wg) // create another goroutine
wg.Wait() // the current (main) goroutine stops until MouseDoTheJob() returns
```

``` go
// MouseDoTheJob() goroutine

// ...
wg.Done() // can use defer to make sure it's done at the end
```

A summary of `WorkGroup` methods:

* `Add` increments the *counter*
* `Done` decrements the *counter*. It's executed at end of each goroutine.
* `Wait` would block its calling goroutine, until the *counter* is zero.

### Example

``` go
func foo(wg *sync.WaitGroup) {
    fmt.Println("'Mamka Tvoya', said the Horse.")
}

func main() {
    var wg sync.WaitGroup
    wg.Add(1)
    go foo(&wg) // because Go is pass by value, remember, and foo must call Done,
    // which decrements the counter
    wg.Wait()
    fmt.Println("But the Mouse heard only 'Neigh!'")
}
```

### Goroutine communication

Simple form of communication between the goroutines:

* the initial data send to the goroutines
* the results are sent back from the goroutines

* The *goroutines* communicate using *channels*. 
* The *channels* are, essentially, *pipes*. 
* The *channels* are *typed*.

Use `make()` to create a channel:

``` go
c := make(chan int)
```

Once the channel is made, one cand send and receive the data using the *arrow operator*:

* Send data on a channel: `c <- 3`
* Receive data from a channel: `x := <- c`

By default the channels are *unbuffered*. It means it cannot hold the data in channel:

* the *sending* operation *has to block* until the data is *received*. 
* the *receiving* operation *has to block* until the data is *sent*.

So, when using the channels in this way (unbuffered), they also perform *synchronisation*.

* **Channel communication is synchronous.**
* *Blocking* is the same as *waiting for communication*.

This means the channels can be used just for synchronisation, and the result can be dropped.

Not assigning to a variable, throw away the value received, synchronise only:

``` go
<- c
```

### Buffered channels

The default capacity of a channel is zero, that is the channel is *unbuffered*.

But one can make a *buffered* channel, which have some capacity to hold the data in transit.

The example below creates a *buffered channel* of capacity three, that is it can hold three integers without blocking, unless the channel is full:

``` go
c := make(chan int, 3)
```

So, this channel would *block* iff the buffer is full.

The main reason to use buffering is when two goroutines operate at a different speeds. It's a classic *consumer/producer* problem.

Producer -> [ B| U | F | F | E | R ] -> Consumer

If the producer is faster than a consumer (*on average*), the buffer will allow both of them to continue without *blocking*, that is without reducing concurrency.

*On average* requirement is there because if the producer is *always* faster than the consumer, with a fixed buffer size, at some point the buffer is going to be full.

## Revision interlude

>
> ... the size of an array is part of its type ...
>
> ...
>
> There is a built-in function called `len` that returns the number of elements of an array or slice and also of a few other data types.
>
> ...
>
> Arrays have their place—they are a good representation of a transformation matrix for instance—but their most common purpose in Go is to hold storage for a slice.
>
> ...

[Arrays, slices (and strings): The mechanics of 'append'](https://blog.golang.org/slices) by... Rob Pike!


## Iterating through a channel

The following loop will continue to read from channel `c`, blocking when there is no data to be read. The loop will run one iteration each time a new value is received. The variable `i` is assigned to the read value.

``` go
// "c" is a channel as defined before

for i := range c {
    // ...
}
```

This `for` loop is infinite loop, unless the *sender* calls `Close` method on the channel `c`:

``` go
// Some sender goroutine...
close(c)
// Now another goroutine which listens on that channel, can quit the for loop
```

There is no need to call `close` on a channel, unless there is a `for` listening on it.

## Receiving from multiple goroutines

The data can be read from *multiple* goroutines using *multiple* channels.

*Sequential* read (blocking):

``` go
a := <- c1
b := <- c2
fmt.Println(a*b)
```

*Select* statement (having a value read from just one channel is enough):

``` go
// Whichever value comes first, it gets processed and that's that...
select {
    case a = <- c1:
        fmt.Println(a)
    case b = <- c2:
        fmt.Println(b)
}
```

It reads whatever comes first and doesn't block on the other channel. **First come first served!**

## Synchronised communication

In the previous example using `select` we've been blocking on *receiving* data. But we can block on *sending* data, too.

May `select` either *send* **or** *receive* operations.

``` go
select {
    case a = <- inchan:
      fmt.Println("Received a")
    case outchan <- b:
      fmt.Println("sent b")
}
```

*Either* one of these cases can block. Whatever is unblocked first, happens. 

## Select with an Abort channel

``` go
for {
    select {
        case a <- c:
            fmt.Println(a) // process the data
        case <- abort
            return  // another signal received on the abort channel
    }
}
```

## Default select

To avoid blocking, use a `default` clause in a `select` statement.

``` go
select {
    case a = <- c1:
      fmt.Println(a)
    case b = <- c2:
      fmt.Println(b)
    default:
      fmt.Println("nop")
}
```

## Mutual exclusion

Sharing variables between goroutines can cause problems. A thread program is said to be *concurrency-safe* if it can be invoked concurrently with other goroutines without interfering with those other goroutines. 

### Variable sharing example

The following example *does not always return* two.

``` go
var i int
var wg sync.WaitGroup

func inc() {
    i = i + 1
    wg.Done()
}

func main() {
    wg.Add(2)
    go inc()
    go inc()
    wg.Wait()
    fmt.Println(i)

}
```

To understand why, think about how the statement `i = i + 1` is represented in assembly. It *may* take more than a single instruction. Now, the *interleaving* between the two goroutines happens at the machine instruction level, so it is possible that the first goroutine has read the value from memory but got interrupted right after, and then the second goroutine has done the same... I see where this is going!

**The *granularity of concurrency* is at the level of machine code instructions, not Go statements.**

So, with the wrong interleaving, the value of `1`, instead of `2` will be written into the variable.

## Mutex

* Don't let two goroutines write to a shared variable at the same time! Interleavings can cause problems.
* Need to restrict possible interleavings. Access to shared variables cannot be interleaved.
* The technique is called *mutual exclusion*, or *mutex*.
* The means there will be *code segments* in *different* goroutines which cannot execute *concurrently*, so they'll never *interleave*.
* *Mutex* (as in `sync.Mutex`) ensure *mutual exclusion*. Uses a *binary semaphore*: flag up, flag down.

## Mutex methods

Methods of `sync.Mutex`:

* `Lock` method puts the flag up; shared variable in use; second call to `Lock` method from another goroutine will *block* until the first flag is lifted.
* `Unlock` method puts the flag down; done using shared variable; when `Unlock` is called, a blocked call can proceed.

### Mutex example

``` go
var i int = 0
var mut sync.Mutex     // creates a mutex; shared between all instances of inc()

func inc() {
    mut.Lock()         // locks a mutex, "flag up"
    i = i + 1
    mut.Unlock()       // unlocks a mutex, "flag down"
}
```

## Once synchronisation

### Synchronous initialisation

By definition, *initialisation* happens once and *before everything else*. But this can be hard to guarantee in a concurrent environment.

How do you guarantee in a *concurrent environment*, that:

* initialisation happens *only once*; and 
* initialisation happens *first*, before anything else?

Solution:

* One way is to initialise *before* starting the goroutines. But sometimes we don't have that option.
* Another way is to use `sync.Once` object. It has a method `Do`, which runs the given function *only once*. 

``` go
once.Do(f)
```

This can be put in *lots of different goroutines*, but it'll be run only once.

* *All* calls to `once.Do()` block until the first returns. This ensures that initialisation executes first.

### Synchronous initialisation example

The main program creates two goroutines which both rely on some shared data which must be initialised before anything else happens:

``` go
var wg sync.WaitGroup

func main() {
    wg.Add(2)
    go bleat()
    go bleat()
    wg.Wait()
}
```

The `setup` function sets up the environment and will have been finished before the goroutines can proceed. This is ensured by the `on.Do(setup)` statement.

``` go
var on sync.Once

func setup() {
    fmt.Println("Init")
}

func bleat() {
    on.Do(setup)
    fmt.Println("Baa!")
    wg.Done()
}
```

Result:

``` shell
Init
Baa!
Baa!
```

## Deadlocks

So, *channels* and the primitives provided in the `sync` package allow for various forms of *synchronisation*.

*Deadlocks* are caused by *synchronisation dependencies*. Specifically, the *circular depenendencies*. A goroutine `A` is blocked because it is waiting on something done by a goroutine `B`. The latter goroutine, actually is blocked too, because it is waiting on the goroutine `A` to complete something else! Both goroutines are blocked waiting on one another!

### Example

* G1 is waiting on G2 to unlock some mutex
* G2 is waiting on G1 to write something into some channel

## Deadlock detection

* If *all* goroutines are deadlockes, Go runtime will detect it and `panic()`
* If only *some* goroutines are deadlocked, the Go runtime cannot detect that.

## Dining philosophers problem

* Classic problem involving *concurrency* and *synchronisation*

The problem:

* Five philosophers sitting at a round table
* One chopstick is placed between each adjacent pair
* Want to eat rice from their plate, but needs two chopsticks
* Only one philosopher can hold a chopstick at a time
* Not enough chopsticks for everyone to eat at once

This problem was lifted from [Hoare's book](http://www.usingcsp.com/). I highly recommend it, it's rather accessible and it explaines the problem and the model on which concurrency in Go is based on!
