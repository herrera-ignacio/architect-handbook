# Unix Philosophy

- [Unix Philosophy](#unix-philosophy)
  - [Definition](#definition)
  - [Origin](#origin)
  - [Eric Raymond's 17 Unix Rules](#eric-raymonds-17-unix-rules)
  - [Mike Gancarz Principles](#mike-gancarz-principles)
  - ["Worse is better"](#worse-is-better)

## Definition

The *Unix philosophy*, originated by *Ken Thompson*, is a set of cultural norms and philosophical approaches to minimialist, modular software development. It is based on the experience of leading developers of the Unix operating system.

The Unix philosophy emphasizes building simple, short, clear, modular, and extensible code that can be easily maintained and repurposed by developers other than its creators. It favors *composability* as opposed to *monolithic design*.

## Origin

The Unix philosophy is documented by *Dough Mcllory* in the Bell System Technical Journal from 1978:

1. Make each program do one thing well. To do a new job, build afresh rather than complicate old programs by adding new "features".
2. Expect the output of every program to become the input of another, as yet unknown, program. Don't clutter output with extraneous information. Avoid stringently columnar or binary input formats. Don't insist on interactive input.
3. Design and build software, even operating systems, to be tried early, ideally within weeks. Don't hesitate to throw away the clumsy parts and rebuild them.
4. Use tools in preference to unskilled help to lighten a programming task, even if you have to detour to build the tools and expect to throw some of them out after you've finished using them.

It was later summarized by *Peter H.Salus* in A Quarter-Century of Unix (1994):

* Write programs to do one thing and do it well.
* Write programs to work together.
* Write programs to handle text streams, because that is a universal interface.

## Eric Raymond's 17 Unix Rules

Eric S. Raymond summarizes the Unix philosophy as KISS principle in his book *The Art of Unix Programming* (2003) and provides a series of design rules:

* Build *modular* programs
* Write *readable* programs
* Use *composition*
* Separate mechanisms from policy
* Write *simple* programs
* Write *small* programs
* Write *transparent* programs
* Write *robust* programs
* Make data complicated when required, not the program
* Build on potential users' expected knowledge
* Avoid unnecessary output
* Write programs which fail in a way that is *easy to diagnose*
* Value *developer time* over machine time
* Write *abstract* programs that generate code instead of writing code by hand
* *Prototype* software before polishing it
* Write *flexible* and *open* programs
* Make the program and protocols *extensible*

## Mike Gancarz Principles

Mike Cancarz, a member of the team that designed the [X Window System](https://en.wikipedia.org/wiki/X_Window_System) sums Unix Philosohpy in nineparamount precepts:

1. Small is beautiful.
2. Make each program do one thing well.
3. Build a prototype as soon as possible.
4. Choose portability over efficiency.
5. Store data in flat text files.
6. Use software leverage to your advantage.
7. Use shell scripts to increase leverage and portability.
8. Avoid captive user interfaces.
9. Make every program a filter.

## "Worse is better"

*Richard P. Gabriel* suggests that a key advantage of Unix was that it embodied a design philosophy he termed *"worse is better"*, in which *simplicity* of both the interface and the implementation are more important than any other attributes of the system — including correctness, consistency, and completeness.
