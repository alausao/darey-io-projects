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

```bash
cat /etc/shells
```

**`output`**
```bash
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

```bash
Tue Sep 26 13:34:01 UTC 2023
```

The basic concept of a shell script is a list of commands, which are listed in the order of execution. A good shell script will have comments, preceded by `#` sign, describing the steps. There are conditional tests, such as value A is greater than value B, loops allowing us to go through massive amounts of data, files to read and store data, and variables to read and store data, and the script may include functions.

Assume we create a `test.sh` script. Note all the scripts would have the `.sh` extension. Before you add anything else to your script, you need to alert the system that a shell script is being started. This is done using the `shebang` construct. For example

```bash
#!/bin/sh
```
This tells the system that the commands that follow are to be executed by the Bourne shell. It's called a shebang because the `#` symbol is called a `hash`, and the `!` symbol is called a `bang`

To create a script containing these commands, you put the shebang line first and then add the commands

```bash
#!/bin/bash
pwd
ls
```
### Shell Comments

You can put your comments in your script as follows
```bash
#!/bin/bash

# Author : OLUWASEUN
# Copyright (c) darey.io
# Script follows here:
pwd
ls
```

Save the above content and make the script executable.

```bash
chmod +x test.sh
```
The shell script is now ready to be executed
```bash
./test.sh
```
Upon execution, you will receive the following result
```bash
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
```bash
_ALI
TOKEN_A
VAR_1
VAR_2
```
Following are the examples of invalid variable names:
```bash
2_VAR
-VARIABLE
VAR1-VAR2
VAR_A!
```
The reason you cannot use other characters such as `!`, `*`, or `-` is that these characters have a special meaning for the shell.

### Defining Variables

Variables are defined as follows:
```bash
variable_name=variable_value
```
For example:
```bash
NAME="DevOps"
```
The above example defines the variable `NAME` and assigns the value `"DevOps"` to it.

### Accessing Values

To access the value stored in a variable, prefix its name with the dollar sign `($)`
```bash
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

```bash
echo $$
```
The above command writes the `PID` of the current shell
```bash
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
```bash
NAME01="Zara"
NAME02="Qadir"
NAME03="Mahnaz"
NAME04="Ayan"
NAME05="Daisy"
```
We can use a single array to store all the above mentioned names. Following is the simplest method of creating an array variable. This helps assign a value to one of its indices.
```bash
array_name[index]=value
```
Here array_name is the name of the array, index is the index of the item in the array that you want to set, and value is the value you want to set for that item. As an example, the following commands:
```bash
NAME[0]="Zara"
NAME[1]="Qadir"
NAME[2]="Mahnaz"
NAME[3]="Ayan"
NAME[4]="Daisy"
```

If you are using the `bash` shell, here is the syntax of array initialization:
```bash
array_name=(value1 ... valuen)
```
### Accessing Array Values

After you have set any array variable, you access it as follows:
```bash
${array_name[index]}
```
Here array_name is the name of the array, and index is the index of the value to be accessed. Following is an example to understand the concept:
```bash
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
```bash
First Index: Zara
Second Index: Qadir
```
You can access all the items in an array in one of the following ways:
```bash
${array_name[*]}
${array_name[@]}
```
Here array_name is the name of the array you are interested in. Following example will help you understand the concept:
```bash
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
```bash
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

Bourne shell didn't originally have any mechanism to perform simple arithmetic operations but it uses external programs, either `awk` or `expr`

The following example shows how to add two numbers:
```bash
#!/bin/sh

val=`expr 2 + 2`
echo "Total value : $val"
```
The above script will generate the following result:
```bash
Total value : 4
```
The following points need to be considered while adding:

There must be spaces between operators and expressions. For example, `2+2` is not correct; it should be written as `2 + 2`. The complete expression should be enclosed between `‘ ‘`, called the `backtick`.

### Arithmetic Operators

The following arithmetic operators are supported by Bourne Shell:

Assume variable a holds **`10`** and variable b holds **`20`** then

| Operator      | Description                           | Example                         |
| --------------| --------------------------------------| --------------------------------|
|**`+`** (Addition)|Adds values on either side of the operator| `expr $a + $b` will give 30|
|**`-`** (Subtraction)|Subtracts right hand operand from left hand operand|`expr $a - $b` will give -10|
|**`*`** (Multiplication)|Multiplies values on either side of the operator|`expr $a * $b` will give 200|
|**`/`** (Division)|Divides left hand operand by right hand operand|`expr $b / $a` will give 2|
|**`%`** (Modulus)|Divides left hand operand by right hand operand and returns remainder|`expr $b % $a` will give 0|
|**`=`** (Assignment)|Assigns right operand in left operand|`a = $b` would assign value of b into a|
|**`==`** (Equality)|Compares two numbers, if both are the same then returns true|`[ $a == $b ]` would return false|
|**`!=`** (Not Equality)|Compares two numbers, if both are different then returns true|`[ $a != $b ]` would return true.|

