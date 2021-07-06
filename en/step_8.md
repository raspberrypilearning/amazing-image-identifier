## Classify your image
You need to load a model to do your image identification. In order to create an application that can identify most things it is shown, a powerful and well-trained model is needed. You could collect and label tens of thousands of images, design a model, and train it like in the 'Teach a computer to read' project, but it would take days of work. It is much faster to use a model that has already been trained to identify a wide variety of things. Luckily, TensorFlow contains several models suited for this purpose, so you can just load one of them: VGG16.


### Import a model from TensorFlow
This code imports a model from TensorFlow and stores it in a model variable. It is helpful to create a variable to store the image in the size the model expects at the same time, as you need thhis information later. For this version of VGG16, that is 224x224 pixels. This means VGG16 expects square images. The code to get a classification below resizes any image it is given to match the model's expectations. If the image wasn't originally square, it will end up a bit squished, which may confuse the model. Similarly, if the image provided is much bigger, or much smaller, than what the model expects, then that may also cause issues. You may want to include guidance or instructions to your users on the types of image to supply. In a more advanced version of your application, you could give them the tools to specifically choose a square section of their image to be classified.

```python
import tensorflow as tf
import numpy as np

model = tf.keras.applications.VGG16()
IMAGE_SIZE = 224
```

### Get a classification from the model
To get a classification from the model, you need to use a series of commands that take the path to an image, prepare that image for use by the model, ask the model for a classification, and select the model’s highest-ranked classification from the results. This function takes the path to an image and returns a string that contains the highest-ranked classification of that image.

```python
def identify_image(image_path):
    # Load the image from the supplied file path
    # At the same time, resize it to the size the model expects
    image = tf.keras.preprocessing.image.load_img(image_path, 
    target_size=(IMAGE_SIZE, IMAGE_SIZE)
    )
    # Convert the image to an array of numbers,
    # and shape that array as the model expects
    image = tf.keras.preprocessing.image.img_to_array(image)
    image = np.expand_dims(image, axis=0)
    # Get the model's classifiaction of the image
    classifications = model.predict(image, batch_size=1)
    # Select the single most likely classifiaction 
    best_classification = tf.keras.applications.imagenet_utils.decode_predictions(classifications, top=1)
    # Return the string that identifies that classification
    return best_classification[0][0][1]
```
If you want to understand the function in more detail, look at the ['Testing your computer's vision' project](https://projects.raspberrypi.org/en/projects/testing-your-computers-vision).
