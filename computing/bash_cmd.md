---
title: Bash and Command line
parent: Computing
---


# Bash and Linux command line
BASH (or Bourne against Shell) is the basic command line interpteter for the UNIX-based operation systems (Like MacOS, or Linux). Most of the apps and scripts used in the lab are based on Bash.

The [University of Toronto Coders](https://uoftcoders.github.io/studyGroup/lessons/misc/bash-intro/lesson/) have a great tutorial lesson where they cover basic aspects of interacting with computer and file system using BASH.

### Shell-command cheat sheet
Here you can find the most frequently used BASH commands.
| Shell command | action |
|:------------|:-------------|
| pwd | present working directory |
| ls [dir] | list the directory contents |
| mkdir _dir_ | create a directory |
| cd [dir] |  change directory |
| man _cmd_ | command’s man page |
| echo arg | echo the argument |
| source _file_ | run the cmds in _file_ |
| cp _file1_ _file2_ | copy a file |
| mv _file1_ _file2_ | move/rename a file |
| rm _file_ | delete a file |
| wc _file_ | word count data of file |
| grep _arg_ _file_ |search for arg in file |
| rmdir _dir_ | delete a directory |
| history _[num]_ | print the shell history |
| file _file_ |  type of file |
| more _file_ | scroll through file |
| less _file_ | scroll through file |
| cat _file_ | print the file contents |
| cmd > _file_ | redirect output to file |
| cmd >> _file_ | append output to file |
| cmd < _file_ | use file as input to cmd |
| head _file_ | print first 10 lines of file |
| tail _file_ |print last 10 lines of file |
| curl _url_ | downloads the url |
| tar _file_ | handles tar files |
| sort _file_ | sorts the lines of file |
| cut _flags_ _output_ | cut part of output |
| for..do..done | for loop in bash |
| if..then..fi | if statement in bash |
| tail -f _filename_ | tail the log file (useful for the sbatch cluster jobs) |
| logout | close the terminal session |
