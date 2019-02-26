---
title: In the beginning was the command line
author: Phillip M. Alday
date: 2019-02-28
---

# Computers, how do they work?

## A very modern use of the word
* until relatively recently, a *computer* was a human who did computations
* several millenia of mechanial assistance of increasing complexity
* but such devices as a rule could only perform a single operation

## Computer science is as much as computers as astronomy is about telescopes
* early 20th century mathematics started examining what it means to compute
	- what can we actually compute?
	- what if a machine can implement the "essence" of computation instead of a particular computation?
* various formalisms for studying this with deep relationships / equivalences between them:
	- lamdba calculus
	- Turing machine
	- formal lanugage theory

## But implementation ultimately matters
* these abstract formalisms are powerful tools but often assume impossible things like "an infinite tape"
* most modern computing devices are von Neumann machines:
	- central executive that actually does the computation
	- memory for instructions for that executive
	- memory for data
* (for cognitive neuroscientists -- does this seem like a plausible analogy for brain-based computations?)
* but because of deep equivalence, other architectures can be emulated, simulated or otherwise executed (e.g. artificial neural networks)
* many of these insights would have played a role in the 19th Century Babbage designs, had the engineering technology existed to build them!

## Electric and electromechnical digital computers
* consist entirely of wires and switches of various types:
	- originally mechanical relays
	- then vaccuum tubes
	- then transistors (although modern transistors are over a billion times smaller than the original ones)
* the entire state of the computer are the open and closed connections!
* computations are just well defined state transitions

## Assembly language
* a somewhat readable list of state transitions based on primitic operations which already exist in the processor
* originally developed by Grace Hopper, USN (later admiral!)
* not exactly easy to read:

		mov ax, 13h
        int 10h
        mov dx, 3c8h
        xor al, al
        out dx, al
        inc dx
* but still much better than manually flipping switches / plugging wires to express the original program
* converted into machine code -- the zeros and ones -- via a program called an assembler

## Dawn of the Higher Level Languages

### Quite high on early on
* FORTRAN (FORmula TRANslator) and LISP (LISt Processor) were the first high-level languages but these were not easy to use for many things
* nonetheless still very useful for nearly abstracting away the physical machine from the notation or *language* used to describe and solve the problems of that day

### But then lower again a bit later
* C (1960s) and later C++ and Objective-C (1980s) were in many ways lower-level languages than Fortran or Lisp in that they exposed more of the details of the hardware (such as with manual memory management) to the programmer.
* These languages form the basis for the majority of software that you now use, including your operating system

## Hello World in C

	#include <stdio.h>

	int main(int argc, char **argv){
		printf("Hello World!\n");

		return 0;
	}

Much like assembly language had to be assembled, many higher level languages first have to be *compiled* before than can be used. Most popular languages have several compilers -- the language is distinct from the compiler.

## Operating Systems and User Interfaces
* on all computers, there is tiny bit of code to load in the initial instructrions / programs called the bootloader.
* on the earliest computers, this was all you had, which meant that your program had to deal with making the entirety of the user interface as well as all the machine specific-stuff for memory allocation, data loading, etc etc.
* today, the bootloader generally loads another program that provides all the basic infrastructure, called the operating system:
	- Windows
	- macOS, iOS
	- Linux, Android
