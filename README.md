# Car Damage Detection 🛠️

A computer vision project to automatically detect damage on vehicles, intended for insurance and claims assessment workflows.  
---

## Table of Contents

- [Motivation & Problem Statement](#motivation--problem-statement)  
- [Features](#features)  
- [Architecture & Approach](#architecture--approach)  
- [Dataset](#dataset)  
- [Installation & Setup](#installation--setup)  
- [Usage](#usage)  
- [Results & Evaluation](#results--evaluation)  
- [Limitations & Future Work](#limitations--future-work)  

---

## Motivation & Problem Statement

When a car is involved in an accident or damage event, insurance companies rely on manual inspections and assessments. This process is slow, subjective, and costly. Automating damage detection helps:

- Speed up claim verification  
- Reduce human error / subjectivity  
- Cut operational costs  
- Scale to many claims with minimal human intervention  

This project aims to detect damage regions (dents, scratches, breakage, etc.) in vehicle images, supporting downstream tasks like severity estimation or cost estimation.

---

## Features

- Object detection of damaged regions (bounding boxes)  
- Bounding box fusion / ensemble voting to reduce false positives  
- Training / fine-tuning of detection models  
- Inference pipeline to run damage detection on new images  
- Modular design to swap or experiment with different detector backbones  

---

## Architecture & Approach

1. **Multiple detectors / ensemble**  
   The system uses several object-detection models (e.g. different versions of YOLO or variants) in parallel to generate candidate damage bounding boxes.

2. **Confidence threshold optimization**  
   Each model has its own threshold for filtering predictions. These thresholds are optimized (e.g. via heuristics or metaheuristics) to minimize false positives while preserving recall.

3. **Bounding box fusion / voting**  
   Predictions from different models are fused. Overlapping boxes (above a certain IoU) vote to keep or discard candidate boxes. If a cluster of overlapping boxes meets a minimum vote count, they are merged into a final bounding box.

4. **Classification / damage type labeling (optional)**  
   Once damage regions are localized, a separate classifier can label the damage type (scratch, dent, break, etc.) if applicable.

This design helps reduce spurious detections and leverage model complementarities.

---

## Dataset

This repository does not appear to package a full public dataset. (You may include your dataset or point to external sources.)  
However, common datasets and references in the domain:

- **CarDD (Car Damage Detection Dataset)** — 4,000+ images, ~9,000 annotated instances across six damage types   
- Domain-specific datasets collected under insurance guidelines (e.g. consistent shot angles)

If you have a custom dataset, please describe:

- Directory structure (images, annotations)  
- Annotation format (e.g. COCO JSON, PASCAL VOC, YOLO TXT)  
- Split strategy (train / validation / test)  

---

## Installation & Setup

1. **Clone the repository**  
   ```bash
   git clone https://github.com/ramzaansari/car-damage-detection.git
   cd car-damage-detection

2. **Create a Python environment (recommended)**
    python3 -m venv venv
    source venv/bin/activate   # or `venv\Scripts\activate` on Windows

3. **Install dependencies**
    There may be a requirements.txt or environment spec. If not, typical dependencies include:
    pip install torch torchvision opencv-python matplotlib numpy
    # plus detection libraries such as yolov5 / detectron2 / custom ones
   
5. **Model weights**
    Provide or download pretrained/fine-tuned model weights. You may store them in a models/ directory.

6. **Prepare dataset**
    Place your training, validation, and test sets in the designated folder structure. Ensure annotation files are properly formatted.


