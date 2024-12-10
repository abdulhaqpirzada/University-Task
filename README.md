<pre><code>
import cv2
import numpy as np
import matplotlib.pyplot as plt
from google.colab import files

print("Upload an image for corner detection:")
uploaded = files.upload()

# Load and preprocess the image
file_name = list(uploaded.keys())[0]
input_image = cv2.imread(file_name)
gray_scale_image = cv2.cvtColor(input_image, cv2.COLOR_BGR2GRAY)
float_gray = np.float32(gray_scale_image)

# Compute gradients
gradient_x = cv2.Sobel(float_gray, cv2.CV_64F, 1, 0, ksize=3)
gradient_y = cv2.Sobel(float_gray, cv2.CV_64F, 0, 1, ksize=3)

# Compute second-order gradients
gradient_xx = gradient_x ** 2
gradient_yy = gradient_y ** 2
gradient_xy = gradient_x * gradient_y

# Apply Gaussian smoothing
kernel_size = 5
smooth_xx = cv2.GaussianBlur(gradient_xx, (kernel_size, kernel_size), sigmaX=1)
smooth_yy = cv2.GaussianBlur(gradient_yy, (kernel_size, kernel_size), sigmaX=1)
</code></pre>
