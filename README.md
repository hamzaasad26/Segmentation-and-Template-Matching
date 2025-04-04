# Adaptive Thresholding and Digit Recognition Project

This project involves multiple techniques for image preprocessing, adaptive thresholding, and digit recognition, including Niblack, Sauvola thresholding methods, and template matching for credit card number recognition.

---

## Table of Contents

- [Question 1: Niblack Thresholding](#question-1)
- [Question 2: Sauvola Thresholding](#question-2)
- [Question 3: ZNCC Template Matching and KNN Classification](#question-3)
- [Question 4: Credit Card Number Recognition](#question-4)
- [Conclusion](#conclusion)

---

## Question 1: Niblack Thresholding

The Niblack thresholding method is a local adaptive thresholding algorithm that calculates thresholds dynamically based on local mean and standard deviation.

### Main Features of the Application

1. **Grayscale Image Processing**
2. **Adaptive Local Thresholding:** Unlike global thresholding, the Niblack method applies different thresholds to different image regions based on local statistics.
3. **Adjustable Parameters:** Users can modify the window size and the `k` parameter to control the segmentation effect.
4. **Multiple Configurations Comparison:** The script evaluates different window sizes to observe their impact on the thresholded output.
5. **Visualization of Results:** The processed images are displayed for comparison to determine the best settings.

### Implementation Details

1. Load an image in grayscale mode.
2. Convert the image to a floating-point format for numerical stability.
3. Compute the local mean and standard deviation within a given window size.
4. Determine the threshold using Niblack’s formula: `Threshold = mean(x) + k * stddev(x)`.
5. Generate a binary image based on the computed threshold.
6. Process the image for different window sizes and display results for comparison.

### Results and Comparisons

The algorithm was tested on an input image (`selfie.jpg`) using four different window sizes: 15, 25, 35, and 45. The results of each are presented below:

- **Window Size = 15:** Small window captures finer details but may introduce noise in regions with small variations.
- **Window Size = 25:** Balances fine details and noise suppression, providing a clearer thresholded image.
- **Window Size = 35:** Captures larger structural variations, reducing noise but blurring finer details.
- **Window Size = 45:** Over-smooth small details, making edges less distinct.

**Best Window Size Selection:** Based on visual evaluation, a window size of 25 provided the best trade-off between detail preservation and noise reduction.

---

## Question 2: Sauvola Thresholding

Sauvola methods dynamically calculate thresholds based on local mean and standard deviation, making them well-suited for images with varying illumination conditions.

### Main Features of the Application

1. **Grayscale Image Processing**
2. **Adaptive Local Thresholding:** Unlike global thresholding, these methods apply different thresholds to different image regions based on local statistics.
3. **Adjustable Parameters:** Users can modify the window size and key parameters (`k` for Niblack, `k` and `R` for Sauvola) to control the segmentation effect.
4. **Multiple Configurations Comparison:** The script evaluates different window sizes to observe their impact on the thresholded output.
5. **Visualization of Results:** The processed images are displayed for comparison to determine the best settings.

### Implementation Details

1. Load an image in grayscale mode.
2. Convert the image to a floating-point format for numerical stability.
3. Compute the local mean and standard deviation within a given window size.
4. Determine the threshold using the respective formula:
   - **Sauvola Formula:** `Threshold = mean(x) * (1 + k * ((stddev(x) / R) - 1))`
5. Generate a binary image based on the computed threshold.
6. Process the image for different window sizes and display results for comparison.

### Results and Comparisons

The algorithms were tested on an input image (`selfie.jpg`) using four different window sizes: 15, 25, 35, and 45. The results of each are presented below:

- **Window Size = 15:** Generates sharper edges with better text preservation.
- **Window Size = 25:** Maintains details while reducing background noise.
- **Window Size = 35:** Smoothens the image while preserving important features.
- **Window Size = 45:** Reduces noise but may blur finer elements.

**Best Window Size for Sauvola:** 25

---

## Question 3: ZNCC Template Matching and KNN Classification

This section involves the classification of digits based on template matching (ZNCC) and KNN classification.

### Main Features

1. **Image Preprocessing:** Converts input images to grayscale, resizes them to 28x28 pixels, applies Gaussian blur, and performs adaptive thresholding.
2. **Template Loading:** Loads preprocessed digit templates (0-9) for comparison.
3. **ZNCC Template Matching:** Compares the test image with stored templates and selects the best match based on correlation score.
4. **KNN Classification:** Uses Euclidean distance to determine the closest matching digit from the templates.
5. **Dual-Method Prediction:** The system provides predictions from both ZNCC and KNN classification for comparison.

### Clear Outputs

For a test image (e.g., `test/3.11.png`), the system outputs:
- **Template Matching Prediction:** 3
- **KNN Classification Prediction:** 3

Both methods correctly classify the digit as '3'.

### Comparison of Methods

| Method                    | Approach                   | Pros                           | Cons                           |
|---------------------------|----------------------------|--------------------------------|--------------------------------|
| **ZNCC Template Matching** | Measures correlation similarity | Works well with structured templates | Sensitive to distortions       |
| **KNN Classification**     | Uses Euclidean distance    | More flexible with variations  | Requires more computation      |

### Observations

- Both ZNCC Template Matching and KNN Classification correctly classify digits in the test set.
- ZNCC is effective when the test image closely matches the stored templates but may struggle with variations.
- KNN is more robust against variations but requires additional computations.
- The combination of both methods ensures a reliable prediction system.

---

## Question 4: Credit Card Number Recognition

The project focuses on recognizing credit card numbers using digit templates and contour detection.

### Key Functions

1. **preprocess_card_image(image):** Converts the image to grayscale, applies Gaussian blur, and uses Otsu thresholding to create a binary image that highlights the digits.
2. **refine_roi(roi):** Applies morphological operations (closing followed by opening) to the region of interest (ROI) to better separate the digits.
3. **find_digit_contours(roi_thresh):** Detects contours in the thresholded ROI and sorts them from left to right.
4. **create_digit_templates():** Generates templates for digits 0–9 using OpenCV’s text rendering. The templates are normalized and centered for better matching accuracy.
5. **match_digit(roi, templates):** Uses template matching (with normalized cross-correlation) to compare a candidate digit ROI against each template and determine the best match.
6. **process_contour(contour, roi_thresh, templates):** Processes each detected contour by resizing it to the template size and matching it with the available digit templates.
7. **recognize_credit_card_number(image_path):** Orchestrates the overall workflow of loading the image, extracting ROI, preprocessing, and contour detection, and recognizing the digits.

### Initial Issue: Incomplete Recognition

The initial code output was incomplete, showing only "703" instead of the full number. The issues were:

1. **Wide Contour Splitting:** Removed the wide-contour splitting logic, which resulted in more accurate digit detection.
2. **Template Accuracy:** Improved the template creation by centering the text and using a larger font (scale 2.0, thickness 3).
3. **Threshold Tuning:** Adjusted the contour area and match acceptance threshold.
4. **Morphological Operations:** Increased kernel sizes for better separation of touching digits.

### Verification and Results

After making the necessary changes, the system now recognizes full credit card numbers (e.g., "512345575901").

---

## Conclusion

Through several debugging iterations, the system now robustly recognizes credit card numbers from images by improving template accuracy, adjusting morphological operations, and fine-tuning the thresholds. This project demonstrates the importance of image preprocessing, adaptive thresholding, and template matching for accurate digit recognition.
