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
  - [multi line commands `\`](#multi-line-commands-)
  - [Editing and Viewing Files](#editing-and-viewing-files)
  - [stdin, stdout & Redirection (piping)](#stdin-stdout--redirection-piping)
  - [Searching for Text](#searching-for-text)
  - [Finding Files and Directories](#finding-files-and-directories)
  - [Chaining Commands](#chaining-commands)
    - [; (semi-colon)](#-semi-colon)
    - [&& (logical and)](#-logical-and)
    - [|| (logical or)](#-logical-or)
    - [| (pipe)](#-pipe)
  - [Nested Commands, `$()`](#nested-commands-)
  - [Environmental Variables](#environmental-variables)
  - [PATH, .bashrc, export and alias](#path-bashrc-export-and-alias)
  - [Managing Processes](#managing-processes)
    - [lsof](#lsof)
  - [Managing Users](#managing-users)
  - [User's Config files](#users-config-files)
    - [`/etc/passwd`](#etcpasswd)
    - [`/etc/shadow`](#etcshadow)
  - [Managing Groups](#managing-groups)
    - [`/etc/group`](#etcgroup)
  - [File Permissions](#file-permissions)
    - [Changing file permissions](#changing-file-permissions)
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

# ssh used to connect to other computers from terminal
ssh 192.168.50.02 #just an example

# multi line commands
mkdir hello;\
> cd hello;\
> echo done
```

## Managing packages

Ubuntu other linux distributions have their own package manager (like npm, yarn, pip, Nuget).

Ubunt has `apt` which is short for `advanced package tools`

The package manger has access to all packages through a package database (ie the local 'apt' package cache) on our machine. `apt list` will show our machine's package database.

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

## multi line commands `\`

Use `\`

```bash
mkdir hello;\
> cd hello;\
> echo done
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

They are `executed left to right`

### ; (semi-colon)

If a command files, it will still try to execute the next one as long as there is commands remaining

```bash
# doesn't care if a command fails, continues on
mkdir test; cd test; echo done
```

### && (logical and)

If a command fails, then stops. Does not continue

```bash
# stop on failure
mkdir test; cd test; echo done
```

### || (logical or)

If command passes then stops, continues if command fails. only one command will run

```bash
# stops on success (one or the other)
mkdir test; cd test; echo done
```

### | (pipe)

Output of current command is the Input of the next command

```bash
# scroll through /bin
ls  /bin | less
```

## Nested Commands, `$()`

Sometimes we want to run a command inside another. I mean we want the result of the inner command as part of the outter command. We use $() for that. You can kind of think of it as like a variable but it really isn't imo.

```bash
# Example 1: map source code in host to docker container for live updates
# Given that src code reside in the pwd
# we need the result of pwd
docker run -v $(pwd):/app <image>

# Example 2: remove all containers
# inner command returns a list of all containers
docker container rm $(docker container ls -a -q)
```

## Environmental Variables

Variables used to store config settings. They are `case sensitive` like pretty much everything in linux.

We can temporarily add enviroment variables to the current terminal session using `export`. The are removed once the session ends

You can `permanently` add new envirometal variables by adding them to your `bash profile`, in Ubuntu it's the `.bashrc` file. See [PATH, .bashrc, export and alias](#path-bashrc-export-and-alias)

```bash
printenv                # see all env variables
print PATH              # print a env variable
echo $PATH              # same as above
export DB_USER=saad     # ad env var for current session
```

## PATH, .bashrc, export and alias

`PATH` is where the OS checks for all installed programs. It's a list of folders.

The `.bashrc` file is a script file that’s executed when a user logs in. The file itself contains a series of configurations for the terminal session. This includes setting up or enabling: coloring, completion, shell history, command aliases, and more.

If you edit the file, you have to run it again

```bash
. ./.bashrc  # run script
```

We can add new folders to `PATH` using `export`

Finally we can create new names for commands using `alias`. Often done after adding new software folder to `PATH`

Examples from my `.bashrc` file.

```bash
# Adding folder $HOME/Bash-Scripts to PATH
if it exists
if [ -d $HOME/Bash-Scripts ]; then
    export PATH="$HOME/Bash-Scripts:$PATH"
fi

alias cbwd='cbwd.sh'
alias cbds='cbds.sh'
alias jupnb='jupnb.sh'
alias astd='astd.sh'

# Adding Krita app files to PATH
if [ -d $HOME/Krita ]; then
    export PATH="$HOME/Krita:$PATH"
fi
# alias for really long command
alias krita='krita-4.2.9-x86_64.appimage'

# Setting up env var JAVA_HOME to point at default JDK
export JAVA_HOME=/usr/lib/jvm/jdk-11.0.11+9

# Adding ANDROID_SDK application folders to PATH
# Creating an alias to run the shell script
export ANDROID_SDK=/home/sadnan/Android/Sdk
export PATH=/home/sadnan/Android/Sdk/platform-tools:$PATH
alias astd='astd.sh'
```

## Managing Processes

A process is an instance of a running program,

We can list all processes using `ps` but I prefer `lsof` (built in for linux dists)

```bash
ps           #see all running processes for the session I beleive
# Output of ps, see table for brakdown
   PID TTY          TIME CMD
 260761 pts/0    00:00:00 bash
 263970 pts/0    00:00:00 ps

sleep 3      # sends terminal to sleep for 3 seconds
sleep 100 &  # sleep for 100 sec in background, can still use terminal
kill pid     # kill process with given pid
kill -9 pid  # 9 means KILL signal that is not catchable or ignorable.
```

|            | Details                                                                       |
| :--------- | :---------------------------------------------------------------------------- |
| PID        | process id                                                                    |
| TTY        | teletype, the type of terminal                                                |
| pts        | psedo-terminal, a type of terminal (pretty much all terminal seem to be this) |
| pts/number | all the terminals we open are numbered, this number is the terminal number    |

### lsof

The lsof (list open files) command returns the user processes that are actively using a file system. It is sometimes helpful in determining why a file system remains in use and cannot be unmounted. Remember everything is a file in linux.

Morea about [`lsof`](https://www.geeksforgeeks.org/lsof-command-in-linux-with-examples/)

## Managing Users

For root user command prompt ends wit h `#`
For all other users command prompt ends wit h `$`

```bash
useradd/mod/del # help menu, when no options
useradd name    # add a new user, use adduser instead.
usermod name    # modify an user
userdel name    # del an user

                # more interactive version of useradd, uses useradd itself
adduser name    # can set password and additional info for user easily

# Modifying the default shell of a user
# usermod -s /pathToShell username
# also see next section
usermod -s /bin/bash sadnan
```

## User's Config files

### `/etc/passwd`

Each user has their own configuration file called `passwd` in the `/etc` folder.

The filename is misleading from user pov, passwords are not tored here. Just user account info.

```bash
cat /etc/passwd  # see the config file in terminal
```

After modyfying the default shell, you can check for it in the `passwd` file

```bash
usermod -s /bin/bash sadnan
cat /etc/passwd
# it's this line
# each piece of info is seperated by :
# x means password is stored somewhere else
# sadnan:x :1000:1000:Sadnan Saquif,,,:/home/sadnan:/bin/bash
```

### `/etc/shadow`

Where passwords are stored and only accessible to the rootuser

## Managing Groups

Have similar commands to managing users. Users of the same group have same permissions.

Every linux user has a primary group, and 0 or more secondary groups

By default every user is placed into a group whose name is same as the user name. It is also the default primary group for the user. This is done for file permission purposes mainly

First group listed is the primary group.

Can use `usermod` to update user groups

```bash
groupadd        # no options = help menu
groudadd devs   # add a group
groudadd devs   # add a group
groups uname    # see all the groups of the user
```

### `/etc/group`

In this file we can see all the groups for the system

## File Permissions

See the `10 characters` string before each file when you list them like `ls -l`,

First character signifies whether it's file or directory

1. `d` = directory
2. `-` = file

Remaining 9 represent 3 groups. Left to right they are

1. First 3: Represents permissions for the `user` who owns this file
2. Second 3: Represents permissions for the `group` that owns this file
3. Last 3: Represents permissions for everyone else

When you list files using something like `ls -l`. The `first name, 3rd column usually,` is the user who owns the file. The `next name or 4th column` is the group that owns the file

For each group we have `r`, `w`, `x` or `-`

1. r = readable to group
2. w = writableto group
3. x = executable to group
4. - = not r/w/x to group

For directories having `x` or `execute` means we have permission to go into the directory, ie `cd` into it
By default all directories have the 'x' or `execute` permission

### Changing file permissions

We use the change mode command to change file permissions `chmod`

We can chose which groups (user/group/others) permission to change using `u`, `g` or `o` switches

> Side Note: You usually have to update permissions of newly created `shell scripts`

```bash
chmod u+x filename  # add execute permission for user
chmod g-x filename  # remove execute permission for group
                          # add execute and write permissions
                          # remove read permission
chmod og+x+w-r filename   # for groups others and group

chmod -R 775 /home/node/app  # This ones uses octal
# can also use chown
# chown - change file owner and group
# common switch -R = recursive
# see examples below

chown -R node:root /home/node/app
```

`Important:` Look more inot chmod vs chown

- [chown examples](https://www.thegeekstuff.com/2012/06/chown-examples/)
- [a website for generating chmod commands](https://chmodcommand.com/chmod-775/)

## Resources

- [Section from Mosh's Docker Course](https://codewithmosh.com/courses/the-ultimate-docker-course/lectures/31447539)
- [Brian Holt's Course Website](https://btholt.github.io/complete-intro-to-linux-and-the-cli/)
