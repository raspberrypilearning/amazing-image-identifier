## Choose an application

This project is a bit different to the previous machine vision projects, in that it doesn’t tell you what to build, or provide specific instructions on how to create a particular final product. Instead, you’re given the parts to create a product that you design.

Over the next few pages, the key components of a desktop application, web application, and command line tool are explained. 

Pick one of these types of applications to build, decide what it’s going to do, and then use those pieces, along with the instructions on how to include a machine vision model, to build something cool!

### General tips

#### Using library code
Libraries are collections of code written by other programmers, which have been packaged so you can easily install them and then include them in your own programs. Several libraries you might find useful for this project were installed when you ran the setup script.

To use library code, you need to import it into your program, using import statements, like this:
```python
from guizero import App, Button, Picture
import tensorflow as tf
```
Note that you can use extra keywords, like `from` to include only parts of a larger library (to load faster), or `as` to rename a library with a longer name, so you don’t have to keep typing it.

Usually, programmers try to put all of their imports at the start of their program, and keep all imports from the same library on the same line, separated by commas.

#### Running programs
Using the same command line interface (CLI) you used to install the software earlier, you can run a Python program by using the `cd` command to navigate to the directory your program is in and then entering running it with the `python` command on Windows, or the `python3` command on Mac OS or Liunx, like so:

```bash
python project.py
```

But replace `project.py` with whatever you call the file you're writing your program in.