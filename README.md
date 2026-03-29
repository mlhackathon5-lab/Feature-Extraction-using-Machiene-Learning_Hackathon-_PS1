# Feature-Extraction-using-Machiene-Learning_Hackathon-_PS1
Deep learning pipeline for extracting GIS features (roads, water bodies, utilities, etc.) from drone orthophotos using a U-Net segmentation model and converting predictions into vector shapefiles.

AI Feature Extraction From Orthophotos
Overview

This project implements an end-to-end deep learning pipeline for automatic geospatial feature extraction from orthophoto images. The system uses a U-Net semantic segmentation model with a ResNet34 encoder to detect and classify various infrastructure and environmental features such as roads, bridges, railways, utilities, and water bodies.

The pipeline combines geospatial data processing with deep learning to convert orthophoto images and vector labels into a trained segmentation model capable of generating GIS-ready shapefiles from raw imagery.

The predicted segmentation masks are converted into vector geometries, making the outputs directly usable in GIS software such as QGIS or ArcGIS.

Features
End-to-end geospatial deep learning pipeline
Supports multi-class semantic segmentation
Automatic vector-to-raster label conversion
Patch-based training for large orthophotos
U-Net + ResNet34 architecture
Tile-based prediction for very large raster files
Converts predicted segmentation masks into GIS shapefiles
Works with GeoTIFF and shapefile datasets
Classes Detected

The model supports the following geospatial feature classes:

Class	ID
Bridge	0
Built Up Area	1
Railway	2
Road	3
Road Centre Line	4
Utility	5
Utility Polygon	6
Water Body	7
Water Body Line	8
Waterbody Point	9
Project Pipeline
Orthophoto (.tif) + Vector Labels (.shp)
            │
            ▼
      Data Preprocessing
            │
            ▼
    Rasterization of Labels
            │
            ▼
      Patch Generation
        (256 × 256)
            │
            ▼
        Model Training
       (U-Net + ResNet34)
            │
            ▼
        Model Inference
            │
            ▼
   Segmentation Mask Output
            │
            ▼
 Raster → Vector Conversion
            │
            ▼
      Output Shapefile
Project Structure
project/
│
├── config.py
├── preprocess.py
├── dataset.py
├── utils.py
├── train.py
├── predict.py
├── predict_tile_by_tile.py
├── main.py
│
├── data/
│   ├── orthophotos/
│   ├── shapefiles/
│
├── output/
│   ├── patches/
│   ├── masks/
│   ├── models/
│   └── predictions/
Installation

Clone the repository

git clone https://github.com/yourusername/feature-extraction-orthophotos.git
cd feature-extraction-orthophotos

Install dependencies

pip install torch
pip install segmentation-models-pytorch
pip install rasterio
pip install geopandas
pip install opencv-python
pip install numpy
pip install matplotlib
Data Preparation

Input data required:

1. Orthophoto Image
GeoTIFF (.tif)

Example:

NADALA_28996_ORTHO.tif
2. Vector Shapefiles

Training labels in shapefile format

Examples:

Bridge.shp
Road.shp
Water_Body.shp
Railway.shp
Utility.shp

These shapefiles are converted into a segmentation mask during preprocessing.

Preprocessing

Run preprocessing to create segmentation masks and patches.

python main.py

This step performs:

Load orthophoto raster
Load vector shapefiles
Convert shapefiles to raster masks
Generate image and mask patches

Output:

output/
   patches/images/
   patches/masks/
Model Training

Train the segmentation model:

python train.py

Training details:

Model: U-Net
Encoder: ResNet34
Loss: CrossEntropyLoss
Optimizer: Adam
Epochs: 45

Output:

output/models/unet_with_45_Epochs.pth
Prediction

Run inference on a raster image:

python predict.py --predict_file image_name.tif

This will:

Load trained model
Predict segmentation mask
Convert mask into shapefile

Output:

output/predictions/output.shp
Large Image Prediction

For very large orthophotos (1–3GB), use tile-based prediction:

python predict_tile_by_tile.py

This splits the raster into tiles and predicts each tile separately.

Output

The pipeline produces:

Segmentation Mask
prediction.tif

Pixel-wise classification.

GIS Shapefile
output.shp

Vector geometries for detected features.

These files can be directly loaded into:

QGIS
ArcGIS
PostGIS
Technologies Used
Python
PyTorch
segmentation_models_pytorch
Rasterio
GeoPandas
OpenCV
NumPy
Matplotlib
Applications

This project can be used for:

Automated drone mapping
Road extraction
Water body detection
Infrastructure mapping
Urban planning
Land use classification
Geospatial AI pipelines
Future Improvements
Add data augmentation
Use larger encoder architectures (EfficientNet / Swin Transformer)
Implement Dice Loss or Focal Loss
Add model evaluation metrics
Improve tile merging for large images
License

MIT License

If you want, I can also give you a much more impressive README including:

architecture diagram
training visualization
model performance section
GIF demo
example prediction images

(which makes your repo look like a professional AI research project).
