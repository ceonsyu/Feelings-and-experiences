---
Description: personal note of missing-semester lecture2
---
# Shell Tools and Scripting
## Shell scripting
### variables and Strings
To assign variables in bash, use the syntax `foo=bar` and access the value of the variable with `$foo`. Note that `foo = bar` won't work since it is interpreted as calling the `foo` program with arguments `=` and `bar`.  
**In general, in shell scripts the space character will perform argument splitting**
```shell
➜  ~ foo=bar
➜  ~ echo "$foo"
bar
➜  ~ echo '$foo'
$foo
```
NOTE: Strings in bash can be defined with `'` or `"`, but there is difference between them. Inside `'`, everything will be interpreted as Strings, but inside `"`, some special variables referring to arguments will stay special, such as `$`.  
### Command substitution and process substitution
Bash supports control flow techniques, and has functions that take arguments and can operate with them. Such as:
```shell
mcd(){
    mkdir -p "$1"
    cd "$1"
}
```
Here `$1` is the first argument to the function, similarly, `$2` is the second and so on.  

The return code or exit status is the way scripts have to communicate how execution went. A value of 0 usually means everything went ok. Exit codes can be used to conditionally execute commands using `&&` and `||`. The `true` program will always have a 0 return code and the `false` program will always have 1 return code.  

About getting the output of a command as a variable, It can be done with **command substitution**, which usually can be done using `$`. For example, if I do `for file in $(ls)`, the shell will first call `ls` and then iterate over those values. Except for command substitution, another similar feature is **process substitution**. This is useful when commands expect values to be passed by file instead of by STDIN. For example, `diff <(ls foo) <(ls bar)` will show differences between files in dirs `foo` and `bar`.
```shell
➜  ~ diff <(ls IdeaProjects) <(ls code)
1,4c1,10
< k8s-model-deploy-demo
< maven-test
< s3-download-test
< test-IDEA
---
> bdd56b25a5f547599f7f
> dtreeviz-demo
> dtreeviz-master
> git-test
> git-test2
> qd-ha
> qdha2
> regression
> xcode-demo
> ymals
```
`grep`(global search regular expression and print out the line)
```shell
grep [options] [pattern] file
     -i: ignore case
     -o: print only the matched parts of a matching line
```
### Shell globbing（通配符）
- Wildcards-Using `?` and `*` to match one or any amount of characters respectively. For instance, given files `foo`, `foo1`, `foo2`, `bar`, the command `rm foo?` will delete`foo1`, `foo2` whereas `rm foo*` will delete all but `bar`.
- Curly braces `{}`-It can expand common substring in a series of commadns automatically. Like:
```shell
convert image.{png,jpg}
# Will expand to :
convert image.png image.jpg
```
Curly braces and wildcards can be used together.
### Shebang(#!)
```shell
#!/user/local/bin/python
import sys
for arg in reversed(sys.argv[1:]):
    print(arg)
```
The kernel knows to execute this with a python interpreter instead of a shell command because we included a `shebang` line at the top op the script. `env` command and the `PATH` environment is good practice of shebang lines.
### Something should keep in mind:
- Functions have to be in the same language as the shell, while scripts can be written in any language.
- Functions are loaded once when their definition is read. Scripts are loaded every time they are executed.
- Functions are executed in the current shell environment whereas scripts execute in their own process. Thus, functions can modify environment variables, e.g, change current directory. 
## Shell Tools
### Finding how to use commands
The first-order approach is to call said command with the `-h` or `--help` flags. A more detailed approach is to use the `man` command to open the manpage of command, short for manual page.  
Sometimes manpage may make it hard to decipher what flags/syntax to use. [TLDR pages](https://tldr.sh).
```shell
#Cannot success inside the wall without VPN.
 ~ tldr cat

  cat

  打印和拼接文件的工具。
  更多信息：https://www.gnu.org/software/coreutils/cat.

  - 以标准输出，打印文件内容：
    cat file

  - 多文件合并到目标文件：
    cat file1 file2 > target_file

  - 多文件合并，并追加到目标文件：
    cat file1 file2 >> target_file

  - 显示行号：
    cat -n file

  - 显示不可打印和空白的字符（使用 `M-` 前缀标记非 ASCII 字符）：
    cat -v -t -e file
```
### Finding files
`find`, `fzf`, `fd`, `locate` and so on.
### Finding code
`grep`. A generic tool for matching patterns from the input text. Many flags that make it very versatile tool. Such as `-C`(get context around the matching line), `-v`(invert the match), `-R`(recursively go into directories). `ag` is a `grep` alternative. 
### Finding shell commands
`history`, UP/DOWN in `zsh`, `fish` and so on.

