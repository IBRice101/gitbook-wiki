---
description: An introduction to Linux for those who may not have played around with it before
---

# Linux for Beginners

_By_ [_Isaac_](../../../members/members/isaac.md)

This page aims to teach you the basics of using the Linux operating system from the perspective of a total beginner, with a heavy slant towards the command line interface, or CLI. Consider this more of a reference document than something you have to read all the way through, it is, of course, very long.

The structure of this page is based on Dr Ian Ferguson's "Linux-Fu" document that he hands out to second year digital forensics students, although I've taken great care not to plagiarise anything in there.

Note: For demonstration purposes I will be using Ubuntu. This is because it is, in my opinion, the ideal Linux "Distribution" (like a flavour of Linux) for beginners, being comfortable enough for beginners whilst also providing a marked difference from operating systems like Windows. This tutorial assumes you have a Linux distribution installed already, if you do not, I recommend checking out [this walkthrough](./kali-walkthrough.md) that shows you how to install Kali, for example, or 

# Introduction

So, first off, why learn Linux at all? In short, it's because you're *going* to need to at some point in your life as a technical person, and often (once you get the hang of it) it can actually be easier and/or quicker for you to use the Linux command line than to do anything else. By the end of this page you should be a convert to this way of thinking, or if not that then at least you will know what you're doing when you're inevitably plonked down in front of a terminal and expected to get to work achieving something.

## The Command Line

So let's get to work, depending on the distribution you're using there will be one of numerous "terminal emulators" available. if you're using Ubuntu, for example, this default will be GNOME Terminal, others such as Konsole, Alacritty, Terminator, Yakuake, and xterm are also available.

Begin by opening up the terminal, you can do this (in Ubuntu) by pressing the windows (aka meta) key and typing in "terminal". The fundamental idea behind every command is that you type in the name of a process and that causes the process to run. It's also worth knowing that two processes are actually running for a terminal to be functional. In this case we have the GNOME Terminal, which is the terminal emulator, abd Bash, which is the shell. 

![A blank terminal in stock, freshly installed Ubuntu](/.gitbook/assets/LinuxForBeginners/blank_terminal.png)

## First Commands

Now we approach our very first commands in the CLI, how exciting!

- Firstly, type `whoami` (who am I), this should return your username
- Then, type `pwd` (print working directory), this should return the file path to your current working directory
- Finally, type `ls` (list), this will list all of the files present in the current working directory

![The expected result of the three above commands (where "izbr" is replaced with your username)](/.gitbook/assets/LinuxForBeginners/whoami-pwd-ls.png)

FYI: in Linux, the word "directory" is used in place of "folder". 

## Parameters and Switches

Many commands in Linux take parameters, things that are acted upon or used somehow by the process you're calling, as well as "switches" or "flags" (both are used interchangeably to refer to the same thing). let's take `ls` as an example.

- Firstly, concerning parameters type `ls /etc`
  - This should result in the contents of `/etc`, the parameter we specified, being listed
  - the `/` at the start indicates this is an "absolute" file path, that is, from the very start, or root, of the Linux file system

![The result of the above command](/.gitbook/assets/LinuxForBeginners/ls-etc.png)

- Next, try to type in `ls -l`
  - This should result in the files in the home directory being listed, alongside other information such as the owner of the file, and the time and date it was created
  - the `-l` stands for "long", as in "long listing"

![The result of the ls -l command](/.gitbook/assets/LinuxForBeginners/ls-l.png)

- Switches can also be used in tandem with one another. try giving `ls -al` or `ls -a -l` (they both do the same thing) a go. 
  - This will display further information including, but not limited to:
    - Read/Write access
    - Ownership fo the file
    - Date of last file edit
    - name of the file

## Getting Help

If at any stage you need any help with specific commands, the `man` pages are an absolutely invaluable resource. The syntax for accessing man pages is `man [command you want to learn about]`, so for example, if we wanted to learn more information about the `ls` command, we would write `man ls`. The result of this command can be seen below.

