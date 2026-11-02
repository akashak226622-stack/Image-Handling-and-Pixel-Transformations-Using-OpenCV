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

img_gray = cv2.imread('Screenshot 2026-11-02 095320.png', cv2.IMREAD_GRAYSCALE)

plt.imshow(img_gray, cmap='gray')
plt.axis('off')
plt.show()
```

#### 2. Print the image width, height & Channel.
```
# 2. Print width, height & channels
height, width = img_gray.shape[:2]
channels = 1 if img_gray.ndim == 2 else img_gray.shape[2]
print("Width:", width, "Height:", height, "Channels:", channels)
```

#### 3. Display the image using matplotlib imshow().
```
# 3. Display using matplotlib
plt.imshow(img_gray, cmap='gray')
plt.title("Grayscale Image")
plt.show()
```
<img width="433" height="556" alt="image" src="https://github.com/user-attachments/assets/1a9f9a2c-6c48-4c14-aba0-2ef75bac66da" />


#### 4. Save the image as a PNG file using OpenCV imwrite().
```
# 4. Save as PNG
cv2.imwrite('Screenshot 2026-11-02 095320.png', img_gray)
```

#### 5. Read the saved image above as a color image using cv2.cvtColor().
```
import cv2
import matplotlib.pyplot as plt

# 5. Read the saved image as a color image
img_saved = cv2.imread('Screenshot 2026-11-02 095320.png', cv2.IMREAD_COLOR)

# Convert BGR to RGB
img_color = cv2.cvtColor(img_saved, cv2.COLOR_BGR2RGB)

# Display image
plt.imshow(img_color)
plt.axis('off')
plt.show()
```

#### 6. Display the Colour image using matplotlib imshow() & Print the image width, height & channel.
```
# 6. Display the color image & print width, height, channels
plt.imshow(img_color)
plt.title("Color Image")
plt.show()
height, width, channels = img_color.shape
print("Width:", width, "Height:", height, "Channels:", channels)
```
<img width="491" height="540" alt="image" src="https://github.com/user-attachments/assets/aee914d5-7fc7-4fad-a682-5680b4928879" />


#### 7. Crop the image to extract any specific (Eagle alone) object from the image.
```
# 7. Crop the lion (central region; adjust the fractions to fit your image)
h, w = img_color.shape[:2]
y1, y2 = int(0.20 * h), int(0.80 * h)
x1, x2 = int(0.20 * w), int(0.80 * w)
img_cropped = img_color[y1:y2, x1:x2]

plt.imshow(img_cropped)
plt.title("Cropped Lion")
plt.show()
```
<img width="433" height="551" alt="image" src="https://github.com/user-attachments/assets/658722be-5951-47b2-845a-f23fcd6c6e0d" />


#### 8. Resize the image up by a factor of 2x.
```
# 8. Resize up by 2x
img_resized = cv2.resize(img_cropped, None, fx=2, fy=2, interpolation=cv2.INTER_LINEAR)
plt.imshow(img_resized)
plt.title("Resized (2x)")
plt.show()
```
<img width="431" height="560" alt="image" src="https://github.com/user-attachments/assets/ac1549cd-7d9d-4a98-80a0-7c2b4b78cb60" />


#### 9. Flip the cropped/resized image horizontally.
```
# 9. Flip horizontally
img_flipped = cv2.flip(img_resized, 1)
plt.imshow(img_flipped)
plt.title("Flipped Horizontally")a
plt.show()
```
<img width="431" height="560" alt="image" src="https://github.com/user-attachments/assets/bb1e1901-eca9-4478-a49f-51526e30a3a7" />


#### 10. Read in the image ('Apollo-11-launch.jpg').
```
import cv2
import matplotlib.pyplot as plt

# 10. Read the image
img_jet = cv2.imread('Screenshot 2026-11-02 095320.png', cv2.IMREAD_COLOR)

# Convert BGR to RGB
img_jet = cv2.cvtColor(img_jet, cv2.COLOR_BGR2RGB)

plt.imshow(img_jet)
plt.axis('off')
plt.show()
```
<img width="375" height="500" alt="image" src="https://github.com/user-attachments/assets/d9fd245c-76ba-4c0f-a2d4-5ab53a79977c" />


#### 11. Add the following text to the dark area at the bottom of the image (centered on the image):
```
# 11. Add centered text at the bottom
img_annotated = img_jet.copy()
img_h, img_w = img_annotated.shape[:2]

