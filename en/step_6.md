## Build a command line tool
A command line tool is a program that is intended to run in the command prompt, or terminal, of your computer. It accepts user inputs, does something with them, and produces outputs. In the case of this project, a command line tool could identify an image or take that identification and use it to fetch information from the web, or it could do any other task you like.

### Parsing arguments
The only specialised piece of code needed to write a command line tool is code to parse those arguments and make them accessible to your program.

To parse arguments, Python uses the argparse library, which is built in to the language. While there is a lot you can do with this library, this project only addresses a small number of the features that are likely to be of the most use to you. If you want to learn more about the library, you can read [its documentation](https://docs.python.org/3/library/argparse.html).

--- collapse ---
---
title: What are arguments?
---

Arguments are extra pieces of information that you pass to the program when you run it, like this:

```bash
python3 my_program.py images/my_image.png -s wikipedia
```

In this case, the program is passed two arguments:
 + `images/my_image.png` is a positional argument. The program knows what the argument is by where it is positioned in the list of arguments provided.
 + `-s wikipedia` is a flagged argument. Flagged arguments always begin with a minus sign, followed by a text string (often a single letter). This helps the user to identify the argument in use. Then, if necessary, the user can provide additional input to the argument to instruct the program to search, this is where the `s` comes from. In this case, the user instructs the program to search Wikipedia for an entry about the classification result. Flagged arguments are optional by convention.

--- /collapse ---

--- collapse ---
---
title: Create an argument parser
---

To parse arguments, you need to import and create an `ArgumentParser`, like this:

```python
from argparse import ArgumentParser

parser = ArgumentParser()
```
--- /collapse ---

--- collapse ---
---
title: Add arguments to your program
---

Once it is created, you need to add each argument used by your program to the parser.
```python
parser.add_argument(argument_name,
                    help=argument_help,
                    type=value_type)
```
 + `argument_name` is a string that gives the name of the argument. This string also decides whether the argument is positional, or flagged, by whether it begins with a minus. For example, `image_path` would be positional, while `-search` would be flagged.
 + `argument_help` is a string that describes what the argument does and the types of values it expects.
 + `value_type` is a Python data type. The parser treats arguments as strings by default. So, if you want to take in a string, you do not need to include a type parameter. If you want to take in values of other types, you need to specify the expected type here. There are a lot of options, but the ones you might need are:
    + `pathlib.Path` — the path to a file
    + `int` — an integer
    + `float` — a floating-point number (a number with a decimal point)

Below is an example of how you might create a parser and add some suitable arguments to it.

```python
from argparse import ArgumentParser

parser = ArgumentParser()
parser.add_argument("image",
                    help="The image you want identified",
                    type=pathlib.Path)
parser.add_argument("-s",
                    help="Where to lookup image details")
```
--- /collapse ---

--- collapse ---
---
title: Get arguments from the parser
---
Once you have added all the arguments you need, you should read them and use them elsewhere in your program.

First, you need to parse the arguments into a variable. You can work on this with the code below:

```python
args = parser.parse_args()
```
+ `parser` is an argument parser created by you

Once completed, your variable contains an object that has properties that match each of the argument names set by you. You can access these properties through the dot operator. For example, you would access a property called `image` like this:

```python
image = args.image
```

Below is an example of how you can create an argument and fetch its value into a variable.

```python
from argparse import ArgumentParser

parser = ArgumentParser()
parser.add_argument("image",
                    help="The image you want identified",
                    type=pathlib.Path)

args = parser.parse_args()

image = args.image
```
--- /collapse ---
