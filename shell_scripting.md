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

When run, this script will `echo` (i.e. print) the string _Hello World!_ in the terminal.

Save the file.

### Step 2: Make it executable

Make the script executable with `chmod 755 hello_world` (this will make it so that anyone can execute it, or use `chmod 700 hello_world` to make the owner the only person that can execute it).

### Step 3: Put it somewhere the shell can find it

If you are in the same folder as the script, you will be able to execute the script with:

```bash
$ ./hello_world
Hello World!
```

If you are in another directory, you will need to specify the explicit path to the script (otherwise you will get the error message `command not found`):

```bash
$ ./home/sam/scripts/hello_world
Hello World!
```

To make the script accessible from anywhere in the filesystem, add the script to a directory that is used for executables (`/usr/local/bin`, for example; you can get a list of these directories using the command `echo $PATH`):

```bash
$ mv hello_world /usr/local/bin
$ hello_world
Hello World!
```

Scripts you've created yourself typically live in the `/usr/local/bin` directory (or `/usr/local/sbin` if you're the system administrator). Don't use `/bin` or `/usr/bin`, as these are reserved for binaries that come pre-installed with your operating system.

## Using variables and constants

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

In this case, `$HOSTNAME` and `$USER` are _Bash variables_; these are provided by your system, so don't need to be declared in the script. A list of Bash variables can be found in the [Bash manual](https://www.gnu.org/software/bash/manual/html_node/Bash-Variables.html).

Ways that variables can be assigned include:

```bash
a=b
c="A string"
d="A string and a $variable"

# The result of a command
e=$(ls -l)

# Mathematical expansion
f=((4 * 2))

# Escape sequences, such as tabs and new lines
g="\t\Tabbed content\n"

# Multiple variables can be assigned on the same line
h="The answer to the ultimate question of life, the universe, and everything is " i=42
```

## Using functions

Shell functions are a good way of breaking a big task into smaller, simpler steps. The use the format:

```bash
function name {
    commands
    return
}
```

The `return` command, used at the end of each function, terminates it and return control to the program.

Functions need to be defined at the beginning of a script, before they are executed in the program:

```bash
#!/bin/bash

# Functions defined here
function steptwo {
    echo "Step 2"
    return
}

function theend {
    echo "End of steps"
    return
}

# Program defined here
echo "Step 1"
steptwo
echo "Step 3"
theend
```

As an example, if we wanted to add some information to our system report with information on the amount of **disk space**, the amount of space in the **home folder**, and the **system uptime**, we could do this using shell functions:

```bash
#!/bin/bash

# Program for outputting system information page

TITLE="System report for $HOSTNAME"
CURRENT_TIME=$(date +"%x %r %Z")
TIME_STAMP="Generated $CURRENT_TIME, by $USER"

report_disk_space () {
    echo "<h2>Disk space used</h2>
    <PRE>$(df --h)</PRE>"
    return
}

report_home_space () {
    echo "<h2>Home space used</h2>
    <PRE>$(df --h /home/*)</PRE>"
    return
}

report_uptime () {
    echo "<h2>System uptime</h2>
    <PRE>$(uptime)</PRE>"
    return
}

echo "<HTML>
    <HEAD>
        <TITLE>$TITLE</TITLE>
    </HEAD>
    <BODY>
        <H1>$TITLE</H1>
        <P>$TIME_STAMP</P>
        $(report_disk_space)
        $(report_home_space)
        $(report_uptime)
    </BODY>
</HTML>"
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
$ find ~ \( -type f -not -perm 0600 \) -or \( -type d -not -perm 0700 \)
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

The end of each line needs to be denoted with a `\`.

### Use stubs

Stubs are text that is added to a shell script as it is being developed, to help the person creating the script how it will run.

For example, if we are writing a program to print a system report, you might want to include a function that checks the disk space. Before you have defined this function in your script, you can use `echo "Running function disk_space"` to understand how the function it will be executed.

```bash
report_disk_space () {
    echo "Running function disk_space."
    return
}
```

Then later replace this with the code that you intend to use:

```bash
report_disk_space () {
    echo"<h2>Disk space used</h2>
    <PRE>$(df -h)</PRE>"
    return
}
```
