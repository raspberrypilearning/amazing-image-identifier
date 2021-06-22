## Choose an application

This project is different to the previous machine vision projects, because it doesn’t tell you what to build or provide specific instructions on how to create a final product. Instead, you have the parts to create a product designed by you.

The next few steps explain the key components of a desktop application, web application, and command line tool. 

You can pick one of these types of applications to build and decide what you want it to do. Then it is time to use those pieces, along with the instructions on how to include a machine vision model, to build something cool!

### General tips

#### How to use library code
Libraries are collections of code written by other programmers. They have been packaged so you can install them easily and then include them in your own programs. Libraries that you may find useful for this project were installed when you ran the setup script.

To use library code, you need to use import statements to import it into your program, like this:
```python
from guizero import App, Button, Picture
import tensorflow as tf
```
You can use extra keywords, like `from` to include only parts of a larger library (to load faster), or `as` to rename a library with a longer name, so you don’t have to type it.

Usually, programmers try to put all of their imports at the start of their program, and keep all imports from the same library on the same line, separated by commas.

#### How to run programs
You can use the same command line interface (CLI) you used to install the software earlier to run a Python program, using the `cd` command to navigate to the directory of your program and then entering running it with the `python` command on Windows, or the `python3` command on macOS or Linux, like so:

```bash
python project.py
```

Make sure you replace `project.py` with whatever you call the file that you write your program in.
