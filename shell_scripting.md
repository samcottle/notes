# Shell scripting

A _shell script_ is a file containing a series of commands. The shell reads the file, and executes the commands in it as if they were being entered directly into the command line.

To create and run a shell script, you need to:

1. Write the script.
2. Make it executable (in other words, set the file permissions to make it executable).
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
$ mv hello_world /usr/bin
$ hello_world
Hello World!
```

Scripts you've created yourself should live in the `/usr/local/bin` directory (or `/usr/local/sbin` if you're a system administrator). The directories `/bin` and `/usr/bin` are often reserved for binaries that are pre-installed on your operating system (as per the Linux Filesystem Hierarchy Standard).

## Best practices

To make a shell script easier to maintain, the following are recommended.

### Use long option commands

Many commands can be expressed as both short and long options. For example, `ls -a` can also be expressed as `ls --all`; the result is identical for both.

While it is quicker to use a short option when working directly in the shell, using the long option is easier to read when looking at a shell script.

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
        -not -perm 0700 \
    \)
```

To indent a shell script, tab-spaces can also be used (depending on which style guide is being followed), and a `\` donates the end of a line.
