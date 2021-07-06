## Build a web application
You can use the Flask library to create a Python-powered web application. While the library is very powerful, what’s included here are just the pieces that are most likely to be useful to you in building and running your machine-vision powered application. If you would like to learn more about Flask, check out our ['Build a Python web server with Flask'](https://projects.raspberrypi.org/en/projects/python-web-server-with-flask) project or review the [Flask documentation](https://flask.palletsprojects.com/).

--- collapse ---
---
title: Create an application
---

First you need to create an application. This only takes a couple of lines of code.

```python
from flask import Flask

app = Flask(__name__)
```

Flask applications use **routes** to define the URLs of the pages they create.

```python
@app.route(my_route)
def my_page():
    return page_content
```

 + `my_route` is a string that begins with a forward slash (for example, `/images`) and serves as the end of the URL for your page. The start of the URL is determined by your IP address, or domain name (if you deploy the site on the web). A `/` with no additional text as the route creates the home page for your site.
 + `page_content` is a string of text. It can include HTML, CSS, and JavaScript, as you’ll see below.

Once you’ve added a route to your application, you can add the `run` command to the end of the file to cause Flask to start serving your website when the program is run.

```python
app.run(debug=True, host='0.0.0.0')
```

Here is an example of a simple application that will run and serve a web page.
```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Hello world!"

app.run(debug=True, host="0.0.0.0")
```

Once you run this application, you can access your website. Simply enter `127.0.0.1:5000` into your browser's URL bar.
--- /collapse ---

--- collapse ---
---
title: Serve a web page
---
The response returned by your page functions can be more than a simple string of text. You can include HTML in the string, but be careful to avoid breaking the quotes around the string with quotes inside the HTML. Use single quotes in your HTML if you have used double quotes in Python or vice versa.

Here is an example of how you could include HTML in one of your route functions.
```python
@app.route("/")
def index():
    return """
    <!doctype html>
    <head>    
    <title>Image identifier</title>
    </head>
    <body>
    <h1>Amazing image identifier!</h1>
    <p>This application will identify images and tell you about their contents. Simply upload an image to see how it works.</p>
    </body>
    """
```

#### Include variables in your page
You can include Python variables in your HTML just as you can in any other string. For example:
```python
f"""
<!doctype html>
<h1>{article.title}</h1>
<p>{article.summary}</p>
"""
```
--- /collapse ---

--- collapse ---
---
title: Let users upload files
---

In order to use your web app to classify images, users need to be able to upload images to the app. To achieve this, you need an upload form and a function to handle the upload.

#### Create a form
This is the HTML for a short form that attempts to upload the supplied image through the POST method.
```html
<!doctype html>
   <h1>Upload new File</h1>
   <form method=post enctype=multipart/form-data>
     <input type=file name=image_to_classify>
     <input type=submit value=Upload>
   </form>
```


#### Handle the upload request and reroute the user
Once the form is submitted, it attempts to use the same route that created the form to process it. To handle this, the function associated with that route needs to be expanded to handle a POST request, save the image it is sent as part of that request, and reroute the user to a page that does something with the image.

You also need to define an upload folder as part while you create the upload page. **Make sure that this folder exists, as Flask cannot create it for you.**

```python
from flask import Flask, request, redirect, url_for
import os

# Define the upload folder for the app
app.config["UPLOAD_FOLDER"] = "static/uploads"

@app.route('/', methods=["GET", "POST"])
def upload_file():
    # Check if it's a POST request
    if request.method == "POST":
        # Get the image file from the request
        file = request.files["image_to_classify"]
        # Get the filename of the image
        filename = file.filename
        # Save the file into the upload folder so it can be used elsewhere
        file.save(os.path.join(app.config["UPLOAD_FOLDER"], filename))
        # Redirect the user to the "uploaded_file" function, 
        # passing it the filename of the file that was just saved
        return redirect(url_for("uploaded_file",
                                filename=filename))
    # If it's not a POST request
    else:
        return """
            <!doctype html>
            <h1>Upload new File</h1>
            <form method=post enctype=multipart/form-data>
                <input type=file name=image_to_classify>
                <input type=submit value=Upload>
            </form>
            """
```

#### Display the uploaded image
You also need to create a route and function that takes the uploaded image and does something with it. In the case of this project, the program needs to classify it and maybe fetch some additional data based on that classification, for example, from Wikipedia. The example below shows you how to display the image, but you can replace or extend that with whatever you do with the classification.

```python
from flask import Flask, url_for
import os

app.config["UPLOAD_FOLDER"] = "static/uploads"

@app.route('/uploads/<filename>')
def uploaded_file(filename):
    image_path = os.path.join(app.config["UPLOAD_FOLDER"], filename)
    image_url = url_for('static', filename=f"uploads/{filename}")
    return f"""
    <!doctype html>
    <img src='{image_url}' />
    """
```
--- /collapse ---


### Share your web app in a coding club

You can share your Flask web app with other computers on the same WiFi or network. To do this, you need to find your IP address, which you can do from the command line.

--- collapse ---
---
title: What is an IP address?
---
An IP address is a set of numbers that uniquely identifies your computer on a network and can be used to have one computer talk to another. An IP address is four sets of numbers, broken up by dots, like this: `192.168.86.229`.

The whole internet works based on computers using IP addresses to talk to each other — IP actually stands for Internet Protocol. Domain names like raspberrypi.org are just used to look up the right IP address, although they are a lot easier for people to remember!

The IP address you use for this project is called your **private IP address**, because it only works inside your local network. The entire network usually shares a single IP address for connecting to other computers over the internet.
--- /collapse ---

--- collapse ---
---
title: Find your IP address on Windows
---
In your command prompt, run this command:

```batch
ipconfig
```

You should get a lot of information back, but just find the line that begins with `IPv4 Address` — the number on that line is what you need.
--- /collapse ---

--- collapse ---
---
title: Find your IP address on macOS
---
In your terminal, run this command:

```bash
ipconfig getifaddr en1
```

The response is your IP address.
--- /collapse ---

--- collapse ---
---
title: Find your IP address on Linux (includes Raspberry Pi)
---
In your terminal, run this command:

```bash
hostname -I
```

The response is your IP address.
--- /collapse ---

--- collapse ---
---
title:  Share your app
---
Once you have your IP address, all other people on your network need to do is open their web browser and type your IP address followed by `:5000` into the address bar. For example, `192.168.86.229:5000` would work for a computer with that IP address.

--- /collapse ---
