## Build a web application
You can create a Python-powered web application using the Flask library. While the library is very powerful, what’s included here are just the pieces that are most likely to be useful to you in building and running your machine-vision powered application. If you’d like to learn more about Flask, check out either the [Build a Python Web Server with Flask](https://projects.raspberrypi.org/en/projects/python-web-server-with-flask) project elsewhere on this site, or the [Flask documentation](https://flask.palletsprojects.com/).

--- collapse ---
---
title: Creating an application
---

The first thing you need to do in Flask is create an application. This only takes a couple of lines of code.

```python
from flask import Flask

app = Flask(__name__)
```

Flask applications use “routes” to define the URLs of the pages they create.

```python
@app.route(my_route)
def my_page():
    return page_content
```

 + `my_route` is a string, beginning with a forward slash (e.g. `/images`), that will serve as the end of the URL for your page. The start of the URL will be determined by your IP address, or domain name if you deploy the site on the web. Using a `/` with no additional text as the route will create the homepage for your site.
 + `page_content` is a string of text. This can include HTML, CSS, and JavaScript, as you’ll see below.

Once you’ve added a route to your application, you can add the run command at the end of the file, to cause Flask to start serving your website when the program is run.

```python
app.run(debug=True, host='0.0.0.0')
```

Here is an example of a simple application that will run and serve a webpage.
```python
from flask import Flask

app = Flask(__name__)

@app.route("/")
def index():
    return "Hello world!"

app.run(debug=True, host="0.0.0.0")
```
--- /collapse ---

--- collapse ---
---
title: Serving a web page
---
The response returned by your page functions can be more than a simple string of text. You can include HTML in the string, but be careful to avoid breaking the quotes around the string with quotes inside the HTML. Use single quotes in your HTML if you’re using double quotes in Python, or vice versa.

Here’s an example of how you could include HTML in one of your route functions.
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

#### Including variables in your page
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
title: Letting users upload files
---

In order to use your web app to classify images, users will need to be able to upload images to the app. To achieve this, you’ll need an upload form and a function that handles the upload.

#### Creating a form
This is the HTML for a simple form that will attempt to upload the supplied image through the POST method.
```html
<!doctype html>
   <h1>Upload new File</h1>
   <form method=post enctype=multipart/form-data>
     <input type=file name=image_to_classify>
     <input type=submit value=Upload>
   </form>
```


#### Handling the upload request & rerouting the user
Once the form is submitted, it will attempt to use the same route that created the form to process it. To handle this, the function associated with that route needs to be expanded to handle a POST request, save the image it is sent as part of that request, and re-route the user to a page that will do something with the image.

You will also need to define an upload folder as part of creating the upload page. **Make sure that this folder exists, as Flask will not create it for you.**

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

#### Displaying the uploaded image
You will also need to create a route and function that takes the uploaded image and does something with it. In the case of this project, that will involve classifying it, and maybe fetching some additional data based on that classification, e.g. from Wikipedia. The example below shows you how to display the image, but you can replace or extend that with whatever you do with the classification.

```python
from flask import Flask, url_for
import os

@app.route('/uploads/<filename>')
def uploaded_file(filename):
    image_path = os.path.join(UPLOAD_FOLDER, filename)
    image_url = url_for('static', filename='uploads/' + filename)
    return f"""
    <!doctype html>
    <img src='{image_url}' />
    """
```
--- /collapse ---