* we can thus program for a particular operating system instead of a particular hardware configuration (and in many cases, it's possible to program for a particular library that translates things to OS-specific calls)

## In the beginning was the command line
* One of the oldest and most widely spread OS's is Unix
* Both the direct and indirect descendants of Unix power almost all the computers in the world -- macOS is based on BSD Unix, Android is based on Linux, which is a reimplementation of SysV Unix, etc.
* Despite the dominance of Windows on the PC, Unix remains #1 across all computational devices.
* Unix has a very basic interface, called the "shell" or "command line interpreter" , which interprets basic user commands
* Windows, as a legacy of its DOS roots, has something similar with `cmd.exe` but it's not as tuned to a programmer's needs, although PowerShell does address some of these issues.

---

This command line is not user friendly because it offers fewer "hints" about what you can perform next. Nonetheless, it is an immensely powerful tool because it was written for and by people who wanted to complicated things with their computers.

----

Today, you learn not to fear the command line.

	phillip@thorfinn:~/Work/pragmatic-python$ ls
	00-introduction.md  00-introduction.pdf  Makefile

. . .

Please note though: on modern Macs and modern Linux, the command line is slightly hidden, but it's still at the core of machine. The command line on Windows is less well integrated, so some things may be a little bit tougher at first. :(

## Plain Text for the People
* At about the same time Unix was becoming popular, a broad consenus was established in the US on a particular way to encode text as binary, i.e. computer, data.
* This standard is known as ASCII and while there were many extensions to this basic standard, the world eventually agreed on Unicode with its various encoding schemes.
* If you work with text extensively, especially with odd letters, you'll have lots of fun learning more about these different coding schemes, but for now it suffices to say that we all agree on the core part consisting only of English letters and punctuation.
* Plain text files -- regardless of extension -- are the foundation of working with the computer as a programmer. There are dozens of tools refined over the generations for processing and manipulating plain text. Compilers are arguably just one more such tool -- they read in plain text and translate it according to a set of rules into machine code.

-----

Your life will be easier if you have a decent plain text editor (and aren't always tied to RStudio), so let's install some software.

* macOS: TextWrangler
* Windows: KomodoEdit, Notepad++,  Geany
* Linux: KomodoEdit, Geany,  Kate, vim/emacs, if you can handle it


## Line endings are annoying, so watch out!

ASCII was originally developed to transmit characters to a teletype, which was basically a machine-driven typewriter. As such, it has two different commands for moving to the next line:

* \\r carriage return (characters that aren't printable often has an equivalent expression as an escape sequence of backslash followed by a single letter code)

* \\n new line

Because that distinction doesn't matter as much when you're just manipulating text and not moving it to a teletype, the different OSes use different ones to express the concept of new line:

* Windows: \\r\\n
* Unix:     \\n
* old MacOS \\r

If you get weird errors where you're missing linebreaks, this is usually what happened. A good programmer's editor can deal with automatically.

-------

## The Command Line and the REPL {.allowframebreaks}

    >>> 1+2
    3
    >>> "Hello World!"
    'Hello World!'
    >>> 'Hello World!'
    'Hello World!'
    >>> 2**8
    256
    >>> 7 // 8
    0
    >>> 7 % 8
	7
    >>> 7 / 8
    0.875
    >>> 7.0 / 8
    0.875
    >>> sqrt(2)
    Traceback (most recent call last):
    File "<stdin>", line 1, in <module>
    NameError: name 'sqrt' is not defined
    >>> import math
    >>> math.sqrt(2)
    1.4142135623730951
    >>> from math import *
    >>> sqrt(2)
    1.4142135623730951
    >>> _
    1.4142135623730951
    >>> print(1.0 - 0.9)
    0.1
    >>> _
    1.4142135623730951

* The language Python is distinct from the program Python, which carries out commands written in that language. There are many alternative programs capable of executing Python code (including one written entirely in Python itself!), so if we wish emphasize that we are using the "usual" Python program, we can say "CPython".
* If given a filename with commands to execute, the Python program will simply execute all the commands in that file and terminate.
* If started without a filename, then the Python program will enter the interactive **REPL**: **R**ead  **E**valuate **P**rint **L**oop
* MATLAB and R also have a REPL, but we often interact with them when they're wrapped up in a large integrated development environment (IDE).
* Note that the REPL is a command line interface of sorts, but it is not the system / OS command line!

# Find your command line

# The Unix Philosophy

## Pipelines in Unix and in R

# Text Encoding: It's line endings all over again

## Time to install some sofware
- Install Git -- either alone or via SourceTree (free Bitbucket/Atalassian account required for the latter)
	- (I find Git generally much more awkward on Windows than Mercurial but it SourceTree makes it bearable, it works better with RStudio and you will all also be using R, right?)
- Install R and RStudio
- Install pandoc
- (If you're way ahead and twiddling your thumbs, install R and RStudio)
- (Remind me to discuss the whole Python 2 vs Python 3 briefly here.)
