What is **metaprogramming**, it was the best collective term we could come up with for the set of things that are more about **process** than they are about writing code or working more efficiently. It also means **programs that operate on programs**.
### Build systems 
For most projects, whether they contain code or not, there is a "build process". Some sequence of operations you need to do to go from your inputs to your outputs. Often, that process might have many steps, and many branches. 

You define a number of **dependencies**, a number of **targets**, and **rules** for going from one to the other. You tell the **build system** that you want a particular target, and its job is to find all the transitive dependencies of that target, and then apply the rules to produce intermediate targets all the way until the final target has been produced.

`make` is one of the most common build systems out there. It works quite well for **simple-to-moderate** projects. When you run `make`, it consults a file called `makefile` in the current directory. All the targets, their dependencies, and the rules are defined in this file.
Create a file named `makefile`, add below stings to it:
```shell
paper.pdf: paper.tex plot-data.png
plot-%.png: %.dat plot.py
```
The things named on the right-hand(right of the `:`) are dependencies, and the left-hand side is the target. The first directive defines the **default** goal, so if we run `make` without arguments:
```shell
make
make: *** No rule to make target `paper.tex', needed by `paper.pdf'.  Stop.
```
And then:
```shell
(base) ➜  code touch paper.tex
(base) ➜  code make
make: *** No rule to make target `plot-data.png', needed by `paper.pdf'.  Stop.
```
Let's create all the files:
```shell
$ cat paper.tex
\documentclass{article}
\usepackage{graphicx}
\begin{document}
\includegraphics[scale=0.65]{plot-data.png}
\end{document}
$ cat plot.py
#!/usr/bin/env python
import matplotlib
import matplotlib.pyplot as plt
import numpy as np
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('-i', type=argparse.FileType('r'))
parser.add_argument('-o')
args = parser.parse_args()

data = np.loadtxt(args.i)
plt.plot(data[:, 0], data[:, 1])
plt.savefig(args.o)
$ cat data.dat
1 1
2 2
3 3
4 4
5 8
```
And `make` again:
```shell
$ make
./plot.py -i data.dat -o plot-data.png
pdflatex paper.tex
... lots of output ...
```
### Dependency management
