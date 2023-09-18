To create a random grayscale image and display it using Matplotlib in Python, you can use the following steps:

1. Import the necessary libraries.
2. Generate random grayscale pixel values.
3. Create an image using NumPy.
4. Display the image using Matplotlib.

Here's a step-by-step example:

```python
import numpy as np
import matplotlib.pyplot as plt

# Set the dimensions of the image (e.g., 256x256 pixels)
width, height = 256, 256

# Generate random grayscale pixel values between 0 (black) and 255 (white)
random_grayscale_values = np.random.randint(0, 256, (height, width), dtype=np.uint8)

# Create the grayscale image
random_grayscale_image = np.array(random_grayscale_values, dtype=np.uint8)

# Display the image using Matplotlib
plt.imshow(random_grayscale_image, cmap='gray')
plt.title('Random Grayscale Image')
plt.axis('off')  # Turn off axis labels and ticks
plt.show()
```

In this code:

- We import `numpy` as `np` to generate random pixel values and manipulate arrays.
- We import `matplotlib.pyplot` as `plt` to display the image.
- You can adjust the `width` and `height` variables to set the dimensions of the image as per your requirements.
- We generate random grayscale pixel values using `np.random.randint()` to create a NumPy array with random integer values between 0 and 255.
- We create the grayscale image by converting the array to the `uint8` data type, which is suitable for representing pixel values in the range 0-255.
- Finally, we display the grayscale image using `plt.imshow()`, set a title, and turn off axis labels and ticks using `plt.title()` and `plt.axis('off')`, respectively. The `cmap='gray'` argument ensures that Matplotlib interprets the data as grayscale.

When you run this code, it will generate a random grayscale image and display it in a Matplotlib window.
