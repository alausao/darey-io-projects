# Bash Shell Scripting: Bourne Again Shell

## What is BASH?

BASH is an acronym for Bourne Again Shell, a punning name, which is a tribute to Bourne Shell (i.e., invented by Steven Bourne). Bash is a shell program written by Brian Fox as an upgraded version of Bourne Shell program `'sh'`. It is an open source GNU project. It was released in 1989 as one of the most popular shell distribution of GNU/Linux operating systems. It provides functional improvements over Bourne Shell for both programming and interactive uses. 

It includes command line editing, key bindings, command history with unlimited size, etc. In basic terms, Bash is a command line interpreter that typically runs in a text window where user can interpret commands to carry out various actions. The combination of these commands as a series within a file is known as a Shell Script. Bash can read and execute the commands from a Shell Script.

## Before You Begin 🚀

Before learning Bash Shell, you must have the basic knowledge of the Linux Operating System. Although this tutorial is designed to help beginners and professionals.

### Now have a look at what a Shell is known for.

**Shell**: A UNIX Shell is a program or a command line interpreter that interprets the user commands which are either entered by the user directly or which can be read from a file (i.e., Shall Script), and then pass them to the operating system for processing. It is important to note that Shall scripts are interpreted and not compiled, as the computer system interprets them and there is not any need to compile Shell Scripts in order of execution.

There are different types of shells available in Linux Operating Systems. Some of which are as follows:

1. Bourne Shell
2. C shell
3. Korn Shell
4. GNU Bourne Shell

To know, which shell types your operating system supports, type the command into the terminal as given below:

```
cat /etc/shells
```

**`output`**
```
# /etc/shells: valid login shells
/bin/sh
/bin/bash
/usr/bin/bash
/bin/rbash
/usr/bin/rbash
/usr/bin/sh
/bin/dash
/usr/bin/dash
/usr/bin/tmux
/usr/bin/screen
```

## Let's look a bit of History

    Previously, most of the software in the UNIX world was proprietary and closed source. UNIX system was also not open-sourced for which, you had to use a shell. There was a shell existed at that time named by "Bourne Shell" under the /bin/sh command which was proprietary and closed source. Bourne named after its inventor- Steven Bourne.
    Richard Stallman at that time began GNU project with Free Software Foundation (FSF) to create a UNIX-compatible operating system aiming everything as open-source. There was a lack of progress in the revolution. He needed a free shell that could run existing shell scripts. It was imperative to a completely open-source system built as one of the few projects he funded with FSF. Then on January 110, 1988, Brian Fox (FSF employee) began coding on Bash and released Bash as beta, version 0.99 on June 8, 1989.
    Brian Fox remained in FSF as the primary Bash maintainer till 1993. Then he laid off from FSF, and Chet Ramey (earlier contributor in FSF) got his responsibility.
    Further, on December 23, 1996, Chet Ramey released another bash version 2.0 for the public with a range of new features over the old bash version.
    And now Chet Ramey is known for the official bash maintainer, and he continues to make further enhancements in bash.




