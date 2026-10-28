# Image-Handling-and-Pixel-Transformations-Using-OpenCV 

## AIM:
Write a Python program using OpenCV that performs the following tasks:

1) Read and Display an Image.  
2) Adjust the brightness of an image.  
3) Modify the image contrast.  
4) Generate a third image using bitwise operations.

## Software Required:
- Anaconda - Python 3.7
- Jupyter Notebook (for interactive development and execution)

## Algorithm:
### Step 1:
Load an image from your local directory and display it.

### Step 2:
Create a matrix of ones (with data type float64) to adjust brightness.

### Step 3:
Create brighter and darker images by adding and subtracting the matrix from the original image.  
Display the original, brighter, and darker images.

### Step 4:
Modify the image contrast by creating two higher contrast images using scaling factors of 1.1 and 1.2 (without overflow fix).  
Display the original, lower contrast, and higher contrast images.

### Step 5:
Split the image (boy.jpg) into B, G, R components and display the channels

## Program Developed By:
- Name: ASHWIN BAALAJI V K
- Register Number: 212225230026

  ### Ex. No. 01

#### 1. Read the image ('Eagle_in_Flight.jpg') using OpenCV imread() as a grayscale image.
```
import cv2
import matplotlib.pyplot as plt

img = cv2.imread('image.png', cv2.IMREAD_GRAYSCALE)
```

#### 2. Print the image width, height & Channel.
```
height, width = img.shape

print("Width:", width)
print("Height:", height)
print("Channel: 1")
```

#### 3. Display the image using matplotlib imshow().
```
plt.imshow(img, cmap='gray')
plt.title("Grayscale Image")
plt.axis('off')
plt.show()
```

#### 4. Save the image as a PNG file using OpenCV imwrite().
```
cv2.imwrite('output.png', img)
print("Image saved successfully!")
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```
img_gray = cv2.imread('output.png', cv2.IMREAD_GRAYSCALE)
img_color = cv2.cvtColor(img_gray, cv2.COLOR_GRAY2BGR)
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```
import cv2
import matplotlib.pyplot as plt

img_color = cv2.imread('image.png', cv2.IMREAD_COLOR)

plt.imshow(cv2.cvtColor(img_color, cv2.COLOR_BGR2RGB))
plt.title("Colour Image")
plt.axis('off')
plt.show()

height, width, channel = img_color.shape

print("Width:", width)
print("Height:", height)
print("Channel:", channel)
```

#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```
import cv2
import matplotlib.pyplot as plt

img = cv2.imread('image.png')

# Dog mattum crop panna
dog = img[40:650, 60:410]

print("Original image size:", img.shape)
print("Cropped image size:", dog.shape)

plt.figure(figsize=(5, 7))
plt.imshow(cv2.cvtColor(dog, cv2.COLOR_BGR2RGB))
plt.title("Cropped Dog")
plt.axis('off')
plt.show()
```

#### 8. Resize the image up by a factor of 2x.
```
import cv2
import matplotlib.pyplot as plt

img = cv2.imread('image.png')

# Crop the image
dog = img[40:650, 60:410]

# Resize the cropped image by 2x
resized_img = cv2.resize(dog, None, fx=2, fy=2)

plt.imshow(cv2.cvtColor(resized_img, cv2.COLOR_BGR2RGB))
plt.title("Resized Image 2x")
plt.axis('off')
plt.show()
```

#### 9. Flip the cropped/resized image horizontally.
```
import cv2
import matplotlib.pyplot as plt

flipped_img = cv2.flip(resized_img, 1)

plt.imshow(cv2.cvtColor(flipped_img, cv2.COLOR_BGR2RGB))
plt.title("Horizontally Flipped Image")
plt.axis('off')
plt.show()
```

#### 10. Read in the image ('Apollo-11-launch.jpg').
```
import cv2
import numpy as np
import matplotlib.pyplot as plt

apollo_img = cv2.imread('image.png')
```

#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```
text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font_face = cv2.FONT_HERSHEY_PLAIN

