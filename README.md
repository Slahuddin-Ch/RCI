# **Road Condition Inspector (RCI) - Debirs**

A comprehensive tool for analyzing road conditions using satellite imagery and machine learning. RCI transforms satellite imagery into actionable metrics through a fusion of geospatial analysis, computer vision, and statistical methods.

## Features

- **Image Processing**
  - Support for GeoTIFF files with geographic coordinate systems
  - Automatic coordinate extraction and transformation
  - Batch processing capabilities for large datasets
  - Ground Sample Distance (GSD) calculation for accurate measurements

- **Tiling System**
  - Splits large satellite images (9415x9415 pixels) into manageable 640×640 tiles
  - Preserves geographic metadata for each tile
  - Non-overlapping tile generation for efficient processing
  - Grid visualization for tile boundaries


## Proper Selection of Area
An appropriate area should be selected to use its satellite images for the next steps. This includes areas impacted by storms or hurricanes. A potential candidate is **Hurricane MILTON Imagery**, specifically from the **Oct 11, 2024** flight **a**.

## Satellite Image Preprocessing
- High-resolution satellite images need to be preprocessed for annotations.
- These images should be tiled into **640×640** pixel images.
- Each satellite image results in **~200-500 small images**, depending on the original image dimensions.
- **Selection for annotation**: 50 images of size **640×640**.

## Saving Image Data with Geocoordinates
- A **CSV file** should be created, saving the following information for each small image:
  - **Geocoordinates**: The **center point** (longitude & latitude).

## Setting Up Training, Validation, and Test Sets
- Although tiled images from satellite imagery have minimal overlap, necessary **checks must be performed** to prevent data leakage.
- **Stratified dataset split**:
  - **80%** for training
  - **10%** for validation
  - **10%** for testing