![the man page for ls](/.gitbook/assets/LinuxForBeginners/man-ls.png)

You can use the up and down arrow keys to navigate, the `/` character in tandem with `n` and `N` to search (like ctrl+F), and `q` to quit out at any time.

Naturally, there are also many excellent resources online for Linux, particularly good ones are StackOverflow and StackExchange more generally, although often its best to simply query your search engine of choice for specific questions.

Before we move on to anything else, it's important to note a few things down about how we use Linux in the command line. In particular the fact that Linux is a case sensitive software, meaning `LS` and `ls` do two entirely different things.

# Files and Directories

## File Structure Basics

Linux's file structure is kind of like a tree. you have "root", which is at the base of the file structure, this is where every single thing on the computer resides. THere are then directories in root which have many multiple subdirectories, which you can kind of think of like the branches of the tree. 

Every single file and directory has a path to it, with each step one takes to get to that file being delineated by a `/` character. For example, the home directory is stored at path `/home/username`, so in the root directory there is a directory called `home` and under that is one or more directories each representing the home directory of each user on the device. There are no drive letters like Windows has in linux, so no `C:\users\`.

As we saw earlier with the `pwd` command, there is the concept of a current working directory, you can only be in one directory at a time (in a single session, at least, multiplexing makes things more complex, but I'm getting ahead of myself).

To change the current working directory you must use the `cd` command, like so:

![Changing the current working directory to root, and running LS to prove it](/.gitbook/assets/LinuxForBeginners/cd-root.png)

Here I have changed the current working directory to the root directory, but as long as you know where the path of the file is you can move around anywhere you like, for example say I was in my home directory and had a subdirectory located at `Documents/Coursework/CMP209`, I can simply run the command `cd Documents/Coursework/CMP209` and voila.

As you can see above, also, the prompt (the thing before the cursor) also tells you what directory you're in. the `~` character is another name for your home directory.

## Creating and Removing Directories

Creating directories is as easy as `mkdir [directory name here]`. 

- Go to your home directory (type `cd` or `cd ~`)
- type `mkdir hacksoc`
- change directories into hacksoc by typing `cd hacksoc`
- Make some more directories of your choosing
  - you are able to pass multiple parameters into the `mkdir` command to make multiple directories in a single go, how neat
  - make sure not to put spaces in your directory names, however, as the command will interpret, for example `mkdir holiday pictures` as you telling it to make 2 directories called `holiday` and `pictures`

If you'd like to remove a directory, it's similarly very simple, the `rmdir` command can be used there! Say you made a directory called `cat-pics` that you didn't mean to make in that directory, simply type `rmdir cat-pics` to get rid of it!

Note: `rmdir` does not remove directories that contain files, we cover how to do this later on.

## More Powerful Navigation Stuff

We can also change directories using complete paths, say we're in the home directory and want to go elsewhere, we can type `cd hacksoc/subdirectory-1/subdirectory-2` to get there.

We already know that the tilde (`~`) is a symbol that's used in place of the home directory, but did you know there are other symbols we can use to navigate in Linux?

The most important of these is `..`, this means "up one directory", so lets say you're 2 directories deep into your newly created `hacksoc` directory, to get home and then move to the Documents directory, you can type `cd ../../Documents`. A single `.` represents the directory you're currently in.

You can also navigate relative to the home directory, say you're in the same position as earlier, you can just type `cd ~/Documents` to achieve the same thing.

A lot of the time, especially with the `cd` command, when you need to pass a parameter to an program that is a file path, you can hit the tab key to autocomplete, so `cd hac[TAB]` will autofill `cd hacksoc` for you

## Quick Overview of Directory Structure

You can use the `tree` command to generate a quick overview of the directory structure in any given directory. `tree` does not come pre-installed in most commonly used distros so to install it in ubuntu, type `sudo apt install tree` (if it doesn't work immediately run the command `sudo apt-get update && sudo apt-get upgrade`).

![An example of the tree command being used in our (fairly bare) home directory](/.gitbook/assets/LinuxForBeginners/tree.png)

## Creating and Removing Files

In Linux, there are many ways of creating a file. The first you should learn is the `touch` command. The intended effect of this command (to update time-related metadata) is fairly irrelevant, but a side effect of running the command on a file that doesn't exist yet is that it creates the file!

- `cd` into the `hacksoc` directory
- type `touch myInfo.txt`
- type `ls -al`

You should see the `myInfo.txt` file there! Note that file extensions are quite important in Linux so don't forget them!

![the touch command being used to create a new file](/.gitbook/assets/LinuxForBeginners/touch.png)

To remove the file you just created you can type `rm myInfo.txt`, but don't do it just yet, we need to learn how to edit text. Note also that using `rm -rf` (remove recursive force) will delete the contents of any directory you point it towards, as well as the directory itself. **DO NOT** run `rm -rf /`, that will delete everything. 

## Editing Text

There are, frankly, a shocking number of ways to edit text in Linux. These are roughly split into two types of ways to do so, terminal and GUI based applications. Here we will go over a few by using each of the programs below to add a single line of text to the `myInfo.txt` document. 

### CLI-Based

#### Pico/Nano

Pico and Nano are two of the simplest command line editors, and are often used for quick editing of configuration files. They are grouped together here because, whilst they do have differences, they are outwith the scope of this article, bear in mind, however, that nano is the more "advanced" of the two, and as such I will be using that for demonstration purposes.

To get started type `nano myInfo.txt` (hopefully using tab completion). You will be greeted with this screen:

![Nano's screen on startup](/.gitbook/assets/LinuxForBeginners/nano.png)

Once you're at this screen type "Name: " followed by your own name. To save press `Ctrl+O` (write Out) and hit enter when it prompts you for "File Name to Write", and to quit press `Ctrl+X` (eXit).

#### Vi/Vim

Vi and its successor Vim are *modal* editors, meaning there is some more complexity to editing files, but once you get the hang of it it often results in much higher text editing efficiency. Some really cute person [wrote an article on Vim for this wiki](../tools/vim.md) so check that out for more information.

Vim does not come pre-installed with many Linux distributions and can be installed through the same method mentioned earlier for `tree`. To begin editing with vim (or vi if vim is not installed) type `vi myInfo.txt`.

![Vim being used to edit the file](/.gitbook/assets/LinuxForBeginners/vim.png)

Vim is an entirely keyboard-based text editor, meaning all navigation is designed to be performed on keyboard. When you open vim you will be in what is called "normal mode", which allows for navigation. To go to the end of the line you can hit `$`, or use the right arrow key or the `l` key repeatedly. To insert text, use the `i` key and hit enter to create a new line. Alternatively, from normal mode you can simply hit `o` to automatically create a new line and be put into insert mode

Do this, now and type in `Student Number: " followed by your student number.

