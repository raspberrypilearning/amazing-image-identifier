## Build a desktop application

[The guizero website](https://lawsie.github.io/guizero/start/) has full documentation on how to use the `guizero` library, and all of the application components — which are called widgets. A few of the most relevant ones have been included here for you to use.

--- collapse ---
---
title: Create an app
---
When creating a program with guizero, you must use an App widget to create your app. This widget creates an empty app, with no content or controls.

The code below shows how to create this app and make it appear with the `display()` function.
```python
from guizero import App
app = App()
app.display()
```

#### Give your app a title
You can give your app a title using the title property when you create it.
```python
from guizero import App
app = App(title="My app")
```
You can also set, or change, the app title after you have created the app. You just need to change the app’s title property.
```python
from guizero import App
app = App(title="My app")
app.title = "New title"
```

#### Change the size of your app
Just like the title, you can set these properties at the start of your project, or update them afterwards. They are integer values, which means that they refer to the number of pixels in the width and height of the app.
```python
from guizero import App
app = App(height=300, width=200)
app.height = 500
app.display()
```
--- /collapse ---

--- collapse ---
---
title: Get an image from users
---
To classify an image, your app needs to have the path to an image file. In guizero, there is a built-in file picker.

```python
from guizero import App
app = App()
app.display()
image_path = app.select_file()
```

The `select_file()` function gives users a standard file picker for their operating system and then returns the path to the file they select. 
--- /collapse ---

### Add widgets to your app
Below is a collection of widgets you might want to use in your app. Note that you must add the widgets before you call the `display()` function.

--- collapse ---
---
title: PushButton
---
This widget creates a button that users can click. The button can be connected to a function to trigger behaviour in response to user actions.

#### Add a `PushButton` widget

The code below shows you how to use guizero's `PushButton` widget to add a button to an application. 
```python
from guizero import PushButton
my_button = PushButton(container, command=my_function)
```
 + `container` is the widget you want to add the image inside of. This can be an App, [Box](https://lawsie.github.io/guizero/box/), or [Window](https://lawsie.github.io/guizero/window/) widget.
 + `my_function` is the name of a function elsewhere in your program that does something you want to happen when the button is clicked.

Below is an example of a simple application that uses the `PushButton` widget.

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

#### Add a `Picture` widget
The code below shows you how to add an image to an application using guizero’s `Picture` widget.
```python
from guizero import Picture

my_image = Picture(container, image=image_path)
```

 + `container` is the widget to use for the image. This can be an App, [Box](https://lawsie.github.io/guizero/box/), or [Window](https://lawsie.github.io/guizero/window/) widget.
 + `image_path` is a string that gives the path to your image.

Below is an example of a simple application that uses the `Picture` widget.
```python
from guizero import App, Picture
my_app  = App()
my_image = Picture(my_app, image="pictures/my_picture.jpg")
my_app.display()
```

#### Update a `Picture` widget
To update an image in your application, you can modify its image property.
```python
from guizero import Picture

my_image = Picture(container, image=image_path)
my_image.image = new_image_path
```

 + `new_image_path` is a string that gives the path to the image that you want to use to update the original image.

Below is an example of how you might update an image based on user input.

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
This widget displays a single line of text. If you want to display multiple lines of text, look at the `Textbox` widget below.

#### Add a `Text` widget
The code below shows you how to add a line of text to an application using guizero’s `Text` widget.
```python
from guizero import Text

my_text = Text(container, text=display_text)
```
 + `container` is the widget you want to add the image inside of. This can be an App, [Box](https://lawsie.github.io/guizero/box/), or [Window](https://lawsie.github.io/guizero/window/) widget.
 + `display_text` is a string that gives the text to display.


Below is an example of a simple application that uses the `Text` widget.
```python
from guizero import App, Text

my_app  = App()
my_text = Text(my_app, text=“Hello World!”)
my_app.display()
```

#### Update a `Text` widget
To update a `Text` widget in your application, you can modify its value property.

```python
from guizero import Text

my_text = Text(container, text=display_text)
my_text.value = new_display_text
```
 + `new_display_text` is a string that gives the new text to display.


Below is an example of how you might update text based on user input.
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
This widget is a box of text. You can use it as a place for users to enter one or more lines of text, or as a way to display multiple lines of text. The examples below focus on how to display text, but you can refer to the details in the guizero documentation if you want to learn how to use it to allow users to enter text.

#### Add a `TextBox` widget
The code below shows you how to add multiple lines of text to an application using guizero’s `TextBox` widget.

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
 + The `multiline` property tells the `TextBox` whether or not to display multiple lines of text.
 + The `enabled` property tells the `TextBox` whether or not its content can be modified.
 + The `scrollbar` property tells the `TextBox` whether or not to display a scrollbar.
 + `display_text` is a string that gives the text to display.

Below is an example of a simple application that uses the `TextBox` widget.

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

#### Update a `TextBox` widget
To update a `TextBox` widget, you need to make it modifiable, empty it, add new contents, and then make it unmodifiable again. 

Of course, if you use a user-editable text box, then you don’t need to change the enabled property at all (it will already be modifiable).

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


Below is an example of how you might update the text box based on user input.
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
