## Build a command line tool
A command line tool is a program that is intended to run in the command prompt, or terminal, of your computer. It accepts user inputs, does something with them, and produces outputs. In the case of this project, that could be a tool that identifies an image, or takes that identification and uses it to fetch information from the web, or do any other task you can think of.

### Parsing arguments
The only specialised piece of code you’ll need to write a command line tool is code to parse those arguments and make them accessible to your program.

To parse arguments, Python uses the argparse library, which comes built-in to the language. While there is a lot you can do with this library, this project will only address a small number of the features that are likely to be of the most use to you. If you want, you can learn more about the library by reading [its documentation](https://docs.python.org/3/library/argparse.html).

--- collapse ---
---
title: What are arguments?
---

Arguments are extra pieces of information that you pass to the program when you run it, like this:

```bash
python3 my_program.py images/my_image.png -s wikipedia
```

In this case, the program is being passed two arguments:
 + `images/my_image.png` is a positional argument — the program knows what the argument is by where it is positioned in the list of arguments provided.
 + `-s wikipedia` is a flagged argument. Flagged arguments always begin with a minus sign, followed by a text string, often a single letter. This lets the user identify which argument they are using. Then, if necessary, they can provide additional input to the argument — in this case `wikipedia`, instructing the program to search (which is where the `s` comes from) wikipedia for an entry about the classification result. Flagged arguments are, by convention, optional.

--- /collapse ---

--- collapse ---
---
title: Creating an argument parser
---

To parse arguments, you will need to import and create an ArgumentParser, like so.

```python
from argparse import ArgumentParser

parser = ArgumentParser()
```
--- /collapse ---

--- collapse ---
---
title: Adding arguments to your program
---

Once it’s created, you will need to add each argument your program uses to the parser.
```python
parser.add_argument(argument_name,
                    help=argument_help,
                    type=value_type)
```
 + `argument_name` is a string that gives the name of the argument. This string also decides whether the argument is positional, or flagged, by whether it begins with a minus. For example `image_path` would be positional, while `-search` would be flagged.
 + `argument_help` is a string describing what the argument does, and the types of values it expects.
 + `value_type` is a Python data type. The parser treats arguments as strings by default. So, if you want to take in a string, you don’t need to include a type parameter. If you want to take in values of other types, you will need to specify the expected type here. There are a lot of these, but the ones you might need are:
    + `pathlib.Path` — the path to a file
    + `int` — an integer
    + `float` — a floating point number (a number with a decimal point)

Here’s an example of how you might create a parser and add some suitable arguments to it.

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



