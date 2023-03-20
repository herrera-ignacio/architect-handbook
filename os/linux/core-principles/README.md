# Linux - Core Principles

Linux follows five core principles.

- [Everything is a file](#everything-is-a-file)
- [Small, single-purpose programs](#small-single-purpose-programs)
- [Ability to chain programs together to perform complex tasks](#ability-to-chain-programs-together-to-perform-complex-tasks)
- [Avoid captive user interfaces](#avoid-captive-user-interfaces)
- [Configuration data stored in a text file](#configuration-data-stored-in-a-text-file)

## Everything is a file

Everything is treated as a file. You can access to the hardware in the same way as you access to a document.

> For example, the UNIX security model is based around the security of files.

## Small, single-purpose programs

Prefer small programs that solve one task very well. When new functionality is required, create a separate program rather than extending an existing utility with new features.

## Ability to chain programs together to perform complex tasks

The output of one program can be the input for another. This gives the flexibility to combine many small programs together to perform a larger, more complex task.

## Avoid captive user interfaces

Linux is designed to work with the shell, which gives the user greater control over the OS.

Interactive commands are rare in UNIX. Most commands expect their options and arguments to be typed when the command is launched. Then, the command produces output or generates an error message and quits.

## Configuration data stored in a text file

Storing configuration in text allows an administrator to move a configuration from one machine to another easily. Moreover, you may have an history of changes, and the ability to rollback to a previous version.

> An example of such file is the `/etc/passwd` file, which stores all users registered on the system.
