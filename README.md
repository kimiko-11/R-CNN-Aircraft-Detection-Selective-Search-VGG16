# ✈️ R-CNN Aircraft Detection
An R-CNN-based object detection pipeline for identifying and localizing aircraft in images. The project combines Selective Search, VGG16 feature extraction, and region-based classification to demonstrate the fundamentals of two-stage object detection.

## 🔍 Pipeline

```text
Input Image
     ↓
Selective Search
     ↓
Region Proposals
     ↓
VGG16 Feature Extraction
     ↓
Region Classification
     ↓
Bounding Box Regression
     ↓
Final Aircraft Detection
```
## 1. Data Preparation

Aircraft images and their corresponding bounding-box annotations are loaded and processed to generate training samples.

Selective Search is used to generate candidate object regions, which are separated into positive and negative samples based on their overlap with the ground-truth bounding boxes.

## 2. Feature Extraction

Each proposed region is resized and passed through VGG16, a pretrained convolutional neural network, to extract fixed-size visual feature representations.

## 3. Region Classification

The extracted features are classified as either:

Aircraft
Background

Classification can be performed using an SVM or a fully connected neural-network classifier.

## 4. Bounding Box Regression

A bounding-box regression stage can refine the predicted coordinates of detected aircraft, improving localization accuracy.

## 5. Visualization

The final predictions are visualized by drawing bounding boxes around detected aircraft in the input images.

✨ Key Features
Implements the fundamental R-CNN object detection pipeline
Uses Selective Search for region proposal generation
Uses pretrained VGG16 for feature extraction
Explores SVM-based region classification
Supports bounding-box regression
Visualizes detected aircraft with bounding boxes
Demonstrates the combination of classical computer vision and deep learning
☁️ Google Colab

The project can be run using Google Colab with Google Drive used for dataset storage.

Drive mounting is performed per user:

from google.colab import drive
drive.mount('/content/drive')

This prompts the user to authorize their own Google account. No personal Google Drive credentials are stored in the repository.