text = 'Apollo 11 Saturn V Launch, July 16, 1969'
font_face = cv2.FONT_HERSHEY_PLAIN

# pick a font scale so the text fills about 80% of the image width
(base_w, base_h), _ = cv2.getTextSize(text, font_face, 1, 1)
font_scale = 0.8 * img_w / base_w
thickness = max(1, int(font_scale))

(text_w, text_h), baseline = cv2.getTextSize(text, font_face, font_scale, thickness)
x = (img_w - text_w) // 2             # centered horizontally
y = img_h - int(0.05 * img_h)         # near the bottom

cv2.putText(img_annotated, text, (x, y), font_face, font_scale,
            (255, 255, 255), thickness, cv2.LINE_AA)

```

#### 12. Draw a magenta rectangle that encompasses the launch tower and the rocket.
```
# 12. Draw a magenta rectangle around the main object (jet)
magenta = (255, 0, 255)
rect_color = magenta
pt1 = (int(0.15 * img_w), int(0.15 * img_h))   # top-left
pt2 = (int(0.85 * img_w), int(0.80 * img_h))   # bottom-right
cv2.rectangle(img_annotated, pt1, pt2, rect_color, thickness=3)
```

#### 13. Display the final annotated image.
```
# 13. Display the final annotated image
plt.figure(figsize=(10, 8))
plt.imshow(img_annotated)
plt.title("Annotated Image")
plt.show()
```
<img width="756" height="880" alt="image" src="https://github.com/user-attachments/assets/e3d8b282-9665-4a2b-b677-e55ab2da9b8b" />


#### 14. Read the image ('Boy.jpg').
```
import cv2
import matplotlib.pyplot as plt

# 14. Read the image
img = cv2.imread('Screenshot 2026-11-02 095320.png', cv2.IMREAD_COLOR)

img_rgb = cv2.cvtColor(img, cv2.COLOR_BGR2RGB)

plt.imshow(img_rgb)
plt.axis('off')
plt.show()
```
<img width="367" height="486" alt="image" src="https://github.com/user-attachments/assets/3c685b44-415f-4c17-ba28-c4db8c2c5ac9" />


#### 15. Adjust the brightness of the image.
```
import numpy as np

# 15. Matrix of ones (float64) for brightness
matrix = np.ones(img.shape, dtype='float64') * 50

print(matrix)
```

#### 16. Create brighter and darker images.
```
# 16. Brighter and darker images
img_brighter = cv2.add(img, matrix, dtype=cv2.CV_8U)
img_darker   = cv2.subtract(img, matrix, dtype=cv2.CV_8U)
```

#### 17. Display the images (Original Image, Darker Image, Brighter Image).
```
# 17. Display Original, Darker, Brighter
plt.figure(figsize=(15, 5))
plt.subplot(131); plt.imshow(img_rgb); plt.title("Original Image"); plt.axis("off")
plt.subplot(132); plt.imshow(cv2.cvtColor(img_darker, cv2.COLOR_BGR2RGB)); plt.title("Darker Image"); plt.axis("off")
plt.subplot(133); plt.imshow(cv2.cvtColor(img_brighter, cv2.COLOR_BGR2RGB)); plt.title("Brighter Image"); plt.axis("off")
plt.show()
```
<img width="830" height="337" alt="image" src="https://github.com/user-attachments/assets/9dc51867-4624-4287-8b06-e59a301c8d1d" />


#### 18. Modify the image contrast.
```
# 18. Modify contrast (factors 1.1 and 1.2, without overflow fix)
matrix1 = np.ones(img.shape, dtype='float64') * 1.1
matrix2 = np.ones(img.shape, dtype='float64') * 1.2
matrix0 = np.ones(img.shape, dtype='float64') * 0.8     # extra, for the "lower contrast" display

