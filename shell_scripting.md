# Shell scripting

A _shell script_ is a file containing a series of commands. The shell reads the file, and executes the commands in it as if they were being entered directly into the command line.

To create and run a shell script, you need to:

1. Write the script.
2. Make it executable (in other words, set the file permissions to allow this).
3. Put it somewhere that the shell can find it (i.e. in a folder where it can be executed).

## Example: Hello world

The following is a basic "Hello World!" example.

### Step 1: Write the script

Create a file called `hello_world` using the command `touch hello_world`, and open the file in a text editor. For example, `nano hello_world`.

Edit the file, and include:

```bash
#!/bin/bash

# This is our first script.

echo "Hello World!"
```

When run, this script will `echo` (i.e. print or log) the string _Hello World!_ in the terminal.

Save the file.

### Step 2: Make it executable

Make the script executable with `chmod 755 hello_world` (this will make it so that anyone can execute it, or use `chmod 700 hello_world` to make the owner the only person that can execute it).

### Step 3: Put it somewhere the shell can find it

If you are in the same folder as the script, and you have _execute_ permissions, you will be able to execute the script with `./hello_world`.

If you are in any other directory, you will need to specify an explicit path to the script (otherwise you will get a **command not found** error).

Alternatively, to make the script accessible from anywhere, add the script to one of the default directories that the system checks in for executables (`/usr/local/bin`, for example; you can get a list of these directories using the command `echo $PATH`):

```bash
$ mv hello_world /usr/local/bin
$ hello_world
Hello World!
```

Scripts you've created yourself should live in the `/usr/local/bin` directory (or `/usr/local/sbin` if you're a system administrator). The directories `/bin` and `/usr/bin` are often reserved for binaries that are pre-installed on your operating system (as per the Linux Filesystem Hierarchy Standard).

## Using variables can constants

Bash constants use the format `$CONSTANT`, and variables use the format `$variable`. This is how they are declared in shell scripts:

```bash
CONSTANT="A constant is declared like this."
variable="A variable is declared like this."
```

You can also declare a variable within a variable (or a constant within a constant):

```bash
#!/bin/bash

# Program for outputting system information to HTML file

TITLE="System report for $HOSTNAME"
CURRENT_TIME=$(date +"%x %r %Z")
TIME_STAMP="Generated $CURRENT_TIME, by $USER"

echo "<HTML>
    <HEAD>
        <TITLE>$TITLE</TITLE>
    </HEAD>
    <BODY>
        <H1>$TITLE</H1>
        <P>$TIME_STAMP</P>
    </BODY>
</HTML>"
```

In this case, `$HOSTNAME` and `$USER` are _Bash variables_; these are provided by your system, so don't need to declared explicitly in the script. A list of Bash variables can be found in the [Bash manual](https://www.gnu.org/software/bash/manual/html_node/Bash-Variables.html).

Variables can be assigned in the formats:

```bash
a=b
c="String"
d="A string and a $variable"

# The result of a command
e=$(ls -la)

# Mathematical expansion
f=((4 * 2))

# Escape sequences, such as tabs and new lines
g="\t\Tabbed content\n"

# Multiple variables can occupy the same line
h="The first variable is " i=42
```

## Best practices

To make a shell script easier to maintain, the following practices are recommended.

### Use long option commands

Many commands can be expressed as both short and long options. For example, `ls -a` can also be expressed as `ls --all`; the result is identical for both.

While it is quicker to use a short option when working directly in the shell, using the long option is easier to read when looking at a shell script.

### Variables and constants

Bash constants use the format `$CONSTANT`, and variables use the format `$variable`.

Curly braces can optionally be used to make them visually stand out in a script, or to ensure the shell interprets the script correctly:

```bash
# The following would not work
mv $file $file1

# The following would
mv $file ${file}1

# This is because the shell is interpreting the 1 as part of the variable name
```

### Indentation and formatting

When working with script that are long or contain conditionals (e.g. `-and`, -`or`, `-not`), indentation and formatting can help make the script easier to read.

For example, the command to find all the files and subdirectories in a directory with secure permissions (i.e. not `0600` and `0700`) can be expressed like this:

```bash
$ find ~ \(-type f -not -perm 0600 \) -or \( -type d -not -perm 0700 \)
```

This command can also be expressed so that it's more readable:

```bash
find ~ \
    \( \
        -type f \
        -not -perm 0600 \
    \) \
    -or
    \( \
        -type d \
        -not -perm 0700  donates the end of a line.\
    \)
```

Double, triple, or tab-spaces can be used (depending on the style guide being followed).

The end of each line can be denoted with a `\`.