### Relational Operators

Bourne Shell supports the following relational operators that are specific to numeric values. These operators do not work for string values unless their value is numeric.

For example, following operators will work to check a relation between `10` and `20` as well as in between `"10"` and `"20"` but not in between `"ten"` and `"twenty"`.

Assume variable `a` holds **`10`** and variable `b` holds **`20`** then:

| Operator      | Description                           | Example                         |
| --------------| --------------------------------------| --------------------------------|
|**`-eq`**|Checks if the value of two operands are equal; if yes, then the condition becomes true| `[ $a -eq $b ]` is not true.|
|**`-ne`**|Checks if the value of two operands are not equal; if values are not equal, then the condition becomes true.|`[ $a -ne $b ]` is true.|
|**`-gt`**|Checks if the value of the left operand is greater than the value of the right operand; if yes, then the condition becomes true.|`[ $a -gt $b ]` is not true.|
|**`-lt`**|Checks if the value of the left operand is less than the value of the right operand; if yes, then the condition becomes true.|`[ $a -lt $b ]` is true.|
|**`-ge`**|Checks if the value of the left operand is greater than or equal to the value of the right operand; if yes, then the condition becomes true.|`[ $a -ge $b ]` is not true.|
|**`-le`**|Checks if the value of the left operand is less than or equal to the value of the right operand; if yes, then the condition becomes true.|`[ $a -le $b ]` is true.|

### Boolean Operators

The following Boolean operators are supported by the Bourne Shell.

Assume variable `a` holds `10` and variable `b` holds `20` then:

| Operator      | Description                           | Example                         |
| --------------| --------------------------------------| --------------------------------|
|**`!`**|This is logical negation. This inverts a true condition into false and vice versa.| `[ ! false ]` is true.|
|**`-o`**|This is logical OR. If one of the operands is true, then the condition becomes true.|`[ $a -lt 20 -o $b -gt 100 ]` is true.|
|**`-a`**|This is logical AND. If both operands are true, then the condition becomes true; otherwise, it is false.|`[ $a -lt 20 -a $b -gt 100 ]` is false.|

### String Operators

The following string operators are supported by Bourne Shell.

Assume variable `a` holds `"abc"` and variable `b` holds `"efg"` then:

| Operator      | Description                           | Example                         |
| --------------| --------------------------------------| --------------------------------|
|**`=`**|Checks if the value of two operands are equal; if yes, then the condition becomes true.| `[ $a = $b ]` is not true.|
|**`!=`**|Checks if the value of two operands are not equal; if values are not equal, then the condition becomes true.|`[ $a != $b ]` is true.|
|**`-z`**|Checks if the given string operand size is zero; if it is zero length, then it returns true.|`[ -z $a ]` is not true.|
|**`-n`**|Checks if the given string operand size is non-zero; if it is non-zero length, then it returns true.|`[ -n $a ]` is not false.|
|**`str`**|Checks if `str` is not an empty string; if it is empty, then it returns false.|`[ $a ]` is not false.|

## Shell Decision Making

Let us understand shell decision-making in Unix. While writing a shell script, there may be a situation when you need to adopt one path out of the given two paths. So you need to make use of conditional statements that allow your program to make correct decisions and perform the right actions.

Unix Shell supports conditional statements which are used to perform different actions based on different conditions. We will now understand two decision-making statements here:
```
if....else statement
```

### The if...else statements

If else statements are useful decision-making statements which can be used to select an option from a given set of options.

Unix Shell supports following forms of **`if…else`** statement

    if...fi statement
    if...else...fi statement
    if...elif...else...fi statement

Most of the if statements check relations using relational operators discussed in the previous section.

**Example 1**
```bash
#!/bin/bash

# Prompt the user for their age
echo "Please enter your age:"
read age

# Check if the age is greater than or equal to 18
if [ "$age" -ge 18 ]; then
  echo "You are an adult."
else
  echo "You are a minor."
fi
```
**Example 2**
```bash
#!/bin/bash

# Prompt the user to enter two numbers
echo "Please enter the first number:"
read num1
echo "Please enter the second number:"
read num2

# Check if num1 is greater than num2
if ((num1 > num2)); then
  echo "$num1 is greater than $num2."
elif ((num1 < num2)); then
  echo "$num1 is less than $num2."
else
  echo "$num1 is equal to $num2."
fi
```