img_higher1 = np.uint8(cv2.multiply(np.float64(img), matrix1))
img_higher2 = np.uint8(cv2.multiply(np.float64(img), matrix2))
img_lower   = np.uint8(cv2.multiply(np.float64(img), matrix0))
```


#### 19. Display the images (Original, Lower Contrast, Higher Contrast).
```
# 19. Display Original, Lower Contrast, Higher Contrast
plt.figure(figsize=(18, 5))
plt.subplot(141); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.subplot(142); plt.imshow(cv2.cvtColor(img_lower, cv2.COLOR_BGR2RGB)); plt.title("Lower Contrast (0.8)"); plt.axis("off")
plt.subplot(143); plt.imshow(cv2.cvtColor(img_higher1, cv2.COLOR_BGR2RGB)); plt.title("Higher Contrast (1.1)"); plt.axis("off")
plt.subplot(144); plt.imshow(cv2.cvtColor(img_higher2, cv2.COLOR_BGR2RGB)); plt.title("Higher Contrast (1.2)"); plt.axis("off")
plt.show()
```
<img width="832" height="275" alt="image" src="https://github.com/user-attachments/assets/dd3a3004-18b3-4f28-b18a-1a96c2761dc6" />


#### 20. Split the image (boy.jpg) into the B,G,R components & Display the channels.
```
# 20. Split into B, G, R and display the channels
b, g, r = cv2.split(img)

plt.figure(figsize=(18, 5))
plt.subplot(141); plt.imshow(b, cmap='gray'); plt.title("Blue Channel"); plt.axis("off")
plt.subplot(142); plt.imshow(g, cmap='gray'); plt.title("Green Channel"); plt.axis("off")
plt.subplot(143); plt.imshow(r, cmap='gray'); plt.title("Red Channel"); plt.axis("off")
plt.subplot(144); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.show()
```
<img width="817" height="242" alt="image" src="https://github.com/user-attachments/assets/f9330c21-ad63-46d7-bdba-5ab731fd1c24" />


#### 21. Merged the R, G, B , displays along with the original image
```
# 21. Merge the channels and display with the original
merged_bgr = cv2.merge((b, g, r))

plt.figure(figsize=(10, 5))
plt.subplot(121); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.subplot(122); plt.imshow(cv2.cvtColor(merged_bgr, cv2.COLOR_BGR2RGB)); plt.title("Merged (B,G,R)"); plt.axis("off")
plt.show()
```
<img width="797" height="506" alt="image" src="https://github.com/user-attachments/assets/5f3fad91-bc78-4d1b-837b-7e748945ee97" />


#### 22. Split the image into the H, S, V components & Display the channels.
```
# 22. Split into H, S, V and display the channels
img_hsv = cv2.cvtColor(img, cv2.COLOR_BGR2HSV)
hue, sat, val = cv2.split(img_hsv)

plt.figure(figsize=(18, 5))
plt.subplot(141); plt.imshow(hue, cmap='gray'); plt.title("Hue"); plt.axis("off")
plt.subplot(142); plt.imshow(sat, cmap='gray'); plt.title("Saturation"); plt.axis("off")
plt.subplot(143); plt.imshow(val, cmap='gray'); plt.title("Value"); plt.axis("off")
plt.subplot(144); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.show()
```
<img width="832" height="277" alt="image" src="https://github.com/user-attachments/assets/0b17eb1e-1f3c-4a06-b3db-a58a45e713bd" />

#### 23. Merged the H, S, V, displays along with original image.
```
# 23. Merge H, S, V and display with the original
merged_hsv = cv2.merge((hue, sat, val))
merged_hsv_rgb = cv2.cvtColor(cv2.cvtColor(merged_hsv, cv2.COLOR_HSV2BGR), cv2.COLOR_BGR2RGB)

plt.figure(figsize=(10, 5))
plt.subplot(121); plt.imshow(img_rgb); plt.title("Original"); plt.axis("off")
plt.subplot(122); plt.imshow(merged_hsv_rgb); plt.title("Merged (H,S,V)"); plt.axis("off")
plt.show()
```
<img width="821" height="492" alt="image" src="https://github.com/user-attachments/assets/7542914b-1655-4eec-accf-c8e87161d2e6" />


## Output:
- **i)** Read and Display an Image.
<img width="345" height="475" alt="image" src="https://github.com/user-attachments/assets/2deef337-88b0-406e-a184-5106afdcad4c" />


- **ii)** Adjust Image Brightness.
<img width="853" height="322" alt="image" src="https://github.com/user-attachments/assets/9081521e-6f7f-4060-8374-13667df05e25" />

  
- **iii)** Modify Image Contrast.
<img width="857" height="277" alt="image" src="https://github.com/user-attachments/assets/062dcf35-c242-468c-930a-1f3ddc8ad4cb" />

 

## Result:
Thus, the images were read, displayed, brightness and contrast adjustments were made, and bitwise operations were performed successfully using the Python program.

