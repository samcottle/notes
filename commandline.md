# Linux command line

## Basic commands
- `cd`: Change the working directory. `cd folder1` would change you to the working directory with the name `folder1`.
- `ls`: List the files in a directory. For more information (such as permissions) on each of the files in the directory, use `ls -l`.
- `pwd`: Print working directory. Returns the name of the working directory (i.e. the one you're in).
- `file`: Determine the contents of a specified file. `file me.jpg` would return `JPEG image data. JFIF standard 1.01.`, for example.
- `mkdir`: Make a new directory. `mkdir newfolder` mwould make a new directory called `newfolder`. Can make multiple new directories by specifying more than one after `mkdir`. For example `mkdir newfolder1 newfolder2` would create two new directories: `newfolder1` and `newfolder2`.
- `cp`: Copies a file or folder. `cp file1 file2` would make a copy of `file1` and call it `file2`. `cp file1 /folder1` would make a copy of `file1` in `folder1`.
- `mv`: Move or rename a file. `mv file1 /folder1` moves `file1` to a folder called `folder1`. `mv file1 file2` renames `file1` to `file2`.
- `rm`: Remove a file or directory. `rm file1 file2` deletes `file1` and `file2`. To delete directories, you often need to use `rm -r folder1`, which recursively deletes all the files and subdirectories within it (otherwise you get the error `rm: cannot remove 'folder1': Is a directory`.
- `shutdown`: Shuts down the computer. `sudo shutdown -h now` would shutdown the computer immediately (i.e. `now`).

### Using wildcards
The most commonly used wildcards are:
- `*`: Any characters. For example, `g*` would match any files beginning with `g`. **Note**: A `*` by itself would match all files.
- `?`: Any single character. For example, `g?.txt` would match any files starting with `g` followed by any one character, followed by `.txt`.
- `[characters]`: Any of the characters specified between the square brackets.
- `[!characters]`: Any characters that is not specified between the square brackets.

### Useful directories
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

### Using `apt`
Many `apt` commands need to be run in superuser (i.e. `sudo`) mode.
- `apt update`: Checks for updates to installed packages.
- `apt upgrade`: Updates (or *upgrades*) installed packages.
- `apt dist-upgrade`: Updates installed packages, including kernel packages.
- `apt search package_name`: Searches for a specified package. For example `apt search hugo` returns a list of available packages containing `hugo`.
- `apt install package_name`: Installs a specified package. For example `sudo apt install hugo` installs the package `hugo`.
- `apt remove package_name`: Removes an installed package. For example `sudo apt remove hugo` removes (i.e. *uninstalls*) the package `hugo`.

### Using an `alias` to create commands
This is a way of stringing multiple commands together in a sequence, referred to as an `alias`. Each command in an alias is seperated by a semicolon. Here's what defining an alias, `myAlias`, with three commands looks like:
`alias myAlias='cd ..; mkdir new; ls'`

Now we can use the command `myAlias` to invoke those three commands.

**Tip**: Use the `type` command (i.e. `type myAlias`) for info on an alias you've defined.

**Note**: Before creating an alias, check whether it's already in use by an installed program. An easy way to do this is using the `type` command. So `type myAlias` will either return information on what type of file `myAlias` is (you probably shouldn't create an alias with this name, unless you want to overwrite it), or `not found` (it's fair game).

### Getting help
The commands for getting help aren't standardised, but generally speaking you can use the following to find out about a command:
- `help`: Gets help information for built-in programs. For help information on how to use the change directory command, you'd use `help cd`.
- `--help`: Gets more info on the syntax of a command. So `mkdir --help` gives you a list of arguments you can use with the `mkdir` command, for example.
- `info`: Gets the programs manual. `info ls` brings up the manual for the `ls` command. This gives you a very similar result to `man`, but more to the point.
- `man`: Gets the programs manual. `man ls` brings up the manual for the `ls` command. This gives you a very similar result to `info`, but with more contextual information.
- `whatis`: Display a brief discription of the command. `whatis ls` Gives you a short description (in this case the description `list directory contents`).

### Verifying a Checksum
- `md5sum`: Checks the MD5 Checksum of a file. For example `md5sum test.txt` would print the MD5 Checksum for the file `test.txt`.
- `sha1sum`: Checks the SHA-1 Checksum of a file. For example `sha1sum test.txt` would print the SHA-1 Checksum for the file `test.txt`.
- `sha256sum`: Checks the SHA-256 Checksum of a file. For example `sha256sum test.txt` would print the SHA-256 Checksum for the file `test.txt`.

## Raspberry Pi

### VNC
- `vncserver`: Starts the VNC server, and provides the IP address/display number to connect to.
- `vncserver -kill :1`: This terminates the VNC server with display number `1` (change the `1` to whatever display number was being used).