There are many *hilarious* memes about quitting vim but it's actually very easy. To save a file from vim, type `:w`. The `:` symbol puts you into command mode, and the `w` stands for "write". Follow this with `:q` for quit. You can also do this in one fluid motion, `:wq`.

### GUI-Based

#### Emacs

Emacs is a GUI and terminal based editor, it is extremely powerful (if inferior to vim #sorrynotsorry xoxox) editor with an absolute plethora of options and customisability.

Open our text file with `emacs myInfo.txt` and add "Favourite Animal: " followed by your favourite animal.

![Emacs being used to edit the file](/.gitbook/assets/LinuxForBeginners/emacs.png)

As an example of the absolute behemoth that Emacs is, from the editor press `esc` followed by `x`, and then type `tetris` because yes, there is an in-built tetris game, so you can procrastinate without even leaving your editor!

![Tetris in emacs (ignore the horrible score I'm not used to the controls)](/.gitbook/assets/LinuxForBeginners/emacs-tetris.png)

There are also other functions such as a psychotherapist and snake!

To exit emacs, perform `Ctrl+X` `Ctrl+C`

#### Others

Many Linux based systems (or more accurately, desktop environments like GNOME or KDE) have their own pre-installed text editor you can think of as being like Notepad in Windows. In Ubuntu that text editor is `gedit`. Open our file in gedit as you have done the three previous editors and finally add your favourite colour.

When done your final file should look something like this:

![Final edited file in gedit.](/.gitbook/assets/LinuxForBeginners/gedit.png)

Save and exit in gedit by hitting `Ctrl+S` and then hitting the `x` button in the top right hand corner.

Many other text editors are available on linux, including but not limited to 

- Kate
- Sublime Text
- VS Code
- Notepad++
- KWrite
- Ed (the original)

## Quick File Viewing

In Linux occasionally you want to see the contents of a text file without actually opening said file in an editor. The commands for you here are `cat`, `head`, and `tail`, which show the entire file, the first ten lines, and last ten lines respectively. Linux contains a dictionary of valid English words at `/usr/share/dict/words`, lets view this file like this.

What you will notice when using `cat` on this file is that it is incredibly long, and due to the fact that the Linux terminal has a set number of lines it can display at any given time it is impossible to see the top few lines. To do this we can type `head /usr/share/dict/words`.

![The head command running on /usr/share/dict/words](/.gitbook/assets/LinuxForBeginners/head.png)

And the end of the file? `tail /usr/share/dict/words`.

![The tail command running on /usr/share/dict/words](/.gitbook/assets/LinuxForBeginners/tail.png)

## Speeding Things Up and Getting Out Of Trouble

In addition to the tab completion we mentioned earlier, there are other ways of speeding up navigation and command line usage. Here are a few:

- The wildcard `!!` will run (or load) the previous command. This is particularly useful when you run a command that has to be ran as admin, in this case you can simply type `sudo !!` and the last command will be run using root.
- You can use the arrow keys to go back up one or multiple commands to re-find and run them.
- The `history` command will also give a full history of the commands you have previously run.
- Finally, you can repeat any command by typing `![num]` where `[num]` is the number of the command you wish to repeat

`Ctrl+C` is the shortcut for ending or killing processes if you've typed something wrong, to copy/paste from terminal use `Ctrl+Shift+V`. Additionally, `Ctrl+D` sends the `logout` command to the shell, if you wish to quit the terminal entirely (or if you've SSH'd into a box, but once again I'm getting ahead of myself)

## Copying and Moving Files

Copying and moving files from the command line can be achieved with the `cp` and `mv` commands. Let's test this out by copying and moving our `myInfo.txt` file.

- `cd` back into the `hacksoc/` directory if you haven't already
- Type `cp myInfo.txt myInfoCopy.txt` 
- Use `ls` and/or `cat myInfoCopy.txt` to see that a new file containing the same info has been generated
- Now type `mv myInfoCopy.txt talks/`, this will move `myInfoCopy.txt` into the `talks` directory
- Finally, `mv` can be used to rename the file, type `mv myInfo.txt [name]Info.txt` where `[name]` is your own first name 

The full set of steps carried out can be seen in the image below

![Copying and moving files in Linux](/.gitbook/assets/LinuxForBeginners/cp-mv.png)

## Hidden files

Due to an odd quirk of UNIX (on which Linux is based), that was actually originally a bug, Linux has the ability to hide files and directories if you prepend a `.` at the start of the file name. To demonstrate this, perform the following steps:

- Create a directory named `.hidden` (remember `mkdir`)
- type `ls` and note that it isn't there in the normal output
- type `ls -al` and note that it is, in fact, there (this also works with just `ls -a`, but not `ls -l`)

![A hidden file in Linux](/.gitbook/assets/LinuxForBeginners/hidden-file.png)

