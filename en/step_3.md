## Choose an application

In other machine vision projects, you were told what to build or received specific instructions on how to create a final product. In this project, you have the parts to create a product designed by you.

The next few steps explain the key components of a desktop application, web application, and command line tool. 

You can pick one of these types of applications to build and decide what you want it to do. Then it is time to use those pieces, along with the instructions on how to include a machine vision model, to build something cool!

#### How to use library code
Libraries are collections of code written by other programmers. They have been packaged so you can install them easily and then include them in your own programs. Libraries that you may find useful for this project were installed when you ran the setup script.

To use library code, you need to use `import` statements to move it into your program, like this:
```python
from guizero import App, Button, Picture
import tensorflow as tf
```
You can use extra keywords like `from` to include only parts of a larger library (to load faster). Or you could use `as` to rename a library with a longer name.

Usually, programmers try to put all of their imports at the start of their program, and keep all imports from the same library on the same line, separated by commas.

#### How to run programs
You can use the same command line interface (CLI) you used to install the software earlier to run a Python program. The `cd` command takes you to the directory of your program, then you can enter and run it with the `python` command on Windows, or the `python3` command on macOS or Linux, like so:

```bash
python project.py
```

Make sure you replace `project.py` with whatever you call the file that you write your program in.
