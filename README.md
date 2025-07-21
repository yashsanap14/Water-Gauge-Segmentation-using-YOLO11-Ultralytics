# Pinewood Site Data Review and Segmentation with Ultralytics
This project focuses on reviewing Pinewood site data and creating a segmentation model using Ultralytics' YOLO and SAM2 models. The goal is to segment the gauge in water level images, using rectangles as initial annotations, and then apply segmentation to automatically identify the exact water segment. This process serves as a preprocessor for further analysis.

---

## Project Workflow

1. **Image Collection**
   - There are 7,196 images available. For initial experiments, the first 1,000 images are used.
   - Image URLs are provided in an Excel file. A script is included to download these images automatically.

2. **Annotation Creation**
   - Rectangle annotations are generated to capture the gauge in each image.
   - The annotation script uses basic computer vision to propose rectangles, which can be refined later.

3. **Segmentation Model Training**
   - The annotated images are used to train a segmentation model with Ultralytics (YOLO11 + SAM2).
   - The segmentation model is then applied to see how well it can automatically segment the water region.

4. **Comparison and Preprocessing**
   - The results are compared to previous work (200 images annotated in Roboflow).
   - The segmentation output is intended to be used as a preprocessor for downstream tasks.

---

## Directory Structure

```
pinewood_segmentation_project/
├── download_images.py        # Download images from Excel URLs
├── create_annotations.py     # Create rectangle annotations for gauges
├── requirements.txt          # Python dependencies
├── README.md                 # Project documentation
├── images/
│   └── raw/                  # Downloaded images
├── annotations/
│   ├── yolo/
│   │   ├── train/            # YOLO train annotations
│   │   └── val/              # YOLO val annotations
│   ├── metadata.json         # Annotation metadata
│   └── dataset.yaml          # YOLO dataset config
└── ...
```

---

## Usage

### 1. Install Dependencies
```bash
pip install -r requirements.txt
```

### 2. Download Images
- Place your Excel file with image URLs in the project directory.
- Run:
```bash
python download_images.py
```

### 3. Create Annotations
```bash
python create_annotations.py
```

### 4. Train Segmentation Model (Ultralytics YOLO + SAM2)
- Use the generated `annotations/dataset.yaml` as your dataset config.
- Example (replace with actual YOLO11 + SAM2 command):
```python
from ultralytics import YOLO
model = YOLO('yolov8n-seg.pt')  # Replace with YOLO11+SAM2 if available
model.train(data='annotations/dataset.yaml', epochs=50, imgsz=640)
```

### 5. Apply Segmentation and Evaluate
- Use the trained model to predict and visualize segmentation results.

---

## Notes
- 200 images have already been annotated in Roboflow for comparison.
- The initial rectangle-based approach is used as a preprocessor; further refinement is possible.
- This project is designed for experimentation and benchmarking with Ultralytics' latest models.

---

## References
- [Ultralytics YOLO Documentation](https://docs.ultralytics.com/)
- [SAM2 Model Info](https://github.com/facebookresearch/segment-anything)
- [Roboflow](https://roboflow.com/)
