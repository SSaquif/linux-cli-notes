### Resources

[Brian Holt's Course Website](https://btholt.github.io/complete-intro-to-linux-and-the-cli/)

### The Linux CLI

#### Notes

1. When copying anything to the terminal make sure you trust the source: <br> For example there could be a secret return char at the eol and the moment you paste it, it will run without hitting enter. Websites could use JS to switch what you actually thought you copied with something malicious, that could steal all your passwords etc.

#### Shortcuts

> 1. CTRL + A – takes you to the beginning of the line
> 2. CTRL + E – takes you to the end of the line
> 3. CTRL + K – "yank" everything after the cursor
> 4. CTRL + U – "yank" everything before the cursor
> 5. CTRL + Y – "paste" (paste in quotes because it doesn't actually go into your system clipboard) everything you yanked
> 6. CTRL + L – clear the screen
> 7. CTRL + R – reverse search through history
> 8. CTRL + SHIFT + C – copy
> 9. CTRL + SHIFT + P – paste

#### Signals

> 1. CTRL + C – Signal Interrupt == SIGINT
> 2. CTRL + D – Signal Quit == SIGQUIT
> 3. SIGKILL == kill -9
> 4. kill -l == list all valid signals (see that 9 is SIGKILL)

#### Useful commands

```bash

# head == get stuff from top of file (default = 1st 10 lines)
head ~/.bash_history

# tail == get stuff from end of file
tail ~/.bash_history

# less == open a file for read mode (navigate like vim)
# good for reading long files, if you can't use VSCode or something
# less is the newer version of more
less filename

# man == manual, man uses less apparently (not every program has a man)
man less

# cat = concatnate to stdout
# following prints to screen
can filename

# grep
# Prints out all the lines that contains the word Hamlet in the hamlet.txt
grep "Hamlet" hamlet.txt

### ssh used to connect to other computers from terminal
ssh 192.168.50.02 #just an example
```
