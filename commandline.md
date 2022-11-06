# Basic Linux commands

- `cd`: Change the working directory. `cd folder1` would change you to the working directory with the name `folder1`.
- `ls`: List the files in a directory. For more information (such as permissions) on each of the files in the directory, use `ls -l`. To list all files, including hidden files, use `ls -a`.
- `pwd`: Print working directory. Returns the name of the working directory (i.e. the one you're in).
- `file`: Determine the contents of a specified file. `file me.jpg` would return `JPEG image data. JFIF standard 1.01.`, for example.
- `mkdir`: Make a new directory. `mkdir newfolder` would make a new directory called `newfolder`. Can make multiple new directories by specifying more than one after `mkdir`. For example `mkdir newfolder1 newfolder2` would create two new directories: `newfolder1` and `newfolder2`.
- `cp`: Copy a file or folder. `cp file1 file2` would make a copy of `file1` and call it `file2`. `cp file1 /folder1` would make a copy of `file1` in `folder1`.
- `mv`: Move or rename a file. `mv file1 /folder1` moves `file1` to a folder called `folder1`. `mv file1 file2` renames `file1` to `file2`.
- `rm`: Remove a file or directory. `rm file1 file2` deletes `file1` and `file2`. To delete directories, you often need to use `rm -r folder1`, which recursively deletes all the files and subdirectories within it (otherwise you get the error `rm: cannot remove 'folder1': Is a directory`.
- `echo`: Display text. Using wildcards, you could use `echo` to display all files in a folder ending in an _s_ with `echo *s`.
- `clear`: Clears the terminal.
- `history`: Displays a list of recently typed commands (to a maximum of 500).
- `shutdown`: Shut down the computer. `sudo shutdown now` would shutdown the computer immediately (i.e. `now`). To reboot, use `sudo shutdown -r`.

## Common directories

Useful directories within a 'standard' Linux filesystem include:

- `/`: The root directory.
- `/home`: The user's home directory.
- `/bin`: Contains binaries that are needed for the system to run.
- `/boot`: Contains the files needed to boot. Includes `/boot/grub/grub.conf` (the boot loader), and `/boot/vmlinuz` (the Linux kernel).
- `/dev`: Contains a list of all the devices that Linux understands.
- `/etc`: Contains systemwide configuration files and shell scripts. Includes `/etc/crontab` (used for running automated jobs), and `etc/fstab` (the table of strage devices).
- `/lib`: Contains shared library files used by system programs.
- `/media`: Contains mount points for removable media.
- `/mnt`: Contains mount points removable media that were manually mounted. This is typically used on older Linux systems.
- `/opt`: Contains 'optional' software. This is often where commercial software is stored.
- `/root`: The home directory for the `root` account.
- `/sbin`: Contains system binaries, which are used to perform important system tasks. This folder is off limits to anyone but the `superuser`.
- `/tmp`: Contains temporary files. This is often emptied with each reboot.
- `/usr`: Contains all the program and support files availabe to regular users:
  - `/usr/bin`: The binary files available to all regular users.
  - `/usr/local`: The binary files that did not come with the distro.
  - `/usr/sbin`: System binaries.
  - `/usr/share`: Shared data used by the binaries in `/usr/bin`.
  - `/usr/share/doc`: Documentation for the binaries in `/usr/bin`. This is organised by package.
- `/var`: Contains 'various' data. Any data that will likely change, such as databases or mail files.
- `/var/log`: Contains log files of system activity. `/var/log/messages` is probably the most used.

## Finding stuff

There are several commands that can be used for finding files:

- `find`: Finds a file. `find -name myfile.txt` would display the location of all files with the name `myfile.txt`. To find files in a specific folder (such as all `.conf` files in the folder `/etc`), you would use `find /etc -name *.conf`. You can also use find to search for files using other parameters, such as a specific file size range, or have been modified within a certain number of days.
- `whereis`: Finds a binary file. `whereis ls` would display the location of the `ls` command.
- `which`: Finds programs, and prints their location. For example, `which ls` prints `/usr/bin/ls`.

## Logging

- `last`: View history of successful login attempts.
- `lastb`: View history of bad login attempts.

## Getting help

The commands for getting help aren't standardized, but generally speaking you can use the following to find out about a command:

- `help`: Gets help for built-in programs. For help information on how to use the change directory command, you'd use `help cd`.
- `--help`: Gets more info on the syntax of a command. So `mkdir --help` gives you a list of arguments you can use with the `mkdir` command, for example.
- `info`: Gets the programs manual. `info ls` brings up the manual for the `ls` command. This gives you a very similar result to `man`, but more to the point.
- `man`: Gets the programs manual. `man ls` brings up the manual for the `ls` command. This gives you a very similar result to `info`, but with more contextual information. **Note**: For more user-friendly man pages, you can use curl to get online cheat sheets for popular linux commands. For example, `curl cheat.sh/grep` would get you information and examples for the `grep` command.
- `apropos`: Searches for a specific term in installed `man` pages. For example, `apropos archive` will search through all `man` pages for the term "archive", and print a list of results.
- `whatis`: Display a brief description of the command. `whatis ls` Gives you a short description (in this case the description `list directory contents`).

## Viewing files

- `cat`: Very basic text display command. For example, to display the contents of `file.txt` you'd use `cat file.txt`.
- `head`: Displays the first lines of a file. For example, to display the first 5 lines of `file.txt` you'd use `head -5 file.txt`.
- `tail`: Displays the last lines of a file. For example, to display the last 15 lines of `file.txt` you'd use `head -15 file.txt`.
- `nl`: Similar to `cat`, but uses numbered lines. For example, to display the contents of `file.txt` with numbered lines you'd use `nl file.txt`.
- `more`: Displays a file in pages (similar to `man` pages). For example, `more file.txt`.
- `less`: Essentially `more` with _more_ functionality (counter intuitively). For example, `less file.txt`. From here, you can search within the file with the **/** key.
- `grep`: Can be used in combination with other commands to filter the contents of a file. For example, to find all instances of the word `configure` in the file called `settings.conf` you could use `cat settings.conf | grep configure`. Or if you wanted numbered lines you could use `nl settings.conf | grep configure`. To do a case _insensitive_ filter, use the `-i` flag.
- `sed`: Search and replace text in a file. For example, to replace the word `set` with `configure` in the file called `settings.conf` you would use `sed s/set/configure settings.conf`.
- `diff`: Compare differences between two files. To present the results in a more Git-like manner, use the `-u` flag. For example, to compare the differences between the files `Dogs.txt` and `MoreDogs.txt` you would use `diff -u Dogs.txt MoreDogs.txt`.

## Encrypting files

- `openssl -aes-256-cbc -in file.txt -out file.txt.encrypted`: Encrypts `file.txt`.
- `openssl -aes-256-cbc -d -in file.txt.encrypted -out file.txt`: Decrypts `file.txt.encrypted`.

## Downloading files

### `curl`

The `curl` command can be used to download files or data from a host, and POST data to a host:

- `curl example.com/file.zip`: Downloads the file from the location `example.com/file.zip`.
- `curl cheat.sh/curl`: Downloads information from `cheat.sh` on `curl`.
- `curl wttr.in`: Downloads weather information for your location, and prints it in the terminal.
- `curl wttr.in/auckland`: Downloads weather information for a specified location (in this case Auckland), and prints it in the terminal.
- `curl -H "Content-Type: application/json" -X POST -d '{"user":"bob","pass":"123"}' http://example.com`: POST json data to `example.com`.

### `wget`

The `wget` command can be used to download a single or multiple files, or even entire websites.

- `wget example.com/index.html`: Downloads the file from the location `example.com/index.html`.
- `wget -r ftp:example.com/directory`: Downloads a folder from the location specified.
- `wget -m -convert-links -page-requisites example.com`: Downloads the entire public-facing website for `example.com`.
- `wget -c`: Resumes a previous download that didn't finish.

## Compressing or decompressing files

### `gzip`

`gzip` is the 'classic' compression tool, for working with `.gz` files:

- `gzip data.txt`: Compresses the file `data.txt`, and gives it a `.gz` extension.
- `gzip -8 data.txt`: Compresses the file `data.txt` with a better and slower level of compression (the levels range from `1` - fastest but least compression - to `9` - slowest but best compression).
- `gzip -r data`: Compresses the folder called `data`, and gives it a `.gz` extension.
- `gzip -d data.gz`: Decompresses the file `data.gz`.

### `tar` archives

`tar` files are archives that contain multiple files:

- `tar -cf archive.tar file1 file2`: Creates an archive called `archive.tar` with the files `file1` and `file2`.
- `tar -xf archive.tar`: Extracts the contents of `archive.tar`.
- `tar -tf archive.tar`: View the contents of `archive.tar`.

A `tar` archive can be compressed using `gzip` (resulting in a file with the extension `.tar.gz`) or `bzip2` (resulting in a file with the extension `.tar.bz2`):

- `tar czvf compressed.tar.gz data.txt`: Compresses the file `data.txt` as a file called `compressed.tar.gz`.
- `tar tzvf compressed.tar.gz`: Views the contents of `compressed.tar.gz`.
- `tar xzvf compressed.tar.gz`: Decompresses a `.tar.gz` file.
- `tar cjvf compressed.tar.bz2 data.txt`: Compresses the file `data.txt` as a file called `compressed.tar.bz2`.
- `tar tjvf compressed.tar.bz2`: Views the contents of `compressed.tar.bz2`.
- `tar xjvf compressed.tar.bz2`: Decompresses the file `compressed.tar.bz2`.

## Permissions

These characters translate into attributes, such as the file type, and who can read (`r`), write (`w`), and execute (`x`) the file. For example, `drwxr-xr--` would translate into:

- `d`: The file type. This is usually either a file (`-`), or directory (`d`).
- `rwx`: The owner permissions.
- `r-x`: The group permissions.
- `r--`: The world permissions.

So for this example, the file is a folder, and anyone can see it. The owner and anyone else in their group can enter (i.e. execute) it. Only the owner can make changes to the folder.

### Changing permissions

The user that created a file (or the superuser) is its owner. They are able to change its permissions, using the command `chmod` followed by three numbers. These numbers use octal (base 8) notation, and represent the following permissions:

| Octal | Permissions |
| :---- | :---------- |
| 0     | `---`       |
| 1     | `--x`       |
| 2     | `-w-`       |
| 3     | `-wx`       |
| 4     | `r--`       |
| 5     | `r-x`       |
| 6     | `rw-`       |
| 7     | `rwx`       |

For example, to change permissions of a file to `-rwxr-xr-x` you would use `chmod 755 file.txt`.

### Changing ownership

To change the owner of a file, use `chown`, followed by the name of the user and/or group that will become the new owner. For example:

- `chown samcottle` changes the owner to the user `samcottle`.
- `chown :admins` changes the owner to members of the group called `admins`.
- `chown samcottle:admins` changes the owners to the user `samcottle` and members of the group called `admins`.

## Processes

A list of processes can be viewed with:

- `ps`: Displays the processes associated with the current terminal session.
- `ps x`: Displays the processes for all active terminal sessions.
- `top`: Displays a dynamic list of processes. This is like the command line version of the Gnome **System Monitor** or macOS **Activity Monitor**. Press **Ctrl + c** to stop `top`.
- `jobs`: Displays a list of processes running in the background.

### Running processes in the background

If a program is running in the terminal (i.e. you need to press **Ctrl + c** to use the terminal again), and you want to use the terminal for other commands, you can run the task in the background. To do this add `&` after the command. For example, `xlogo &` runs `xlogo` in the background.

You can display a list of background processes with `jobs`. This also displays a number before to each process:

```bash
[1]-  Running                 xlogo &
[2]+  Running                 gedit &
```

To bring a process to the foreground, use `fg` followed by a `%` + the job number of the process. For example, to bring `gedit` to the foreground, you'd use `fg %2`.

You can also pause a running process, allowing you to move it to the background, with **Ctrl + z**.

### Closing processes

If you need to close a process use `kill`, followed by `%` + the job number of the process. For example, to close `xlogo` you would use `kill %1`.

To close all instances of a process, use `killall` followed by the name of the process. For example, `killall gedit` would close all instances of `gedit` that are running.

## Using wildcards

The most commonly used wildcards are:

- `*`: Any characters. For example, `g*` would match any files beginning with `g`. **Note**: A `*` by itself would match all files.
- `?`: Any single character. For example, `g?.txt` would match any files starting with `g` followed by any one character, followed by `.txt`.
- `[characters]`: Any of the characters specified between the square brackets.
- `[!characters]`: Any characters that is not specified between the square brackets.
- `~`: Home directory. For example, `echo ~` would print the user's home directory. Instead of `cd /home/user/folder`, you can use the more concise `cd ~/folder`.

## Command line editing

Apart from using the arrow keys to move the cursor you can use the following key combinations to interact with text.

### Moving the cursor

- **Ctrl + a**: Move cursor to the beginning of the line.
- **Ctrl + e**: Move cursor to the end of the line.
- **Alt + f**: Move cursor forward one word.
- **Alt + b**: Move cursor back one word.
- **Ctrl + l**: Clears the screen and puts the cursor in the top left.

### Text editing

- **Alt + t**: Swaps the word with the word preceding it.
- **Alt + l**: Convert remainder of the word to lowercase.
- **Alt + u**: Convert remainder of the word to uppercase.

### Cutting and pasting

- **Ctrl + k**: Cuts text between cursor and the end of the line.
- **Ctrl + u**: Cuts text between cursor and the beginning of the line.
- **Alt + d**: Cuts text between cursor and the end of the word.
- **Alt + Backspace**: Cuts text between cursor and the end of the word.
- **Ctrl + y**: Pastes text.

## Using expansion

### Brace expansion

Brace expansion (`{}`) can be used as a sort of wildcard. For example, to display the letters between _a_ and _r_ you can use `echo {a..r}`.

This can be really useful if you need to create, for example, multiple folders that use a similar format. Instead of manually creating a folder to store files for each month of the years 2017 and 2019, you could use `mkdir {2017..2019}-0{1..9} {2017..2019}-{10..12}`.

### Parameter expansion

Parameters can be used as a sort of wildcard in place of a username (i.e. `$USER`) and many other variables.

### Using quotes to control expansion

Using the command `echo The total is $100` displays `The total is 00` (because `$100` is interpreted as two things: the wildcard `$1`, and `00`). To avoid these kinds of scenario, you can use:

- Double quotes: `"`s around text will suppress most special characters, such as word splitting, pathname expansion, tilde expansion, and brace expansion (but not a `$`, `/`, or back tick). Example: `mv "two words.txt" two_words.txt`.
- Single quotes: `'`s around text will suppress all unwanted expansion. Example: `echo 'The total is $100'` would display `The total is $100`.
- Escape character: A `\` will suppress a single character. This is often used to:
  - Suppress one character within a string of double quotes: `echo "The balance of $USER is: \$5.00"`.
  - Prevent accidental expansion in poorly named files: `rn bad\&filename.txt good_filename.txt`.

## Verifying a Checksum

Three common commands to get the Checksum of a file are:

- `md5sum`: Checks the MD5 Checksum of a file. For example `md5sum test.txt` would print the MD5 Checksum for the file `test.txt`.
- `sha1sum`: Checks the SHA-1 Checksum of a file. For example `sha1sum test.txt` would print the SHA-1 Checksum for the file `test.txt`.
- `sha256sum`: Checks the SHA-256 Checksum of a file. For example `sha256sum test.txt` would print the SHA-256 Checksum for the file `test.txt`.

### Changing a Checksum

To alter a file's Checksum:

- `truncate`: Appends data to the end of a file. For example `truncate -s +10 test.txt` would add 10 bytes of data to the end of the file.

## Installing and removing software

### Using `apt`

Many `apt` commands need to be run in superuser (i.e. `sudo`) mode.

- `apt update`: Checks for updates to installed packages.
- `apt upgrade`: Updates (or _upgrades_) installed packages.
- `apt dist-upgrade`: Updates installed packages, including kernel packages.
- `apt search package_name`: Searches for a specified package. For example `apt search hugo` returns a list of available packages containing `hugo`.
- `apt install package_name`: Installs a specified package. For example `sudo apt install hugo` installs the package `hugo`.
- `apt remove package_name`: Removes an installed package (but leaves the configuration files). For example `sudo apt remove hugo` removes (i.e. _uninstalls_) the package `hugo`.
- `apt purge package_name`: Removes everything related to an installed package (think of it as `remove` + deletes configuration files).
- `apt autoremove`: Removes any dependencies (i.e. libraries and packages) that are no longer required.

### Using `dpkg`

The installation and removal of `.deb` files is done with `dpkg` (Debian Package Management System). These need to be run in superuser (i.e. `sudo`) mode.

- `dpkg-query -l`: Lists installed packages.
- `dpkg -i`: Installs a package from a `.deb` file. For example, `sudo dpkg -i app_v1.1_linux.deb` installs a package from `app_v1.1_linux.deb` (the actual package may have a different name than the file).
- `dpkg -r`: Removes an installed package. For example, `sudo dpkg -r app` removes the package called `app`.

## Using an `alias` to create commands

This is a way of stringing multiple commands together in a sequence, referred to as an `alias`. Each command in an alias is separated by a semicolon. Here's what defining an alias, `myAlias`, with three commands looks like:
`alias myAlias='cd ..; mkdir new; ls'`

Now we can use the command `myAlias` to invoke those three commands.

**Tip**: Use the `type` command (i.e. `type myAlias`) for info on an alias you've defined.

**Note**: Before creating an alias, check whether it's already in use by an installed program. An easy way to do this is using the `type` command. So `type myAlias` will either return information on what type of file `myAlias` is (you probably shouldn't create an alias with this name, unless you want to overwrite it), or `not found` (it's fair game).

## Using redirection

The `>` operator is used to _redirect_ output from a command to a file. For example, to redirect the output of the `ls -l` command to a file called `list.txt` you would use:
`ls -l > list.txt`.

This can be combined with the following commands:

- `cat`: Concatenates (or combines) multiple files into one. For example, to combine the files `movie.mp4.01`, `movie.mp4.02`, and `movie.mp4.03` into one file called `movie.mp4` you would use `cat movie.mp4.0* > movie.mp4` (with `*` being a wildcard).
  - `cat` can also be used to create small text files, for example `cat > textfile.txt` would then give you the opportunity to enter some text. **Ctrl + c** will output this text to a file.
  - `cat` can also be used to print the contents of files to the terminal. For example `cat textfile.txt.` would display the contents of `textfile.txt`.

## Using pipelining

The pipe operator, or `|`, is used to pipe the output of one command into another. This can be used to chain multiple commands together.

Here are some commands you can do this with:

- `less`: This is used to display information in the terminal, one page at a time. Using pipelining, this can be used in combination with, for example, `ls` to display the contents of a large directory one page at a time, with `ls -l /usr/bin | less`.
- `sort`: Unsurprisingly, this sorts information. So if you wanted to list the contents of two directories, `/bin` and `/usr/bin`, and combine the output in a sorted list, displayed one page at a time, you would use `ls /bin /usr/bin | sort | less`.
- `uniq`: Removes (or lists) all duplicates. For example, `ls /bin /usr/bin | sort | uniq | less` is the same as above, but all the duplicated file names are removed. You can also use `uniq` to list _only_ the duplicates, with the `-d` option: `ls /bin /usr/bin | sort |uniq -d | less`.
- `wc`: Counts the number of lines, words, and bytes in a file (or list). For example, to count the number of unique items in `/bin` and `/usr/bin` you could use `ls /bin /usr/bin | sort | uniq | wc -l` (**note**: the `-l` option limits the output to report lines only).
- `grep`: Very powerful command, but in this case it can be used to match patterns in a file (a bit like a search, or a filter). So to list all commands related to `zip` compression in the `/bin` and `/usr/bin` folders, you could use `ls /bin /usr/bin | sort | uniq | grep zip`.
- `head` and `tail`: Get the first or last lines of a file or folder (by default, the first or last 10 lines). For example, to get the last `5` files of the `/usr/bin` folder you could use `ls /usr/bin | tail -n 5` (the `-n` option, followed by a number, prints that number of lines).
  - `tail` can also be used to view file changes in real time, with the `-f` option (and you may need to be in superuser-mode to run this command). For example, `sudo tail -f /var/log/messages` monitors changes to this file (until you stop with **Ctrl + c**).
- `tee`: Used to copy information, mid-pipeline, to a file. So to capture the contents of the `/usr/bin` directory, before filtering it for commands with `zip` (using `grep`) you could use `ls /usr/bin | tee list.txt | grep zip`.

## Networking

- `ifconfig`: Examines active network devices. Can also be used to change your IP address on the network with, for example, to request the IP address of **192.168.1.2** you would use `ifconfig eth0 192.168.1.2`. The network mask (`netmask`), broadcast address (`broadcast`), and MAC address (`hw`) can also be changed.
- `iwconfig`: Examines active _wireless_ network devices.
- `dhclient`: Request a new IP address. For example, `dhclient eth0` will request a new IP address for the ethernet connection.
- `dig`: Checks DNS information relating to a website. For example, to get the name server (`ns`) information for Google.com you'd use `dig www.google.com ns`.
- `ping`: Continually pings a host with packets, to see how it responds. `ping` prints the host's IP address, and statistics about network performance between you and the host.
- `traceroute`: Prints the route of packets between your device and the host. For example, `traceroute google.com` provides the details of where packets travel between the device and `google.com`.

## App-specific commands

Commands for other CLI apps I use frequently.

### Finger

The [Finger protocol](https://en.wikipedia.org/wiki/Finger_(protocol)) is the original social network (and perhaps also the [original IoT protocol](https://www.cs.cmu.edu/~coke/history_long.txt)?).

Your profile and status are updated by maintaining the following files in your `/home` directory:
- `.plan`: Your profile and/or status.
- `.project`: The project you're working on.

Common commands are:
- `finger`: Lists all users on your server.
- `finger @example.com`: Lists all users on a _remote_ server.
- `finger -l`: Lists all users on the server, as well as user information.
- `finger user`: Shows information for a user on your server.
- `finger user@example.com`: Shows information for a user on a _remote_ server.

Examples of users:
- `finger amsterdam@graph.no` (get the weather forecast for Amsterdam)
- `finger blast-rules@happynetbox.com` (play a game)
- `finger random@happynetbox.com` (view a random HappyNetBox user)

Some finger servers:
- `finger @finger.farm`
- `finger @happynetbox`
- `finger @plan.cat`

### Glow

[Glow](https://github.com/charmbracelet/glow) renders markdown in the command line.

- `glow`: Starts the textual user interface, where you can open a markdown file from the current folder.
- `glow content.md`: Opens the file `content.md` in the CLI (which is not scrollable, like the textual user interface).
- `glow https://raw.githubusercontent.com/samcottle/notes/master/commandline.md`: Fetches a markdown file from a URL.
- `glow github.com/charmbracelet/glow`: Fetches a README.md from Github or Gitlab.

### Hugo

Common commands for the [Hugo static site generator](https://www.gohugo.io/):

- `hugo new posts/new-post.md`: Creates a new post called **new-post.md**.
- `hugo server -D`: Starts a [localhost](http://localhost:1313/) server with your site, including any draft posts.
- `hugo -D`: Build static site. This site can be deployed to a production web server.

### VNC server

If you want to start or stop the VNC server from the command line:

- `vncserver`: Starts the VNC server, and provides the IP address/display number to connect to.
- `vncserver -kill :1`: This terminates the VNC server with display number `1` (change the `1` to whatever display number was being used).

### Weechat

After opening `weechat`, you can use the following commands in the buffer.

Getting set up:

- `/server add liberachat irc.libera.chat/6697 -ssl`: Adds a server to the list, gives it an alias (in this case `liberachat`), and connects to it over SSL.
- `/fset liberachat`: Sets `liberachat` as the default IRC server.

Connecting:

- `/connect liberachat`: Connects to the server `liberachat`.
- `/msg NickServ IDENTIFY NicknameHere PasswordHere`: Logs in with an existing account.

Using Weechat:

- `/join #channelname`: Joins the channel `#channelname`.
- `/part #channelname`: Leave the channel `#channelname`.
- **Alt** + number: Switches the active channel (a list of available channels is shown on the left side of the screen).
- `/list -re topic`: Lists channels on the server that contain the `topic`.
- `/msg alis LIST *topic*`: Returns a list of channels on the server that contain the `topic`.
- `/query username`: Start a private conversation with the user `username`.
- `/quit`: Quits `weechat`.
