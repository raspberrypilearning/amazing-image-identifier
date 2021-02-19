## Classify your image
You need to load a model to do your image identification. While you could collect and label tens of thousands of images, design a model, and train it like in Teach a computer to read, that would take days of work. It’s much faster to use a model that has already been trained to identify a wide variety of things. Luckily, TensorFlow contains several such models, so you can just load one of them: VGG16.


### Importing a model from TensorFlow
This code imports a model from TensorFlow and stores it in a model variable. It’s helpful to create a variable to store the image size the model expects at the same time, as you’ll need that later. For this version of VGG16 that’s 224x224 pixels.

```python
import tensorflow as tf

model = tf.keras.applications.VGG16()
IMAGE_SIZE = 224
```

### Getting a classification from the model
To get a classification from the model, you need to use a series of commands that take the path to an image, prepare that image for use by the model, ask the model for a classification, and select the model’s highest ranked classification from the results. This function will take the path to an image and return a string that contains the highest rannked classification of that image.

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
    best_classification = tf.keras.applications.imagenet_utils.decode_predictions(prediction_result, top=1)
    # Return the string that identifies that classification
    return best_classification[0][0][1]
```
If you want to understand the function in more detail, look at the [Testing your computer's vision project](https://projects.raspberrypi.org/en/projects/testing-your-computers-vision) elsewhere on this site.