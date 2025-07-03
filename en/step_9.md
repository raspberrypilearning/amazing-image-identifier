## Do something with the classification

Once you have the image and have used your machine vision model to identify it, you need to do something with it. Below are a few suggestions, but you can make whatever you want!

### Output the classification to the user

--- collapse ---
---
title: Print it out as text
---

If you have built a command line tool, you can print the classification out with the print function. This creates a useful tool that can easily be connected to other command line tools to achieve more complex goals.

--- /collapse ---

--- collapse ---
---
title: Use a text field in a desktop application
---

You can display the classification in a desktop application with a `Text` or `TextBox` widget. You can also use a `Picture` widget to display the image itself. 
--- /collapse ---

--- collapse ---
---
title: Display it on a web page
---

If you’ve built a web application, you can display the classification on a web page. You can also display the image itself on the web page with the `img` HTML tag.

--- /collapse ---

--- collapse ---
---
title: Have the computer speak it
---
With the `pyttsx3` library, you can use a few quick library commands to have the computer read out the classification, or any text you want. Think how useful that could be for someone who might have difficulty seeing an image!

```python
import pyttsx3

# Create a text-to-speech engine
engine = pyttsx3.init()

# Tell the engine what to say
engine.say("Hello world!")

# Have the engine say it, 
# and have your program wait until it finishes
engine.runAndWait()
```
--- /collapse --- 

### Get some more information about the classification
Users might want to know more about the object in the image they have asked your program to identify for them. You can help them with a search of Wikipedia for the classification your model returns. Conveniently, there is a Python library for doing exactly this! You can see below how to use it to fetch information on your classification. You then need to combine this information with one of the forms of output to share it with your user.

```python
import wikipedia as wiki

article = wiki.page(classification)

# At this point you could print out article, 
# to see all of the data that you get back 
# and pick some pieces you'd like to work with

# Get the title and some short details 
# from the Wikipedia article
title = article.title
details = article.summary
```
