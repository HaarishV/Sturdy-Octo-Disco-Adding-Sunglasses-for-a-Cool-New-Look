# Sturdy-Octo-Disco-Adding-Sunglasses-for-a-Cool-New-Look
### NAME: HAARISH V
### REG NO: 212223230067
Sturdy Octo Disco is a fun project that adds sunglasses to photos using image processing.

Welcome to Sturdy Octo Disco, a fun and creative project designed to overlay sunglasses on individual passport photos! This repository demonstrates how to use image processing techniques to create a playful transformation, making ordinary photos look extraordinary. Whether you're a beginner exploring computer vision or just looking for a quirky project to try, this is for you!

## FEATURES:
- Detects the face in an image.
- Places a stylish sunglass overlay perfectly on the face.
- Works seamlessly with individual passport-size photos.
- Customizable for different sunglasses styles or photo types.

## TECHNOLOGIES USED:
- Python
- OpenCV for image processing
- Numpy for array manipulations

## HOW TO USE:
1. Clone this repository.
2. Add your passport-sized photo to the `images` folder.
3. Run the script to see your "cool" transformation!

## APPLICATIONS:
- Learning basic image processing techniques.
- Adding flair to your photos for fun.
- Practicing computer vision workflows.

## PROGRAM AND OUTPUT:
```pyhton
import cv2
import numpy as np
import matplotlib.pyplot as plt
faceImage = cv2.imread('photo.jpg')
plt.imshow(faceImage[:,:,::-1]);plt.title("Face")
```
<img width="463" height="572" alt="image" src="https://github.com/user-attachments/assets/5e60f5eb-8542-43ef-9437-e1dc31911e91" />


```python
faceImage.shape
```

<img width="129" height="32" alt="image" src="https://github.com/user-attachments/assets/d27d2d1a-b88c-4db8-8791-5334645f2d6c" />


```python
glassPNG = cv2.imread('glass.png',-1)
plt.imshow(glassPNG[:,:,::-1]);plt.title("glassPNG")
```
<img width="727" height="389" alt="image" src="https://github.com/user-attachments/assets/8ef82bb9-f6a8-4551-918a-f6e77452593e" />


```python
plt.figure(figsize=[15,15])
plt.subplot(121);plt.imshow(glassBGR[:,:,::-1]);plt.title('Sunglass Color channels');
plt.subplot(122);plt.imshow(glassMask1,cmap='gray');plt.title('Sunglass Alpha channel');
```
<img width="1373" height="321" alt="image" src="https://github.com/user-attachments/assets/888f51ad-b650-4f4d-b040-8e9f2932c7ed" />


```python
import cv2
import matplotlib.pyplot as plt

# Load images
faceImage = cv2.imread("Photo.jpg")
glassPNG = cv2.imread("glass.png", -1)

# Extract BGR channels (ignore alpha for naive placement)
glassBGR = glassPNG[:, :, :3]

# Resize glasses to fit
glassBGR = cv2.resize(glassBGR, (180, 75))  # (width, height)

# Copy face
faceWithGlassesNaive = faceImage.copy()

# Define region coordinates properly (y:y+h, x:x+w)
y, x = 150, 110   # top-left corner
h, w = glassBGR.shape[:2]

# Replace ROI with glasses
faceWithGlassesNaive[y:y+h, x:x+w] = glassBGR

# Show result
plt.imshow(faceWithGlassesNaive[..., ::-1])
plt.title("Naive Overlay (No Mask)")
plt.show()
```
<img width="454" height="547" alt="image" src="https://github.com/user-attachments/assets/cecdbb04-f9aa-45c6-8595-c13309f1806d" />

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt

# Load your face image
faceImage = cv2.imread("Photo.jpg")
print("Face shape:", faceImage.shape)

# Load sunglasses PNG with alpha channel
glassPNG = cv2.imread("glass.png", -1)   # must have 4 channels
print("Original Glasses shape:", glassPNG.shape)

# Resize sunglasses (adjust size as needed)
glassPNG = cv2.resize(glassPNG, (180, 75))  # width=250, height=80
print("Resized Glasses shape:", glassPNG.shape)

# Separate BGR and Alpha
glassBGR = glassPNG[:, :, :3]
glassMask1 = glassPNG[:, :, 3]

# Convert alpha channel (1-channel) to 3 channels
glassMask = cv2.merge((glassMask1, glassMask1, glassMask1))

# Normalize mask (0 or 1 values)
glassMask = np.uint8(glassMask / 255)

# Copy face image
faceWithGlasses = faceImage.copy()

# Define placement (top-left corner of sunglasses)
x, y = 111, 145  # adjust these values for position
h, w = glassBGR.shape[:2]

# Extract Region of Interest (ROI) from the face
roi = faceWithGlasses[y:y+h, x:x+w]

# Masked regions
maskedEye   = cv2.multiply(roi, (1 - glassMask))   # remove sunglass area from ROI
maskedGlass = cv2.multiply(glassBGR, glassMask)    # keep sunglass area

# Combine both
roiFinal = cv2.add(maskedEye, maskedGlass)

# Place combined result back on face
faceWithGlasses[y:y+h, x:x+w] = roiFinal

# Show results
plt.figure(figsize=[15,10])
plt.subplot(121); plt.imshow(faceImage[:,:,::-1]); plt.title("Original")
plt.subplot(122); plt.imshow(faceWithGlasses[:,:,::-1]); plt.title("With Sunglasses (Masked)")
plt.show()
```
<img width="1079" height="721" alt="image" src="https://github.com/user-attachments/assets/407c17c2-e5e0-40b6-b849-012f873d753a" />

## RESULT:
Thus Adding Sunglasses to Your Passport Photo Using OpenCV is executed successfully.
