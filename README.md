# Morphological Image Processing with OpenCV + Persian Report

This repository contains the implementation and analysis of fundamental morphological image processing operations using OpenCV in Python. The project investigates the behavior of **Dilation** and **Erosion** using different structuring elements and kernel sizes. The effects of these operations are evaluated on binary and grayscale images for shape transformation, noise reduction, and edge detection.

---

## Project Objectives

- Understand the principles of morphological image processing.
- Compare square and circular structuring elements.
- Analyze the effect of kernel size on image transformations.
- Apply dilation and erosion for practical image processing tasks.
- Evaluate morphological methods for noise reduction and edge extraction.

---

## Technologies Used

- Python
- OpenCV
- NumPy
- Matplotlib

---

## OpenCV Functions Used

### Image Loading

```python
image = cv2.imread("image.png", cv2.IMREAD_GRAYSCALE)
```

Loads an image from disk and converts it into a grayscale image suitable for morphological operations.

### Binary Thresholding

```python
_, binary = cv2.threshold(image, 127, 255, cv2.THRESH_BINARY)
```

Converts a grayscale image into a binary image by assigning pixels to either black (0) or white (255) based on a threshold value.

### Structuring Element Creation

```python
kernel = cv2.getStructuringElement(cv2.MORPH_RECT, (5, 5))
```

Creates a structuring element (kernel) used in morphological operations.

Available shapes:

- `cv2.MORPH_RECT` → Square kernel
- `cv2.MORPH_ELLIPSE` → Circular/Elliptical kernel

### Dilation

```python
dilated = cv2.dilate(binary, kernel, iterations=1)
```

Expands foreground regions and enlarges object boundaries.

### Erosion

```python
eroded = cv2.erode(binary, kernel, iterations=1)
```

Shrinks foreground regions and reduces object boundaries.

### Edge Detection

```python
edges = cv2.subtract(dilated, original)
```

Extracts object boundaries using a simple morphological gradient approach.

### Saving Images

```python
cv2.imwrite("result.png", output)
```

Stores processed images on disk.

---

# Question 1 – Dilation

## Part 1: Dilation Using Square and Circular Structuring Elements

### Input Image

`circle-square.png`

Dilation was applied using both square and circular kernels with the following kernel sizes:

```text
4 × 4
7 × 7
10 × 10
15 × 15
```

### Observations

- Square kernels expand objects primarily along horizontal and vertical directions.
- Circular kernels expand objects uniformly in all directions.
- Dilation gradually enlarges foreground regions.
- Larger kernels produce stronger expansion effects.
- Increasing kernel size reduces image details.
- Circular kernels preserve rounded boundaries more naturally.
- Larger kernels can completely fill holes inside objects.

### Conclusion

For images containing curved structures, circular structuring elements generally provide more natural and visually appealing results.

---

## Part 2: Pepper Noise Reduction Using Dilation

### Input Image

`cameraman.png`

Dilation was applied using circular kernels of size:

```text
3 × 3
5 × 5
7 × 7
9 × 9
11 × 11
```

### Observations

- Pepper noise appears as isolated dark pixels.
- Dilation replaces dark pixels with neighboring brighter values.
- Noise decreases as kernel size increases.
- Excessively large kernels blur image details.
- Small kernels preserve image quality more effectively.

### Why Circular Kernels?

Pepper noise is randomly distributed and has no preferred direction. Circular structuring elements are isotropic, meaning they influence all directions equally.

Advantages:

- Uniform expansion around noisy pixels.
- Better preservation of natural image structures.
- Reduced directional artifacts.
- Smoother visual appearance.

### Conclusion

A small circular kernel (3×3) provides a good balance between noise removal and detail preservation.

---

## Part 3: Edge Detection Using Dilation

### Input Image

`lady.png`

Edges were extracted using:

```python
edge = dilated_image - original_image
```

This approach represents a simple morphological gradient.

### Kernel Sizes

```text
3 × 3
5 × 5
7 × 7
9 × 9
11 × 11
```

Both square and circular kernels were evaluated.

### Observations

- Larger kernels produce thicker edges.
- More image structures become visible as kernel size increases.
- Circular kernels generate more uniform edges in all directions.
- Results obtained with circular and square kernels are visually similar.
- Circular kernels better preserve diagonal and curved boundaries.

### Conclusion

A circular kernel of size 9×9 provided a good compromise between edge visibility and boundary accuracy.

### Limitation

Although computationally simple, morphological edge extraction is generally less accurate than advanced methods such as the Canny edge detector.

---

# Question 2 – Erosion

## Part 1: Erosion Using Square and Circular Structuring Elements

### Input Image

`circle-square.png`

Erosion was applied using kernel sizes:

```text
4 × 4
7 × 7
10 × 10
15 × 15
20 × 20
```

### Observations

- Foreground regions become smaller.
- Dark regions and holes grow larger.
- Square kernels introduce angular distortions.
- Circular kernels preserve rounded object shapes more effectively.

### Conclusion

Circular structuring elements are better suited for preserving natural object geometry during erosion.

---

## Part 2: Salt-and-Pepper Noise Reduction Using Erosion

### Input Image

`cameraman.png`

Circular kernels of sizes:

```text
3 × 3
5 × 5
7 × 7
9 × 9
11 × 11
```

were used.

### Observations

- Bright details become thinner.
- Salt noise is effectively removed.
- Pepper noise is not removed and may become more prominent.
- Increasing kernel size darkens and blurs the image.
- Excessive erosion removes useful image information.

### Conclusion

Erosion is primarily effective for removing salt noise (bright pixels). A 3×3 kernel produced the most balanced result.

---

# Final Analysis

The experiments demonstrate the importance of selecting appropriate structuring elements and kernel sizes in morphological image processing.

### Key Findings

- Larger kernels produce stronger morphological effects.
- Increasing kernel size often leads to loss of image details.
- Structuring element shape significantly affects the output.
- Circular kernels generally preserve natural object geometry better than square kernels.
- Dilation is more effective for removing pepper noise.
- Erosion is more effective for removing salt noise.
- Proper kernel selection depends on the target application and image characteristics.

---
