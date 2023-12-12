# Problem Set 2 Report

[Colab Notebook](https://colab.research.google.com/drive/1FpKbci3DbaIsIQW5Sc1XSkklu1kWYWO1?usp=sharing)

```python
!pip install imageio
import imageio

import cv2
import numpy as np
import matplotlib.pyplot as plt
import requests
from PIL import Image
from io import BytesIO
```

```
Requirement already satisfied: imageio in /usr/local/lib/python3.10/dist-packages (2.31.6)
Requirement already satisfied: numpy in /usr/local/lib/python3.10/dist-packages (from imageio) (1.23.5)
Requirement already satisfied: pillow<10.1.0,>=8.3.2 in /usr/local/lib/python3.10/dist-packages (from imageio) (9.4.0)

```

```python
# Load an RGB image of your choice from a URL

img = imageio.imread('https://c8.alamy.com/zooms/9/4acdc6e0919143dbbea48e31be673b8d/ke55gh.jpg')


plt.imshow(img)
plt.axis('off') # to turn off the axis
plt.show()
```

```
<ipython-input-11-2a1f039c0712>:3: DeprecationWarning: Starting with ImageIO v3 the behavior of this function will switch to that of iio.v3.imread. To keep the current behavior (and make this warning disappear) use `import imageio.v2 as imageio` or call `imageio.v2.imread` directly.
  img = imageio.imread('https://c8.alamy.com/zooms/9/4acdc6e0919143dbbea48e31be673b8d/ke55gh.jpg')

```

```python
image.shape
```

```
(452, 640, 3)
```

```python
def plot(x):
    fig, ax = plt.subplots()
    im = ax.imshow(x, cmap='gray')
    ax.axis('off')
    fig.set_size_inches(224, 224) # resizing to 224 x 224
    plt.show()
```

```python
plot(image)

# Russian/Soviet composers Sergei Prokofiev (left), Dmitri Shostakovitch (middle), and Aram Khachaturian (right)
```

```python
# Show a grayscale copy

import cv2
import matplotlib.pyplot as plt

# Convert the image to grayscale
gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

def plot(x):
    fig, ax = plt.subplots()
    im = ax.imshow(x, cmap='gray')
    ax.axis('off')
    fig.set_size_inches(224, 224) # resizing to 224 x 224
    plt.show()

# Display the grayscale image
#plt.imshow(gray_image, cmap='gray')
#plt.axis('off')
#plt.show()

plot(gray_image)
```

```python
x=image
```

```python
# Generate 10 random 5x5 filters
num_filters = 10
filter_size = 5
filters = generate_random_filters(num_filters, filter_size)

# Show the color image
plt.figure(figsize=(6, 6))
plt.imshow(np.array(img))
plt.axis('off')
plt.title('Color Image (224x224)')
plt.show()

# Show the shape of the grayscale image
print("Shape of the grayscale image:", gray_image.shape)

# Plot the grayscale image
plt.figure(figsize=(6, 6))
plt.imshow(gray_image, cmap='gray')
plt.axis('off')
plt.title('Grayscale Image (224x224)')
plt.show()
```

```
Shape of the grayscale image: (452, 640)

```

```python
# Convolve the image with each filter and plot filter-feature map pairs
plt.figure(figsize=(12, 12))

for i, filter in enumerate(filters):
    feature_map = cv2.filter2D(gray_image, -1, filter)

    # Plot the filter
    plt.subplot(num_filters, 2, i * 2 + 1)
    plt.imshow(filter, cmap='gray')
    plt.axis('off')
    plt.title(f'Filter {i + 1}')

    # Plot the corresponding feature map
    plt.subplot(num_filters, 2, i * 2 + 2)
    plt.imshow(feature_map, cmap='gray')
    plt.axis('off')
    plt.title(f'Feature Map {i + 1}')

plt.tight_layout()
plt.show()
```
