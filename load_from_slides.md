# PDF to Image Conversion Environment Setup

This code is designed to set up the environment for converting PDF files to images using Python. It includes the installation of required dependencies and the importation of essential Python libraries.

'''python
%%capture
!apt-get install poppler-utils
!pip install pdf2image
from pdf2image import convert_from_path
import requests
import matplotlib.pyplot as plt
import numpy as np
from skimage.io import imread
from skimage.transform import resize

## Code Explanation

1. `%%capture`: This is a Jupyter Notebook magic command that captures the output of subsequent shell commands (commands prefixed with `!`) and prevents them from being displayed in the notebook cell's output. It's often used to hide command output when running cells in a notebook.

2. `!apt-get install poppler-utils`: This is a shell command executed within the Jupyter Notebook cell. It uses `apt-get` to install the `poppler-utils` package. `poppler-utils` is a set of command-line utilities for working with PDF files.

3. `!pip install pdf2image`: This is another shell command that uses `pip` to install the `pdf2image` Python package. `pdf2image` is a Python library for converting PDF files to images.

4. The code then imports several Python libraries, including `pdf2image`, `requests`, `matplotlib.pyplot`, `numpy`, `skimage.io`, and `skimage.transform`. These libraries are commonly used for image processing and manipulation in Python.

## Prerequisites

Before running the code, ensure that you have the following prerequisites installed:

- **poppler-utils**: This package is essential for working with PDF files. You can install it using the following command:

    ```
    !apt-get install poppler-utils
    ```

- **pdf2image**: This Python package allows you to convert PDF files to images. You can install it using pip:

    ```
    !pip install pdf2image
    ```

- Additionally, make sure you have the required Python libraries installed. You can typically install them using `pip`.

## Usage

The provided code sets up the necessary environment for PDF to image conversion but does not perform the actual conversion. To use this environment for converting PDF files to images, you should:

1. Write additional code to fetch a PDF file, convert it to images using `pdf2image`, and perform any required image processing or analysis.

2. Utilize the imported libraries such as `requests`, `matplotlib.pyplot`, `numpy`, `skimage.io`, and `skimage.transform` to work with the converted images as needed.

---


# Image Plotter and Google Slides to Images Converter

'''python
def plot(x):
    fig, ax = plt.subplots()
    im = ax.imshow(x, cmap = 'gray')
    ax.axis('off')
    fig.set_size_inches(5, 5)
    plt.show()

def get_google_slide(url):
    url_head = "https://docs.google.com/presentation/d/"
    url_body = url.split('/')[5]
    page_id = url.split('.')[-1]
    return url_head + url_body + "/export/pdf?id=" + url_body + "&pageid=" + page_id

def get_slides(url):
    url = get_google_slide(url)
    r = requests.get(url, allow_redirects=True)
    open('file.pdf', 'wb').write(r.content)
    images = convert_from_path('file.pdf', 500)
    return images
    
This code is a Python script that provides two main functions: one for plotting images and another for converting Google Slides presentations to images. Below is an explanation for each of these functions:

## 1. `plot(x)`

The `plot` function is designed to visualize a 2D array `x` as an image using Matplotlib. It includes the following steps:

- Creates a figure and axes for plotting.
- Displays the input data `x` as an image with a grayscale colormap (`cmap='gray'`).
- Removes axis labels and ticks for a cleaner image display.
- Sets the size of the displayed image to 5x5 inches.
- Finally, it shows the image using `plt.show()`.

This function is useful for visualizing 2D data arrays as images.

## 2. `get_google_slide(url)`

The `get_google_slide` function takes a Google Slides URL as input and constructs a URL for exporting the presentation as a PDF file. It performs the following steps:

- Constructs the base URL for Google Slides presentations (`url_head`).
- Extracts the unique identifier of the presentation from the input URL.
- Extracts the page ID from the input URL.
- Combines these components to create the final export URL, which includes the presentation ID and page ID.

This function is a part of the workflow for accessing and exporting Google Slides presentations.

## 3. `get_slides(url)`

The `get_slides` function combines the previous two functions to download a Google Slides presentation, convert it to a PDF, and then convert the PDF into a list of images. Here are the steps it follows:

- Calls `get_google_slide(url)` to obtain the export URL for the Google Slides presentation.
- Sends an HTTP GET request to the export URL, allowing redirects, and saves the downloaded PDF as 'file.pdf'.
- Uses the `pdf2image` library to convert the PDF file into a list of images. The images are generated at a resolution of 500 DPI (dots per inch).
- Returns the list of images, which represent the slides in the Google Slides presentation.

This function simplifies the process of converting Google Slides presentations into a format suitable for further analysis or display.

## Usage

To use these functions:

1. Import the necessary libraries: Ensure you have Matplotlib, requests, and pdf2image installed.

2. Call the `plot(x)` function with a 2D array `x` to visualize it as an image.

3. Use the `get_slides(url)` function to convert a Google Slides presentation to a list of images. Provide the Google Slides URL as the argument.

4. You can then work with the returned list of images as needed.


# Understanding a Loop for Plotting Images and Printing Shapes

## Code Explanation

```python
for i in range(n):
    plot(image_list[i])
    print(np.array(image_list[i]).shape)
```

- `for i in range(n):`: This line starts a loop that iterates `n` times, where `n` is a predefined number. The loop variable `i` takes on values from 0 to `n-1`, inclusive.

- `plot(image_list[i])`: Inside the loop, this line calls a function or method named `plot` with an argument `image_list[i]`. This implies that there is a list of images stored in `image_list`, and the code plots the `i`-th image in the list.

- `print(np.array(image_list[i]).shape)`: After plotting the image, this line converts the `i`-th image from `image_list` into a NumPy array using `np.array(image_list[i])`. It then calculates and prints the shape of the NumPy array using the `.shape` attribute. This shape represents the dimensions of the image, typically in the form `(height, width, channels)` for color images, or `(height, width)` for grayscale images.

## Purpose

The purpose of this code is to visualize a series of images and obtain information about their shapes. It can be useful in scenarios where you want to explore a collection of images, verify their dimensions, or identify any discrepancies in the dataset.

## Example Usage

Here's an example of how this code might be used:

```python
# Define a list of images
image_list = [image1, image2, image3, ...]

# Set the number of images to process
n = len(image_list)

# Loop through the images and plot each one
for i in range(n):
    plot(image_list[i])
    print(np.array(image_list[i]).shape)
```

In this example, replace `image1`, `image2`, `image3`, etc., with actual image data, and the code will plot each image and print its shape during each iteration of the loop.

## Conclusion

This code snippet is a simple but effective way to visualize and gather information about a collection of images in Python, making it a handy tool for image analysis and data exploration tasks.
