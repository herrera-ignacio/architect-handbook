# Splitting the Monolith

- [Splitting the Monolith](#splitting-the-monolith)
  - [Summary](#summary)
  - [To Change the Monolith, or Not?](#to-change-the-monolith-or-not)
    - [Cut, Copy, or Reimplement?](#cut-copy-or-reimplement)
    - [Refactoring the Monolith](#refactoring-the-monolith)
    - [Seam](#seam)
    - [A modular monolith](#a-modular-monolith)
    - [Incremental rewrites](#incremental-rewrites)

## Summary

> For incremental rollout to work we have to ensure that we can continue to work with, and make use of, the existing monolithic software.

## To Change the Monolith, or Not?

Consider whether or not you plan (or be able) to change the existing monolith.

* If you have the ability to change the existing system, this will give you the most flexibility in terms of the various patterns at your disposal.
* The existing system may be a vendor product for which you don't have the source code, or it may also be written in a technology that you no longer have the skills for.
* The current monolith may be in such a bad state that the cost of change is too high.
* The current monolith may be being worked on by many other people, and you're worried about hetting in their way.
* You are looking to incrementally re-platform an existing system.

### Cut, Copy, or Reimplement?

We want to *copy* the code from from the existing code, and at this stage, at least, we don't want to remove the functionality from the monolith itself. Why? Because leaving the functionality in the monolith for a period of time gives you more options. It can give us a *rollback point*, or perhaps the opportunity to run both implementations in parallel.

Once you're happy that the migration has been successful, you can remove the functionality from the monolith.

### Refactoring the Monolith

> Often the biggest barrier to making use of existing code in the monolith in your new microservices is that existing codebases are traditionally not organized around business domain concepts. *Technical categorizations* are more prominent (e.g., MVC).

When you're trying to move business domain functionality, this can be difficult: the existing codebase doesn't match that categorization, so even finding the code you're trying to move can be problematic.

### Seam

> Michael Feathers defines the concept of seam in *Working Effectively with Legacy Code*.

A *seam* is a place where you can change the behavior of a program without having to edit the existing behavior. Essentially, you define a seam around the piece of code you want to change, work on a new implementation of the seam, and swap it in after the change has been made.

### A modular monolith

It is worth considering to take your newly identified seams and start to extract them as separate modules, making your monolith a *modular monolith*.

Having modules that can be veloped independently can deliver many benefits while side-stepping many of the challenges of a microservice architecture.

### Incremental rewrites

We are in danger of repeating the problems associated with big bang rewrites if we start reimplementing our functionality. The key is to ensure you're **rewriting only small pieces** of functionality at a time, **and shipping** this reworked functionality to your customers regularly.
