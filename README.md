# cosmothon-computer-vision
Python pipeline for detecting, segmenting, and classifying buildings, roads, and vegetation from high-resolution drone imagery. Combines OpenCV, GDAL, and machine learning to generate vectorized outputs for geospatial analysis.

## Aerial Image Land Use Classification & Vectorization
To automatically identify and classify objects in an aerial image into categories like buildings, roads, and vegetation, and output vectorized or raster-labeled data for geospatial analysis.

1. Input Data
- A high-resolution drone image (DJI_0538.JPG or similar).
- Image is in standard RGB format.
- Goal: extract spatial features and classify them.

2. Preprocessing & Feature Detection
   a. Edge Detection
     - Convert image to grayscale.
     - Apply Gaussian blur.
     - Use Canny Edge Detection with dynamic thresholds (based on Otsu's method).
     - Highlight structural boundaries.

   b. Contour Extraction
     - Detect object contours using morphological operations (dilate and erode) to close gaps.
     - Visualize detected contours over the original image.

3. Vegetation Masking
     - Convert the image to HSV color space.
     - Apply color thresholding to isolate green and brown hues.
     - Generate a binary vegetation mask using cv2.inRange.

4. Raster to Vector Conversion
   - Create a binary raster image from the contour mask.
   - Use GDAL and OGR libraries to convert the raster (GeoTIFF) into vector polygons using Polygonize.

5. Mask Creation for Classes
   Separate masks for:
     - Houses/Buildings (from contours)
     - Roads (using inverse binary masking)
     - Vegetation (HSV thresholding)

6. Polygon Feature Extraction
   - Extract contours from each mask.
   - Calculate area and perimeter for each polygon (features).
   - Label data as:
       - 'House'
       - 'Road'
       - 'Vegetation'

7. Machine Learning Classification
   - Use Random Forest Classifier to classify regions based on contour features.
   - Encode labels and split data into training and testing sets.
   - Evaluate model accuracy (reported).

8. Visualization
   - Visualize classified polygons in an RGB image:
       - Red for houses
       - Blue for roads
       - Green for vegetation
   - Save the result as an image.

9. Export Results
   Save:
   - Binary masks
   - GeoTIFF of contours
   - Final classification image

## Final Output
- Visual classification image of land use
- Polygonized vector layer of features
- Accuracy score from machine learning model

## Potential Applications
- Urban planning & infrastructure monitoring
- GIS data generation from drone imagery
- Environmental mapping
- Automated cadastral updates
