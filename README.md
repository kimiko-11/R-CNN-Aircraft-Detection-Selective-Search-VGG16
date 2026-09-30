# ✈️ R-CNN Aircraft Detection

### Region-Based Object Detection using Selective Search and VGG16

An implementation of the **R-CNN (Regions with CNN features)** object detection pipeline for detecting and localizing aircraft in images.

This project demonstrates how classical computer vision techniques can be combined with deep learning to build a two-stage object detection system.

The pipeline uses **Selective Search** to generate candidate regions and **VGG16** to extract visual features from those regions before classifying them as aircraft or background.

---

## 🔍 Detection Pipeline

```text
Input Image
     ↓
Selective Search
     ↓
Region Proposals
     ↓
IoU-based Positive / Negative Sampling
     ↓
Resize Regions to 224 × 224
     ↓
VGG16 Feature Extraction
     ↓
Region Classification
     ↓
Final Aircraft Detection
```
##  How It Works
1. Dataset Preparation

The project uses an aircraft image dataset containing images and corresponding bounding-box annotations.

The dataset is organized into:

Images/
└── *.jpg

Airplanes_Annotations/
└── *.csv

Each annotation file contains the bounding-box coordinates corresponding to the aircraft present in the associated image.

Note: The dataset itself is not included in this repository. Please download it from the original dataset source and place it in the required directory structure.

2. Ground-Truth Bounding Boxes

The annotation files are read and converted into bounding-box coordinates:

x1, y1
x2, y2

These ground-truth boxes are later used to determine whether a Selective Search region represents an aircraft or background.

3. Region Proposal Generation

Instead of directly predicting bounding boxes using a neural network, this implementation uses Selective Search to generate candidate object regions.

Up to approximately 2000 region proposals can be examined for each image.

Each proposal is compared with the ground-truth bounding boxes using Intersection over Union (IoU).

                 Ground Truth
              ┌───────────────┐
              │               │
              │    ✈️         │
              │               │
              └───────────────┘
                    ∩
              ┌─────────────┐
              │   Proposal  │
              └─────────────┘

Regions with sufficient overlap are treated as positive samples, while regions with low overlap are used as negative samples.

4. Region Preprocessing

The selected region proposals are cropped from the original image and resized to:

224 × 224 pixels

This allows them to be passed into the pretrained VGG16 network.

5. VGG16 Feature Extraction

Each region is passed through a pretrained VGG16 network using ImageNet weights.

The convolutional network extracts visual features representing characteristics such as:

Edges
Shapes
Textures
Object structures

The pretrained layers provide a strong visual representation without requiring the entire network to be trained from scratch.

6. Region Classification

The extracted features are used to determine whether a region contains:

Aircraft
   or
Background

This transforms the collection of region proposals into candidate aircraft detections.
