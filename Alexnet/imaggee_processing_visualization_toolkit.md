# Image Processing and Visualization Toolkit

This toolkit provides a series of Python functions designed for handling and processing data, particularly images, using PyTorch and other libraries. These functions enable tasks such as tensor creation on GPU, image plotting, downloading Google Slide presentations as images, and image preprocessing for neural network inputs.

## Table of Contents
1. [Installation](#installation)
2. [Function Descriptions](#function-descriptions)
   - [GPU](#gpu)
   - [GPU_data](#gpu_data)
   - [plot](#plot)
   - [get_google_slide](#get_google_slide)
   - [get_slides](#get_slides)
   - [load](#load)
3. [Usage](#usage)

## Installation

(Instructions on how to install and setup the toolkit go here)

## Function Descriptions

### GPU
Converts data into a PyTorch tensor, enabling gradients for training neural networks. The tensor is set to float data type and placed on a CUDA-enabled GPU device.

```python
def GPU(data):
    return torch.tensor(data, requires_grad=True, dtype=torch.float, device=torch.device('cuda'))
```

### GPU_data
Similar to `GPU`, but creates a tensor without enabling gradients. Useful for inference where gradient computation is not required.

```python
def GPU_data(data):
    return torch.tensor(data, requires_grad=False, dtype=torch.float, device=torch.device('cuda'))
```

### plot
Uses Matplotlib to display the input data `x` as a grayscale image. This function is used for visualizing 2D data or matrices.

```python
def plot(x):
    fig, ax = plt.subplots()
    im = ax.imshow(x, cmap = 'gray')
    ax.axis('off')
    fig.set_size_inches(5, 5)
    plt.show()
```

### get_google_slide
Generates a URL to download a specific page of a Google Slides presentation in PDF format.

```python
def get_google_slide(url):
    url_head = "https://docs.google.com/presentation/d/"
    url_body = url.split('/')[5]
    page_id = url.split('.')[-1]
    return url_head + url_body + "/export/pdf?id=" + url_body + "&pageid=" + page_id
```

### get_slides
Downloads a Google Slides presentation as a PDF and converts it to images. This function is useful for extracting images from presentations.

```python
def get_slides(url):
    url = get_google_slide(url)
    r = requests.get(url, allow_redirects=True)
    open('file.pdf', 'wb').write(r.content)
    images = convert_from_path('file.pdf', 500)
    return images
```

### load
Preprocesses an image for neural network input by resizing, cropping, converting to tensor, and normalizing. The image is then moved to the designated computing device.

```python
def load(image, size=224):
    means = [0.485, 0.456, 0.406]
    stds = [0.229, 0.224, 0.225]
    transform = transforms.Compose([
        transforms.Resize(size),
        transforms.CenterCrop(size),
        transforms.ToTensor(),
        transforms.Normalize(means, stds)
    ])
    tensor = transform(image).unsqueeze(0).to(device)
    tensor.requires_grad = True
    return tensor
```

## Usage

### Creating Tensors for GPU

To create a tensor on a GPU with gradients enabled (useful for training models):

```python
data = [1, 2, 3]  # Replace with your data
tensor = GPU(data)
```

For inference or when gradients are not needed:

```python
data = [1, 2, 3]  # Replace with your data
tensor = GPU_data(data)
```

### Plotting Data

To visualize data as an image:

```python
import numpy as np

x = np.random.rand(10, 10)  # Example 2D data
plot(x)
```

### Downloading Google Slides as Images

To download a specific Google Slides page as an image:

```python
url = "Your_Google_Slides_URL_here"
images = get_slides(url)
# images now contains the slides as images
```

### Preprocessing Images for Neural Networks

To preprocess an image for a neural network:

```python
from PIL import Image

image_path = 'path/to/your/image.jpg'
image = Image.open(image_path)
preprocessed_image = load(image)
# preprocessed_image is now ready to be used as neural network input
```