## Shell Loop Types

A loop is a powerful programming tool that enables you to execute a set of commands repeatedly. In this section, we will examine the `for` and `while` loops available to shell programmers

In Bash scripting, a `for` loop is used to iterate over a list of items, such as elements in an array, files in a directory, or a sequence of numbers. The loop will execute a specified set of commands for each item in the list. Here's the basic syntax of a `for` loop in Bash:

**`Syntax:`**
```bash
for item in list
do
    # Commands to be executed for each item
done
```
Here's an example of a `for` loop that iterates over a list of numbers and prints each number:
```bash
#!/bin/bash

# Define a list of numbers
numbers=(1 2 3 4 5)

# Iterate over each number in the list
for num in "${numbers[@]}"
do
    echo "Number: $num"
done
```
**`The output of this script will be:`**
```bash
Number: 1
Number: 2
Number: 3
Number: 4
Number: 5
```
You can use `for` loops in Bash to automate tasks that involve iterating over a set of items, like processing files, generating sequences, or performing repetitive actions on a list of elements.

#### While loop

A `while` loop in Bash is used to repeatedly execute a block of commands as long as a specified condition is true. It continues execution until the condition becomes false. If the condition is initially false, the loop's commands may never execute.

**`Syntax:`**
```bash
while [condition]
do
    # Commands to be executed as long as the condition is true
done
```

**`Example of a while Loop:`**
```bash
#!/bin/bash

# Initialize a counter
count=1

# Define the condition (loop until count is less than or equal to 5)
while [ "$count" -le 5 ]
do
    echo "Count: $count"
    ((count++))  # Increment the counter
done
```

**`The output of this script will be:`**
```bash
Count: 1
Count: 2
Count: 3
Count: 4
Count: 5
```
## Command Substitution in BASH

**Command substitution** in Bash scripting is a mechanism that allows you to capture the output of a command and use it as part of another command or assign it to a variable. It provides a way to dynamically incorporate the results of one command into another.

There are two common ways to perform command substitution in Bash:

