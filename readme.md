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
  - [Redirection](#redirection)
  - [Searching for Text](#searching-for-text)
  - [Finding Files and Directories](#finding-files-and-directories)
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

## Keyboard Shortcuts

> 1. CTRL + A – takes you to the beginning of the line
> 2. CTRL + E – takes you to the end of the line
> 3. CTRL + K – "yank" everything after the cursor
> 4. CTRL + U – "yank" everything before the cursor
> 5. CTRL + Y – "paste" (paste in quotes because it doesn't actually go into your system clipboard) everything you yanked
> 6. CTRL + L – clear the screen
> 7. CTRL + R – reverse search through history
> 8. CTRL + SHIFT + C – copy
> 9. CTRL + SHIFT + P – paste

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
# Prints out all the lines that contains the word Hamlet in the hamlet.txt
grep "Hamlet" hamlet.txt

### ssh used to connect to other computers from terminal
ssh 192.168.50.02 #just an example

## go to root directory
cd /

## go to home directory
cd ~
```

## Managing packages

Ubuntu other linux distributions have their own package manager (like npm, yarn, pip, Nuget).

Ubunt has `apt` which is short for `advanced package tools`

The package manger has access to all packages through a package database on our machine. `apt list` will show our machine's package database.

Very Frequently this pacakge db is outdated (or perhaps cleared and keeps the list of installed packages only). For this reason install software using apt is a 2 step process. Otherwise installation might fail

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

## Navigating File System

## Manipulating Files & Directories

## Editing and Viewing Files

## Redirection

## Searching for Text

## Finding Files and Directories

## Environmental Variables

## Managing Processes

## Managing Users

## Managing Gropus

## File Permissions

## Resources

[Section from Mosh's Docker Course](https://codewithmosh.com/courses/the-ultimate-docker-course/lectures/31447539)
[Brian Holt's Course Website](https://btholt.github.io/complete-intro-to-linux-and-the-cli/)
