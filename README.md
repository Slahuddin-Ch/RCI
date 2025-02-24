# Road Condition Inspector (RCI)

A comprehensive tool for analyzing road conditions using satellite imagery and machine learning. RCI transforms satellite imagery into actionable metrics through a fusion of geospatial analysis, computer vision, and statistical methods.

## Features

- **Image Processing**
  - Support for GeoTIFF files with geographic coordinate systems
  - Automatic coordinate extraction and transformation
  - Batch processing capabilities for large datasets
  - Ground Sample Distance (GSD) calculation for accurate measurements

- **Tiling System**
  - Splits large satellite images (4707×4707 pixels) into manageable 640×640 tiles
  - Preserves geographic metadata for each tile
  - Non-overlapping tile generation for efficient processing
  - Grid visualization for tile boundaries

- **Linear Reference System (LRS)**
  - Principal Component Analysis (PCA) for road dimension estimation
  - Accurate road width and length measurements
  - Lane estimation based on standard width (3.6m)
  - Integration with existing transportation networks

- **YOLO Implementation**
  - YOLOv8 integration for road detection and segmentation
  - Custom dataset preparation and training pipeline
  - Support for both detection and segmentation modes
  - Real-time inference capabilities

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
pip install -r requirements.txt
```

Note: GDAL may require additional system-level installations depending on your OS.

## Technical Components

### Coordinate Transformations
- Pixel to geographic coordinate conversion
- Support for various map projections
- Geotransformation matrix handling
- Ground control point integration

### Road Analysis
- Width calculation using PCA
- Lane estimation algorithms
- Statistical analysis of road segments
- Integration with LRS networks

### Dataset Organization
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

## Key Formulas

- Pixel to Longitude: `lon = GT₀ + (x + 0.5) · GT₁`
- Pixel to Latitude: `lat = GT₃ + (y + 0.5) · GT₅`
- GSD (Longitudinal): `GSD_x = GT₁ · 111319.9 · cos(lat)`
- Road Width: `Width_meters = avg_horizontal_pixel · GSD_x`
- Compare the pixel values of the road in vertical and horizental direction to determine the road width.Which is smaller than other direction then that is the road width.

## Validation & Calibration

- Coordinate accuracy requirement: ≤5 meters error vs. ground control points
- Width calibration: Apply correction factor if model vs. ground truth discrepancy >15%
- Performance evaluation using IoU (Intersection over Union)
- Dataset split: 80% training, 10% validation, 10% test

## Usage

The project includes three main Jupyter notebooks:
- `RCI.ipynb`: Core image processing and tiling functionality
- `LRS.ipynb`: Linear Reference System implementation
- `yolo.ipynb`: YOLO training and inference examples



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

## File Format Support

- **TIFF/GeoTIFF**: Geographic coordinate systems, map projections
- **Shapefile (.shp)**: Geographic features and geometry
- **Database File (.dbf)**: Attribute storage
- **Projection File (.prj)**: Coordinate system definitions

For implementation details and methodology, refer to the individual notebook documentation.