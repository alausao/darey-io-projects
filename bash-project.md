# Bash Shell Scripting: Bourne Again Shell

## What is BASH?

BASH is an acronym for Bourne Again Shell, a punning name, which is a tribute to Bourne Shell (i.e., invented by Steven Bourne). Bash is a shell program written by Brian Fox as an upgraded version of Bourne Shell program `'sh'`. It is an open source GNU project. It was released in 1989 as one of the most popular shell distribution of GNU/Linux operating systems. It provides functional improvements over Bourne Shell for both programming and interactive uses. 

It includes command line editing, key bindings, command history with unlimited size, etc. In basic terms, Bash is a command line interpreter that typically runs in a text window where user can interpret commands to carry out various actions. The combination of these commands as a series within a file is known as a Shell Script. Bash can read and execute the commands from a Shell Script.

## Before You Begin 🚀

Before learning Bash Shell, you must have the basic knowledge of the Linux Operating System. Although this tutorial is designed to help beginners and professionals.

### Let's Understand Shell itself.

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

## Let's take a look at BASH History

    Previously, most of the software in the UNIX world was proprietary and closed source. UNIX system was also not open-sourced for which, you had to use a shell. There was a shell existed at that time named by "Bourne Shell" under the /bin/sh command which was proprietary and closed source. Bourne named after its inventor- Steven Bourne.
    Richard Stallman at that time began GNU project with Free Software Foundation (FSF) to create a UNIX-compatible operating system aiming everything as open-source. There was a lack of progress in the revolution. He needed a free shell that could run existing shell scripts. It was imperative to a completely open-source system built as one of the few projects he funded with FSF. Then on January 110, 1988, Brian Fox (FSF employee) began coding on Bash and released Bash as beta, version 0.99 on June 8, 1989.
    Brian Fox remained in FSF as the primary Bash maintainer till 1993. Then he laid off from FSF, and Chet Ramey (earlier contributor in FSF) got his responsibility.
    Further, on December 23, 1996, Chet Ramey released another bash version 2.0 for the public with a range of new features over the old bash version.
    And now Chet Ramey is known for the official bash maintainer, and he continues to make further enhancements in bash.

### Shell Prompt

The prompt, `$`, which is called the `command prompt`, is issued by the shell. While the prompt is displayed, you can type a command. Shell reads your input after you press `Enter`. It determines the command you want executed by looking at the first word of your input. A word is an unbroken set of characters. Spaces and tabs separate words. Following is a simple example of the `date` command, which displays the current date and time −

```
Tue Sep 26 13:34:01 UTC 2023
```

The basic concept of a shell script is a list of commands, which are listed in the order of execution. A good shell script will have comments, preceded by `#` sign, describing the steps. There are conditional tests, such as value A is greater than value B, loops allowing us to go through massive amounts of data, files to read and store data, and variables to read and store data, and the script may include functions.

Assume we create a `test.sh` script. Note all the scripts would have the `.sh` extension. Before you add anything else to your script, you need to alert the system that a shell script is being started. This is done using the `shebang` construct. For example

```
#!/bin/sh
```
This tells the system that the commands that follow are to be executed by the Bourne shell. It's called a shebang because the `#` symbol is called a `hash`, and the `!` symbol is called a `bang`

To create a script containing these commands, you put the shebang line first and then add the commands

```
#!/bin/bash
pwd
ls
```
### Shell Comments

You can put your comments in your script as follows
```
#!/bin/bash

# Author : OLUWASEUN
# Copyright (c) darey.io
# Script follows here:
pwd
ls
```

Save the above content and make the script executable.

```
chmod +x test.sh
```
The shell script is now ready to be executed
```
./test.sh
```
Upon execution, you will receive the following result
```
/root
health.sh 
```
**Note** − To execute a program available in the current directory, use `./program_name`

## Using Shell Variables

A variable is a character string to which we assign a value. The value assigned could be a number, text, filename, device, or any other type of data. A variable is nothing more than a pointer to the actual data. The shell enables you to create, assign, and delete variables.

### Variable Names

The name of a variable can contain only letters (a to z or A to Z), numbers ( 0 to 9) or the underscore character ( _).

By convention, Unix shell variables will have their names in UPPERCASE.

The following examples are valid variable names:
```
_ALI
TOKEN_A
VAR_1
VAR_2
```
Following are the examples of invalid variable names:
```
2_VAR
-VARIABLE
VAR1-VAR2
VAR_A!
```
The reason you cannot use other characters such as `!`, `*`, or `-` is that these characters have a special meaning for the shell.

### Defining Variables

Variables are defined as follows:
```
variable_name=variable_value
```
For example:
```
NAME="DevOps"
```
The above example defines the variable `NAME` and assigns the value `"DevOps"` to it.

### Accessing Values

To access the value stored in a variable, prefix its name with the dollar sign `($)`
```
echo $NAME
DevOps
```

### Variable Types

- Local Variables − A local variable is a variable that is present within the current instance of the shell. It is not available to programs that are started by the shell. They are set at the command prompt.

- Environment Variables − An environment variable is available to any child process of the shell. Some programs need environment variables in order to function correctly. Usually, a shell script defines only those environment variables that are needed by the programs that it runs.

- Shell Variables − A shell variable is a special variable that is set by the shell and is required by the shell in order to function correctly. Some of these variables are environment variables whereas others are local variables.