height, width = apollo_img.shape[:2]
text_size = cv2.getTextSize(text, font_face, 1.5, 2)[0]
x = (width - text_size[0]) // 2
y = height - 20

cv2.putText(apollo_img, text, (x, y), font_face, 1.5, (255, 255, 255), 2)
```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```
rect_color = (255, 0, 255)

cv2.rectangle(apollo_img, (50, 50), (250, 300), rect_color, 3)
```

#### 13. Display the final annotated image.
```
plt.imshow(cv2.cvtColor(apollo_img, cv2.COLOR_BGR2RGB))
plt.axis('off')
plt.show()
```

#### 14. Read the image ('Boy.jpg').
```
img = cv2.imread('image.png')
```

#### 15. Adjust the brightness of the image.
```
matrix_ones = np.ones(img.shape, dtype=np.float64)
matrix = matrix_ones * 50
matrix = matrix.astype(np.uint8)
```

#### 16. Create brighter and darker images.
```
img_brighter = cv2.add(img, matrix)
img_darker = cv2.subtract(img, matrix)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```
plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(img_darker, cv2.COLOR_BGR2RGB))
plt.title('Darker Image')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(img_brighter, cv2.COLOR_BGR2RGB))
plt.title('Brighter Image')
plt.axis('off')

plt.show()
```

#### 18. Modify the image contrast.
```
matrix1 = np.ones(img.shape, dtype=np.uint8)
matrix2 = np.ones(img.shape, dtype=np.uint8)

img_higher1 = cv2.multiply(img, matrix1, scale=1.1)
img_higher2 = cv2.multiply(img, matrix2, scale=1.2)
img_lower = cv2.multiply(img, matrix1, scale=0.8)
```

#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```
plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(cv2.cvtColor(img_lower, cv2.COLOR_BGR2RGB))
plt.title('Lower Contrast')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(cv2.cvtColor(img_higher1, cv2.COLOR_BGR2RGB))
plt.title('Higher Contrast')
plt.axis('off')

plt.show()
```

#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```
b, g, r = cv2.split(img)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(b, cmap='gray')
plt.title('Blue Channel')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(g, cmap='gray')
plt.title('Green Channel')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(r, cmap='gray')
plt.title('Red Channel')
plt.axis('off')

plt.show()
```

#### 21. Merged the R, G, B , displays along with the original image
```
merged_img = cv2.merge([r, g, b])

plt.figure(figsize=(8, 4))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(merged_img)
plt.title('Merged RGB Image')
plt.axis('off')

plt.show()
```

#### 22. Split the image into the H, S, V components & Display the channels.
```
hsv_img = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
h, s, v = cv2.split(hsv_img)

plt.figure(figsize=(12, 4))

plt.subplot(1, 3, 1)
plt.imshow(h, cmap='gray')
plt.title('Hue Channel')
plt.axis('off')

plt.subplot(1, 3, 2)
plt.imshow(s, cmap='gray')
plt.title('Saturation Channel')
plt.axis('off')

plt.subplot(1, 3, 3)
plt.imshow(v, cmap='gray')
plt.title('Value Channel')
plt.axis('off')

plt.show()
```
#### 23. Merged the H, S, V, displays along with original image.
```
merged_hsv = cv2.merge([h, s, v])
merged_bgr = cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR)

plt.figure(figsize=(8, 4))

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(img, cv2.COLOR_BGR2RGB))
plt.title('Original Image')
plt.axis('off')

plt.subplot(1, 2, 2)
plt.imshow(cv2.cvtColor(merged_bgr, cv2.COLOR_BGR2RGB))
plt.title('Merged HSV Image')
plt.axis('off')

plt.show()
```

## Output:
- **i)** Read and Display an Image.

- **ii)** Adjust Image Brightness.
- 
- **iii)** Modify Image Contrast.
<img width="823" height="160" alt="image" src="https://github.com/user-attachments/assets/3a544bd2-b65a-4bff-8c9f-bfc06d5e5ecf" />

- 
- **iv)** Generate Third Image Using Bitwise Operations.

## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.

