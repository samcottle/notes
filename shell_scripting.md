# Shell scripting

A _shell script_ is a file containing a series of commands. The shell reads the file, and executes the commands in it as if they were being entered directly into the command line.

To create and run a shell script, you need to:

1. Write the script.
2. Make it executable (in other words, set the file permissions to make it executable).
3. Put it somewhere that the shell can find it (i.e. in a folder where it can be executed).

## Example: Hello world

The following is a really basic "Hello World!" example.

### Step 1: Write the script

Create a file called `hello_world` using the command `touch hello_world`, and open the file in a text editor. For example, `nano hello_world`.

Edit the file, and include:

```bash
#!/bin/bash

# This is our first script.

echo "Hello World!"
```

When run, this script will `echo` the string _Hello World!_ in the terminal.

Save the file.

### Step 2: Make it executable

Make the script executable with `chmod 755 hello_world` (this will make it so that anyone can execute it, or use `chmod 700 hello_world` to make the owner the only person that can execute it).

### Step 3: Put it somewhere the shell can find it

If you are in the same folder as the script, and you have _execute_ permissions, you will be able to execute the script with `./hello_world`.

If you are in any other directory, you will need to specify an explicit path to the script (otherwise you will get a **command not found** error).

Alternatively, to make the script accessible from anywhere, we can add the script to one of the default directories that the system checks in for executables (`/usr/bin`, for example - you can get a list of directories with `echo $PATH`).