### Let's discuss Special Variable

We will discuss in detail about special variable in Unix. Before now we understood how to be careful when we use certain nonalphanumeric characters in variable names. This is because those characters are used in the names of special Unix variables. These variables are reserved for specific functions.

For example, the `$` character represents the `process ID number`, or `PID`, of the current shell.

```
echo $$
```
The above command writes the `PID` of the current shell
```
969
```
| No. | Variable & Description                                  |
| --- | -------------------------------------------------------- |
| 1.  | `$0` - The filename of the current script.                |
| 2.  | `$n` - These variables correspond to the arguments with   |
|     |       which a script was invoked. Here, `n` is a positive |
|     |       decimal number corresponding to the position of an |
|     |       argument (the first argument is `$1`, the second   |
|     |       argument is `$2`, and so on).                       |
| 3.  | `$#` - The number of arguments supplied to a script.    |
| 4.  | `$*` - All the arguments are double quoted. If a script |
|     |        receives two arguments, `$*` is equivalent to `$1` `$2` |
| 5.  | `$@` - All the arguments are individually double quoted. |
|     |        If a script receives two arguments, `$@` |
|     |        is equivalent to `$1` `$2.`|
| 6.  | `$?` - The exit status of the last command executed. |
| 7.  | `$$` - The process number of the current shell. For shell scripts, | 
|     |        this is the process ID under which they are executing. |
| 8.  | `$!` - The process number of the last background command. |

### Exit Status

The `$?` variable represents the exit status of the previous command. Exit status is a numerical value returned by every command upon its completion. As a rule, most commands return an exit status of `0` if they were successful, and `1` if they were unsuccessful.

## Defining Array Values

Shell supports a different type of variable called an **array variable**. This can hold multiple values at the same time. Arrays provide a method of grouping a set of variables. Instead of creating a new name for each variable that is required, you can use a single array variable that stores all the other variables.

Suppose you are trying to represent the names of various students as a set of variables. Each of the individual variables is a scalar variable as follows:
```
NAME01="Zara"
NAME02="Qadir"
NAME03="Mahnaz"
NAME04="Ayan"
NAME05="Daisy"
```
We can use a single array to store all the above mentioned names. Following is the simplest method of creating an array variable. This helps assign a value to one of its indices.
```
array_name[index]=value
```
Here array_name is the name of the array, index is the index of the item in the array that you want to set, and value is the value you want to set for that item. As an example, the following commands:
```
NAME[0]="Zara"
NAME[1]="Qadir"
NAME[2]="Mahnaz"
NAME[3]="Ayan"
NAME[4]="Daisy"
```

If you are using the `bash` shell, here is the syntax of array initialization:
```
array_name=(value1 ... valuen)
```
### Accessing Array Values

After you have set any array variable, you access it as follows:
```
${array_name[index]}
```
Here array_name is the name of the array, and index is the index of the value to be accessed. Following is an example to understand the concept:
```
#!/bin/sh

NAME[0]="Zara"
NAME[1]="Qadir"
NAME[2]="Mahnaz"
NAME[3]="Ayan"
NAME[4]="Daisy"
echo "First Index: ${NAME[0]}"
echo "Second Index: ${NAME[1]}"
```

The above example will generate the following result:
```
First Index: Zara
Second Index: Qadir
```
You can access all the items in an array in one of the following ways:
```
${array_name[*]}
${array_name[@]}
```
Here array_name is the name of the array you are interested in. Following example will help you understand the concept:
```
#!/bin/sh

NAME[0]="Zara"
NAME[1]="Qadir"
NAME[2]="Mahnaz"
NAME[3]="Ayan"
NAME[4]="Daisy"
echo "First Method: ${NAME[*]}"
echo "Second Method: ${NAME[@]}"
```
The above example will generate the following result:
```
First Method: Zara Qadir Mahnaz Ayan Daisy
Second Method: Zara Qadir Mahnaz Ayan Daisy
```

## Shell Basic Operators

There are various operators supported by each shell. We will discuss in detail about Bourne shell (default shell) in this section.

The following operators will be discussed:

1. Arithmetic Operators
2. Relational Operators
3. Boolean Operators
4. String Operators
5. File Test Operators

Bourne shell didn't originally have any mechanism to perform simple arithmetic operations but it uses external programs, either `awk` or `expr`

The following example shows how to add two numbers:
```
#!/bin/sh

val=`expr 2 + 2`
echo "Total value : $val"
```
The above script will generate the following result:
```
Total value : 4
```
The following points need to be considered while adding:

There must be spaces between operators and expressions. For example, `2+2` is not correct; it should be written as `2 + 2`. The complete expression should be enclosed between `‘ ‘`, called the `backtick`.

### Arithmetic Operators

The following arithmetic operators are supported by Bourne Shell:

Assume variable a holds `**10**` and variable b holds `**20**` then

| Operator      | Description                           | Example                         |
| --------------| --------------------------------------| --------------------------------|
|+ (Addition)|Adds values on either side of the operator| `expr $a + $b` will give 30|
|- (Subtraction)|Subtracts right hand operand from left hand operand|`expr $a - $b` will give -10|
|* (Multiplication)|Multiplies values on either side of the operator|`expr $a * $b` will give 200|