1. **Using Backticks `(``)`** You can enclose the command you want to execute within backticks (`` ` ``) to capture its output. For example:

    ```bash
    current_date=`date`
    echo "The current date is: $current_date"
    ```

   Here, the `date` command is executed, and its output (the current date and time) is stored in the `current_date` variable.

2. **Using `$()` (dollar-parentheses):** You can also use the `$()` syntax to achieve command substitution. It has the advantage of being more readable and allows for nesting. For example:

    ```bash
    current_date=$(date)
    echo "The current date is: $current_date"
    ```

   This accomplishes the same result as the previous example but with a more modern and preferred syntax.

Command substitution is useful when you need to use the result of one command as an argument or parameter for another command, or when you want to store the output of a command in a variable for further processing within your script.

**Example 1**
```bash
#!/bin/bash

# Capture the current username using the `whoami` command
current_user=`whoami`

# Print a greeting message with the captured username
echo "Hello, $current_user! You are currently logged in as $(whoami)."
```
**`output`**
```bash
Hello, root! You are currently logged in as root
```
**Example 2**
```bash
#!/bin/bash

# Calculate the square of a number using command substitution
number=5
square=$(echo "$number * $number" | bc)

# Print the result
echo "The square of $number is $square."
```
**`output`**
```bash
The square of 5 is 25.
```
## Variable Substitution in Bash

Variable substitution in Bash scripting allows you to replace a variable with its value. Bash provides several methods for variable substitution, making it flexible for incorporating variable values into strings or commands.

### 1. Basic Variable Substitution

You can access the value of a variable by prefixing the variable name with a dollar sign (`$`). For example, if `name="Alice"`, then `$name` will be replaced with "Alice" in your script.

### 2. String Concatenation

Variables can be concatenated with strings using the `${}` syntax. For example, `${name}'s birthday is on ${birthdate}` allows you to create a string with variable values.

### 3. Default Value

You can provide a default value for a variable using `${variable:-default}`. If `variable` is not set or is null, it will use the `default` value. For example, `${city:-Unknown}` will use "Unknown" if `city` is not defined.

### 4. Null or Unset Check

You can check if a variable is unset or null using `${variable}`. If it's null or unset, this expression evaluates to an empty string.

**Example 1: Basic Variable Substitution:**

```bash
#!/bin/bash

# Define a variable
name="Alice"

# Use variable substitution to greet the user
echo "Hello, $name! Welcome to our website."
```
In this script, we use basic variable substitution to include the value of the `name` variable within a greeting message.

**Example 2: Default Value and Null Check:**

```bash
#!/bin/bash

# Check if a variable is set or provide a default value
city="New York"
echo "You are from \${city:-Unknown}"

# Check if an unset variable is set or provide a default value
unset country
echo "You are from \${country:-Unknown}"
```
In this script, we demonstrate both default value and null/unset variable checks. We use `\${city:-Unknown}` to check if the `city` variable is set, and if not, it defaults to "Unknown." Similarly, `\${country:-Unknown}` checks for an unset variable and provides a default value of "Unknown."

## Quoting in Shell Scripting

Quoting is an essential concept in shell scripting that allows you to control how the shell interprets special characters and spaces within strings. It ensures that text is treated as literal and prevents unexpected behavior in commands. There are three primary types of quoting in shell scripting: single quotes, double quotes, and backslashes.

### 1. Single Quotes (`'`)

- Enclosed within single quotes, all characters are treated as literal, and no variable or command substitution takes place.

**Example:**
```bash
#!/bin/bash
USER="Alice"
message='Hello $USER'
echo "$message"  # Output: Hello $USER
```
### 2. Double Quotes (`"`)
- Double quotes allow variable and command substitution to occur within the string, while still preserving spaces and most special characters.

**Example:**
```bash
#!/bin/bash

name="Alice"
greeting="Hello, $name!"
echo "$greeting"  # Output: Hello, Alice!
```
### 3. Backslashes (`\`)

- Backslashes are used to escape special characters within double-quoted strings, preventing their interpretation as commands or special characters.

**Example:**
```bash
#!/bin/bash

echo "This is a \"quote\" inside double quotes."  # Output: This is a "quote" inside double quotes.
```
Quoting is a fundamental aspect of shell scripting that allows you to control how the shell interprets and processes strings. Whether you need to preserve spaces, include variables, or escape special characters, using the appropriate quoting style is crucial for writing robust and reliable shell scripts.

## Input and Output Redirection in Shell Scripting

Input and output redirection are powerful features in shell scripting that allow you to control where data comes from and where it goes. You can use various symbols and commands to redirect standard input, standard output, and standard error.

### Redirection Symbols

- `<`: Redirects standard input (stdin) from a file.
- `>`: Redirects standard output (stdout) to a file, overwriting the file if it exists.
- `>>`: Redirects standard output (stdout) to a file, appending the output to the file if it exists.
- `2>`: Redirects standard error (stderr) to a file.
- `2>>`: Redirects standard error (stderr) to a file, appending the error to the file if it exists.
- `&>` or `2>&1`: Redirects both standard output and standard error to the same location.

**Example 1: Output Redirection (`>` and `>>`)**

```bash
#!/bin/bash

# Redirect stdout to a file (overwrite if exists)
echo "This is standard output." > output.txt

# Append stdout to the same file
echo "This is additional output." >> output.txt

# Redirect stderr to a file (overwrite if exists)
echo "This is standard error." 2> error.txt

# Append stderr to the same file
echo "This is additional error." 2>> error.txt
```
In this script, we demonstrate output redirection using `>` and `>>`. It redirects both standard output and standard error to separate files, overwriting or appending as needed.

**Example 2: Input Redirection (`<`)**

```bash
#!/bin/bash

# Redirect stdin from a file
while read line; do
    echo "Line read from file: $line"
done < input.txt
```
In this script, we redirect standard input (`stdin`) from a file named `input.txt`. The `while` loop reads each line from the file and processes it, demonstrating input redirection. Input and output redirection are essential for controlling the flow of data in shell scripts. They allow you to work with files, handle errors, and process input efficiently, making your scripts more versatile and powerful.

## **💡Side Hustle Task ⏰**

### Summarize the Bash Script Below
```shell
#!/bin/bash

source_file="example.txt"
backup_dir="backup"
log_file="backup.log"

if [ ! -e "$source_file" ]; then
    echo "Error: The source file '$source_file' does not exist."
    exit 1
fi

if [ ! -d "$backup_dir" ]; then
    mkdir -p "$backup_dir"
fi

timestamp=$(date +"%Y%m%d%H%M%S")

echo "Compressing '$source_file'..."
tar -czf "$backup_dir/backup_$timestamp.tar.gz" "$source_file" > "$log_file" 2>&1

if [ $? -eq 0 ]; then
    echo "Backup successful. Compressed file created: 'backup_$timestamp.tar.gz'"
else
    echo "Error: Backup failed. See '$log_file' for details."
fi
```