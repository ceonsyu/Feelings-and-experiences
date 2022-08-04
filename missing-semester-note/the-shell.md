---
description: personal note of missing-semester lecture1
---

# The shell

### What is the Shell

* Textual interface of all platforms we can get our hand on. Shell allows us to run programs, give them input, and inspect their output

### Using the shell

To open a shell prompt, we need a terminal like:

![](<.gitbook/assets/截屏2022-08-03 下午5.21.34.png>)

a prompt often looks like:&#x20;

```shell
missing:~$
```

it tells you that you are on the machine `missing` and current working directory(`~`, short for "home"). The `$`  tells you that you are not the root user. In occasionally, the machine name and `$` will be omitted, that is:

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

### **Navigating in the shell**

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
