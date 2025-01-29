# Road Condition Inspector (RCI)

A comprehensive tool for analyzing road conditions using satellite imagery and machine learning.

## Table of Contents
- [Environment Setup](#environment-setup)
- [Project Components](#project-components)
  - [Image Processing](#image-processing)
  - [Tiling System](#tiling-system)
  - [Linear Reference System (LRS)](#linear-reference-system-lrs)
  - [YOLO Implementation](#yolo-implementation)
- [Technical Details](#technical-details)
  - [GSD (Ground Sample Distance)](#gsd-ground-sample-distance)
  - [GIS File Formats](#gis-file-formats)
- [Usage](#usage)

## Environment Setup

1. **Create Virtual Environment**
```bash
# Create venv
python -m venv .venv

# Activate venv
# Windows
.venv\Scripts\activate
# Linux/Mac
source .venv/bin/activate
```

2. **Install Dependencies**
```bash
# Install from requirements.txt
pip install -r requirements.txt
```

**Note:** GDAL may require additional system-level installations depending on your OS.

## Project Components

### Image Processing
- Supports GeoTIFF files (Geographic Tagged Image File Format)
- GSD (Ground Sample Distance): Represents the physical size (typically in meters) that each pixel covers on the ground
- Batch processing capabilities for large datasets
- Automatic coordinate extraction and center point calculation

### Tiling System
- Splits large satellite images into 640x640 pixel tiles
- Preserves geographic metadata for each tile
- Grid visualization for tile boundaries
- Template matching for tile position validation

### Linear Reference System (LRS)
The LRS component provides sophisticated road analysis capabilities through computer vision and geospatial techniques:

#### Technical Components
- **Principal Component Analysis (PCA)**
  - Estimates road dimensions by finding major/minor axes
  - Projects contour points onto principal axes for accurate measurements
  - Calculates road orientation and direction

- **Ground Sampling Distance (GSD)**
  - Converts pixel measurements to real-world distances
  - Accounts for Earth's curvature in longitude calculations
  - Uses geographic metadata for precise measurements
  ```python
  meters_per_degree_lat = 111319.9
  meters_per_degree_lon = meters_per_degree_lat * cos(latitude)
  gsd_x = pixel_scale_x * meters_per_degree_lon
  gsd_y = pixel_scale_y * meters_per_degree_lat
  ```

- **Contour Detection**
  - Uses OpenCV's findContours with RETR_EXTERNAL mode
  - Filters noise by excluding small contours (area < 500 pixels)
  - Identifies continuous road segments

#### Analysis Features
- **Road Dimension Analysis**
  - Width and length measurements in meters
  - Lane estimation based on standard lane width (3.6m)
  - Area calculations for road segments
  - Automated road width assessment

- **Statistical Analysis**
  - Mean width calculation with standard deviation
  - Min/max width detection
  - Total length and area computations
  - Per-segment metrics and aggregated statistics

- **Coordinate Integration**
  - Pixel-to-meter conversion using GSD
  - Geographic coordinate system support
  - Location-aware measurements

### YOLO Implementation
YOLOv8 is integrated for automated road detection and segmentation, providing state-of-the-art deep learning capabilities:

#### Mask Processing System
- **Format Conversion Pipeline**
  ```python
  # Example annotation format for segmentation
  class_id x1 y1 x2 y2 x3 y3 ...  # Polygon points
  0 0.5 0.5 0.6 0.6 0.7 0.5 ...   # Normalized coordinates
  ```
  - Converts binary masks to YOLO-compatible formats
  - Supports both detection (bounding boxes) and segmentation modes
  - Automated contour extraction and normalization
  - Preserves spatial relationships in annotations

#### Dataset Organization
- **Directory Structure**
  ```
  dataset/
  ├── train/
  │   ├── images/
  │   └── labels/
  ├── valid/
  │   ├── images/
  │   └── labels/
  └── test/
      ├── images/
      └── labels/
  ```
  - Automatic split into train/valid/test sets
  - Maintains paired image-label relationships
  - Supports both jpg/png image formats

#### Training Configuration
- **YOLOv8 Integration**
  - Uses pre-trained YOLOv8 segmentation models
  - Custom configuration via data.yaml:
    ```yaml
    path: /path/to/dataset
    train: train/images
    val: valid/images
    test: test/images
    nc: 1  # Number of classes
    names: ['road']  # Class names
    ```
  - Hyperparameter optimization for road detection
  - Multi-scale training support

#### Model Capabilities
- **Segmentation Features**
  - Instance-level road segmentation
  - Real-time processing capabilities
  - Confidence thresholding for precision control
  - Post-processing for enhanced boundary detection

- **Deployment Options**
  - Batch processing for large datasets
  - Real-time inference support
  - Export to various formats (ONNX, TensorRT)
  - GPU acceleration support

#### Visualization and Analysis
- Built-in visualization tools
- Performance metrics tracking
- Confusion matrix analysis
- Integration with plotting libraries

## Technical Details

### GSD (Ground Sample Distance)
Ground Sample Distance in remote sensing and aerial imagery:

**Definition**: The physical ground distance represented by a single image pixel.

**Key Points**:
- Measured in units/pixel (e.g., meters/pixel)
- Lower GSD = Higher spatial resolution
- Example: 0.3m GSD means each pixel represents 30cm on the ground

**Factors Affecting GSD**:
- Flying height/satellite altitude
- Sensor resolution
- Camera focal length

**Applications**:
- Image quality assessment
- Feature detection capabilities
- Mission planning
- Map scale determination

### GIS File Formats

**TIFF (Tagged Image File Format):**
- Geographic coordinate systems
- Map projections
- Ground control points
- Pixel resolution data
- Spatial reference info

**.shp (Shapefile)**
- Main file containing geographic features and geometry
- Stores points, lines, polygons representing map features

**.shx (Shape Index)**
- Index file enabling quick searching of shapes
- Contains position index of geographic features

**.dbf (Database File)**
- Attribute database storing feature properties
- Contains tabular data linked to geometric features
- Readable by spreadsheet software

**.prj (Projection)**
- Text file defining coordinate system
- Contains spatial reference information
- Specifies map projection parameters

**.tar (Tape Archive)**
- Container file that bundles multiple files
- Used to package and compress GIS datasets
- Common for distributing complete datasets with all components

*Note: .shp, .shx, .dbf, and .prj typically work together as a set and are required for full shapefile functionality.*

## Usage

Detailed usage instructions and examples can be found in the included Jupyter notebooks:
- `RCI.ipynb`: Main image processing and tiling functionality
- `LRS.ipynb`: Linear Reference System implementation
- `yolo.ipynb`: YOLO training and inference

For implementation details and methodology, refer to the individual notebook documentation.