#  Lane Detection

##  Aim

To implement a basic lane detection pipeline using OpenCV by completing missing code segments at specified locations.

---

## Learning Objective

* Understand each stage of image processing
* Learn how to build a complete computer vision pipeline
* Practice writing code in guided sections

**Important Instruction:**
👉 Write code **ONLY in places marked as `# Your Code Here`**
👉 Do NOT modify any other part of the code

---

##  Software Used

* Anaconda – Python 3.7
* Jupyter Notebook / VS Code
* OpenCV (cv2)
* NumPy
* Matplotlib

---

##  Algorithm & Explanation

---

###  Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

###  Step 2: Read the Image

```python
# Read the image using OpenCV

###
# Your Code Here
###

image = cv2.imread('Qn_7_.jpg')
```

---

###  Step 3: Convert to Grayscale

# Convert to grayscale.

###
# Your Code Here
###

gray_image = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

###  Step 4: Display Images

plt.figure(figsize=(10,5))

###
# Your Code Here
###

plt.subplot(1, 2, 1)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(gray_image, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")

plt.show()

###  Step 5: Thresholding
---
# Apply thresholding

threshold = cv2.threshold(
    gray_image,
    127,
    255,
    cv2.THRESH_BINARY
)[1]

plt.imshow(threshold, cmap="gray")
plt.title("Thresholded Image")
plt.axis("off")
plt.show()
---

###  Step 6: Region of Interest (ROI)

```
# ROI masking already provided
height, width = threshold.shape

# Define a broad polygonal region of interest
roi_vertices = np.array([[
    (0, height),
    (0, int(height * 0.45)),
    (width, int(height * 0.45)),
    (width, height)
]], dtype=np.int32)

roi_mask = np.zeros_like(threshold)
cv2.fillPoly(roi_mask, roi_vertices, 255)
roi_image = cv2.bitwise_and(threshold, roi_mask)
```

---

### Step 7: Edge Detection (Canny)

```
# Perform Edge Detection

###
# Your Code Here
###

edges = cv2.Canny(
    gray_image,
    50,
    150
)

plt.imshow(edges, cmap="gray")
plt.title("Canny Edge Detection")
plt.axis("off")
plt.show()
```

---

###  Step 8: Gaussian Blur

```
# Apply Gaussian Blur

###
# Your Code Here
###

blurred = cv2.GaussianBlur(
    edges,
    (5, 5),
    0
)

plt.imshow(blurred, cmap="gray")
plt.title("Smoothed Image")
plt.axis("off")
plt.show()
```

---

###  Step 9: Hough Transform

```python
# Detect lines using Hough Transform

###
# Your Code Here
###

lines = cv2.HoughLinesP(
    blurred,
    1,
    np.pi / 180,
    threshold=100,
    minLineLength=50,
    maxLineGap=10
)
```

---

### Step 10: Lane Detection Logic

```
# Already implemented
# Step 5: Detect lines using HoughLinesP
lines = cv2.HoughLinesP(
    edges,
    1,
    np.pi / 180,
    100,
    minLineLength=50,
    maxLineGap=10
)
# Step 6: Using a for loop, draw the lines on the original image using the detected coordinates
# The lines variable contains the endpoints of the detected lines
if lines is not None:
    print(lines.shape)
    print(lines[:5])
    for line in lines:
        x1, y1, x2, y2 = line
        cv2.line(image, (x1, y1), (x2, y2), (0, 255, 0), 2)
# Display the result of Hough Transform (Image with lines)
plt.imshow(cv2.cvtColor(image, cv2.COLOR_BGR2RGB))  # Image with lines drawn
plt.title("Result of Hough Transform")
plt.axis('off')

```

---

##  Expected Output

* Original image

  <img width="463" height="587" alt="image" src="https://github.com/user-attachments/assets/a0b22bb2-e5d9-4e22-83a2-7e3a499e2e61" />

* Grayscale image
<img width="427" height="607" alt="image" src="https://github.com/user-attachments/assets/851e87d5-8a99-462a-9083-626bdddd5af2" />


* Thresholded image
<img width="416" height="563" alt="image" src="https://github.com/user-attachments/assets/1e3025d6-685e-44ec-b449-0c803fd3b2e0" />

* Edge detected image
<img width="452" height="566" alt="image" src="https://github.com/user-attachments/assets/20879e7c-6931-4b15-bae0-b15cf4df3d41" />

* Smoothed image
<img width="428" height="717" alt="image" src="https://github.com/user-attachments/assets/6bcf0dcd-765d-45f8-adba-bf1ecfb01d4f" />


* Final lane detection output
<img width="787" height="601" alt="image" src="https://github.com/user-attachments/assets/6376d537-76ae-4484-b8ed-552b2388e365" />

---

##  Instructions

* Fill ONLY in `# Your Code Here` sections
* Do NOT change existing code
* Run step-by-step
* Verify outputs

---

## Result

Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.

---

##  Developed By

* **Name:** SUWETHA T
* **Register No:** 212225040446
