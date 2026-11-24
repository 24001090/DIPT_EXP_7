# DIPT_EXP_7
# Lane Detection

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
##  Developed By

* **Name:** POOJA PRIYA B
* **Register No:** 212224230196

###  Step 1: Import Libraries

```python
import cv2
import numpy as np
import matplotlib.pyplot as plt
```

---

###  Step 2: Read the Image

```python
image = cv2.imread("tulip.jpg")

if image is None:
    raise FileNotFoundError("Could not load 'lan_img1.jpg'. Check the file path.")
image_rgb = cv2.cvtColor(image, cv2.COLOR_BGR2RGB)

```

---

###  Step 3: Convert to Grayscale

```python
gray = cv2.cvtColor(image, cv2.COLOR_BGR2GRAY)

```

---

###  Step 4: Display Images

```python
plt.figure(figsize=(10,5))
plt.figure(figsize=(10,5))

plt.figure(figsize=(10, 5))

plt.subplot(1, 2, 1)
plt.imshow(image_rgb)
plt.title("Original Image")
plt.axis("off")

plt.subplot(1, 2, 2)
plt.imshow(gray, cmap="gray")
plt.title("Grayscale Image")
plt.axis("off")

plt.tight_layout()
plt.show()

```
<img width="727" height="461" alt="image" src="https://github.com/user-attachments/assets/2b08049c-3283-4fb2-b562-d58556ff857c" />

---

###  Step 5: Thresholding

```python


threshold = 
threshold = 150
_, thresh = cv2.threshold(gray, threshold, 255, cv2.THRESH_BINARY)

plt.figure(figsize=(6, 6))
plt.imshow(thresh, cmap="gray")
plt.title("Thresholded Image")
plt.axis("off")
plt.show()

```
<img width="462" height="472" alt="image" src="https://github.com/user-attachments/assets/0250f17e-1840-4775-b742-c0e0273f382a" />


---

###  Step 6: Region of Interest (ROI)

```python

height, width = thresh.shape

roi_vertices = np.array([[
    (int(0.1 * width), height),
    (int(0.45 * width), int(0.6 * height)),
    (int(0.55 * width), int(0.6 * height)),
    (int(0.9 * width), height)
]], dtype=np.int32)

mask = np.zeros_like(thresh)
cv2.fillPoly(mask, roi_vertices, 255)
roi_masked = cv2.bitwise_and(thresh, mask)

plt.figure(figsize=(6, 6))
plt.imshow(roi_masked, cmap="gray")
plt.title("ROI Masked Image")
plt.axis("off")
plt.show()
```
<img width="418" height="495" alt="image" src="https://github.com/user-attachments/assets/3c119299-8c22-4eee-a987-a4dc2e79bcfe" />


### Step 7: Edge Detection (Canny)

```python


edges = cv2.Canny(roi_masked, 50, 150)
plt.figure(figsize=(6, 6))
plt.imshow(edges, cmap="gray")
plt.title("Edge Detected Image")
plt.axis("off")
plt.show()

```
<img width="371" height="486" alt="image" src="https://github.com/user-attachments/assets/a8fa387c-62ee-4e2c-a916-2f19cc48cbf8" />


---

###  Step 8: Gaussian Blur

```python


smoothed = cv2.GaussianBlur(edges, (5, 5), 0)
plt.figure(figsize=(6, 6))
plt.imshow(smoothed, cmap="gray")
plt.title("Smoothed (Blurred) Edge Image")
plt.axis("off")
plt.show()

```
<img width="421" height="482" alt="image" src="https://github.com/user-attachments/assets/4d848119-6981-464c-970f-fcc9ddbdf681" />


---

###  Step 9: Hough Transform

```python
lines = cv2.HoughLinesP(
    smoothed,
    rho=2,
    theta=np.pi / 180,
    threshold=50,
    minLineLength=40,
    maxLineGap=100
)

line_image = np.zeros_like(image)
if lines is not None:
    for line in lines:
        x1, y1, x2, y2 = line[0]
        cv2.line(line_image, (x1, y1), (x2, y2), (255, 0, 0), 5)

line_image_rgb = cv2.cvtColor(line_image, cv2.COLOR_BGR2RGB)

plt.figure(figsize=(6, 6))
plt.imshow(line_image_rgb)
plt.title("Detected Lines")
plt.axis("off")
plt.show()

```
<img width="440" height="495" alt="image" src="https://github.com/user-attachments/assets/4409b041-c55f-408c-a0ac-ec5ab56a12d4" />

---

### Step 10: Lane Detection Logic

```
final_output = cv2.addWeighted(image, 0.8, line_image, 1.0, 0.0)
final_output_rgb = cv2.cvtColor(final_output, cv2.COLOR_BGR2RGB)
plt.figure(figsize=(6, 6))
plt.imshow(final_output_rgb)
plt.title("Final Lane Detection Output")
plt.axis("off")
plt.show()
```
<img width="412" height="467" alt="image" src="https://github.com/user-attachments/assets/88a9cf4f-5f42-48e3-b649-697c018c0150" />

---


## Result

Thus, the lane detection pipeline is successfully implemented by completing the missing code sections. The system detects and highlights lane lines effectively.

---
