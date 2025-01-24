# RCI
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


## Key Features

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

### Mask Images
Binary or grayscale images (0-255 values) used for:
- Semantic segmentation of features (e.g., roads, buildings)
- Region highlighting/isolation
- Overlay visualization with original imagery

## GSD (Ground Sample Distance)
GSD (Ground Sample Distance) in remote sensing and aerial imagery:

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


## GIS File Format Extensions

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


For detailed implementation and methodology, refer to the included Jupyter notebook.