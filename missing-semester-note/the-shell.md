---
description: personal note of missing-semester lecture1
---

# The shell

### What is the Shell

* Textual interface of all platforms we can get our hand on. Shell allows us to run programs, give them input, and inspect their output

### Using the shell

To open a shell prompt, we need a terminal like:

![](../.gitbook/assets/%E6%88%AA%E5%B1%8F2022-08-03%20%E4%B8%8B%E5%8D%885.21.34.png)
a prompt often looks like:&#x20;

```shell
missing:~$
```

It tells you that you are on the machine `missing` and current working directory(`~`, short for "home"). The `$` tells you that you are not the root user. In occasionally, the machine name and `$` will be omitted, that is:

```
~
```

We can execute a command wit arguments:

```
~ echo hello
hello
```

In this case, we told the shell to execute the program `echo` with the argument `hello`. The `echo` program simply prints out its argument.

**The shell parses the command by splitting it by whitespace.** 

When you run commands in your shell, you are really writing a small bit of code that your shell interprets. If the shell is asked to execute a command that doesn’t match one of its programming keywords, it consults an **environment variable** called `$PATH` that lists which directories the shell should search for programs when it is given a command.

### Navigating in the shell

* A path on shell is a list of directories separated by `/` on linux and macOS, by `\` on windows.&#x20;

The path `/` is the root of the file system on linux and macOS. Windows has one root for each disk partition(like `C:\`). We can see the current working directory with the `pwd` command and change it with `cd` .&#x20;

We can use `ls` to print the contents of the current directory, `ll`  to print it with long listing format:

```shell
(base) ➜  code ls
bdd56b25a5f547599f7f dtreeviz-demo        dtreeviz-master      qd-ha                regression           xcode-demo
(base) ➜  code ll
total 0
drwxr-xr-x   8 qinshunong1  staff   256B  8  3 13:50 bdd56b25a5f547599f7f
drwxr-xr-x  20 qinshunong1  staff   640B  7 28 15:51 dtreeviz-demo
drwxrwxr-x@ 16 qinshunong1  staff   512B  7 28 15:06 dtreeviz-master
drwxr-xr-x  14 qinshunong1  staff   448B  8  1 18:33 qd-ha
drwxr-xr-x   5 qinshunong1  staff   160B  7 27 16:31 regression
drwxr-xr-x   7 qinshunong1  staff   224B  7 27 00:13 xcode-demo
```

In this case, `(base)` is my python virtual environment, `code` is the current working directory. 

what dose `drwxr-xr-x` mean: 

* `d`  --> this file is a directory 
* `rwx` --> read, write, execute. Only for the owning group

some other handy programs: 

`mv`:to rename/move a file, `cp`:to copy a file, `mkdir`:to make a new directory, `man`:to show manpage of a command.
### Connecting programs
In the shell, programs have two primary "streams" associated with them: input stream and output stream. Normally, a program's input and output are both our terminal. However we can also rewire those streams. The simplest form of redirection is `< file` and `> file`:
```shell
➜  ~ echo hello > hello.txt
➜  ~ cat hello.txt
hello
➜  ~ cat < hello.txt
hello
➜  ~ cat < hello.txt > hello2.txt
➜  ~ cat hello2.txt
hello
```
`cat` prints the contents of each of the files in sequence to its output stream. But when `cat` is not given any argument, it prints contents from its input stream to its output stream, like in the third example.
**Where this kind of input/output redirection really shines is in the use of `|`. The `|` operator lets us "chain" programs such that the output of one is the input of another.**