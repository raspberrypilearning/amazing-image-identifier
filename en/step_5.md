## Build a desktop application

Full documentation on using the guizero library, and all of the application components (which guizero calls widgets) it comes with, is [available on the guizero site](https://lawsie.github.io/guizero/start/), but a few of the most relevant have been included here for easy reference.

--- collapse ---
---
title: Creating an app
---
When creating a program with guizero, you must use an App widget to create your app. This widget creates an empty app, with no content or controls.

The code below shows how to create such an app, and make it appear with the `display()` function.
```python
from guizero import App
app = App()
app.display()
```

#### Giving your app a title
You can give your app a title using the title property when creating it.
```python
from guizero import App
app = App(title="My app")
```
You can also set, or change, the app title after you have created the app by changing the app’s title property.
```python
from guizero import App
app = App(title="My app")
app.title = "New title"
```

#### Changing the size of your app
Just like the title, you can set these properties at creation, or update them afterwards. They are integer values, and refer to the number of pixels in the width and height of the app.
```python
from guizero import App
app = App(height=300, width=200)
app.height = 500
app.display()
```
--- /collapse ---

--- collapse ---
---
title: Getting an image from users
---
To classify an image, your app will need to have the path to an image file. Guizero gives you an easy to use built-in file picker, which works like this.

```python
from guizero import App
app = App()
app.display()
image_path = app.select_file()
```

The `select_file()` function gives users a standard file picker for their operating system, and then returns the path to the file they select. 
--- /collapse ---

### Adding widgets to your app
The following is a collection of widgets you might want to use in your app. Note that you must add the widgets before calling the display() function.

--- collapse ---
---
title: PushButton
---
This widget creates a button that users can click. The button can be connected to a function, to trigger behaviour in response to user actions.

#### Adding a PushButton widget

The code below shows you how to add a button to an application using guizero’s PushButton widget.
```python
from guizero import PushButton
my_button = PushButton(container, command=my_function)
```
 + `container` is the widget you want to add the image inside of. This can be an App, [Box](https://lawsie.github.io/guizero/box/), or [Window](https://lawsie.github.io/guizero/window/) widget.
 + `my_function` is the name of a function elsewhere in your program that does something you want to happen when the button is clicked.

Here’s an example of a simple application using the PushButton widget:

```python
from guizero import App, PushButton

def log_button_press():
    print("Button pressed")

my_app  = App()
my_button = PushButton(container, command=log_button_press)
my_app.display()
```
--- /collapse ---


--- collapse ---
---
title: Picture
---
This widget displays an image in the .png, .gif, or .jpg file format.

#### Adding a Picture widget
The code below shows you how to add an image to an application using guizero’s Picture widget.
```python
from guizero import Picture

my_image = Picture(container, image=image_path)
```

 + `container` is the widget you want to add the image inside of. This can be an App, [Box](https://lawsie.github.io/guizero/box/), or [Window](https://lawsie.github.io/guizero/window/) widget.
 + `image_path` is a string that gives the path to your image.

Here’s an example of a simple application using the Picture widget:
```python
from guizero import App, Picture
my_app  = App()
my_image = Picture(my_app, image="pictures/my_picture.jpg")
my_app.display()
```

#### Updating a  Picture widget
You can update an image in your application by modifying its image property, as shown:
```python
from guizero import Picture

my_image = Picture(container, image=image_path)
my_image.image = new_image_path
```

 + `new_image_path` is a string that gives the path to the image you want to update to.

Here’s an example of how you might update an image based on user input:

```python
from guizero import App, Picture

my_app  = App()
my_image = Picture(my_app, image="pictures/my_picture.jpg")
my_app.display()

# After the app has loaded, 
# get the location of a new image from the user
new_image_path = get_new_image_from_user()
my_image.image = new_image_path
```
--- /collapse ---

--- collapse ---
---
title: Text
---
This widget displays a single line of text. If you want to display multiple lines of text, look at the Text box widget, below.

#### Adding a Text widget
The code below shows you how to add a line of text to an application using guizero’s Text widget.
```python
from guizero import Text

my_text = Text(container, text=display_text)
```
 + `container` is the widget you want to add the image inside of. This can be an App, [Box](https://lawsie.github.io/guizero/box/), or [Window](https://lawsie.github.io/guizero/window/) widget.
 + `display_text` is a string that gives the text to display.


Here’s an example of a simple application using the Text widget:
```python
from guizero import App, Text

my_app  = App()
my_text = Text(my_app, text=“Hello World!”)
my_app.display()
```

#### Updating a Text widget
You can update a Text widget in your application by modifying its value property, as shown:

```python
from guizero import Text

my_text = Text(container, text=display_text)
my_text.value = new_display_text
```
 + `new_display_text` is a string that gives the new text to display.


Here’s an example of how you might update Text based on user input:
```python
from guizero import App, Text

my_app  = App()
my_text = Text(my_app, text="Hello World!")
my_app.display()

# After the app has loaded, get some new text from the user
new_display_text = get_new_text_from_user()
my_text.value = new_display_text
```
--- /collapse ---

--- collapse ---
---
title: TextBox
---
This widget is a box of text. It is useable both as a place for users to enter one or more lines of text, or as a way to display multiple lines of text. The examples below will focus on displaying text, but you can refer to the details in  the guizero documentation if you want to learn how to use it to allow users to enter text.

#### Adding a TextBox widget
The code below shows you how to add multiple lines of text to an application using guizero’s TextBox widget.

```python
from guizero import TextBox

my_text_box = TextBox(container,
                      multiline=True,
                      enabled=False,
                      scrollbar=True,
                      text=display_text
                      )
```

 + `container` is the widget you want to add the image inside of. This can be an App, [Box](https://lawsie.github.io/guizero/box/), or [Window](https://lawsie.github.io/guizero/window/) widget.
 + The `multiline` property tells the TextBox whether or not to display multiple lines of text.
 + The `enabled` property tells the TextBox whether or not its content can be modified
 + The `scrollbar` property tells the TextBox whether or not to display a scrollbar
 + `display_text` is a string that gives the text to display.

Here’s an example of a simple application using the Text widget:

```python
from guizero import App, TextBox

my_app  = App()
my_text_box = TextBox(my_app, 
                      multiline=True, 
                      enabled=False, 
                      scrollbar=True, 
                      text="Hello World!")
my_app.display()
```

#### Updating a TextBox widget
Updating a TextBox widget requires making it modifiable, emptying it, adding new contents, and then making it unmodifiable again. 

Of course, if you’re using a user-editable TextBox, then you don’t need to change the enabled property at all, as it will already be modifiable.

```python
from guizero import TextBox

my_text_box = TextBox(container,
                      multiline=True,
                      enabled=False,
                      scrollbar=True,
                      text=display_text
                      )
my_text_box.enable()
my_text_box.clear()
my_text_box.append(new_display_text)
my_text_box.disable()
```
 + `new_display_text` is a string that gives the new text to display.


Here’s an example of how you might update TextBox based on user input:
```python
from guizero import App, TextBox

my_app  = App()
my_text_box = TextBox(my_app, 
                      multiline=True, 
                      enabled=False, 
                      scrollbar=True, 
                      text="Hello World!")
my_app.display()

# After the app has loaded, get some new text from the user
new_display_text = get_new_text_from_user()

my_text_box.enable()
my_text_box.clear()
my_text_box.append(new_display_text)
my_text_box.disable()
```
--- /collapse ---
