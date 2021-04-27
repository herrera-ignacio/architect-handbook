# Why Golang?

* What is Go?
* Compiled language
    * Cross Compiling
* Simplicity
* Static Types
* First class functions
* Simple scoping rules
* Garbage collection
* Scalability & Concurrency
* Drawbacks
    * Package management
    * Debugging

## What is Go?

Go was started by a small team at Google as an attempt to gracefully handle the challenges that large organizations (like Google) face. It's a response to growing trends that seek to reduce the mental overhead that a programming language requires and to reduce compile times to support code-build-test loops required by methodologies such as TDD. Go emphasizes simplicity and clarity in its code so that it's easier to understand and maintain. At the same time, Go incorporates powerful features that allow very sophisticated applications to be built. 

## Compiled Language

Compiled languages are known for their __speed__, as they're converted directly into machine-level code that can be read directly by the computer instead of being interpreted every time the application is run. Go compiler offers additional benefits like __error checking__, __easier deployment__ and the ability to __optimize your code__ for effiency.

Able to detect unused variables, missing packages, or imports necessary to run and mistyped, or invalid operations.

### Cross Compiling

Go compiler has the ability to cross-compile your application to run on a different machine than the one used for development, you can generate executable binaries for different operating systems with simple commands.

## Simplicity

Many languages have numerous keywords that a developer must remember. Several of these keywords are designed to support programming concepts that have been around for decades. With Go, many of these concepts have been condensed as much as possible in order to reduce the amount of keywords required. As a result, __Go currently has around 25 keywords, as opposed to 50 or more languages like Java and C#__.

## Static Types

Operations with data types are __validated during the build__ before we run our program. This leaves less room for unexpected surprises during runtime.

Static types can also help our programs __use memory more efficiently__. By assigning specific data types to our variables, the Go compiler can determine ahead of time exactly how much memory memory space is needed to store values assigned to those variables.

## First Class Functions

When object oriented language dominated the software development landscape, the lowly function was largely relegated to being defined in the context of a class. With the discovery that first-class functions were one of JavaScript’s good parts, many languages have worked to restore functions to first-class status. Go absorbed this lesson and __allows functions to be created and passed around the application__. That doesn’t mean that it has abandoned object-orientation; rather, __it blends the best aspects of functional programming and object-oriented styles__ to provide greater flexibility with as little ceremony as possible.

## Simple Scoping Rules

Many languages offer developers great flexibility to ensure that variables and functions can be hidden from other parts of the code base.

Go has only __three levels of scoping and very simple conventions__ for determining scope:

1. Local variables (declared within a function) are scoped to current block.

2. Package level variables are scoped to the package if they start with a lower-case letter.

3. Package level variables are publicly scoped if they start with an upper-case letter.

There's __no "private" scope__.

## Garbage Collection

Garbage Collection, or automatic memory management, is a key feature of the Go language. Go excels in giving a lot of control over memory allocation and has dramatically reduced latency in the most recent version of the garbage collector by running concurrently with the program and by using a __tricolor mark-and-sweep algorithm__.

## Scalability & Concurrency

Go was designed with scalabiltiy in mind. Go has many built-in features designed to handle concurrency, most notable __goroutines__ and __channels__.

Go adopted the __Communicating Sequential Process (CSP) model (aka The _Actor Model_)__ that's been used successfully by Erlang.

_Goroutines_ (light-weight _green threads_) are functions capable of running concurrently with other functions, so we can write concurrenct code in a much simpler level of abstraction. We never have to deal with threads or manually share memory. Instead Go provides _Channels_ (_communication pipelines_) that allow sharing memory by communicating across goroutines.

This allows an application to run with thousands of actors, without the burden of trying to keep shared memory free from corruption.

## Drawbacks

### Package management

Go's package manager covers the basics, but it doesn't support things like _version pinning_, which can be critical when your application depends on a specific version of a library. The Go core team is improving the tool, but a final solution is still in the distance. The community is working on it with tools like _godep_.

### Debugging

When Go first launched, it used the GNU debugger (_GDB_) as its primary source of debugging support. While this works in limited scenarios, Go's execution model is so different from what GDB expects that it quickly runs into issues. The community is working on it with projects like _delve_, but there's not any deep integration of a debugger in an IDE right now.
