* There is a dictionary tool for macOS on Github, it's written in python, I need to make it executable and can be easily used with command line.
* the tool is an one-file script, to access macOS dictionary in python.
## step1: make it executable
use PyInstaller to accomplish this goal(mind the current working directory):
```
pip install PyInstaller
pyinstaller --onefile $pythonScriptName.py
```
after this, an executable file will be created in the dist folder
## step2: add it to PATH
in my zsh shell, modify .zshrc, add one line in it:
```
export PATH="{dist file path}:$PATH"
```
then
```
source .zshrc
```
done, {pythonScriptName} can be called in command line