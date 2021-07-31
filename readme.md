# The Linux CLI

All things command line

## Contents

<!-- toc -->

- [The Linux CLI](#the-linux-cli)
  - [Contents](#contents)
  - [Genral Things to Know](#genral-things-to-know)
  - [Keyboard Shortcuts](#keyboard-shortcuts)
  - [Signals](#signals)
  - [Useful Commands](#useful-commands)
  - [Managing packages](#managing-packages)
    - [apt vs apt-get](#apt-vs-apt-get)
  - [Linux File System](#linux-file-system)
  - [Navigating File System](#navigating-file-system)
  - [Manipulating Files & Directories](#manipulating-files--directories)
  - [Editing and Viewing Files](#editing-and-viewing-files)
  - [stdin, stdout & Redirection (piping)](#stdin-stdout--redirection-piping)
  - [Searching for Text](#searching-for-text)
  - [Finding Files and Directories](#finding-files-and-directories)
  - [Chaining Commands](#chaining-commands)
  - [Environmental Variables](#environmental-variables)
  - [Managing Processes](#managing-processes)
  - [Managing Users](#managing-users)
  - [Managing Gropus](#managing-gropus)
  - [File Permissions](#file-permissions)
  - [Resources](#resources)

<!-- tocstop -->

## Genral Things to Know

1. When copying anything to the terminal make sure you trust the source: <br> For example there could be a secret return char at the eol and the moment you paste it, it will run without hitting enter. Websites could use JS to switch what you actually thought you copied with something malicious, that could steal all your passwords etc.

2. `Shell`: a program which takes the command we type and passes it the the OS for execution

3. `bash`, bourne again shell. Named after Stephen Bourne who created the `bourne shell`

4. `Linux` is a `case-sensitive` OS

5. In linux we use `/`(forward slash) in pathnames, where as in windows we use `\`(backslash)

6. In linux `everything is a file including directories, devices, network sockets, pipes` and so on

## Keyboard Shortcuts

> 1. CTRL + A – takes you to the beginning of the line
> 2. CTRL + E – takes you to the end of the line
> 3. CTRL + K – "yank" everything after the cursor
> 4. CTRL + U – "yank" everything before the cursor
> 5. CTRL + W – "yank" until the first space before the cursor (so like 1 word/ command)
> 6. CTRL + Y – "paste" (but it doesn't actually go into your system clipboard) everything you yanked
> 7. CTRL + L – clear the screen
> 8. CTRL + R – reverse search through history
> 9. CTRL + SHIFT + C – copy
> 10. CTRL + SHIFT + P – paste

## Signals

> 1. CTRL + C – Signal Interrupt == SIGINT
> 2. CTRL + D – Signal Quit == SIGQUIT
> 3. SIGKILL – kill -9
> 4. kill -l – list all valid signals (see that 9 is SIGKILL)

## Useful Commands

```bash
# head == get stuff from top of file (default = 1st 10 lines)
head ~/.bash_history

# tail == get stuff from end of file
tail ~/.bash_history

# check command history
history

# list all the binaries (programs and commands u use)
# except for the custom ones I beleive
ls /bin

# less == open a file for read mode (navigate like vim)
# good for reading long files, if you can't use VSCode or something
# less is the newer version of more
less filename

# man == manual, man uses less apparently (not every program has a man)
man less

# cat = concatnate to stdout
# following prints to screen
cat filename

# grep
# Prints out all the LINES that contains the word Hamlet in the hamlet.txt
grep Hamlet hamlet.txt
# also valid
grep "Hamlet thou" hamlet.txt

### ssh used to connect to other computers from terminal
ssh 192.168.50.02 #just an example
```

## Managing packages

Ubuntu other linux distributions have their own package manager (like npm, yarn, pip, Nuget).

Ubunt has `apt` which is short for `advanced package tools`

The package manger has access to all packages through a package database on our machine. `apt list` will show our machine's package database.

Very Frequently this pacakge db is outdated (or perhaps cleared and keeps the list of installed packages only). For this reason installing software using `apt` is a `2 step process`. Otherwise installation might fail

```bash
# update machine's pacakge db
apt update
# install package
apt install package-name
```

So install

### apt vs apt-get

apt is the newer package manager

apt-get may be considered as lower-level and "back-end", and support other APT-based tools. apt is designed for end-users (human) and its output may be changed between versions

apt-get and apt-cache's most commonly used commands are available in apt

More about [apt vs apt-get](https://askubuntu.com/questions/445384/what-is-the-difference-between-apt-and-apt-get)

```bash
# to see manual
apt
# list of packages
# lists literally everything, everything in the package database
apt list
# all this are same as apt-get but with enhanced UI
# update machine's package database
apt update
# Install pacakage,
apt install nano
# Uninstall pacakage,
apt remove nano
```

## Linux File System

In linux `everything is a file including directories, devices, network sockets, pipes` and so on

```bash
/       # root dir
 /bin   # binaries or programs
 /boot  # all files related to booting
 /dev   # devices, files needed to access devices
 /etc   # editable text configurations (opinionated), where we have config files
 /home  # In a machine with many user, each user will have a home dir here
 /lib   # for library files, like software library dependencies
 /proc  # files that represent running processes
 /root  # Home directory of root user
 /usr   # unix system resources
 /var   # variable, here we keep files that are updated frequently like lock files
```

\*for me `cd ~` == `cd /home/sadnan`

## Navigating File System

```bash

pwd  # list items
ls   # list items
cd   # change dir
cd / # list items
cd ~ # go to home directory
```

## Manipulating Files & Directories

```bash
mkdir dirName             # create directory
touch file1.txt file2.txt # create 1 or multiple file
mv file1.txt hello.txt    # rename file1.txt to hello.txt
mv file2.txt /sadnan      # move file2.txt into the /sadnan dir
rm file1.txt file2.txt    # remove files(s)
rm file*                  # remove files using pattern (regex)
rm -r dirName             # remove recursively, for directories
```

## Editing and Viewing Files

`cat` stands for concatenate. Has many purposes.

```bash
# see the contents of file on terminal
# useful for small files
cat file1.txt

# see a bit of the file at a time
# press enter to move to next line, q to exit
# can't move up, only down
more filename

# less == open a file for read mode (navigate like vim)
# good for reading long files, if you can't use VSCode or something
# less is the newer version of more, move in both directions
less filename

# head == get stuff from top of file (default = 1st 10 lines)
head ~/.bash_history

# tail == get stuff from end of file
tail ~/.bash_history
```

## stdin, stdout & Redirection (piping)

Linux has a default standard input and output, `stdin` and `stdout`

`Keyboard` is the `stdin`

`Screen/Terminal` is the `stdout`

`>` can be used to redirect/change the `stdout`

`<` can be used to redirect/change the `stdin` (not that manu use cases on the terminal)

```bash
# All this commands should create a newfile, if one does not exist
cat file1.txt                           # shows the content on screen, because screen is stdout
cat file1.txt > file2.txt               # concatnates file1.txt to file2.txt
cat file1.txt file2.txt > combined.txt  # concatnates file1.txt & file2.txt in combined.txt
echo hello > newfile.txt                # log something to file, useful for writing single lines to file
echo hello >> newfile.txt               # echo to end of file and not overwrite, which is default behaviour
ls -l /etc > newfile.txt                # log the output of ls command into newfile.txt
```

## Searching for Text

`grep` stands for `global regular expression print`

The search is case sensitive by default

can use `-i` to make it case insensitive

```bash
grep Hamlet hamlet.txt           # get the LINES with word Hamlet the in file
grep "Hamlet thou" hamlet.txt    # also valid
grep -i "Hamlet thou" hamlet.txt # making search case in-sensitive
                                 # **  Remember everything is a file in linux  **
grep -i root /etc/passwd         # Therefore can search special files like passwd
                                 # folders are also files
grep -ir hello .                 # Search all files in Current Folder, use -r option

# search in multiple files
grep -i hello file1.txt file2.txt
grep -i hello file*
```

## Finding Files and Directories

We have the `find` command to find files and directories and not just text inside them.

```bash
                                       # no args = prints all (hidden files too)
find                                   # the files and directories in the current folder
find -type d                           # find directories only
find -type f                           # find files only
                                       # Can use patterns
find -type f -name "f*"                # find all the files starting with f
find -type f -iname "f*"               # same as above but case in-sensitive
find / -type f -iname "f*"             # same as above but search directory specified as "/" (root dir)
find / -type f -name "f*" > file.txt   # Same as above but write to output to file.txt
```

## Chaining Commands

There are a few ways to chain commands

1. ; (semi-colon)
2. && (logical and)
3. || (logical or)
4. | (pipe)

## Environmental Variables

## Managing Processes

## Managing Users

## Managing Gropus

## File Permissions

## Resources

[Section from Mosh's Docker Course](https://codewithmosh.com/courses/the-ultimate-docker-course/lectures/31447539)
[Brian Holt's Course Website](https://btholt.github.io/complete-intro-to-linux-and-the-cli/)

```

```
